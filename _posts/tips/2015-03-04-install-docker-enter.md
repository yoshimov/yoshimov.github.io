---
layout: post
category: tips
tags: tips docker enter
title: Docker-enterのインストール
---

## 概要

DockerイメージはDockerfileで作成するのが基本ですが、
標準出力以外のログファイルを確認したり、
Jenkinsのように基本のビルド環境をカスタマイズしたいなど、
コンテナ内で何か作業がしたくなった時に使うコマンドの入れ方のメモです。

## 環境

- Docker 1.3.1
- Ubuntu 14.10 (Host)

## 手順

nsenterのイメージをpullしてきます。

    docker pull jpetazzo/nsenter

コマンドをインストールします。

    docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter

envコマンドの実行がエラーになる場合があるので、`/usr/local/bin/docker-enter` を編集して、
以下の様な行を、

    $LAZY_SUDO "$NSENTER" $OPTS env -i - $ENV su -m root
    $LAZY_SUDO "$NSENTER" $OPTS env -i - $ENV "$@"

以下のように編集します。要するに`env -i -`の部分を削除します。

    $LAZY_SUDO "$NSENTER" $OPTS su -m root
    $LAZY_SUDO "$NSENTER" $OPTS $ENV "$@"

あとは、起動中のdockerコンテナの名前を指定して、

    docker-enter <コンテナ名>

とすると、コンテナ内でシェルが使えるようになります。

## 参考

- [nsenter in a can](https://github.com/jpetazzo/nsenter)
