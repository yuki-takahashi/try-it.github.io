title: Github Pagesへの公開
date: 2014-11-01 22:13:19
tags: Git
---
# Github Pages(Project Pages)の公開方法
Github Pagesは、Organization PagesとProject Pagesがある。

Organization Pegesは、アカウント単位でページを公開。
Project Pagesだと、プロジェクトごとにページを公開できる。

Organization Pegesは、remote/masterブランチが公開ファイルとなる。
Project Pegesは、gh-pagesブランチが公開ファイルになるので、
masterブランチで草稿をかいても良いけど、
masterはレビューが終わった後のファイルを置く、というイメージがあるので自分は混乱してしまいそう。
gh-pagesは公開ファイルになるので、できれば草稿とは別のブランチとして確保しておきたい。

なので、sourceというブランチを新たに作成し、草稿はそこで管理したいと思います。

参考として、Tokyo Otaku Modeさんの記事を拝見させて頂きました。
サブドメイン設定する方法とか、運用方法とかが乗っていてわかりやすいので勉強になりました！
Orgnization Pagesの場合の運用方法が詳しく掲載されています。
[チームブログをGitHubとHexoではじめよう！](http://blog.otakumode.com/2014/08/08/Blogging-with-hexoio/)

#新規ブランチとファイルを作成
sourceブランチを作成して、記事の.mdファイルを作成します。
OKなら　
hexo new "ここにタイトル名"
で新しい記事を作成。

#記事が書けたらローカルホストで確認
hexo server
でローカルサーバーが立ちあがるので、
http://localhost:4000　にアクセスして確認。
OKなら、addしてcommitしてpushする。

今回は私一人で運用しているので、そのままpushできちゃいますが、
本来は管理者がいると思うので、直接pushはできないことが多いはず。

その場合はPull Requestを送って、レビューしてもらい、
修正、add/commit/pushしてPull Request送って、レビューしてもらっての繰り返しになります。

#最終原稿ができたら
最終原稿が出来たら、sourceブランチをマージ。
アップ作業する人が、sourceブランチの最新版を取得(pull)して、
hexo deploy
を実行。

hexo deploy はHTMLファイルの作成からプッシュまでを一気にやってくれるコマンドです。
Project Pagesの場合、_config.ymlファイルのdeploy:のbranch:のところは下記のように、gh-pagesに設定します。
deploy:
  type: github
  repo: リポジトリ名
  branch: gh-pages


#本番環境を確認して終了
Github Pagesを確認して終了します。