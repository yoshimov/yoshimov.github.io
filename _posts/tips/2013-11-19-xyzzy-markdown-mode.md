---
layout: post
category: tips
tags: windows xyzzy software markdown
title: xyzzyでMarkdownを編集する
---
{% include keywords.md %}

## 概要

[xyzzy]上でMarkdownファイルを編集時に、
マークアップをハイライトしたりする方法です。

## 環境

* [xyzzy] 0.22.251

## 手順

まずは[Chocolatey]などで[xyzzy]をインストールします。

    > cinst xyzzy

以下のGistから`markdown-mode.l`をダウンロードして、
`xyzzy/site-lisp/`に入れておきます。

* [markdown-mode.l](https://gist.github.com/youz/1339252/)

`xyzzy/site-listp/siteinit.l` に以下の内容を追記します。

    ;; Markdown mode
    (require "markdown-mode")
    (push '("\\.md$" . markdown-mode) *auto-mode-alist*)

一旦xyzzyを終了して、Ctrl+Shiftを押しながらxyzzyを起動します。
こうすると`siteinit.l`が再コンパイルされます。

再度xyzzyを再起動すると、`.md`ファイルを編集時には自動的に
Markdown-modeに入るようになります。

## 参考

* [xyzzyでmarkdown形式を編集できるようにする方法](http://kakakikikeke.blogspot.jp/2013/04/xyzzymarkdown.html)
