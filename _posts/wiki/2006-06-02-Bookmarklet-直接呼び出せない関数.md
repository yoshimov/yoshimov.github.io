---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Bookmarklet内では、返り値のある関数を直接呼び出すと、カレントページが変わってしまう。</p>
<p>これを防ぐには、以下のように void() で囲む必要がある。</p>
<pre>void(window.open('...'))
</pre>
<p>直接呼び出せないのは、上記 window 関連メソッド、location関連メソッド、文字列操作メソッドなど。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
