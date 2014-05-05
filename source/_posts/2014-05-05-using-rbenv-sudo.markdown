---
layout: post
title: "sudoセッションで 'bundle exec' を実行する"
date: 2014-05-05 18:00:54 +0900
comments: true
categories: [ruby, rbenv, github, bundler, hub]
---

sudoセッションでコマンドを実行するためには、[rbenv-sudo](https://github.com/dcarley/rbenv-sudo)を使えばよい。

<!-- more -->

## 事象

[hub](https://github.com/github/hub)をLinux環境(Ubuntu 14.04 LTS)にインストールした際に、以下のエラーが出た。
`/usr/local/bin`にインストールするため、root権限が必要である。

```bash
$ bundle exec rake install
rake aborted!
Permission denied - /usr/local/bin/hub
/home/hina/devel/github/hub/Rakefile:121:in `block in <top (required)>'
Tasks: TOP => install
(See full trace by running task with --trace)
```

## 解決方法

### 前提条件

rbenvがインストールされていること。

* rbenv 0.4.0-97-gfe0b243

### 手順

#### rbenv-sudoをインストールする

```bash
git clone git://github.com/dcarley/rbenv-sudo.git ~/.rbenv/plugins/rbenv-sudo
```

#### hubをインストールする

```bash
rbenv sudo bundle exec rake install
```
#### hubがインストールできたか確認する

```bash
$ which hub
/usr/local/bin/hub
```
