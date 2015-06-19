---
layout: post
category: tips
tags: tips pebble tasker
title:Taskerを使ってPebbleの通知を状況に応じて制御する
---

## 概要

Taskerを使って、Pebbleの通知を状況に応じて制御する方法です。
例えば打ち合わせ中は電話やメールの通知だけを有効にして、
Ingressの通知は切る、というような制御ができます。

![pebble time](https://lh3.googleusercontent.com/-YTEBndszQdc/VYADROYmuQI/AAAAAAADuXM/v_vyEv0Ffoc/w426-h320/16%2B-%2B1)

## 環境

* Android 4.2.2 (Kyocera TORQUE G01)
* Pebble Time Firm 3.0
* Pebble Time App 3.0.1
* Tasker 4.7
* Pebble Notification Center 2.482

## 通知の設定

通知は、基本的にPebble Time AppのNotificationを使うほうが見た目もいいんですが、
Notification Centerを使うとTaskerからコントロールできるので、

- 常に確認したい通知はPebble Time AppのNotificationで選択
- 一時的に止めたい通知などはNotification Centerで選択

としておくと、状況によって通知の量をうまくコントロールできます。
Notification Centerはスマホ側、Pebble Time側両方にアプリのインストールが必要です。

私は、Pebble Time Appのほうでは、

- Google+
- 電話
- Inbox (もしくはGmail)

あたりだけ選択しておいて、Notification Centerで、

- Facebook
- Googleアプリ (詳細は後述)
- Ingress

あたりを、Include指定で選択しています。

Google Now(Googleアプリ)は、普通に選択しただけだとカードの枚数しか通知されないので、
Notification Centerの個別設定で

- Always parse statusbar notificationをチェック
- Excluding Regexに ゜（半濁点）, 職場, 自宅を指定

としています。これでも情報は少ないですが。

## Taskerの設定

Tasker側では、
Plugin->Notification CenterのChange global settings->Disable popup entirelyを
チェックしたTask(ここではPebble Silent)と、
チェックを外したTask(Pebble Notify)を作って、

    Profile: Working
    State: Calendar Entry [ Title:* Location:* Description:* Available:Any Calendar:Google:Work ]
    State: Not Calendar Entry [ Title:年次* Location:* Description:* Available:Any Calendar:Google:Work ]
    Enter: Pebble Silent
    Exit: Pebble Notify

のようなProfileを追加すると、仕事のスケジュールのある時間帯だけ
特定の通知を止められます。

## 参考

- [Notification Center for Pebble - Ultimate notification replacement](http://forums.getpebble.com/discussion/8053/android-notification-center-for-pebble-ultimate-notification-replacement)
- [Notification Center for Pebble](https://play.google.com/store/apps/details?id=com.matejdro.pebblenotificationcenter)
- [Tasker for Android](http://tasker.dinglisch.net/)

