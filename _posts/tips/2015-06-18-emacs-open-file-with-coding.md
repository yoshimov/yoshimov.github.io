--
layout: post
category: tips
tags: tips emacs coding
title: Emacsで文字コードを指定してファイルを開き直す
---

## 概要

Emacsで文字コードを指定してファイルを開き直す方法です。
あんまりコマンドが載ってなかったので。

## 環境

- Emacs 24.4.1 (Windows)

## 手順

一度ファイルを開いた際に、文字コードの判定に失敗して文字化けしている状態で、

    M-x universal-coding-system-argument

と実行すると文字コードを聞かれるので、ここで正しい文字コードを
`utf-8-unix` などと入力すると、さらに実行するコマンドを聞かれるので、

    M-x revert-buffer

とする。

もしくは、

    M-x revert-buffer-with-coding-system

でも良い。

最近EUCのファイルの判定に失敗することがあるので、たまに使うようになりました。

## 参考

- [Specifying a Coding System for File Text](http://www.gnu.org/software/emacs/manual/html_node/emacs/Text-Coding.html)
