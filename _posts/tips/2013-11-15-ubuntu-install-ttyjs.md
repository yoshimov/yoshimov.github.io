---
layout: post
category: tips
tags: ubuntu linux tips nodejs
title: Ubuntu環境でtty.jsを使う
---
{% include keywords.md %}

## 概要

Ubuntu環境に[tty.js]を入れる方法です。
非常に簡単ですが全体の手順がまとまったものがなかったので。

## 環境

* Ubuntu 13.10
* [tty.js] 0.2.13

## 手順

まずはnode.jsとnpmをインストールします。

    > sudo aptitude install nodejs npm

次にtty.jsをインストールします。

    > cd ~
    > sudo npm install tty.js

カレントにnode_modulesというフォルダができるので、
以下の様な内容のconf.jsonを作成して、

<pre>
{
  "shell": "bash",
  "users": {
    "user": "password"
  },
  "port": 8080
}
</pre>

以下のようにしてtty.jsを起動します。

    > ./node_modules/tty.js/bin/tty.js --config ~/conf.json --daemonize

後はブラウザから8080ポートに接続すると、ターミナルを開けます。

設定ファイルなしでも起動しますが、認証なしでターミナルが開けてしまうので、
最低でもパスワードは設定したほうが良いかと思います。

## 参考

* [Github tty.js](https://github.com/chjj/tty.js/)
