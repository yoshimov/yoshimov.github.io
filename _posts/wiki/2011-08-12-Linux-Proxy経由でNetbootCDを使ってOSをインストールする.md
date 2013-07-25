---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://netbootcd.tuxfamily.org/">NetbootCD</a>を使って，Proxyの内側からOSをネットワークインストールする方法のメモ．</p>
<p>OS自体がProxy経由でのネットワークインストールに対応している必要があります．</p>
<h3>環境</h3>
<ul>
<li><a href="http://netbootcd.tuxfamily.org/">NetbootCD</a> 3.2.1</li>
</ul>
<h3>手順</h3>
<ul>
<li>まずは<a href="http://netbootcd.tuxfamily.org/">NetbootCD</a>を起動します．<a href="/?page=Linux%2F%CA%A3%BF%F4OS%A4%F2%B5%AF%C6%B0%A4%C7%A4%AD%A4%EB%A5%E9%A5%A4%A5%D6USB%A4%CE%BA%EE%C0%AE" class="wikipage">isobooster</a>からでも可．</li>
<li>メニューからコマンドプロンプトに入る．</li>
<li>以下のコマンドを打つ</li>
</ul>
<pre>sudo su
export http_proxy=http://proxy.somewhere:8080/
netboot
</pre>
<ul>
<li>あとは，最新のスクリプトをダウンロードしてOSをインストールする．</li>
</ul>
<p>ポイントはsudo suした後にProxyを指定するという点です．</p>
