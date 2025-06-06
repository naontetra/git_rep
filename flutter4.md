# アラートとダイアログ
### 特定条件で出てくる小さなウインドウ
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

class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';

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

            Padding(padding: EdgeInsets.all(10.0)),

            Padding(
              padding: EdgeInsets.all(10.0),
              child: ElevatedButton(//1　"tap me!"と書かれたボタンを押すと
                onPressed: buttonPressed,
                child: Text(
                  "tap me!",
                  style: TextStyle(
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto",
                  ),
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void buttonPressed() {//2　ショーダイアログが発生
    showDialog(
      context: context,
      builder:
          (BuildContext context) => AlertDialog(
            title: Text("Hello!"),//ショーダイアログのタイトル
            content: Text("This is sample."),//ショーダイアログのテキスト
          ),
    );
  }
}

```

## ショーダイアログにボタンを追加
```
// buttonPressed部分に貼り付け
void buttonPressed(){
  showDialog(
    context: context,
    builder: (BuildContext context) => AlertDialog(
      title: Text("Hello!"),
      content: const Text("This is sample."),
      actions: <Widget>[
        TextButton(//ダイアログ内のボタンとなるテキストA
            child: const Text('Cancel'),
            onPressed: () => Navigator.pop<String>(context, 'Cancel')
        ),
        TextButton(//ダイアログ内のボタンとなるテキストB
            child: const Text('OK'),
            onPressed: () => Navigator.pop<String>(context, 'OK')
        )
      ],
    ),
  ).then<void>((value) => resultAlert(value));
}

void resultAlert(String value) {//ダイアログ内のボタンを押した結果(メッセージを変更)
//　表示されるメッセージも変わる
  setState((){
    _message = 'selected: $value';
  });
}
```

## シンプルダイアログ
### pop upメニューから選択肢が選べる
```
void buttonPressed(){//buttonPressedで出てくる
  showDialog(
    context: context,
    builder: (BuildContext context) => SimpleDialog(
      title: const Text('Select assignment'),
      children: <Widget>[
        SimpleDialogOption(//シンプルダイアログの内容1
          onPressed: () => Navigator.pop<String>(context, 'One'),
          child: const Text('One'),
        ),
        SimpleDialogOption(//シンプルダイアログの内容2
          onPressed: () => Navigator.pop<String>(context, 'Two'),
          child: const Text('Two'),
        ),
        SimpleDialogOption(//シンプルダイアログの内容3
          onPressed: () => Navigator.pop<String>(context, 'Three'),
          child: const Text('Three'),
        ),
      ],
    ),
  ).then<void>((value) => resultAlert(value));
}
```