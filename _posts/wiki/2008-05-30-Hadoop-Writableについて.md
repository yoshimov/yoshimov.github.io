---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.17.0</li>
</ul>
<h3>Writableとは</h3>
<p><a href="http://hadoop.apache.org/core/">Hadoop</a>では、keyとvalueのペアを大規模分散処理するが、そのどちらもWritableというインタフェースを実装したクラスとする必要がある。これは、ノード間でkey, valueの転送を行う際に、Serialize, Deserializeを行うため。</p>
<h3>Writableの作り方</h3>
<p>keyに使うクラスは、WritableComparatableを実装し、valueで使用するクラスは、Writableを実装する必要がある。</p>
<p>WritableComparableはGenericに対応していないため、compareToの引数は常にObjectとする必要がある。valueのほうは、Comparableは必須ではないため、Comparable&lt;HogeClass&gt; などのインタフェースを実装することで、compareToの引数に、型制限を加えることが可能。</p>
<p>Reducerが複数の場合にMapの結果を振り分ける処理（shuffle）が行われるが、この際にkeyのhashCodeが利用されるため、同じkeyは同じhashCodeを返すように、hashCode()をオーバーライドしておく必要がある。</p>
