---
layout: post
category: tips
tags: tips windows vagrant docker proxy
title: WindowsのVagrant上でDockerを使う
---
{% include keywords.md %}

## 概要

Windows上でVagrantを使ったVM上でDockerを使う方法です。
例によって[Chocolatey]を使います。

## 環境

* Windows 7 Professional SP1
* [VirtualBox] 4.3.6
* [Vagrant] 1.4.3
* [Docker] 0.7.5

## 手順

まずは[Chocolatey]で[VirtualBox]と[Vagrant]をインストールします。

    > cinst virtualbox
    > cinst vagrant

Proxy環境の場合は、Vagrant用のProxyプラグインもインストールします。

    > vagrant plugin install vagrant-proxyconf

Proxyの設定は、以下のファイルをWindowsのユーザディレクトリの
`~/.vagrant.d/Vagrantfile`
として保存しておきます。

    Vagrant.configure("2") do |config|
      if Vagrant.has_plugin?("vagrant-proxyconf")
        config.proxy.http     = "http://hoge:8080/"
        config.proxy.https    = "http://hoge:8080/"
        config.proxy.no_proxy = "localhost,127.0.0.1"
      end
    end

DockerのVagrantfileを用意して、VMを起動します。

    > mkdir docker; cd docker
    > wget https://raw.github.com/dotcloud/docker/master/Vagrantfile
    > vagrant up

うまくいくとDockerが使えるVMが起動しますが、
Proxy環境では、2014/1/15時点では
DockerのサーバにProxyの設定が反映されないので、
手動でサーバを起動しなおします。

    > vagrant ssh
    > sudo service docker stop
    > sudo docker -d &

あとは、普通にDockerのコマンドが使えるようになります。

    > docker run ubuntu /bin/echo hello

## 参考

* [仮想環境構築に docker を使う](http://apatheia.info/blog/2013/06/17/docker/)
* [vagrant-proxyconf](https://github.com/tmatilai/vagrant-proxyconf)
