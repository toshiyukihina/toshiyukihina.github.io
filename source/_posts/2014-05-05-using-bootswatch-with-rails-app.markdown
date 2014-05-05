---
layout: post
title: "BootswatchをRailsで使う"
date: 2014-05-05 12:11:44 +0900
comments: true
categories: [cheat-sheet, ruby, rails, Bootswatch]
---

[Bootswatch](http://bootswatch.com/)を利用して、簡単にイカしたデザインのWebアプリを構築します。

<!-- more -->

## 環境

### OS

Linux ubuntu 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

### Ruby

1.9.3p545

### Ruby on Rails

4.1.0

## 手順

### Railsのプロジェクトを新規作成する

[Creating a new rails project](/blog/2014/05/04/creating-a-new-rails-project)の手順を参考に、Railsのプロジェクトを新規作成します。
プロジェクト名は、`hello-bootswatch`とします。

### Bootswtchのgemをインストールする

`hello-bootswatch`を新規作成した後、`cd hello-bootswatch`して、`twitter-bootswatch-rails*`をGemfileに追加します。
また、`therubyracer`のコメントを外して有効にします。

```ruby
# コメントを外して有効にする
gem 'therubyracer',  platforms: :ruby

# 以下3つを追加する
gem 'twitter-bootswatch-rails'
gem 'twitter-bootswatch-rails-helpers'
gem 'twitter-bootswatch-rails-fontawesome'
```

`bundle install`します。

```bash
bundle install --path vendor/bundle
```

### テーマのインストール

`twitter-bootswatch-rails`のGeneratorを使って、テーマをインストールします。ここでは`flatly`をインストールします。
`bootswatch:import`実行時に、上書きするか聞かれますが、気にせず上書きします。

```bash
bundle exec rails g bootswatch:install flatly
bundle exec rails g bootswatch:import flatly
bundle exec rails g bootswatch:layout flatly
```

コマンド実行後、生成されるファイルとディレクトリです。

```bash
$ find ./ -name "flatly*"
./app/views/layouts/flatly.html.erb
./app/assets/javascripts/flatly.js
./app/assets/javascripts/flatly
./app/assets/stylesheets/flatly.css
./app/assets/stylesheets/flatly
```

Bootswatchのgeneratorの詳細については、[twitter-bootswatch-rails](https://github.com/scottvrosenthal/twitter-bootswatch-rails)のREADMEを参考に。

### StylesheetsとJavascriptをrequireする

`app/assets/stylesheets/application.css`に、以下の行を追加します。

```
*= require flatly
```

`app/assets/javascripts/application.js`に、以下の行を追加します。

```
//= require flatly
```

### お試し

テーマが正しく表示されるか、`welcome`コントローラを作って試してみます。

```bash
bundle exec rails g controller welcome index --skip-stylesheets
```

`app/views/layouts/application.html.erb`に、`app/views/layouts/flatly.html.erb`の内容をコピペして、`rails s`した後、`http://localhost:3000/welcome/index`にアクセスしてください。以下のような画面が表示されるはずです。

![bootswatch-flatly](/images/bootswatch-flatly.png)

### font-awesomeをインストールする

これまでの手順で、通常のコンポーネントは利用できるようになりましたが、font-awesomeを利用するためには、追加でインストールする必要があります。

```bash
bundle exec rails g bootswatch:fontawesome:install flatly
```

このコマンドを実行すると、`app/assets/stylesheets/flatly`に、font-awesome関連のファイルが追加され、`app/assets/stylesheets/flatly.css`に、`require flatly/font-awesome`が追加されます。
以下のコードを、`app/views/layouts/application.html.erb`にコピペして、正しく表示されるか確認してみます。

```html
<i class="fa fa-camera-retro fa-lg"></i>
<i class="fa fa-camera-retro fa-2x"></i>
<i class="fa fa-camera-retro fa-3x"></i>
<i class="fa fa-camera-retro fa-4x"></i>
<i class="fa fa-camera-retro fa-5x"></i>
```

![bootswatch-flatly-font-awesome](/images/bootswatch-flatly-font-awesome.png)
