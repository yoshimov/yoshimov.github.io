---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://grails.org/">Grails</a> 1.1</li>
</ul>
<h3>概要</h3>
<p><a href="http://grails.org/">Grails</a>はプラグインをダウンロードしてインストールする機能がありますが、Proxyが必要な環境では通常のままではインストールできません。</p>
<h3>手順</h3>
<ul>
<li>proxyを設定するコマンドを実行する</li>
</ul>
<pre>grails set-proxy
</pre>
<p>インタラクティブにproxyサーバ等の情報を入力する。</p>
<p>ここで指定した情報は、ホームディレクトリの</p>
<pre>.grails/scripts/ProxyConfig.groovy
</pre>
<p>に保存される。</p>
<ul>
<li>プラグインをインストール</li>
</ul>
<pre>grails install-plugin webtest
</pre>
<p>などとしてプラグインをインストールする。</p>
<p><a href="http://grails.org/">Grails</a> 1.1からはプラグインはホームディレクトリ内にインストールされ、リポジトリにはプラグインの名前とバージョンだけが記載される。</p>
