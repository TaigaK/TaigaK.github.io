---
layout: post
title:  "rails-template作った"
date:   2017-02-19 23:00:00 +0900
---

# rails-template
rails-template作った。
毎回やるのもめんどくさいので。  
リポジトリは[こっち](https://github.com/taigak/rails-template)  
機能としては以下。すべて対話シェルで選択した物のみ適用される。
* testをrspecに変更
* devise追加
* rails_admin追加
* cancancan追加
* TravisCI連携
  * TravisとSlackの連携
  * TravisとHerokuの連携

## 使い方
リポジトリのREADMEに書いてあるの守れば大丈夫なはず。  
基本的にPostgreSQL対象。  

TravisCIの関係で最初に__gitで管理されてるディレクトリが必要__。  
__remoteも追加しておく必要がある__ ってとこだけ注意

{% highlight bash %}
# need git-managed directory
mkdir app_name
cd app_name
git init
git remote add origin https://github.com/user_name/repo_name.git
cd ../

# rails new
rails new app_name -d postgresql -m https://raw.githubusercontent.com/taigak/rails-template/master/template.rb
{% endhighlight %}

## 各処理
ちょいちょい注意点がある。

### rspec
特になし

### devise
特になし  
作るユーザモデルはUser  
omniauthとかAPIとか後ろ2つに上げたGemとの連携とかできていないのでそのうち。

### rails_admin
特になし  
initializer内の設定ができてないので他のGemとの連携設定がまだ。そのうち。

### cancancan
特になし
ability内の設定がまだできてない。rails_adminのアクセス制御までやるならそのうち。

### travis
githubの求められる名前は全部小文字じゃないとあとでバグる。  
User名とリポジトリ名はURLで探すときに使うっぽいのでそれ基準で入力。  
ここが正常に設定できたっぽいならTravisのWeb画面をいじる必要はなし。

あとRubyのバージョンはHerokuへのデプロイもやるならHeroku対応のバージョンで。

#### travis notification
現在対応してるのはSlackだけ。  

こちらで設定する前にSlack側でTravisのIntegrationを追加しておく必要がある。  
Slack Accountはxx.slack.comみたいになってるとこのxx部分。  
tokenはTravisCIのIntegrationを追加したときに表示されるToken

#### travis Heroku
最初にここでHerokuのアプリを作るか聞くようになってる。作らないならnoを入力して、app_nameを聞かれるので既存のアプリ名を入力。  
作るなら適当な名前を入力。  

ただ一点気をつけるのが、名前が既に誰かが使っているものを入力したり、アプリ作成上限超えていたりすると作成ミスってそのまま次に進む。  
その場合また最初からやるなりHeroku側でアプリ新しく作って次ステップで既存アプリ名として入力して紐付けるなりするかが必要。

アプリを新しく作るならHeroku公式でその名前使えるかと作成上限を確かめたほうがいいかも。  
ちょっとアホっぽいのでどうにかしたいけど、Herokuコマンドにそこらへん確認できるやつあったかな…

## 最後
最後は　`git push origin master`して終了。Travisで正常に回ってデプロイまで行われるのを確認して終了。
