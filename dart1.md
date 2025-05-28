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
### StatelessWiget:最初に表示されたまま変化しない
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
```
### 例題

```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  final title = 'Flutterサンプル';
  final message = 'サンプル・メッセージ。';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MyHomePage(
        title: this.title,
        message: this.message
      ),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;
  final String message;
  const MyHomePage({
    Key? key,
    required this.title,
    required this.message
  }): super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        widget.message,
        style: TextStyle(fontSize:32.0),
      ),
    );
  }
}
```
```
1，メインクラスの設定
void main() {
  runApp(const MyApp());
}
```
```
2, ステートクラスとの連携
@override
  _MyHomePageState createState() => _MyHomePageState();
  
StatefulWidget が、その動的な振る舞いを管理するために _MyHomePageState という専用のクラスのインスタンスを作成し、連携する
```
```
3，MyAppクラスのstatelessWidgetとして、titleに'Flutterサンプル'をmessageに'サンプル・メッセージ。'を設定
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  final title = 'Flutterサンプル';
  final message = 'サンプル・メッセージ。';
｝
final:これ以上上書きされない(ダイヤモンドは砕けない)
```

```
4，homeの設定
デザインのタイトルには'Flutter Demo'を
homeの設定として、statelessWidgetのtitleとmessageを指定(this)
@override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MyHomePage(
        title: this.title,
        message: this.message
      ),
    );
  }
this:子クラスの？
```
```
const MyHomePage({
    Key? key,
    required this.title,
    required this.message
  }): super(key: key);
MyAppクラスで設定した値(title:'Flutterサンプル'とmessage:'サンプル・メッセージ。')がMyHomePageクラスに渡される
```
```
5，2で作られた_MyHomePageStateクラスのインスタンスをMyHomePageに保管したtitleとmessageを使って作成
return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        widget.message,
        style: TextStyle(fontSize:32.0),
      ),
    );
AppBar:Appバーを付けて
fontSize:32.0 フォントサイズを32で
```

