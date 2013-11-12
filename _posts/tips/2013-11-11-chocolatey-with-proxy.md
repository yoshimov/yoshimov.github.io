---
layout: post
category: tips
tags: tips windows chocolatey proxy
title: ChocolateyをProxy環境にインストールする
---
{% include keywords.md %}

## 概要

[Chocolatey]は通常コマンド一発でインストールできますが、
Proxyのある環境では、[Chocolatey]のインストールコマンドで
インストールできないことがありますので、その際のインストールのしかたを
まとめておきます。

## 環境

* [Chocolatey] 0.9.8.20
* Windows 7

## 手順

Proxyがあると、インストール用のスクリプトとChocolatey本体の
ダウンロードに失敗することがあるので、それらをブラウザ等から手動で
ダウンロードして展開すればインストールできます。

まず、以下のURLをブラウザで開いて、ファイルをダウンロードします。

<http://chocolatey.org/api/v2/package/chocolatey/>

ダウンロードした、`chocolatey-*.nupkg` というファイルの
拡張子を `.zip` に変更します。
そして中身を適当な場所に解凍して、コマンドプロンプトで解凍した
フォルダに移動後、

    > @powershell -NoProfile -ExecutionPolicy unrestricted -Command ".\tools\chocolateyInstall.ps1"

と実行します。

その後も、Proxy設定は必要になりますので、以下の
環境変数を設定しておいてください。

    http_proxy=http://proxyhost:port
    https_proxy=http://proxyhost:port

## 参考

* [Installing Chocolatey](https://github.com/chocolatey/chocolatey/wiki/Installation)
