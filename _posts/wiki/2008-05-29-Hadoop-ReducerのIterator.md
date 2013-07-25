---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.17.0</li>
<li><a href="http://java.sun.com/j2se/">JDK</a> 1.6.0_05</li>
</ul>
<h3>Iteratorから取得できるオブジェクト</h3>
<p>Reducerのreduceメソッドには、</p>
<pre>public void reduce(KeyWritable key,
Iterator&lt;ValueWritable&gt; it,
OutputCollector&lt;KeyWritable, ValueWritable&gt; output,
Reporter report) throws IOException \{
</pre>
<p>のような感じで、valueのiteratorが渡されるが、</p>
<pre>it.next()
</pre>
<p>で順次取れるオブジェクトは、基本的に同じオブジェクトが使いまわされている。</p>
<p>なので、</p>
<pre>ValueWritable first = it.next();
ValueWritable second = it.next();
</pre>
<p>としても、first == second (オブジェクトとして同じ) であることに注意。</p>
