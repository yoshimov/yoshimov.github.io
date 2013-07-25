---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://java.sun.com/j2se/">JDK</a> 1.6.0_05</li>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.17.0</li>
</ul>
<h3>Java APIからの利用</h3>
<h4>HDFSへの接続</h4>
<pre>Configuration conf = new Configuration();
FileSystem fs = FileSystem.get(URI.create(&quot;hdfs://hoge:9000/&quot;), conf);
</pre>
<p>としてやると、FileSystemが取得できるので、これに対して、</p>
<pre>FileStatus status = fs.getFileStatus(new Path(&quot;work/input&quot;))
</pre>
<p>などとする。</p>
<h4>ファイルの一覧取得</h4>
<p>一覧は、listStatusを使って、</p>
<pre>FileStatus[] statusList = fs.listStatus(new Path(&quot;work&quot;))
</pre>
<p>という感じでリストを取得して、</p>
<pre>for (FileStatus status: statusList) \{
 if (status.isDir()) \{
  // ディレクトリの処理
 \} else \{
  // ファイルの処理
 \}
</pre>
<p>という感じで処理する。</p>
<h4>ファイルの読み込み</h4>
<p>読み込みは、</p>
<pre>InputStream is = fs.open(new Path(&quot;work/hoge&quot;))
</pre>
<p>というようにInputStream経由で行う。</p>
<h4>SequenceFileの読み込み</h4>
<p>SequenceFileはMapReduceの結果をそのままオブジェクトで出力できるので重宝しますが、これの読み込みの場合は、</p>
<pre>SequenceFile.Reader reader = new SequenceFile.Reader(fs, path, fs.getConf());
Writable key = new KeyWritable()
Writable value = new ValueWritable()
while (reader.next(key, value)) \{
 ..
\}
</pre>
<p>という感じで行う。</p>
