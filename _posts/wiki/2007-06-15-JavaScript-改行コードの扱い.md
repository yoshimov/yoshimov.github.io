---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>IEのJavaScriptで、改行を含む文字列を扱う際の注意事項。div等の通常タグ内に入っている文字列をinnerHTMLで取得すると、改行が空白文字に変換されてしまう。</p>
<p>例えば以下のようなHTMLがある場合、</p>
<pre>&lt;div id=&quot;test&quot;&gt;line1
line2
&lt;/div&gt;
</pre>
<p>以下のようにすると、</p>
<pre>var obj1 = document.getElementById(&quot;test&quot;);
var str1 = obj1.innerHTML;
</pre>
<p>取得できる文字列は以下のようになる。</p>
<pre>line1 line2 (パターン１)
</pre>
<p>改行コードは全くなくなる。</p>
<p>これをtextareaタグにして、</p>
<pre>&lt;textarea id=&quot;test2&quot;&gt;line1
line2
&lt;/textarea&gt;
</pre>
<p>以下のようにすると、</p>
<pre>var obj2 = document.getElementById(&quot;test2&quot;);
var str2 = obj2.value;
</pre>
<p>取得できる文字列は以下のようになる。（ただし改行は\r\n）</p>
<pre>line1\n
line2\n （パターン２）
</pre>
<p>文字列の取得方法は、</p>
<pre>var str2 = obj2.innerHTML;
</pre>
<p>としてもパターン２。セットの際は、</p>
<pre>obj2.innerHTML = str2;
</pre>
<p>とするとパターン１になってしまう。</p>
<pre>obj2.value = str2;
</pre>
<p>でパターン２を維持できる。</p>
<p><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a>ではどの方法でもパターン２になる。</p>
<h3>ブラウザ</h3>
<ul>
<li>IE 6.0</li>
<li><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a> 2.0.0.4</li>
</ul>
