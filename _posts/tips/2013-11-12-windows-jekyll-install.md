---
layout: post
category: tips
tags: windows tips jekyll
title: Windows環境にJekyllをインストールする
---
{% include keywords.md %}

## 概要

Windows環境に[Jekyll]を入れる方法です。
オフィシャルのRuby 2.0を使った方法です。

Cygwin+Ruby 1.9を使った方法はこちら。

* [Cygwin環境にJekyllをインストールする](/tips/cygwin-jekyll-install)

## 環境

* Windows 7
* Ruby 2.0
* [Jekyll] 1.3.0

## 手順

まずは例によって[Chocolatey]を導入しておきます。

次に、RubyとDevKitを導入します。

    > cinst ruby
    > cinst ruby.devkit

あとはコマンドプロントを開き直して、Jekyllをインストールします。

    > gem install jekyll

必要に応じて、Markdownのレンダラも入れておきます。

    > gem install kramdown

Ruby 2.0からはインストールが楽になりました。
