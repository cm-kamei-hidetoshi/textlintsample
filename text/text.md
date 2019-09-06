## モチベーション

普段はAndroidアプリ開発をやってます。最近はPWAやらTWAやらAndroid界隈もWebの話をちょこちょこききますよね、やってみようと思って、React,Vue,Angulerのチュートリアルをやってlocalhostで試すところまではささっとできると思います。

localhostでPCブラウザで確認するだけでなく、実際にAndroid,iPhoneの実機で試してみたい。同じネットワークに繋いでローカルIPで接続したらみれるけど、やっぱり公開した実際の本番環境に近い形で確認したいですよね。

全然AWSのこと詳しくありませんが、`Amplify Framework`を使うといい感じにAWS構築をやってくれるみたいです。とりあえず試してみよう。

## Amplify Framework

Amplify Frameworkは、スケールするモバイルアプリケーションおよびウェブアプリケーションを最速で構築するためのものようです。

- [Amplify フレームワーク（スケールするアプリを最速で構築する方法をご提供）| AWS](https://aws.amazon.com/jp/amplify/framework/)

モバイルエンジニアが使うことを想定してるのか、AWS cliやコンソールでポチポチするのではなく、ユースケースに合わせて勝手にAWSサービスをいい感じに構築してくそうな予感がしました。

## 手順

大きく分けて3つです。

1.適当なWebページを用意します（今回はVue)
2.Amplify Command Line Interface (CLI) のセットアップします
3.Aplify cliを使ってデプロイします

### Vueプロジェクトをつくる

Vue cliを用いて、適当にプロジェクトをつくりました。

```
❯ vue --version
3.11.0
❯ vue create blog_demo
```

- [Installation | Vue CLI](https://cli.vuejs.org/guide/installation.html)
- [Creating a Project | Vue CLI](https://cli.vuejs.org/guide/creating-a-project.html#vue-create)


### Amplify Frameworkを利用するための設定

```
❯ npm install -g @aws-amplify/cli
❯ amplify configure
```

対話式できかれるのでどんどんすすめます。

### Amplify Frameworkでデプロイしてみる

Quickstartを見ながらデプロイします！

- [Quickstart](https://aws-amplify.github.io/docs/cli-toolchain/quickstart?sdk=js)

```
❯ cd blog_demo/
❯ amplify --version
1.12.0
❯ amplify init
```

セットアップチックなのが始まってしばらく待ちます。終わったら今回はWeb Hostingをやりたいのでhostingを追加しましょう。

```
❯ amplify hosting add
```

VueをビルドしてS3においてCloudFront経由でサイト見るところまでやります！

```
❯ amplify publish
```


完了するまで待ちます。完了後デプロイしたURLが表示される。

> Hosting endpoint: https://xxxxxxxx.cloudfront.net


初回は長かったけど、次回以降はソースをあげるだけなので短いです！基本的にデプロイしたいときに `amplify publish` します。

### Amplify Frameworkでつくったリソースを削除

今回は検証だったので、作ったリソースを削除しました！注意S3バケットは消されないようなので、自分で消しましょう。

```
❯ amplify delete
```

## あとがき

意外と簡単に公開ができてびっくりしました。AWSのcliを使ってごにょごにょ、コンソールはいってごにょごにょしないとだめなイメージあったけど、コマンド一発でデプロイできました。

モバイルエンジニアがとりあえず検証用とかMockなどの用途でささっと作れそうな感じでした！

皆さんも是非試してみてください！