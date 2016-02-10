class: center middle
# Hubot ことはじめ

---
class: center middle
# @yukung

---
# Hubot とは？

* GitHub が作成した bot 作成用フレームワーク。
* サイトは[ここ](https://hubot.github.com/)
* リポジトリは[ここ](https://github.com/github/hubot)
* チームやプロジェクトのチャットに常駐させて、さまざまなお仕事をさせるためのもの
    * 時間や天気のお知らせをしたり
    * チーム内でくじびきをしたり
    * リリース作業やデプロイを bot にお願いしたり
    * 定期的に何かをさせたり
    * 他にもいろんなタスクを自動化することができる

---
class: center middle
# つまり ChatOps

---
class: center middle
# ChatOps❓❓

---
class: center middle
# そもそも ChatOps って？

---
# ChatOps とは

* チャットを中心とした開発や運用のフローのこと
* もともとは GitHub での開発のやり方、開発フローがきっかけ
* GitHub では、開発者が世界中に散らばっていて、全員が同じ場所に集まって作業を行うことはほとんどない
* 場所もバラバラ、タイムゾーンもバラバラ
* 必然的に**リモートワーク**中心の文化

---
# 詳しくは

* GitHub の中の人の資料をどうぞ
* [ChatOps at GitHub // Speaker Deck](https://speakerdeck.com/jnewland/chatops-at-github)

---
# ChatOps がなぜ必要か

--

**場所も**バラバラ、**タイムゾーンも**バラバラの中、どうやってコミュニケーションを取りつつ開発をスムーズに進められるか？

--

求められるのは、

* 遠隔でも
* 非同期でも
* お互いの意思疎通が取れること
* かつ**その空間に誰が居るのかが認識できる**こと

--

そこで**チャット**をコミュニケーションの中心に据えることで開発を円滑に回す

---
class: center middle
# チャットがなぜよいのか？

他にもコミュニケーションのツールはたくさんある。例えば？

---
class: center middle
# メール？

---
class: center middle
# 電話？

---
class: center middle
# テレビ会議？

---
class: center middle
# (´・ω・｀)ｼｮﾎﾞｰﾝ

---
class: center middle
# これら全てを兼ね備えているのがチャット

---
# チャットの一番いいところ

--

* **誰**が**何をした**のかが全て残る（これ重要）

--

* かつそれを**誰でも**見れる

--

* 情報を**共有**することがコミュニケーションコストがかからずに自然とできる

---
# 例えばデプロイ

* 個人の端末でコマンド操作をする
* 履歴がその人の端末にしか残らない
    * デプロイ作業が「**属人化**」する
* 結果もいちいち「**その人**」が共有しないといけない
    * 共有されないと闇の中

---
# ChatOps では

* **チャットルームをコマンドライン（Terminal）として扱う**
* すべての手順がチャット上で筒抜け
* 誰が何をやっているのかが手に取るように分かる
* 「**隠し事**」を無くす
    * 結果的に属人化できなくなる
* 結果もわざわざ共有しなくても自動的に全員が把握できる

---
class: center middle
# 前置きが長くなりました

このために生まれたのが Hubot です

---
# Hubot ことはじめ

* インストール
* Heroku 上で動かしてデモ
* 簡単なスクリプトを追加してみる

---
# インストール

* 必要なもの
    * Node.js
    * npm
    * Yeoman（最初のひな形作成の時だけ）
    * Heroku アカウント（今回は Heroku で動かすため）

---
# Node.js

OS やツールによっていろいろインストール方法があるけど、ここでは `nodebrew` というツールを使います。

```shell-session
$ nodebrew install-binary v0.12.9
$ nodebrew use v0.12.9
$ node -v
v0.12.9
```

---
# npm

Node.js と一緒にインストールされます。

```shell-session
$ npm -v
1.4.28
```

---
# Yeoman, Hubot-Generator

npm からインストールします。

```shell-session
$ npm install -g yo generator-hubot
$ npm list -g generator-hubot yo   
/usr/local/lib
├── generator-hubot@0.1.4 
└── yo@1.3.3 
```

---
# bot の作成

yeoman ジェネレータを使ってひな形を作ります。

```shell-session
$ mkdir wedbot && cd wedbot
$ yo hubot
# いろいろ聞かれるけどとりあえず全部デフォルトで
```

---
# とりあえず動かす

Hubot では `adapter` という概念で、bot の入出力を司ります。ここではとりあえず shell 上で動かしてみます。

```shell-session
$ ./bin/hubot --adapter shell -n wedbot 
wedbot>
```

---
# とりあえず動かす

`wedbot>` というプロンプトが表示されるので、bot に話しかけてみます。

```shell-session
wedbot> wedbot help
wedbot> wedbot help
wedbot> wedbot adapter - Reply with the adapter
wedbot animate me <query> - The same thing as `image me`, except adds a few parameters to try to return an animated GIF instead.
wedbot echo <text> - Reply back with <text>
wedbot help - Displays all of the help commands that wedbot knows about.
wedbot help <query> - Displays all help commands that match <query>.
wedbot image me <query> - The Original. Queries Google Images for <query> and returns a random top result.
wedbot map me <query> - Returns a map view of the area returned by `query`.
wedbot mustache me <query> - Searches Google Images for the specified query and mustaches it.
wedbot mustache me <url> - Adds a mustache to the specified URL.
wedbot ping - Reply with pong
wedbot pug bomb N - get N pugs
wedbot pug me - Receive a pug
wedbot the rules - Make sure wedbot still knows the rules.
wedbot time - Reply with current time
wedbot translate me <phrase> - Searches for a translation for the <phrase> and then prints that bad boy out.
wedbot translate me from <source> into <target> <phrase> - Translates <phrase> from <source> into <target>. Both <source> and <target> are optional
wedbot youtube me <query> - Searches YouTube for the query and returns the video embed link.
ship it - Display a motivation squirrel
wedbot>
```

既にいろいろ命令が初期設定としてインストールされています。

---
# Heroku で動かす

時間の都合により事前にやっちゃってます。

---
# あんちょこ

* Slack の Hubot Integration をチームに追加
* token と設定を環境変数に追加

```shell-session
$ heroku config:set \
> HUBOT_SLACK_TOKEN=<token> \
> HUBOT_SLACK_TEAM=wed-ben \
> HUBOT_SLACK_BOTNAME=wedbot
Setting config vars and restarting damp-atoll-2068... done, v4
HUBOT_SLACK_BOTNAME: wedbot
HUBOT_SLACK_TEAM:    wed-ben
HUBOT_SLACK_TOKEN:   <token>
```

---
class: center middle
# いざ動作確認

---
# 簡単なスクリプトを追加してみる

* 都道府県一覧を表示
* `wedbot prefecture list` で起動
* Hubot のスクリプトは CoffeeScript で書く（JavaScript でも OK）

```coffee
module.exports = (robot) ->

  robot.respond /prefecture list/i, (msg) ->
    request = msg.http('http://geoapi.heartrails.com/api/json')
                          .query(method: 'getPrefectures')
                          .get()
    request (err, res, body) ->
      json = JSON.parse body
      msg.send json.response.prefecture.join ','
```

ちょっと CoffeeScript 解説します。

---
class: center middle
# Thankyou for listening!
