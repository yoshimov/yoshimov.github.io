---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10以降に、最新のWineを入れる方法のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 10.10</li>
</ul>
<h3>手順</h3>
<ul>
<li>PPA repositoryの名前を調べる。</li>
</ul>
<p>ここではWineのパッケージなので、</p>
<ul>
<ul>
<li><a href="https://launchpad.net/~ubuntu-wine/+archive/ppa">https://launchpad.net/~ubuntu-wine/+archive/ppa</a></li>
</ul>
</ul>
<p>を開いて、PPA repositoryの名前を調べます。Wineは</p>
<pre>ppa:ubuntu-wine/ppa
</pre>
<p>となっています。</p>
<ul>
<li>PPA repository を追加</li>
</ul>
<p>ターミナルで、</p>
<pre>sudo add-apt-repository ppa:ubuntu-wine/ppa
</pre>
<p>と実行すると、リポジトリが追加されます。</p>
<ul>
<li>APTのキャッシュを更新</li>
</ul>
<pre>sudo aptitude update
</pre>
<ul>
<li>最新のWineをインストール</li>
</ul>
<pre>sudo aptitude search wine
</pre>
<p>などとして、最新のWineパッケージを検索して、</p>
<pre>sudo aptitude install wine1.3
</pre>
<p>とインストールすれば、終了です。</p>
