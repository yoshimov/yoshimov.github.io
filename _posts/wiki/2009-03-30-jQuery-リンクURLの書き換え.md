---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a> 3.0.7</li>
<li><a href="http://jquery.com/">jQuery</a> 1.3.2</li>
</ul>
<h3>概要</h3>
<p>ページ中にあるURLを一括して書き換える場合の方法です。</p>
<h3>方法</h3>
<p>例えば一律ベースURLを追加する場合は以下のようにする。</p>
<pre>jQuery(&quot;a&quot;, document.body).each(function() \{
  var obj = jQuery(this);
  var link = obj.attr('href');
  obj.attr('href', &quot;http://somewhere/&quot; + link);
\});
</pre>
<p>大まかにはこんな流れ。</p>
<ul>
<li><a href="http://jquery.com/">jQuery</a>で対象を絞り込み</li>
<li>eachにcallback関数を渡す</li>
<li>callback関数内で<a href="http://jquery.com/">jQuery</a>(this)で対象のオブジェクトを取得</li>
<li>何やらかんやら操作を行う</li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://semooh.jp/jquery/api/core/each/callback/">jQuery each(callback)</a></li>
</ul>
<h3>コメント</h3>
<ul>
<li>何やらかんやらと書くと、33分探偵を思い出して自分で笑ってしまった。蛇足でした。 - <a href="/?page=Yoshimov" class="wikipage">Yoshimov</a> (2009年03月30日 12時04分46秒)</li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
