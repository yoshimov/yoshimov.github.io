---
layout: post
category: tips
tags: windows python blockdiag diagram
title: Windows環境でblockdiagを使う
---
{% include keywords.md %}

## 概要

Windows環境でblockdiagを使う方法です。
例によってChocolateyを使います。

## 手順

まずはChocolateyを導入しておきます。

* [Chocolatey]

次に、Pythonを導入します。

    > cpython

これで同時にeasy_installも入ります。
CygwinのPythonを使ってもインストールできますが、
ファイル生成の際にパーミッションまわりでエラーが出ることがあるので、
Pythonは単独で入れるのがお勧めです。

コマンドプロンプトを開き直した後、

    > easy_install blockdiag seqdiag actdiag nwdiag

とすれば、blockdiag系のコマンドが使えるようになります。

ついでに、ダイアグラムファイルのコンパイルはmakeがあると楽なので、

    > cyg-get make

でmakeをインストールしておいて、

    all: hoge.png
    hoge.png: hoge.sdiag
        seqdiag hoge.sdiag -Tpng

などというようなMakefileを作っておきます。
