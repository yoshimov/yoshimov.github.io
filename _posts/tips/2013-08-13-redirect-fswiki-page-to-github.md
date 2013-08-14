---
layout: post
category: tips
tags: github fswiki tips javascript
title: FSWikiのページをGitHub Pagesに転送する
---

## 概要

[FSWiki]のクエリとして渡されるページ名で、GitHub Pagesのページに
リダイレクトする方法です。

以下の方法で一括変換したFSWikiのページを想定しています。

* [FSWikiのページを一括でMarkdownに変換する](/tips/convert-fswiki-to-markdown)

## 環境

* [FSWiki] 3.6.4
* [GitHub Pages] (2013.8現在)

## 課題

FSWikiのページ名は、URLのQuery String、つまり `?` の後ろに書かれますが、
GitHub Pagesで使われているJekyllではページ名は静的なパスとして生成されます。

また、最近のWebページではURLもUTF-8でエンコードするのが一般的ですが、FSWikiではページ名はEUCでエンコードされたものをURLEncodeしてあります。

さらに、GitHub Pagesではサーバ側でロジックを動かすことができません。

このあたりを考慮して、ブラウザ内のみでうまく対象のページにリダイレクトしてやる必要があります。

これだとGoogleからのリンクや[Zenback]などを機械的にリダイレクトすることができませんが、
GitHub PagesではHTTP Headerは変えられないので、気長に再インデックスを待ちましょう。

## 方法

やり方は単純で、まず[JavaScriptから文字コード変換ができるライブラリ](#ref)をロード。

    <script src="/assets/js/encoding.js">
    </script>

トップページのJavaScriptでQuery Stringの有無を調べます。

    <script type="text/javascript">
    (function(){
      var url = location.href;
      if (url.match(/.*\/\?page=(.+)/)) {

ページが指定されていればURLDecodeの後、文字コード変換を行なって、

        var decoded = Encoding.urlDecode(RegExp.$1);
        var utf8title = Encoding.convert(decoded, 'UTF8', 'EUCJP');

再度URLEncodeしてスラッシュをハイフンに変換後、

        var newurl = '/' + Encoding.urlEncode(utf8title).replace(/%2F/g, "-");

新しいURLに転送してやります。
URLは相対URLで大丈夫です。

        location.href = newurl;
      }
    })();
    </script>

## 参考
{: #ref}

* [JavaScriptで文字コード変換ライブラリ作ってみた](http://polygon-planet-log.blogspot.jp/2012/04/javascript.html)
