---
layout: post
category: tips
tags: tips android email tasker
title: Androidで特定のメールアドレス宛のメール作成画面を表示する
---
{% include keywords.md %}

## 概要

Androidで、メールアドレスを指定したメールの作成画面を、
一発で表示する方法です。

意外と面倒なので共有しておきます。

## 環境

* Android 2.3.3 ([CASIO IS11CA])

## 手段１：ブックマーク

ブラウザで、メールを作成するブックマークレットを作成して、
これのショートカットをホーム画面に作っておきます。

ブックマークレットは、以下の様な感じです。

    javascript:location.href='mailto:hoge@gmail.com?subject='+(new Date())

`mailto:`は直接ブックマークできないので、javascriptを使って
mailtoを開きます。

ただこれだと、Gmailなどの特定のアプリが起動するのではなく、
メールを作成できるアプリの一覧がまず表示されるので、
ワンクッションあります。

## 手段２：TaskerでCompose Email

Taskerには、Compose EmailというActionがあるので、
これを使ってメール作成画面を開くタスクを作成し、
ホーム画面にショートカットを作るという手もあります。

ただこれも、メールを作成できるアプリの一覧は出てきます。

## 手段３：Taskerでインテントを送信

もう１つは、[Tasker]など、任意のインテントを送信できるアプリを使って、

* Action: Intent.ACTION_SEND
* Data: mailto:hoge@gmail.com
* Package: com.google.android.gm
* Class: com.google.android.gm.ComposeActivityGmail
* Target: Activity

と指定したタスクを作って、ホームにショートカットを作ると、
Gmailのメール作成画面を直接ひらけます。

## 参考

- [Android Intent](http://developer.android.com/reference/android/content/Intent.html)
