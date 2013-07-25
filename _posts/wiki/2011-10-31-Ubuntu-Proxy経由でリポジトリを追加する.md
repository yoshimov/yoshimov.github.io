---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>Proxy越しにadd-apt-repositoryなどを使う方法のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 11.10</li>
</ul>
<h3>手順</h3>
<ul>
<li>通常通りproxyを指定する。<ul>
<li>http_proxyなどの環境変数を事前に設定しておきます。</li>
</ul>
<li>sudo visudo で以下の行を追加して保存。</li>
</ul>
<pre>Defaults env_keep=&quot;http_proxy&quot;
Defaults env_keep=&quot;https_proxy&quot;
</pre>
<ul>
<li>入っていなければpython-software-propertiesをインストール。</li>
</ul>
<pre>sudo aptitude install python-software-properties
</pre>
<ul>
<li>add-apt-repositoryで希望のリポジトリをインストール。</li>
</ul>
<pre>sudo add-apt-repository ppa:juju/pkgs
</pre>
<p>これはwgetなどをsudoから使うときも同じように有効です。</p>
<h3>参考</h3>
<ul>
<li><a href="https://bugs.launchpad.net/ubuntu/+source/software-properties/+bug/516032">add-apt-repository doesn't work behind a proxy</a></li>
</ul>
