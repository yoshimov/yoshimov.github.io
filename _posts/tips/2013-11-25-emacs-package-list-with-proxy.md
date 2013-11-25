---
layout: post
category: tips
tags: tips emacs package proxy
title: Proxy経由でEmacsのパッケージ管理を使う
---
{% include keywords.md %}

## 概要

Emacsのパッケージ管理をProxy経由で利用する方法です。
特に認証の必要なProxyではうまく動かないことが多いので、その解決方法です。

## 環境

* Windows 7
* Emacs 24.3

## 設定

`.emacs.d/init.el`に以下の記述を追加します。

    (setq url-proxy-services
		'(("http" . "proxyhostname:port")
		  ("https" . "proxyhostname:port")))

認証の必要なProxyの場合、`*scratch*`などで事前に

	(base64-encode-string "username:password")

を実行して、ユーザ名、パスワードをBase64に変換した文字列を作成した後、
その文字列を使って以下のように設定します。

	(setq url-http-proxy-basic-auth-storage
		'(("proxyhostname:port" ("Proxy" . "base64string"))))

あとは普通に、`M-x package-list-packages` でパッケージ一覧を
表示できるようになります。

## 参考

* [Use ELPA (emacs) behind proxy requiring authentication](http://stackoverflow.com/questions/10787087/use-elpa-emacs-behind-proxy-requiring-authentication)
