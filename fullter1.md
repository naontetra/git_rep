# Fultterレイアウトの基本フォーマット
```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',//アプリケーションのタイトル名
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: const Color(0xffafafa),
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key? key}) : super(key: key);
  @override
  _MyHomePageState createState() => _MyHomePageState();
}


//テキストの表示方法に付いてのクラス
class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('App Name')),
      body: Text(
        "Hello Flutter!",
        style: TextStyle(
          fontSize: 32.0,　//表示されるテキストのフォントサイズ
          color: const Color(0xff000000),  //テキストの色
          fontWeight: FontWeight.w700, //テキストの太さ
          fontFamily: "Roboto", //使用するフォントの種類（書体）を指定
        ),
      ),
    );
  }
}
//　基本ここまでの差し替えで対応

おまけ:fontFamilyとfontStyleの違い
◎fontFamily: 使用するフォントの種類（書体）を指定します。例えば、"Roboto"、"Arial"、"Times New Roman" など、文字のデザインそのものを決定します。

◎fontStyle: フォントのスタイルを指定します。主に、通常のスタイルかイタリック体（斜体）かを指定するために使われます。

具体的には、fontStyle には以下のいずれかの値を指定
FontStyle.normal: 通常のスタイル
FontStyle.italic: イタリック体
```

## テキストの中央(中央下部)揃え
#### 差し替え部分のみ対応

```
class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('App Name')),
      body: Center(//Center:中央揃えのためのウィジェット
        child: Text(
          "Hello Flutter!",
          style: TextStyle(
            fontSize: 32.0,
            color: const Color(0xff000000),
            fontWeight: FontWeight.w700,
            fontFamily: "Roboto",
          ),
          //テキストの位置を下部に表示させる時に追加
          //padding: const EdgeInsets.all(10.0),
          //alignment: Alignment.bottomCenter,//中央下
        ),
      ),
    );
  }
}
```
