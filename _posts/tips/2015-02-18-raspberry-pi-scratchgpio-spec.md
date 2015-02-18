---
layout: post
tags: tips raspberrypi scratch gpio
category: tips
title: Raspberry Pi 2のScratchGPIOの仕様
---

## 概要

Scratch GPIO V7で使えるセンサー値や変数、broadcastのまとめです。
いまいちドキュメントとしてまとまってないので、ソースから読み取った仕様を
メモしておきます。

## 環境

- Raspberry Pi 2 Type B
- Scratch GPIO V7 (AddOnなし)

## Raspberry Pi 2で使う

2015/2/18現在では、Raspberry Pi 2上ではScratchGPIOはそのまま使えません。
さしあたっては`sgh_GPIOController.py`内のpiRevisionを２固定にすると、Type B相当の26ピンまでは使えるようになります。

## 仕様

### センサー値

基本的に`pin`番号で値(0,1)が返るのみ。

### Input broadcast

- `Triggerpin<pin>`: pinの値が変化した時に送信される。
  事前に下記の`triggerreset`が必要。

### Output変数（Scratchの変数として設定）

- `autostart`: trueにするとScratchのプログラムが自動実行される
- `sghdebug`: 1にすると、デバッグ情報がPython側に表示される
- `pfreq`: PWMの周波数を指定
- `setpins`: `setpinslow`とすると、入力ピンをpulldown lowに変更する。`setpinshigh`とすると、入力ピンをhighにする。
  `setpinsnone`は入力ピンをpullup,pulldownなしにする。
    - `gpio`とすると、7,8,10,22をinputとする。
- `invert<pin>`: pinの信号を逆にする
- `config<pin>`: `in`とすると入力信号、`inpulldown`とするとpulldownモード、`inpullnone`とすると未定に設定する。
- `pin<pin>`: 1とするとhighになる。
- `gpio<pin>`: GPIO番号でpinを指定して設定する。
- `power<pin>`: 1-100のPWMの数値。pin11はmotora、pin12はmotorbと指定できる。

### Output broadcast

- `pin<pin>`: 続けてon,offで値を設定
- `gpio<pin>`: GPIO番号でpinを指定、続けてon,offで値を設定
- `power<pin>`: ,(カンマ)に続けてPWMの数値を設定
- `triggerreset`: 全てのトリガを受け取るように設定する。
- `triggerresetpin<pin>`: pinの値が変化した時にトリガを受け取るように設定する。一度受け取ると毎回リセットが必要。

### MCP3208用拡張（未）

- 変数`setpins`に`spiadc1,mcp3208`を追加
- `adc1,1`をbroadcast
- センサー値`adc1,1`に読み取った数値が返る

