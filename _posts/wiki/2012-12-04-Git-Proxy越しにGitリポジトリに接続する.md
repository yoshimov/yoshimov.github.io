---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://git-scm.com/">Git</a> 1.6.0.4</li>
<li>stone 2.1d</li>
</ul>
<h3>概要</h3>
<p>git://から始まる<a href="http://git-scm.com/">Git</a>リポジトリは、HTTP Proxyがあるとそのままではアクセスできませんが、stoneを使って無理矢理利用する方法です。</p>
<p>(2012.12)最近は<a href="https://github.com/">GitHub</a>もhttpsアクセスができるので、普通にhttps_proxyを設定しておけばProxy越えができます。便利になりました。</p>
<h3>手順</h3>
<ul>
<li>stoneの用意<ul>
<li>以下のページなどからstoneのソースを持ってきてビルド</li>
<li><a href="http://www.gcd.org/sengoku/stone/">http://www.gcd.org/sengoku/stone/</a></li>
</ul>
<li>stoneの起動</li>
</ul>
<p>接続先がsomewhereの場合、</p>
<pre>stone proxyserver:8080/http 9418 &quot;CONNECT somewhere:9418 HTTP/1.0&quot;
</pre>
<p>などと実行する。</p>
<ul>
<li>gitでアクセス</li>
</ul>
<p>あとは、</p>
<pre>git clone git://stoneserver/project.git
</pre>
<p>などとして、stoneを起動しているマシンに対してgitで接続すれば良い。</p>
<h3>参考</h3>
<ul>
<li><a href="http://wiki.spc.gr.jp/tunnel/?DigByStone">stoneで穴掘り</a></li>
</ul>
