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
            TextButton(//ボタンのUIの基本ここから差し替え
              onPressed: _buttonPressed,//ボタンを押したらというメソッド
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

//標準的なジャンケン？の表示コード
//ボタンを押すとランダムでグー、チョキ、パーを表示
```

## テキストボタンをアンドロイドアイコンに差し替え
```
TextButton(
  onPressed:buttonPressed,//ボタンを押したら
  child: Padding(
    padding: EdgeInsets.all(10.0),
    child:Icon (
      Icons.android,//アンドロイドアイコン
      size: 50.0,
    )
  )
)
```

## ElevatedButton
#### ボタンが少し立体的に表示される
```
ElevatedButton(
  onPressed:buttonPressed,
  child: Padding(
    padding: EdgeInsets.all(10.0),
    child:Icon (
      Icons.android,
      size: 50.0,
    )
  )
)
```
## アイコンボタン
#### アイコンをボタンに出来る
```
conButton(
  icon: const Icon(Icons.insert_emoticon),
  //icon:表示するアイコン
  iconSize: 100.0, //アイコンのサイズ(doubleで)
  color: Colors.red, //アイコンの色
  onPressed:buttonPressed, //クリックしたときに実行するメソッド
)
```

## フローティングアクションボタン
#### 画面の右下に自動でボタンを追加
```
FloatingActionButton(
  child: Icon(Icons.android),
  onPressed: buttonPressed
),
```

## ロウマテリアルボタン
#### いろいろ細かい設定できる
##### テーマの影響を受けない為、統一感のあるUIを作成する時は注意
```
RawMaterialButton(
  fillColor: Colors.white, //背景色
  elevation: 10.0, //ボタンの高さ(影の幅)
  // highlightColor:クリックしてハイライトした時の色
  // splashColor:クリックされたことを表す効果として使われる色
  // highlightElevation:クリックしたときのボタンの高さ(影の幅)
  padding: EdgeInsets.all(10.0),
  child: Text(
      "Push me!",
      style: TextStyle(fontSize:32.0,
      color: const Color(0xff000000),
      fontWeight: FontWeight.w400,
      fontFamily: "Roboto"),
    ),
  onPressed: buttonPressed
),
