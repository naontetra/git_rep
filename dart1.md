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

#### 動き：mainのrunApp関数でウィジェット(MyApp)を起動
#### Widget build(BuildContext context):このウィジェットが画面上でどのように見えるかを定義し、その結果としてWidgetオブジェクトを返す」
```
 MaterialApp:  マテリアルデザインを管理
 title:　アプリのタイトル
 home: このアプリに組み込まれるウィジェットを示す
 Text:テキストの表示を行うためのウィジェット
```


