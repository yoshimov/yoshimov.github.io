---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.20.2をWindows上で起動する方法です。0.20からはWindowsサポートも充実してきたので、パッチあてなどは不要になりました。</p>
<h3>環境</h3>
<ul>
<li>Windows Vista</li>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.20.2</li>
<li><a href="http://cygwin.com/">Cygwin</a> 1.7.7</li>
<li>JRE 1.6.0_13</li>
</ul>
<h3>手順</h3>
<h4>Javaのインストール</h4>
<p>OracleからJREをダウンロードしてインストールします。インストール先を、JAVA_HOME環境変数に設定しておきます。</p>
<h4><a href="http://cygwin.com/">Cygwin</a>のインストール</h4>
<p>通常通り、<a href="http://cygwin.com/">Cygwin</a>をインストールします。インストール先はどこでも問題ありません。/bin, /usr/binへのPathは通しておきます。</p>
<h4><a href="http://hadoop.apache.org/core/">Hadoop</a>の展開</h4>
<p>まずはtar.gzをダウンロードしてきて、任意の場所に展開します。Program Files以外の場所のほうが扱いやすいです。</p>
<h4>バッチファイルの修正</h4>
<p>bin/hadoopを編集して、</p>
<pre>JAVA_PLATFORM=`CLASSPATH=${CLASSPATH} ${JAVA} -Xmx32m org.apache.hadoop.util.PlatformName | sed -e &quot;s/ /_/g&quot;`
</pre>
<p>という行を、</p>
<pre>JAVA_PLATFORM=`CLASSPATH=&quot;${CLASSPATH}&quot; &quot;${JAVA}&quot; -Xmx32m org.apache.hadoop.util.PlatformName | sed -e &quot;s/ /_/g&quot;`
</pre>
<p>と修正します。（ダブルクォートを加える）</p>
<h4>設定ファイルの編集</h4>
<ul>
<li>conf/core-site.xml</li>
</ul>
<pre>&lt;configuration&gt;
&lt;property&gt;
	&lt;name&gt;fs.default.name&lt;/name&gt;
	&lt;value&gt;hdfs://hoge:9000&lt;/value&gt;
&lt;/property&gt;
&lt;/configuration&gt;
</pre>
<p>という感じに設定します。ホスト名は、必ず全ての<a href="http://hadoop.apache.org/core/">Hadoop</a>クラスタから解決可能なマスタサーバの名前である必要があります。</p>
<ul>
<li>conf/hdfs-site.xml</li>
</ul>
<pre>&lt;configuration&gt;
&lt;property&gt;
	&lt;name&gt;dfs.replication&lt;/name&gt;
	&lt;value&gt;1&lt;/value&gt;
&lt;/property&gt;
&lt;property&gt;
	&lt;name&gt;dfs.support.append&lt;/name&gt;
	&lt;value&gt;true&lt;/value&gt;
&lt;/property&gt;
&lt;/configuration&gt;
</pre>
<p>という感じに設定します。もちろん、クラスタのDataNodeが多い場合は、3などに設定して問題ありません。</p>
<ul>
<li>conf/mapred-site.xml</li>
</ul>
<pre>&lt;configuration&gt;
&lt;property&gt;
	&lt;name&gt;mapred.job.tracker&lt;/name&gt;
	&lt;value&gt;localhost:9001&lt;/value&gt;
&lt;/property&gt;
&lt;/configuration&gt;
</pre>
<p>のようにします。これもHDFS同様、他のマシンから解決可能なマスターサーバのマシン名を指定します。</p>
<h4>サーバの起動</h4>
<p>あとは各サーバを起動するだけです。Linuxと同じようにsshで起動しても良いですが、以下のように手動で起動するのが楽です。</p>
<ul>
<li>NameNodeの起動</li>
</ul>
<p><a href="http://hadoop.apache.org/core/">Hadoop</a>のインストール先にCDした後、</p>
<pre>bash bin/hadoop namenode -format
bash bin/hadoop-daemon.sh start namenode
</pre>
<p>と実行します。２回目からは -format は不要です。</p>
<ul>
<li>DataNodeの起動</li>
</ul>
<pre>bash bin/hadoop-daemon.sh start datanode
</pre>
<ul>
<li>JobTrackerの起動</li>
</ul>
<pre>bash bin/hadoop-daemon.sh start jobtracker
</pre>
<ul>
<li>TaskTrackerの起動</li>
</ul>
<pre>bash bin/hadoop-daemon.sh start tasktracker
</pre>
<p>マスタサーバで必須なのはNameNodeとJobTracker、スレーブでは任意でDataNodeとTaskTrackerを起動します。各サーバの起動タイミングはある程度前後しても問題ありません。</p>
<h4>サービスとして起動</h4>
<p>core-site.xmlに以下の設定を追加。</p>
<pre>&lt;property&gt;
 &lt;name&gt;hadoop.tmp.dir&lt;/name&gt;
 &lt;value&gt;/tmp/hadoop&lt;/value&gt;
 &lt;description&gt;ユーザによって作業ディレクトリが変わらないように&lt;/description&gt;
&lt;/property&gt;
</pre>
<p>hdfs-site.xmlに以下の設定を追加。</p>
<pre>&lt;property&gt;
 &lt;name&gt;dfs.permissions&lt;/name&gt;
 &lt;value&gt;false&lt;/value&gt;
 &lt;description&gt;Jobをシステム以外のユーザが投入できるように&lt;/description&gt;
&lt;/property&gt;
</pre>
<p>通常通りformatした後、<a href="/?page=Hadoop%2FWindows%BE%E5%A4%C7%A4%CE%BC%C2%B9%D4%280%2E16%2E3%29" class="wikipage">0.16.3</a>と同様、</p>
<pre>cygrunsrv --install HadoopNamenode --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop namenode&quot;
cygrunsrv --install HadoopJobtracker --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop jobtracker&quot;
cygrunsrv --install HadoopDatanode --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop datanode&quot;
cygrunsrv --install HadoopTasktracker --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop tasktracker&quot;
</pre>
<p>などとしてサービスを登録。</p>
<h4><a href="http://hadoop.apache.org/core/">Hadoop</a>を利用</h4>
<p>あとは、どこかにインストールした<a href="http://hadoop.apache.org/core/">Hadoop</a>から</p>
<pre>bash bin/hadoop fs -ls /
</pre>
<p>などとしてコマンドを発行すれば利用できます。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
