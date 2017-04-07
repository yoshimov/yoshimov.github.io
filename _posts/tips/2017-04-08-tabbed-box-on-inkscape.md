---
layout: post
category: tips
tags: tips inkscape lasercutter design box
title: Inkscapeでタブ付き展開図を作る
---

## 環境

- Windows 10
- Inkscape 0.92 (64bit版)

## 準備

- Pythonのlxmlモジュールをダウンロード
    - https://pypi.python.org/pypi/lxml/
    - Windows向け2.7用のwhlをダウンロードする
- lxmlモジュールを `Inkscape/python/Lib` に展開
    - lxmlフォルダ毎展開する
- TabbedBoxMakerのファイルをダウンロード
    - https://github.com/paulh-rnd/TabbedBoxMaker
    - "Clone or download"からdownload ZIPを選ぶ
- `Boxmaker.inx, Schroffmaker.inx, Boxmaker.py` を `Inkscape/share/extensions` に展開
    - フォルダは作らない

## 手順

- Inkscapeを起動
- ドキュメントのプロパティから、用紙を横向きに変える
- エクステンション-Laser Tools-Tabbed Box Makerを選択
- 長さ、幅、高さ、素材の幅（Material Thickness）を指定
- 適用を押す
- すべてを選択
- フィル/ストロークタブから、ストロークのスタイルを選択して、線の太さを指定
    - 線が細すぎて表示されない場合は、表示-表示モードからアウトラインを選択する
