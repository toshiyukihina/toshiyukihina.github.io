---
layout: post
title: "Creating a new rails project"
date: 2014-05-04 14:02:37 +0900
comments: true
categories: [cheat-sheet, ruby, rails]
---

How to create a rails new project without tainting the global rails environment.

<!-- more -->

## Environment

### OS

Linux ubuntu 3.13.0-24-generic #46-Ubuntu SMP Thu Apr 10 19:11:08 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux

### Ruby

1.9.3p545

### Ruby on Rails

4.1.0

### rbenv

rbenv 0.4.0-97-gfe0b243

## Prerequisite

You must install `bundler` at least to your ruby environment.

```bash
$ rbenv exec gem install bundler
$ rbenv rehash
```

## Steps

### Create a working directory

Create a temporary directory for setup the rails environment. This enviroment will be deleted after committing and pushing to your repository.

```
$ mkdir work
$ cd work
```

### Create a 'Gemfile'

Just only 'rails' in the 'Gemfile'.

```
$ cat << EOS > Gemfile
source "http://rubygems.org"
gem "rails", "4.1.0"
EOS
```

### Install Ruby on Ralis

Install the ruby on rails to `vendor/bundle` directory temporarily.

```
$ bundle install --path vendor/bundle
```

### Create a new rails project

`<project>` is a new rails project name.
**Don't forget** to set `--skip-bundle` option, or all gems will be installed global location.

```
$ bundle exec rails new <project> --skip-bundle
```

### Tidy some temporary files and directories

Delete all unnecessary files and directories.

```
$ rm -f Gemfile
$ rm -f Gemfile.lock
$ rm -rf vendor/bundle/
```

### Setup the rails environment

Install gems depend on the Ruby on Rails. A new and official 'Gemfile' is created on `bundle exec rails new <project> --skip-bundle`.

```
$ cd <project>
$ bundle install --path vendor/bundle
```

### Check if the rails server starts successfully

Run `rails server` command and access to `http://localhost:3000` with your browser.

```
$ bundle exec rails s
```

### Update '.gitignore'

Add `/vendor/bundle` to `.gitignore` file.

```
$ echo '/vendor/bundle' >> .gitignore
```

### Finally push a new project to your repository

[Github](https://github.com/)? [Bitbucket](https://bitbucket.org/)? Do what you want.
