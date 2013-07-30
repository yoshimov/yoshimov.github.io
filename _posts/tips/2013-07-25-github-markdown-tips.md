---
layout: post
title: GitHubのMarkdownの注意点
tags: [tips, markdown, github]
category: tips
---
{% include keywords.md %}

## 概要

[FSWiki][]から[GitHub Pages][]に移行しようとしてMarkdownを使うようになって、
ちょっとハマったところや気になったところをまとめておきます。

## Markdownの記述

これは、Wikiと比べてですが、ちょっと書きにくいなと思ったところです。

### リストのインデント

FSWikiでは、

    * item1
    ** item1-1
    * item2

というようにインデントを書きますが、
Markdownは見た目も重視するため、タブを入れる必要があります。

    * item1
        * item1-1
    * item2

'*+-'どれでもリストにできる、というのは自由度があって良いですね。

また、下とも関係しますが、空行を入れてもリストは継続します。

例えば、FSWikiでは

    * item1
    content

と書くと、下の行はリストではなく本文になりますが、Markdownではリストの中になって

* item1
content

となります。
リストとインデントの組み合わせも、

    * item1
        content

とすると、

* item1
    content

とインデント無しと同様になり、

    * item1

        content

と一旦改行を入れると、

* item1

    content

と、リスト内での段落分けになります。

リストを続けるときは、

    * item1
    * item2

と、空行なしの場合も、

    * item1

    * item2

と空行を入れた場合も、結果は同じように

* item1

* item2

となります。

コード片を記載する場合もインデントで記述しますが、
リスト要素の後は以下のようにインデントを２つにする必要があります。

    * item1

            code

### 空行の扱い

FSWikiの場合、本文を区切る場合以外は
空行はほとんど気にする必要はありませんが、
Markdownでは、見出しの前にもきちんと空行を入れないと、
前の本文に結合されてしまいます。

    content
    ## title

ではなくて、

    content

    ## title

と書く必要があります。
リストも、前後に空行が必要です。

これはちょっと間延びしてソースが見にくくなる気がしますが、
そういうものだと思って気をつけましょう。

### テーブル

標準のMarkdownではテーブルを表現する方法がないですが、kramdownなどのレンダリングエンジンを使うとテーブルも書けます。

    |1|2|3|
    |4|5|6|

などとすると、

|1|2|3|
|4|5|6|

となります。

### HTML

Markdownには直接HTMLが書けるので、いきなり本文中にタグを書いてしまえば
自由にHTML要素が記述できます。

JavaScriptなども埋め込むのが非常に簡単なのは良いですね。

##GitHub Pages特有の記述

GitHub Pagesというより、[Jekyll][]固有かもしれませんが。

### 数字とドット

Markdownでは、番号リストは

    1. item1

などと書きますが、これが影響してか

    * 1.2

などというような記述があると、ページのビルドに失敗してしまいます。
日付などをこんな風に記載している場合は注意しましょう。

### スペースが必要な要素

リストは、リスト記号の後ろに必ずスペースが必要です。

    *item1

ではダメで、

    * item1

とする必要があります。
見出しはスペースが無くても大丈夫みたいです。

こういう制約は元のMarkdownには書いてなかった気がするので、こちらに書きました。

### 文字コード

適当なMarkdownでも大抵はなんとかHTMLに変換してくれますが、
文字コードがShift-JISなページがあったりすると、あっさりエラーになります。

必ずバイトオーダーマークなしUTF-8に統一しておきましょう。

### 中カッコと％

Jekyllのテンプレート言語Liquidは、中カッコを使って

    \{\% include ... \%\}

などと書くので、HTML中にも中カッコが出てくる場合は '\\' でエスケープしてやる必要があります。
エスケープされていないと、ビルドエラーになります。

## 参考

* [Markdown syntax](http://daringfireball.net/projects/markdown/syntax)
* [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
