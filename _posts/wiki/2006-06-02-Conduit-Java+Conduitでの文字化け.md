---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Java Conduit では、いろんなところで文字化けが発生するのは良く知られてます。</p>
<p>私の把握している範囲では、以下の部分で文字化けが発生してました。</p>
<ul>
<li> Conduit に渡されるパス名</li>
<li> Category クラスを使った場合のカテゴリ名</li>
<li> AbstractRecord クラスを使った場合のテキスト部分</li>
</ul>
<p>まぁ言ってみれば、日本語の入る可能性のある部分全部です。</p>
<h4>Conduit に渡されるパス名</h4>
<p>パス名は、Shift JIS のパス名が String に無理矢理変換されて渡されます。しかし、Java 内部での文字コードは全て Unicode ですので当然文字化けします。これを回避するには、一旦文字コード変換なしで byte 配列に変換し、それを JISAutoDetect encoding で再び String にしてやる必要があります。</p>
<pre>byte[] bytes = string.getBytes(&quot;8859_1&quot;);
string = new String(bytes, &quot;JISAutoDetect&quot;);
</pre>
<p>という感じ。</p>
<h4>Category クラスのカテゴリ名、AbstractRecord クラスのテキスト部分</h4>
<p>こっちはもっと深刻で、どちらのクラスも元々 2byte の文字を 1byte ずつ読み込んで、2byte 文字に拡張して String 化するという処理をやってしまってます。</p>
<p>これは、Palm から公開されてるソースにパッチを当てるのが一番手っ取り早いです。</p>
<p>具体的には、文字列の読み込み部分（Category#parseCategories の name を読み込む部分、AbstractRecord#readCString）を以下のように一旦バッファリングするように変更します。</p>
<pre>ByteArrayOutputStream bos = new ByteArrayOutputStream();

do {
  c = in.read();
  if (c != 0)
    bos.write(c);
 } while (c &gt; 0);

 bos.flush();
 bos.close();

 return new String(bos.toByteArray(), &quot;JISAutoDetect&quot;);
</pre>
<p>次の <a href="/?page=JSync" class="wikipage">JSync</a> では改善して欲しいですね。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
