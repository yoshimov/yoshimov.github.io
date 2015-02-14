---
layout: post
category: tips
tags: raspberrypi setup tips
title: Raspberry Pi 2の初期設定
---

## 概要

我が家のRaspberry Pi 2の設定をメモしておきます。

## 環境

- Raspberry Pi 2 Type B
- BUFFARO WLI-UC-GNM2
- 16GB microSDHC
- USBキーボード+マウス
- HDMI対応テレビ
- Raspbian (wheezy)

## 手順

NOOBSをダウンロードしてmicroSDHCカードに展開。

- <http://www.raspberrypi.org/downloads/>

Raspberry Piにセットして起動。
Raspbianを選択してインストールを開始。
GUIが起動するオプションを選択する。

再起動してGUIが起動したら、MenuからWifi Configurationを選択して、無線に接続する。

### 日本語環境

日本語入力環境をインストール。

    sudo aptitude install task-japanese task-japanese-desktop
    sudo aptitude install uim uim-anthy

### ツール類

    sudo aptitude install screen chromium

### 共有ディレクトリ

Windowsで使っている共有ディレクトリにアクセスできるように、オートマウントを設定します。

    sudo aptitude install autofs cifs-utils winbind

    sudo vi /etc/auto.master

以下の１行を追加。

    /smb /etc/auto.smb

Windowsのホスト名でアクセスできるように設定します。

    sudo vi /etc/nsswitch.conf

hosts: に `wins`を追加。

autofsを再起動。

    sudo service autofs restart

### IPv6

    sudo vi /etc/modules

以下の行を追加する。

    ipv6

### GPIO関連

Python用のライブラリをインストール。

    sudo aptitude install python-rpi.gpio

Scratch用のGPIOライブラリをインストール。

    wget http://bit.ly/1wxrqdp -O isgh7.sh
    sudo bash isgh7.sh

