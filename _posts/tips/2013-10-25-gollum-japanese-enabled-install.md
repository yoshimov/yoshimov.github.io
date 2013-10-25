---
layout: post
category: tips
tags: tips gollum wiki japanese
title: Gollumで日本語ページを使う
---
{% include keywords.md %}

## 概要

gitをバックエンドに動作するWikiの[Gollum]で、
日本語ページ名を使えるようにする方法です。

## 環境

* Ubuntu 13.10
* [Gollum] 2.5.1
* Ruby 1.9.3

## 手順

まず、依存するパッケージをインストールします。

    > sudo aptitude install git ruby-dev libicu-dev g++ make
    > sudo gem install bundler

日本語対応のGollum-libのソースを持ってきてビルドします。

    > git clone https://github.com/yoshimov/gollum-lib.git
    > cd gollum-lib
    > git checkout -b multibyte origin/multibyte
    > sudo bundle install
    > sudo rake install

日本語対応のGollumのソースを持ってきてビルドします。

    > git clone https://github.com/yoshimov/gollum.git
    > cd gollum
    > git checkout -b multibyte origin/multibyte
    > sudo bundle install

このままだとまだ日本語ファイル名でエラーになるので、
Gritにパッチを当てます。

* <https://gist.github.com/yoshimov/7113140>

    > cd /var/lib/gems/1.9.1/gems/gitlab-grit-2.6.0/lib/grit/
    > sudo wget https://gist.github.com/yoshimov/7113140/raw/95707d8192ede877d8d00265701cbf33c8da8ead/grit-multibyte.diff
    > sudo patch < grit-multibyte.diff

gitのリポジトリを用意します。
core.quotepathをfalseにしておかないと、日本語のファイル名が正しく読めないので
気をつけてください。

    > git init wiki
    > cd wiki
    > git config core.quotepath false

Gollumを起動します。

    > cd ~/gollum
    > ./bin/gollum ~/wiki --port 80 --show-all --allow-uploads

## 参考

* [gollum project](https://github.com/gollum/gollum)
* [gollumで日本語が使えないときの対処法](http://d.hatena.ne.jp/kei_q/20110613/1307981543)
* [Gollumで日本語ファイル名を使う](http://sunnyone41.blogspot.jp/2012/11/gollum.html)
