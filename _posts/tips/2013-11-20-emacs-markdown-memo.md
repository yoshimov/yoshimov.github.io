---
layout: post
category: tips
tags: tips emacs evernote markdown
title: Emacsでお手軽Markdownメモ帳
---
{% include keywords.md %}

## 概要

[Emacs]を使って、キー操作ですぐにMarkdownでメモができるファイルを作成、
保存したファイルをキー操作ですぐに[Evernote]に送信する方法です。

## 環境

* Windows 7
* [Emacs] 24.3

## 手順

まずはMarkdown modeをインストールします。
以下のサイトから`markdown-mode.el`をダウンロードして、
ロードパスに置いてください。
わからなければ、Emacsのsite-lisp内で良いです。

* [Markdown mode](http://jblevins.org/projects/markdown-mode/)

次に、Markdownファイルを置くフォルダを作成します。
普通のフォルダで良いですが、Gitのリポジトリなどにすると
より保存などもやりやすくなります。

    > mkdir c:\markdown-memo

Evernoteクライアントを入れている場合は、インポートフォルダを
設定しておきます。ここでは `c:\evernote` と仮定しています。

そして、`~/.emacs.d/init.el`に以下の記述を追加します。

{% gist 7903242 %}

あとはEmacsを起動なおして、`Ctrl+x c c` で新しいメモファイルの作成、
編集が終わったら `Ctrl+x c e` でEvernoteにテキストとして送信することが
できるようになります。

## 参考

* [Parsing and Formatting Times](http://www.gnu.org/software/emacs/manual/html_node/elisp/Time-Parsing.html)
* [File Name Components](http://www.gnu.org/software/emacs/manual/html_node/elisp/File-Name-Components.html#File-Name-Components)
