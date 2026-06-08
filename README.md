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

