```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: Text(
        'Hello, Flutter World!!',
        style: TextStyle(fontSize:32.0),
      ),
    );
  }
}
```
### Fullter
#### ウィジェットと呼ばれる部品の組み込み(ウィジェットツリー)によって生成される

#### この動き：mainのrunApp関数でウィジェット(MyApp)を起動
#### Widget build(BuildContext context):このウィジェットが画面上でどのように見えるかを定義し、その結果としてWidgetオブジェクトを返す」
```
 MaterialApp:  マテリアルデザインを管理
 title:　アプリのタイトル
 home: このアプリに組み込まれるウィジェットを示す
 Text:テキストの表示を行うためのウィジェット
```
## Stateクラス
### StatelessWiget:最初に表示された、変化しない
### StatefulsWiget:操作によって変化する
### State:状態を扱う為の機能

```
//Stateクラスの基本形形
class ウィジェットクラス extends State<ウィジェットクラス> {

  @override
  Widget build(BuildContext context) {
  }
}

//Statefulwigetクラスの基本形形
class ウィジェットクラス extends StatefulWiget {

  @override
  ステートクラス createState() => ステートクラス; 
}