# FultterやAndroid Studioをインストールする前に  
## ストレージをきちんと確保しておきましょう  
#### VSCインストール前なら空き100G程度、無いなら外付SSD、HDDの購入しそちらにインストールするのがおすすめ
#### 作業中でも結構ストレージくいます

---　

## 詳しい環境構築法はこちら
[Flutter を VSCode で環境構築してみた！＜Windows編＞](https://qiita.com/shimizu-m1127/items/d8dfc2179bc01baaef6b) 
### 情報を補足
### ダウンロードしたFullterを展開(インストール)時、展開先のPATHに日本語(ユーザー名)、OneDriveなどが混ざるとがPATH設定後、コマンドプロンプトが正常に作業しなくなり、先に進めなくなるので注意
#### 特に市販品のPCなどではデフォルトで設定されているものも多いので注意



# Git-HubとVSCの紐づけ
### Git-Hub：ファイルの更新を解り易くするアプリ、ファイル自体に何かあっても復元等がし易い模様(まだ良く解らん)

## 詳しいやり方はこちら
[VSCodeで始めるGit(Hub)管理](https://zenn.dev/kd_gamegikenblg/articles/b220e23b0b7ef9)
### 情報を補足
### SSHの項目で使われる”clip < .ssh/id_rsa.pub”というコマンド
#### 要はrsaの内容のコピー内に一時的に保存しておくという命令の様なので、そのままGitHubのSettings→SSH and GPG keysと進んでKeyの項目に貼り付けるだけでOKです(ssh-rsaから始まる長い文字列が貼り付けられるはず)

#### おまけ(Git初心者あるある…だと思う)
#### 紐づけに成功しても定期的にリポジトリ変更をコミット、プッシュを行わないとGit－Hub内のファイルは更新されないので注意

# Fullter Studio
[Fullter studio](https://flutterstudio.app/)
### WebでFullterの制作物のだいたいの外観やプレビュー・コードが見える便利なツール
#### …がFullterのバージョンによってはエラーや警告が発生し易いので作ったコードに関してはコード合成後AIに添削を頼むのがベターかもしれない
#### 不具合の例
#### accentColor:------------(エラー：現在のFullterでは対応していない)
#### ×:const MyHomePage({Key key}) : super(key: key);  
○:const MyHomePage({Key? key}) : super(key: key);のコード
#### 各constの立て方(基本警告だがたまにエラーになる)