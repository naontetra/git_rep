# Navigater : 画面の切り替え
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
        canvasColor: const Color(0xfffafafa),
      ),
      home: FirstScreen(),
    );
  }
}

// １つ目のスクリーン
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Home'),
      ),
      body: Center(
        child: Container(
          child: const Text('Home Screen',
              style: const TextStyle(fontSize: 32.0)),
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 1,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'Home',
            icon: const Icon(Icons.home, size:32),
          ),
          const BottomNavigationBarItem(
            label: 'next',
            icon: const Icon(Icons.navigate_next, size:32),
          ),
        ],
        onTap: (int value) {
          if (value == 1)
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context)=>SecondScreen()),
            );
        },
      ),
    );
  }
}

// ２つ目のスクリーン
class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Next"),
      ),
      body: Center(
        child: const Text('Next Screen',
            style:const TextStyle(fontSize: 32.0)),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: 0,
        items: <BottomNavigationBarItem>[
          const BottomNavigationBarItem(
            label: 'prev',
            icon: const Icon(Icons.navigate_before, size:32),
          ),
          const BottomNavigationBarItem(
            label: '?',
            icon: const Icon(Icons.android, size:32),
          ),
        ],
        onTap: (int value) {
          if (value == 0) Navigator.pop(context);
        },
      ),
    );
  }
}
```
```
基本形
移動先をpush
Navigator.push(<BuildContext>,<Route>);

移動先をpop
Navigator.pop(<BuildContext>);
```

# Drawer
### Gmailなどで使われる画面左から発生するリスト
```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My Flutter App', // アプリのタイトル
      theme: ThemeData(
        primarySwatch: Colors.blue, // アプリの全体的なテーマカラー
      ),
      home: MyHomePage(), // アプリのメイン画面を指定
    );
  }
}

// MyHomePageをStatefulWidgetとして定義
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

// MyHomePageの状態を管理する_MyHomePageState
class _MyHomePageState extends State<MyHomePage> {
  static var _items = <Widget>[];
  static var _message = 'ok.';
  static var _tapped = 0;

  @override
  void initState() {
    super.initState();
    for (var i = 0; i < 5; i++) {
      var item = ListTile(
        leading: const Icon(Icons.android),
        title: Text('No, $i'),
        onTap: () {
          _tapped = i;
          tapItem();
        },
      );
      _items.add(item);
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Flutter App')),
      body: Center(
        child: Text(_message, style: const TextStyle(fontSize: 32.0)),
      ),
      drawer: Drawer(
        child: ListView(
          shrinkWrap: true,
          padding: const EdgeInsets.all(20.0),
          children: _items,
        ),
      ),
    );
  }

  void tapItem() {
    Navigator.pop(context);
    setState(() {
      _message = 'tapped:[$_tapped]';
    });
  }
}
```