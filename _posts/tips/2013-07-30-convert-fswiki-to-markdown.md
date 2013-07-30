---
layout: post
title: FSWikiのページを一括でMarkdownに変換する
category: tips
tags: [wiki, markdown, github, perl, tips]
---
{% include keywords.md %}

## 概要

FSWikiの \.wiki ファイルをGitHub Pagesの \.md に変換する方法です。
と言っても、中身はほとんどHTMLのまま変換します。

## 環境

* [FSWiki][] 3.6.4
* Perl 5.8
* Ubuntu 13.04

## 手順

FSWikiの展開されているフォルダのルートに移動します。

    > cd /home/hoge/fswiki

以下のURLからPerlスクリプトをダウンロードします。

    > wget https://gist.github.com/yoshimov/6081032/raw/1afefe342db85194b44fedc4f988cf01f332a3e5/translate-wiki2md.pl

{% gist 6081032 %}

htmlフォルダを作って、スクリプトを実行します。

    > mkdir html
    > perl translate-wiki2md.pl

ファイル名、コンテンツがUTF-8に変換された\.mdファイルがhtmlフォルダ内に生成されます。
プラグイン系はだいたい動きません。

\{\} などはエスケープされていないので、sedなどで適宜変換してください。

これをJekyllの_postsフォルダに入れると、
Wikiからの移行が可能です。

## 参考

* [FSWikiのwiki記法形式のファイルを一括でHTMLに変換する](http://d.hatena.ne.jp/suer/20091207/1260164295)
* [JavaScriptで文字コード変換ライブラリ作ってみた](http://polygon-planet-log.blogspot.jp/2012/04/javascript.html)
