---
layout: post
category: tips
tags: tips ruby mail
title: RubyでISO-2022-JPのメールを送信する
---
{% include keywords.md %}

## 概要

RubyでISO-2022-JPエンコードのメールを送信する方法です。

## 環境

- Ruby 2.0.0
- Mail 2.6.1
- Mail-iso-2022-jp 2.0.3

## 準備

gemを２つインストールしておきます。

    > gem install mail mail-iso-2022-jp

## 手順

Mail.deliverだとcharsetがうまく指定できないようなので、
Mailのオブジェクトを使ってメールを送信します。

~~~ ruby
require 'mail'
require 'mail-iso-2022-jp'

mail = Mail.new(charset: 'iso-2022-jp')
mail.from = "hoge@hoge"
mail.to = "hoge@hoge"
mail.subject = "題名"
mail.body = <<EOS
本文
EOS

mail.deliver!
~~~
