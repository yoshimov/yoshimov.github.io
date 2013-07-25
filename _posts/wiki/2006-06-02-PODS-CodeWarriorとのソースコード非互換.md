---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Palm OS Developer Suite (prc-tools)とCodeWarriorとのソースコード非互換について、気が付いた点です。</p>
<h3>一時領域の記述方法</h3>
<p>CodeWarriorでは、</p>
<pre>&amp;(RectangleType){{0,0},{10,10}}
</pre>
<p>のような記述で、一時領域のポインタを渡すことができたんですが、PODSでは、ちゃんと</p>
<pre>RectangleType rect;
rect.topLeft.x = 0;
rect.topLeft.y = 0;
rect.extent.x = 10;
rect.extent.y = 10;
&amp;rect
</pre>
<p>としないと、コンパイラを通りません。真面目に宣言しろということですね。</p>
<h3>プロトタイプ宣言の型が厳格</h3>
<p>CodeWarriorだと、プロトタイプ宣言で引数が</p>
<pre>char *
</pre>
<p>となっていても、実際の引数を</p>
<pre>unsigned char *
</pre>
<p>としても問題ありませんでしたが、PODSではエラーになりました。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
