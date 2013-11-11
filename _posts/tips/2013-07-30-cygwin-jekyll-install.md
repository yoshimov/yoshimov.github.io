---
layout: post
title: Cygwin環境にJekyllをインストールする
category: tips
tags: [tips, cygwin, jekyll]
---
{% include keywords.md %}

## 概要

Cygwin環境でJekyllを動かす手順です。
Webにもこの手の記事はたくさんありますが、そのまま使えるものがなかったので
まとめておきます。

## 環境

* Chocolatey 0.9.8.20
* Cygwin 1.7.22
* Windows 7 64bit
* Jekyll 1.1.2
* Ruby 1.9.3

## 手順

まずは[Chocolatey][]をインストールします。
PowerShellのコマンドを、サイトからコピーしてきて実行してください。

cyg-getをインストールします。

    > cinst cyg-get

もし、Gowがインストール済みであれば、削除しておきます。

    > cuninst gow

必要なパッケージをインストールします。

    > cyg-get default ruby rubygems iconv iconv2 make git gcc-core libcrypt-devel

posix-spawnを手動でインストールします。

    > git clone https://github.com/rtomayko/posix-spawn.git
    > cd posix-spawn/
    > gem build posix-spawn.gemspec
    > gem install --local posix-spawn-0.3.6.gem

gemコマンドでJekyllをインストールします。

    > gem install jekyll

c:\cygwin\bin\jekyll の１行目に、以下のように -Ku オプションを指定します。

    #/usr/bin/ruby.exe -Ku

あとは、jekyll コマンドを使って、サイトのビルドが可能になります。

## 参考

* [Cygwin, jeykll](http://homepage3.nifty.com/k-takata/diary/2012-06.html#06)
* [invalid byte sequence in Windows-31J が出たときは](http://blog.cles.jp/item/5698)
* [Windows環境でUTF-8をベースに使用する](http://www.rubylife.jp/ini/japan/index5.html)
