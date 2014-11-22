# reins

Twitterアカウントのリストのタイムラインから画像を含んだツイートの情報を取得し、
定期的に画像をダウンロードして保存してくれるツールです。


## 使い方

0. [Java SE 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)をインストール。
1. [releases](https://github.com/seriwb/reins/releases)からzipファイルを取得し、適当な場所に展開。
2. 必要に応じてconf/Config.groovyの値を調整。
3. コンソールからreins-0.2.1.jarがある場所まで移動し、以下のコマンドを実行。
```
java -jar reins-0.2.1.jar
```

しばらくするとdirフォルダ配下にダウンロードファイルが保存されていきます。
もう後は画像を見ること以外にやることはありません！ラクチン！！

プログラムは挙動がおかしいと感じるまで動かしたままで大丈夫です。
ダウンロードされてないように感じた場合は、お手数ですが一度終了させて再度起動させてみてください。

終了させる場合は、コンソール上でCtrl+Cを入力してください。


### 動作環境

- Javaが動作するOS（Windows、Mac）
- JRE : 1.8 以上


## ここがすごい！

- リスト毎、ユーザー毎に画像を保存するので見やすい！
- リツイートの場合、リツイート元のユーザー名フォルダに画像を保存するので、
お気に入りのユーザーの開拓が捗る！

そして画像から元のつぶやきがたどれる！・・・ようになる予定です。


## 0.2版での追加機能

##### OAuthでのクライアント認証に対応
もうDeveloper登録は必要ありません！！

Web認証実施後に表示されるPINをプログラムに渡すことでreinsの利用が可能です。


##### ログ出力対応
logフォルダ配下にLTSV形式のログが出力されるようになりました。
バグ報告の際はこちらの情報を合わせて頂けると助かります。


##### ネットワーク接続エラーへの対応（0.2.1版）
Twitterから情報取得時にネットワークエラーが発生した場合、
15分後、再度処理を行うようになりました。


### バグ対応
以下のバグに対応しました。
- 終了処理が動いていなかったのを修正


# プログラムガイド

## ビルド手順

Gradleのbuildタスクを実施してください。

    gradle build

#### プログラムの実行
以下のクラスに含まれるmainメソッドを実行してください。

    /reins/src/main/groovy/white/box/reins/Main.groovy

**※System.inを入れてからgradle runは正常動作しなくなったため、gradleからの実行はできません。**

### ビルド環境

- JDK : 1.8.0_20
- Groovy : 2.3.3
- Gradle : 2.0



## 現在の制約


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



# 今後の予定

- 画像がつぶやかれたツイートページの表示
- Pixivリンクの一覧化と画像取得
- 画像取得対象外リストの設定
- GUIツール化
