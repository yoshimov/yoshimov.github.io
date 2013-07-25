---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<p>RSSを機械的に見つけ出すためのRSS auto-discoveryに対応するにはHTMLのhead部に</p>
<pre>&lt;link rel=&quot;alternate&quot; type=&quot;application/rss+xml&quot; title=&quot;(RSS のタイトル)&quot; href=&quot;(RSS フィードの URL)&quot;&gt;
</pre>
<p>という記述を入れれば良い。</p>
<p><a href="http://fswiki.poi.jp/">FSWiki</a>だと、tmpl/site/default/default.tmpl 内のheadタグの内側に</p>
<pre>&lt;link rel=&quot;alternate&quot; type=&quot;application/rss+xml&quot; title=&quot;Yoshimopedia&quot; href=&quot;/wiki.cgi?action=RSS&quot;&gt;
</pre>
<p>という記述を追加する。これで<a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a>などでRSSアイコンが表示されるようになる。</p>
<h3>リンク</h3>
<ul>
<li><a href="http://www.mozilla-japan.org/products/firefox/live-bookmarks.html">ライブブックマークとは(Mozilla)</a></li>
<li><a href="http://www.infomaker.jp/blog/archives/2005/individual/05_10_2343.html">今更ながらもう一度 RSS auto-discovery</a></li>
</ul>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> <span class="error">trackbackプラグインは存在しません。</span> </p>
