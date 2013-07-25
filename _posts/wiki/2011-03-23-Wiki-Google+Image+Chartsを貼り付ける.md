---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://code.google.com/intl/ja/apis/chart/">Google Image Charts</a>のグラフをWikiに貼り付ける方法です。</p>
<h3>環境</h3>
<ul>
<li>2011.3時点の<a href="http://code.google.com/intl/ja/apis/chart/">Google Image Charts</a> API</li>
<li><a href="http://fswiki.poi.jp/">FSWiki</a> 3.6.3</li>
</ul>
<h3>手順</h3>
<p><a href="http://fswiki.poi.jp/">FSWiki</a>はURLの拡張子でイメージかどうかを判定していますので、基本的にURLに.pngを加えればイメージとして貼りつけられます。その際に、Wiki記法で使われている文字はURLエンコードするようにします。</p>
<p>具体的には、</p>
<pre>{ -&gt; %7b
} -&gt; %7d
| -&gt; %7c
[ -&gt; %5b
] -&gt; %5d
</pre>
<p>という感じです。また、.pngを付けるとグラフの表示が変わってしまう場合は、&amp;.pngとします。</p>
<p>例えば、こんなURLの場合は、</p>
<pre>http://chart.googleapis.com/chart?cht=v&amp;chs=250x150&amp;chd=t:100,20,20,20&amp;chdl=Follow|Friends|News
</pre>
<p>こんな風に書き換えます。</p>
<pre>http://chart.googleapis.com/chart?cht=v&amp;chs=250x150&amp;chd=t:100,20,20,20&amp;chdl=Follow%7cFriends%7cNews&amp;.png
</pre>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
