---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Tungsten T では新しく 5 Way Navigator が搭載されている。SDK は<a href="http://spp.palmos.com/web_special_program_redirect/rdr_pavilion_home.html">Palm OS Resource Pavilion</a> の<a href="http://www.palmos.com/alliance/resources.cgi/devseed/">Development Seeding Area</a>からダウンロードできる。</p>
<p>5 Way Navigator の有無は、以下のように Feature Set を調べる。</p>
<pre>UInt32 version;
Err err = FtrGet(navFtrCreator, navFtrVersion, &amp;version);
</pre>
<p>err が出ず、version が 0より上なら存在する。</p>
<p>5 Way Navigator からの KeyDownEvent は、基本的に２つ以上がセットで発生する。</p>
<p>（表略）</p>
<p>基本は、</p>
<ol>
<li>上下ボタンのchrは、従来と同じ。ただし keyCode が変わる。</li>
<li>左右と中央ボタンのchrは全て vchrNavChange となる。</li>
<li>keyCode には、押されたボタンが navBit* で示され、状態の変わったボタンが navChange* で示される。</li>
<li>長押しした場合は、modifier に autoRepeatKeyMask がセットされ、イベントが複数発行される。</li>
</ol>
<p>となる。</p>
<p>明示的な release イベントはないため、keyCode を調べて、以前に押されていたボタンが押されていなければ、release とみなす必要がある。</p>
<p>各ボタンが押されているかどうかを判断するマクロが用意されているため、以下のようなコードで判断が可能。</p>
<pre>if (NavKeyPressed(eventP, Select))
if (NavKeyPressed(eventP, Left))
if (NavKeyPressed(eventP, Right))
if (NavKeyPressed(eventP, Up))
if (NavKeyPressed(eventP, Down))
</pre>
<p>上記マクロは Up, Down に関しては 5 Way Navigator のない機種でも利用可能。</p>
<p>デフォルトでは、中央ボタンを押すと OK ボタン等が押され、中央ボタンの長押しでランチャーに戻る。これは Form の EventHandler で該当イベントを処理することで変更可能。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
