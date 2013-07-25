---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>MySQL Clusterを使う上での注意点です。MySQL 5.0.34を利用しています。</p>
<p>参考:<a href="http://dev.mysql.com/doc/refman/5.1/ja/mysql-cluster-limitations.html">MySQL Cluster の既知の制限</a></p>
<h4>レコードの最大サイズが4096バイト</h4>
<p>１レコードの最大サイズが4096バイトを超えないようにスキーマ設計しないとClusterでは使用できません。</p>
<h4>BLOB, TEXTは使えない</h4>
<p>BLOBやTEXTはVARCHAR等に変更する必要があります。</p>
<h4>インデックスの大きさ、組み合わせに制限がある</h4>
<p>手元の環境では、以下のようなBIGINTとVARCHARを組み合わせた複合インデックスは作れませんでした。</p>
<pre>CREATE INDEX index1 ON hoge (id, text(10));
</pre>
<p>以下のように個別にインデックスにすることはできます。</p>
<pre>CREATE INDEX index2 on hoge (text(20));
</pre>
<h4>データの保存場所</h4>
<p><a href="http://www.debian.org/">Debian</a>ではデフォルトで以下の場所にデータが保存されます。</p>
<pre>/var/lib/mysql-cluster/
</pre>
<p>MySQL Clusterは基本的にメモリ上にデータを持つため、シャットダウン時にファイルが書き出されるようです。</p>
