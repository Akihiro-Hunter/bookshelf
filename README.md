# github の操作も兼ねて、開発を行う

## 6月8日(月)
MacBookからGitHubに入り、リポジトリを作成。
その後、クローンした。
この時、クローンされた場合はそれがmain ブランチになるようなので、今までのVScode上で新規に作る作業は必要ないらしい。

```
git clone リンクURL
cd クローンしたディレクトリ

# これはいらなかった
git branc -M main

# README.mdを作成してひとまずプルリクまで
touch README.md
git add README.md
git commit -m "first commit"
git branch
```


### Laravelを入れる前に注意
MacBookで開発を始め、Windowsへ移行するという計画ですね。その場合、「開発環境のポータビリティ（持ち運びやすさ）」が非常に重要になります。

結論から言うと、現時点でも「Docker (Laravel Sail)」の使用を強くおすすめします。

その理由と、Windows移行時の注意点をまとめました。

1. なぜ「Docker（Sail）」を今使うべきなのか？
最大の理由は、MacとWindowsという異なるOS間での「環境差異」を完全に無視できるからです。

ローカル直接インストールの場合：

MacにPHP 8.3を入れたからといって、Windowsに同じバージョン、同じ設定（php.iniなど）、同じMySQLの設定を正確に再現するのは非常に手間がかかります。

「Macでは動いたのにWindowsでは動かない」というトラブルが頻発し、学習時間の大半を環境設定に奪われてしまいます。

Docker (Sail) の場合：

プロジェクト内に設定ファイル（docker-compose.ymlなど）が含まれるため、WindowsにDockerをインストールして sail up するだけで、Macと同じ環境が数分で再現されます。

2. リモートリポジトリ（GitHub）へのpushの注意点
Docker環境を共有する場合、以下のファイルを必ずGitHubに上げるようにしてください。

docker-compose.yml: Dockerの構成ファイル。

vendor/ ディレクトリ: 基本的にGit管理外（.gitignoreで除外）ですが、sail 自体もこの中にあるため、sail を使えるようにする必要があります。

もしWindows側でまだComposerが入っていない状態で sail を使いたい場合は、Laravel公式のSailの導入手順 にある通り、php -r "readfile('...');" | php のような初期コマンドを使えば、PHPすら入っていないPCからでも環境構築が可能です。

3. 今後のWindowsへの移行ステップ
Macでプロジェクト作成:

Bash
curl -s "https://laravel.build/my-app" | bash
cd my-app
./vendor/bin/sail up
Git管理を開始してGitHubへpush:

.gitignore が正しく設定されていることを確認してください（sail で作成すれば自動で適切に設定されます）。

Windowsへ移行:

Docker Desktopをインストール。

GitHubから git clone してくる。

Windowsのターミナルで vendor/bin/sail up を実行。

これで、Macで作ったものがそのままWindowsで立ち上がります。

注意点：Windowsの「WSL2」について
WindowsでDockerを使う場合、「WSL2 (Windows Subsystem for Linux)」という機能を使うのが現在のスタンダードです。これを使うことで、Windows上でも非常に高速で快適にDockerが動きます。

アドバイス: Windowsに乗り換える際は、まず「WSL2」を有効化してからDocker Desktopをインストールしてください。

「今はMacでSailを使ってサクッと始め、Windows移行時はDockerを入れ直すだけで開発継続」というルートが、一番挫折が少なくて確実ですよ。