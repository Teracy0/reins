# reins

Twitterアカウントのリストのタイムラインから画像を含んだツイートの情報を取得し、
定期的に画像をダウンロードして保存してくれるツールです。

## ここがすごい！

- リスト毎、ユーザー毎に画像を保存するので見やすい！
- リツイートの場合、リツイート元のユーザー名フォルダに画像を保存するので、
お気に入りのユーザーの開拓が捗る！

そして画像から元のつぶやきがたどれる！・・・ようになる予定です。


## 現在の制約

### 開発者登録が必要
Twitterアカウントを認証させるために、
[TwitterのDevelopersサイト](https://dev.twitter.com/)でTwitterの開発者アカウント登録を行う必要があります。
適当なアプリケーションを登録し、以下をtwitter4j.propertiesに記述してください。

- consumerKey
- consumerSecret
- accessToken
- accessTokenSecret


### rate limit対策が不十分

sleepでwaitしているだけなので、reins.tweet.waittimeをデフォルト値よりも小さくした場合、
Twitterさんに怒られる可能性があります。  
デフォルト値の場合は、1時間動かしていてもrate limitに引っかかることがなかったので、
特に理由がない限り変更しない方がよいです。

### ログ抑制がない

現状ログ抑制を行っていません。
したがって本来出すべきではないエラーも表示されています。  
以下のエラーは問題ないので無視してください。

- 2回目起動時のlist_mstの作成エラー
- 重複画像リンクのDB登録時に発生する一意制約エラー



# プログラムガイド

## 使い方

1. releaseからzipファイルを取得し、適当な場所に展開後、twitter4j.propertiesに各種値を設定。
2. 必要に応じてconf/Config.groovyの値を調整。
3. コンソールからreins-0.1.jarがある場所まで移動し、以下のコマンドを実行。
```
java -jar reins-0.1.jar
```
4. 終了はCtrl+Cで行う。

### 実行環境

- JRE : 1.8 以上


## ビルド手順

Gradleのbuildタスクを実施してください。

    gradle build

runタスクでGradleからプログラムを実行することもできます。

    gradle run

**※Eclipseからgradle runを実行した場合、終了することができないので気を付けてください。**

### ビルド環境

- JDK : 1.8.0_11
- Groovy : 2.3.3
- Gradle : 2.0



# 今後の予定

- 画像がつぶやかれたツイートページの表示
- Pixivリンクの一覧化と画像取得
- 画像取得対象外リストの設定
- GUIツール化