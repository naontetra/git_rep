# 入力の為のUI
## TextField
### テキストを入力する為のUI
```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: Colors.grey[200], 
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

class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static final _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('App Name')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(10.0),
              child: TextField(//テキストフィールドの設定
                controller: _controller,
                style: TextStyle(//テキストフィールドのスタイル詳細
                  fontSize: 28.0,
                  color: const Color(0xffFF0000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
                decoration: InputDecoration( // 追加: TextField の装飾
                  labelText: 'Enter text',
                  border: OutlineInputBorder(),
                ),
              ),
            ),
            ElevatedButton(
              child: Text(
                "Push me!",
                style: TextStyle(
                  fontSize: 32.0,
                  color: const Color(0xff000000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
              ),
              onPressed: buttonPressed,
            ),
          ],
        ),
      ),
    );
  }

  void buttonPressed() {
    setState(() {
      _message = 'you said: ' + _controller.text;
    });
  }
}
```
```
child: TextField(//テキストフィールドの設定
                controller: _controller,
                style: TextStyle(//テキストフィールドのスタイル詳細
                  fontSize: 28.0,
                  color: const Color(0xffFF0000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto",
                ),
)

static final _controller = TextEditingController();
入力値をテキストの値に

  _message = 'you said: ' + _controller.text;
  メッセージの値を書き換える

```
### 応用：：リアルタイムで入力した値を大文字変換(onChannge)
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static final _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(10.0),
              child: TextField(
                onChanged: textChanged,//テキストを大文字に変換
                controller: _controller,
                style: TextStyle(
                  fontSize: 28.0,
                  color: const Color(0xffFF0000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void textChanged(String val){
    setState((){
      _message = val.toUpperCase();
    });
  }
}
```
```
onChanged: textChanged,//テキストを変換

変換内容
void textChanged(String val){//文字列型の値を
    setState((){
      _message = val.toUpperCase();//大文字変換したものをメッセージに代入
    });
  }
```
## checkBoX
### いつもの
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _checked = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(10.0),
              child: Row(
                  mainAxisAlignment: MainAxisAlignment.start,
                  mainAxisSize: MainAxisSize.max,
                  crossAxisAlignment: CrossAxisAlignment.end,
                  children: <Widget>[
                    Checkbox(
                      value:_checked,
                      onChanged: checkChanged,
                    ),
                    Text(
                      "Checkbox",
                      style: TextStyle(fontSize:28.0,
                          fontWeight: FontWeight.w400,
                          fontFamily: "Roboto"),
                    )
                  ]
              )
            ),
          ],
        ),
      ),
    );
  }

  void checkChanged(bool? value){
    setState(() {
      _checked = value!;
      _message = value ? 'checked!' : 'not checked...';
    });
  }

}

```
```
Checkbox(
  value:_checked,(bool値)
  onChanged: 関数,(チェックが変更された場合の処理)
),
```
### おまけ(スイッチ)
#### チェックボックスとほぼ同じ仕様、差し替え可
```
Switch(
  value:_checked,
  onChanged: checkChanged,
),
```
# Radio(ラジオボタン)
### いつもの
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _selected = 'A';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(//縦ならべ配置
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),

            Padding(
              padding: EdgeInsets.all(10.0),
            ),

            Row(
                mainAxisAlignment: MainAxisAlignment.start,
                mainAxisSize: MainAxisSize.max,
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[

                  Radio<String>(
                    value: 'A',
                    groupValue: _selected,
                    onChanged: checkChanged,
                  ),
                  Text(
                    "radio A",
                    style: TextStyle(fontSize:28.0,
                      fontWeight: FontWeight.w400,
                      fontFamily: "Roboto"),
                  )
                ]
            ),

            Row(
                mainAxisAlignment: MainAxisAlignment.start,
                mainAxisSize: MainAxisSize.max,
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[

                  Radio<String>(
                    value: 'B',
                    groupValue: _selected,
                    onChanged: checkChanged,
                  ),
                  Text(
                    "radio B",
                    style: TextStyle(fontSize:28.0,
                      fontWeight: FontWeight.w400,
                      fontFamily: "Roboto"),
                  )
                ]
            ),
          ],
        ),
      ),
    );
  }

  void checkChanged(String? value){
    setState(() {
      _selected = value ?? 'nodata';
      _message = 'select: $_selected';
    });
  }
}

```
```
Radio<型>(
  value: '値(これが重要)',
  groupValue: _selected,
  //このラジオボタンがどのグループにはいっているか？
  //これがないと同一画面にカテゴリの違うラジオボタンを設定できない
  onChanged: checkChanged,
),
```
## DropdownBotton
### これもいつもの(逆三角形)
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _selected = 'One';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),

            Padding(
              padding: EdgeInsets.all(10.0),
            ),

            DropdownButton<String>(
              onChanged: popupSelected,
              value: _selected,
              style: TextStyle(color:Colors.black,
                fontSize:28.0,
                fontWeight: FontWeight.w400,
                fontFamily: 'Roboto'),

              items: <DropdownMenuItem<String>>[
                const DropdownMenuItem<String>(value: 'One',
                  child: const Text('One')),
                const DropdownMenuItem<String>(value: 'Two',
                  child: const Text('Two')),
                const DropdownMenuItem<String>(value: 'Three',
                  child: const Text('Three')),
              ],
            ),
          ],
        ),
      ),
    );
  }

  void popupSelected(String? value){
    setState(() {
      _selected = value ?? 'not selected...';
      _message = 'select: $_selected';
    });
  }
}

```
```
DropdownButton<型>(
  onChanged: popupSelected,//押した時に
  value: _selected,//値
  style: TextStyle(テキストスタイル詳細),
  items: <DropdownMenuItem<String>>[メニュー内のアイテム詳細]
)
 ``` 
## PopupMenuButton(縦三点)
#### DropdownBottonに似た物
##### DropdownBottonインスタンスを差し替え
 ```
 Align(alignment: Alignment.centerRight,
  child: PopupMenuButton(
    onSelected: (String value)=> popupSelected(value),
    itemBuilder: (BuildContext context) =>
    <PopupMenuEntry<String>>[
      const PopupMenuItem( child: const Text("One"), value: "One",),
      const PopupMenuItem( child: const Text("Two"), value: "Two",),
      const PopupMenuItem( child: const Text("Three"), value: "Three",),
    ],
  ),
),

```
# Slider
### (ボリューム調整や動画サイトで使われるスライドして値を設定するやつ)
```
 class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _value = 0.0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),

            Padding(
              padding: EdgeInsets.all(10.0),
            ),

            Slider(
              onChanged: sliderChanged,
              min: 0.0,
              max: 100.0,
              divisions: 20,
              value:_value,
            ),
          ],
        ),
      ),
    );
  }

  void sliderChanged(double value){
    setState(() {
      _value = value.floorToDouble();
      _message = 'set value: $_value';
    });
  }
}
```
```
Slider(
  onChanged: sliderChanged,:変更時の処理
  min: 0.0,：最小値
  max: 100.0,：最大値
  divisions: 20,:分割数(min～maxを何分割するか？)
  value:_value,：現在選択されている値
),
```          
