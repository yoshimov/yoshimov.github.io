---
layout: post
category: tips
tags: tips google github facebook evernote auth
title: ２段階認証の端末の変更方法
---

## 概要

２段階認証の端末を変更する方法です。
サービスによって操作が色々違うのでまとめておきます。

## Google

- My Accountを開く
    - <https://myaccount.google.com/>
- ログインとセキュリティを選択
- Googleへのログインを選択
- ２段階認証プロセスを選択
- Move to a different phoneを選択
- Phoneタイプを選択
- 新しいデバイスでQRコードを読み込むか、もしくは Can't scan the barcode? を選択してコードを表示させて入力する。
- 新しいデバイスに２段階認証が設定できたら表示されたパスワードを入力する。

## GitHub

- Settingsを開く
    - <https://github.com/settings/profile>
- Securityを開く
- Two-factor authenticationのEditを選択
- Reconfigure two-factor authenticationを選択
- Set up using an appを選択
- 新しいデバイスでQRコードを読み込むか、もしくは enter this text codeを選択してコードを表示させて入力する。
- 新しいデバイスに２段階認証が設定できたら表示されたパスワードを入力する。

## Facebook

- 設定を開く
    - <https://www.facebook.com/settings>
- セキュリティを開く
- コードジェネレータの編集を選択
- その他の設定を選択
- 新しいデバイスでQRコードを読み込むか、もしくは シークレットキーを入力する。
- 新しいデバイスに２段階認証が設定できたら表示されたパスワードを入力する。

## Evernote

- Settingsを開く
    - <https://www.evernote.com/Settings.action>
- Security Summaryを開く
- Two-step verificationのManage settingsを開く
- 一旦Text messagesに変更してから、Authenticatorを設定し直す

## Slack

- Account Settingsを開く
    - <https://xxx.slack.com/account/settings>
- Two factor authenticationのExpandを押す
- 一旦Deactivateのリンクを選択して解除してから、再度設定し直す

## QuickAuthでの操作

ついでにPebbleのQuickAuthの操作です。

２段階認証コードの追加はスマホのアプリから設定で行います。

削除はPebbleのアプリを起動後、一度選択ボタンを押して一覧表示にしてから再度選択すると、
Default設定か削除かを選ぶ画面が出るので、下ボタンを押すと削除できます。
一覧表示で選択ボタンを長押しすると順序が変更できます。

## 参考

- [How to get your two-step verification codes on your Pebble](http://www.connectedly.com/how-get-your-two-step-verification-codes-your-pebble)
- [QuickAuth](https://apps.getpebble.com/en_US/application/53131df8bb31cf87cd00019a)
