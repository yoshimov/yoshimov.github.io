---
layout: post
category: tips
tags: tips ruby csv
title: RubyでCSVファイルを読み書きする
---
{% include keywords.md %}

## 概要

Rubyで文字コードがシフトJISのCSVファイルを読み書きする方法です。

## 環境

- Ruby 2.0.0

## 手順

読み込み時に、ファイルの文字コードを指定して開きます。
cp932は、WindowsのShift JISコードです。
またその際に、内部的に利用したい文字コードを指定しておきます。
最近はUTF-8でソースを書くのが一般的になってきたので、
UTF-8にしておくと何かと便利です。

~~~ ruby
require 'csv'
reader = CSV.open("hoge.csv", "rt:cp932:utf-8")
reader.each do |row|
  puts row[1]
end
~~~

書き込みは正しくファイルを閉じるために、do/endの中に書き出しを行うコードを
記述します。
この際に、出力に利用する文字コードを指定します。

読み込み時とは違って、出力の文字コードが指定してあればあとは勝手に変換してくれます。

~~~ ruby
require 'csv'
CSV.open("hoge.csv", "wb:cp932") do |writer|
   writer << ["a", "b"]
end
~~~
