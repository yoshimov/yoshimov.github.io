---
layout: post
category: list
tags: markdown online editor list
title: Webブラウザで使えるMarkdownエディタの比較
---
{: toc}

{% include keywords.md %}

## 概要

Webブラウザから利用できる[Markdown]エディタを比較してみます。

個人的には、テキスト系の保存には[Evernote]を使っているので、
ソフトのインストールが不要でリアルタイムプレビューできてオフラインでも使える、
というのが理想だと思っています。

## 比較

とりあえず全体のまとめ。順不同です。

|サービス名|エンジン|ライブプレビュー|オフライン|編集補助|自動保存|サーバ保存
|:---|---|---|---|---|---|---
|[Backpager](#backpager)|WMD|○|△|○|×|×
|[InstantMark](#instantmark)|Showdown|○|△|×|×|×
|[Markable.in](#markablein)|独自|○|×|○|○|○
|[Markdown: Dingus](#dingus)|Markdown|×|×|×|×|×
|[Markdown Editor by Jon](#jon)|Showdown|○|△|×|×|×
|[Markdown Edit](#markdown-edit)|Marked|○|○|○|○|×
|[Markdown Live Preview](#preview)|Markdown.js|×|△|×|×|×
|[Markdown Live Editor by Jaime](#jaime)|WMD|○|○|○|○|×
|[Markdown Viewer](#markdown-viewer)|Markdown.js|○|△|×|×|×
|[Minimalist Online Markdown Editor](#minimalist)|Showdown|○|△|×|×|×
|[Online Markdown Editor by CtrlShift](#ctrlshift)|[Showdown]|○|△|×|×|×
|[Online Markdown Editor by Werner](#werner)|WMD|○|△|○|×|×
|[Share Memo](#share-memo)|Marked|○|△|△|×|○
|[wri.pe](#wripe)|独自|○|○(予定)|○|○|○

今のところ、[wri.pe](#wripe)がぶっちぎりで使いやすいです。
wri.peのオフライン対応までは[Markdown Edit](#markdown-edit)で、
オフライン対応後に乗り換え、という感じですかね。

これらをChromeでアプリケーションショートカット化すると、
十分エディタとして使えます。

### Markdown: Dingus
{: #dingus}

* <http://daringfireball.net/projects/markdown/dingus>

![Markdown: Dingus](https://lh5.googleusercontent.com/TsFyYe5vznBNr0JCHTXI3KfpWca4VAni-2Pk-JiqkX8y=w285-h222-p-no)

Markdownの提唱元が提供しているオンライン変換サービスです。
基本的にオンラインでのみ動作します。
ライブプレビューなどはありません。
エディタの補助もありません。

### Online Markdown Editor by CtrlShift
{: #ctrlshift}

* <http://www.ctrlshift.net/project/markdowneditor/>

![Online Markdown Editor by CtrlShift](https://lh5.googleusercontent.com/d2zcKn1t9LR94qrMpWqYOhyG5uKl5U5oufHSGOBcPwRu=w288-h222-p-no)

非常にシンプルな機能で、軽快に動きます。
ライブプレビューも見られます。
ほぼ[Showdown]の機能そのままな感じです。
オフラインでの動作機能はありませんが、ブラウザにキャッシュされていれば動作します。
またエディタはtextareaそのままなので、編集時の補助機能などもありません。

### Markdown Viewer

* <http://www.markdownviewer.com/>

![Markdown Viewer](https://lh6.googleusercontent.com/hoZ9aFuzNhcybZFhcrQJnB5VO2N9fVkBHHjUY5wPci_p=w285-h222-p-no)

こちらもシンプルなエディタ。
ライブビューがあって、Markdown記法に従います。
上と同じようにオフラインを正式にはサポートしていませんが、キャッシュにあれば動作します。
編集時の補助はありません。

### Markable.in

* <http://markable.in/>

![Markable.in](https://lh3.googleusercontent.com/_86cfxbdSVWDUP4xSGGrXF3Z7K4QRcqdVZoiLJl5MA_M=w273-h208-p-no)

オンラインにアカウントを作ると、サーバ側で編集内容を保持してくれるエディタです。
ライブビューもあります。
エディタもリスト記号を自動的に付加してくれたり、タブが入力できたりと、補助もあります。
オンラインではないと動作しないのが難点。

### Online Markdown Editor by Werner
{: #werner}

* <http://slhck.info/markdown/>

![Online Markdown Editor by Werner](https://lh6.googleusercontent.com/r1ZIBLX-m5FnjdSG8Im4mlvH5OGcNI7g_iJONJb6fNTs=w295-h219-p-no)

これもシンプルなエディタです。
ライブビューがあって、エディタの編集補助もあります。
基本的にキャッシュにあれば、オフラインでも動きます。

### Markdown Live Preview
{: #preview}

* <http://markdownlivepreview.com/>

![Markdown Live Preview](https://lh5.googleusercontent.com/_J1E7Qburc3aJmuUx-e-t8KtrOEZmOA5_deuDF2U0PWI=w285-h222-p-no)

これはエディタが前面に出てくるエディタです。
ライブビューはなくて、Previewボタンを押すとプレビューができます。
エディタの横幅が固定なのがちょっと気になるところ。

### Minimalist Online Markdown Editor
{: #minimalist}

* <http://markdown.pioul.fr/>

![Minimalist Online Markdown Editor](https://lh6.googleusercontent.com/dwQOGYQ6jXk6XugaESxWuDgO_6VnjA-MS3QRKTzvZd_s=w308-h216-p-no)

画面上にコンテンツ以外ほとんど何も表示されない、非常にシンプルなエディタです。
ライブビューもあります。

### InstantMark

* <http://jrham.es/instantmark/>

![InstantMark](https://lh5.googleusercontent.com/5LU08jYNWlWNgd1vstoZdQWsElsRaSYgJ1nb0VMrZt07=w296-h219-p-no)

これもシンプルなエディタ。
ライブビューもあります。
編集補助はありません。
ファイルへの保存機能が付いています。

### Markdown Editor by Jon
{: #jon}

* <http://joncom.be/experiments/markdown-editor/edit/>

![Markdown Editor by Jon](https://lh5.googleusercontent.com/GwlQG_vnYHNVc31QfKFhPNHHxBPDs0ne42fyotTkzeWK=w296-h219-p-no)

シンプルなエディタ。ライブビューあり。
編集補助はありません。
レイアウトを自由に変更できるので、画面が狭くても使いやすいです。

### Markdown Edit

* <http://georgeosddev.github.io/markdown-edit/>

![Markdown Edit](https://lh3.googleusercontent.com/ruO8aKdsTUskotk3fJoDTPRbdfokpGOsZaww9FEtv6y_=w294-h206-p-no)

ちょっと機能豊富なエディタ。
ライブビューもあります。
HTML5のアプリケーションキャッシュを使って、自動保存をしてくれます。

Markdownのハイライトもしてくれて、
タブキーは利用できるように多少の編集補助もあります。
画面の幅が狭いと、プレビューが下に移動するレスポンシブデザインになっています。

Markdownの横幅が広い、エディタ部分が横にスクロールしてしまうのがちょっと残念なところ。
あと、イメージまわりにバグがあるらしく、編集中に

    ![]http://...

という記述に()を追記しようとすると、エディタが停止してしまいます。(2013/8/2)

### Backpager

* <http://backpager.amasan.co.uk/>

![Backpager](https://lh6.googleusercontent.com/ejzUr05VhUVHnv4379z62eQBXbXOJjfZE9Ub4Ya3G2RB=w301-h207-p-no)

シンプルなエディタ。ライブビューあり。
ベースはWMDなので、[Online Markdown Editor by Werner](#werner)とほぼ同等です。
キーボードショートカットが使える編集補助はありますが、タブは使えません。
画面の見た目は綺麗です。

### wri.pe

* <https://wri.pe/>

![wri.pe](https://lh4.googleusercontent.com/9JIq0U5H4r-VeoeytRTaeYhsI-JxaXqxiM26nXmP8Kk2=w325-h217-p-no)

ライブビューのあるシンプルなエディタで、編集補助あり。
しかもテーブルが表現可能。
将来的にはオフラインで動作します。

今のところオフライン時には保存ができないので、メモ１個しか新規作成できませんが、
Markdownの編集に加えて、自動保存、検索までできてしまう完璧すぎるサービスです。

### Share Memo

* <http://www.sharememo.net/>

![Share Memo](https://lh5.googleusercontent.com/f2m6YhXCjN9v6s-IU5Fs2yxnuXpnHXG8xWVkOVm_ACZZ=w362-h207-p-no)

これは、どちらかというと作成したメモを共有するためのサービス。
ノート１つずつにURLが割り当てられて、共有できます。

[Gist]と違って編集履歴などは残りませんが、FacebookアカウントやTwitterアカウントだけで
手軽にメモを共有できるのが良い感じです。

正式にはオフラインには対応していませんが、新規作成ページがキャッシュされていれば
プレビューも含めて基本的なメモの作成はできます。

### Markdown Live Editor by Jaime
{: #jaime}

* <http://jrmoran.com/playground/markdown-live-editor/>

![](https://lh6.googleusercontent.com/YkCfJdHS5X_mjfwkpciz7jivHHm3qL7RIktj-pFSBavt=w326-h217-p-no)

WMDを使ったシンプルなエディタ。
HTML5のローカルストレージを使って、編集中のコンテンツをブラウザ内に保存しておいてくれます。
オフライン状態でも動作します。