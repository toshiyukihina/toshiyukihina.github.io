---
layout: post
title: "GitHubに新しいリポジトリを作成する"
date: 2014-05-24 11:24:52 +0900
comments: true
categories: [git, github]
---

新しいプロジェクトを作って、GitHubに登録するまでのメモ。

<!-- more -->

## GitHubでリポジトリを作る

リポジトリの名前は、`hello-angular`。

## プロジェクトを作る

[hello-angular](https://github.com/toshiyukihina/hello-angular) を作ったときの。

```bash
$ mkdir hello-angular
$ yo angular
$ cd angular
```

## リポジトリの初期化

```bash
$ git init
```

## ファイルの追加(git add)とコミット(git commit)

```bash
$ git add .
$ git commit -m "some comment"
```

## リモートリポジトリの登録 (git remote add)

`origin`という名前で、`https://github.com/toshiyukihina/hello-angular.git` のリモートリポジトリを指すようになる。

```bash
$ git remote add origin https://github.com/toshiyukihina/hello-angular.git
```

登録できたか確認してみる。まだローカルに作成されただけ。

```bash
$ git remote -v
origin  https://github.com/toshiyukihina/hello-angular.git (fetch)
origin  https://github.com/toshiyukihina/hello-angular.git (push)
```

なんか間違って、一旦削除したい場合は、以下のコマンドで削除する。

```bash
$ git remote rm origin
```

## リモートリポジトリへ送信 (git push)

### masterブランチへ送信する

`-u` オプションは、ローカルブランチの現在のupstreamは、`origin` リポジトリの `master` ブランチであることを同時に設定する。
このオプションをつけると、リモートリポジトリを `pull` するときに特にオプションを与えずとも、このローカルリポジトリのブランチは、
`origin`の`master`から取得するようになる。

```bash
$ git push -u origin master
```

### masterブランチ以外へ送信する

`some-branch`というブランチへ送信する例。

ブランチの作成。

```bash
$ git checkout -b some-branch
```

ブランチの送信。

```bash
$ git push -u origin some-branch
```
