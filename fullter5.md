# 複雑な構造のウィジェット
```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Generated App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xff2196f3),
        canvasColor: const Color(0xffafafaf), // 例: 修正済みの有効なカラーコード
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
  static String _message = 'ok';
  static String _stars = '☆☆☆☆☆';
  static int _star = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('My App'),
        // ここに背景色を追加
        backgroundColor: Colors.deepPurple, // 例としてディープパープルを設定
        leading: const BackButton(color: Colors.white),

        actions: <Widget>[
          IconButton(
            icon: const Icon(Icons.android),
            tooltip: 'add star...',
            onPressed: _iconPressedA,
          ),
          IconButton(
            icon: const Icon(Icons.favorite),
            tooltip: 'subtract star...',
            onPressed: _iconPressedB,
          ),
        ],

        bottom: PreferredSize(
          preferredSize: const Size.fromHeight(30.0),
          child: Center(
            child: Text(
              _stars,
              style: const TextStyle(fontSize: 22.0, color: Colors.white),
            ),
          ),
        ),
      ),

      body: Center(
        child: Text(_message, style: const TextStyle(fontSize: 28.0)),
      ),
    );
  }

  void _iconPressedA() {
    _message = 'tap "android".';
    _star++;
    _update();
  }

  void _iconPressedB() {
    _message = 'tap "favorite".';
    _star--;
    _update();
  }

  void _update() {
    _star = _star.clamp(0, 5);

    setState(() {
      _stars = '★★★★★'.substring(0, _star) + '☆☆☆☆☆'.substring(_star);
      _message = '$_message [$_star]';
    });
  }
}
```
## APPバーの基本形
```
 appBar: (
        title:タイトル表示部分。通常はtext
        (backgroundColor: Colors.APPバー自体の背景色)
        leading: 左端に表示。通常はボタンかアイコン
        actions: タイトルの右側に表示
        bottom:  上記の下に追加表示される部分。PreferredSizeインスタンスを用意
 ) 
 ```

 ## Bottom NavigationBar
 ### 画面下部にバーが表示されて中のアイコンをクリックするとメッセージが表示
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok';
  static var _index = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(//APPバーの設定
        title: Text('My App'),
      ),
      body: Center(
        child: Text(
          _message,
          style: const TextStyle(
            fontSize: 28.0,
          ),
        )
      ),
      bottomNavigationBar: BottomNavigationBar(//ボトムナビゲーションバーの設定
        currentIndex: _index,
        backgroundColor: Colors.lightBlueAccent,
        items: <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            label: 'Android',
            icon: Icon(Icons.android,color: Colors.black, size: 50),
          ),
          BottomNavigationBarItem(
            label: 'Favorite',
            icon: Icon(Icons.favorite,color: Colors.red, size: 50),
          ),
          BottomNavigationBarItem(
            label: 'Home',
            icon: Icon(Icons.home,color: Colors.white, size: 50),
          ),
        ],
        onTap: tapBottomIcon,
      ),
    );
  }

  void tapBottomIcon(int value) {
    var items = ['Android', 'Heart', 'Home'];
    setState(() {
      _index = value;
      _message = 'you tapped: "' + items[_index] + '".';
    });
  }
}
```
```
bottomNavigationBar: BottomNavigationBar(
        currentIndex: <int値>,
        backgroundColor: Colors.lightBlueAccent,
        items: <BottomNavigationBarItem>[標示する項目　例：：アンドロイドアイコンなど]
        ～intの数分上2行繰り返し～
        onTap: アイコンをタップした時に呼び出される処理
)
```



## ListView(リストを表示するだけのウィジェット)
```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),

      body: Column(
        children: <Widget>[
          Text(
            _message,
            style: TextStyle(
              fontSize: 32.0,
            ),
          ),

          ListView(
            shrinkWrap: true,
            padding: const EdgeInsets.all(20.0),

            children: <Widget>[

              Text('First item',
                style: TextStyle(fontSize: 24.0),
              ),
              Text('Second item',
                style: TextStyle(fontSize: 24.0),
              ),
              Text('Third item',
                style: TextStyle(fontSize: 24.0),
              ),
            ],
          ),
        ],
      ),
    );
  }
}

```
```
ListView(
  shrinkWrap: true(bool値),
  padding: 余白,
  children: <Widget>[リスト]
)
```
## ListTile
### ListViewに専用のウィジェットを付けたもの
#### 例)ListViewをクリックするとアクションがおきる


```
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _index = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(

      appBar: AppBar(
        title: Text('My App'),
      ),

      body: Column(
        children: <Widget>[
          Text(
            _message,
            style: TextStyle(
              fontSize: 32.0,
            ),
          ),
          ListView(
            shrinkWrap: true,
            padding: const EdgeInsets.all(20.0),
            children: <Widget>[

              ListTile(
                leading: const Icon(Icons.android, size:32),
                title: const Text('first item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 1,
                onTap: () {
                  _index = 1;
                  tapTile();
                },
              ),

              ListTile(
                leading: const Icon(Icons.favorite, size:32),
                title: const Text('second item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 2,
                onTap: () {
                  _index = 2;
                  tapTile();
                },
              ),

              ListTile(
                leading: const Icon(Icons.home, size:32),
                title: const Text('third item',
                  style: TextStyle(fontSize: 28)),
                selected: _index == 3,
                onTap: () {
                  _index = 3;
                  tapTile();
                },
              ),
            ],
          ),
        ],
      ),
    );
  }

  void tapTile() {
    setState(() {
      _message = 'you tapped: No, $_index.';
    });

  }
}
```
```
ListTileの基本形
leading: const Icon(Icons.home, size:32),//アイコンを設定
  title: const Text('third item',//アイコンとなるテキスト
    style: TextStyle(fontSize: 28)),
  selected: _index == 3,//
  onTap: () {
    _index = 3;
    tapTile();//このメソッドを実行
  },
```

## SingleChildScrollview
### ウィジェットの大きさに併せて自動でスクロールバーを追加
```
class _MyHomePageState extends State<MyHomePage> {

 @override
 Widget build(BuildContext context) {
   return Scaffold(

     appBar: AppBar(
       title: Text('My App'),
     ),

     body: SingleChildScrollView(
       child: Column(
           mainAxisSize: MainAxisSize.min,
           mainAxisAlignment: MainAxisAlignment.spaceAround,
           children: <Widget>[
             Container(
               color: Colors.blue,
               height: 120.0,
               child: const Center(
                 child: Text('One',
               style: const TextStyle(fontSize: 32.0)),
               ),
             ),
             Container(
               color:Colors.white,
               height: 120.0,
               child: const Center(
                 child: Text('Two',
               style: const TextStyle(fontSize: 32.0)),
               ),
             ),
             Container(
               color: Colors.blue,
               height: 120.0,
               child: const Center(
                 child: Text('Three',
               style: const TextStyle(fontSize: 32.0)),
               ),
             ),
             Container(
               color:Colors.white,
               height: 120.0,
               child: const Center(
                 child: Text('Four',
               style: const TextStyle(fontSize: 32.0)),
               ),
             ),
             Container(
               color: Colors.blue,
               height: 120.0,
               child: const Center(
                 child: Text('Five',
               style: const TextStyle(fontSize: 32.0)),
               ),
             ),
           ],
         ),
       ),
   );
 }

}
```
```
基本形
SingleChildScrollView(
   child:ウィジェット
) 
```
