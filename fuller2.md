# ボタン学習の練習用コード
```
import 'package:flutter/material.dart';
import 'dart:math'; // shuffle()を使うためにimport

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'じゃんけんアプリ',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: const Color(0xfff0f0f0), // 少し明るい灰色に修正
      ),
      home: const MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key}) : super(key: key);
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  String _message = 'ボタンを押して！';
  final List<String> _janken = ['グー', 'チョキ', 'パー'];

  void _buttonPressed() {
    setState(() {
      _message = _janken[Random().nextInt(_janken.length)]; // より直接的なランダム選択
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('じゃんけん')), // タイトルを修正
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center, // 中央に配置
          mainAxisSize: MainAxisSize.min, // 必要最小限のサイズ
          crossAxisAlignment: CrossAxisAlignment.center, // 中央揃え
          children: <Widget>[
            Padding(
              padding: const EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: const TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
              ),
            ),
            TextButton(//ボタンのUIの基本
              onPressed: _buttonPressed,
              child: const Padding(
                padding: EdgeInsets.all(10.0),
                child: Text(
                  "じゃんけん！", // ボタンのテキストを変更
                  style: TextStyle(
                    fontSize: 32.0,
                    color: Colors.blue, // TextButtonなのでcolorPrimaryに合わせる
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto",
                  ),
                ),
              ),
            ),//ここの部分までがボタンついてのコード(差し替え利用可)
          ],
        ),
      ),
    );
  }
}
```

## テキストボタンをアンドロイドアイコンに差し替え
```
TextButton(
  onPressed:buttonPressed,
  child: Padding(
    padding: EdgeInsets.all(10.0),
    child:Icon (
      Icons.android,//アンドロイドアイコン
      size: 50.0,
    )
  )
)
```