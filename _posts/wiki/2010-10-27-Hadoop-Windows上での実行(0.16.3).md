---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Windowsはまだサポートしていないと書いてありましたが、<a href="http://cygwin.com/">Cygwin</a>用のコードは入っていますし、Javaですから起動さえできれば使えました。</p>
<h3>環境</h3>
<ul>
<li>Windows Vista Enterprise SP1</li>
<li>Apache <a href="http://hadoop.apache.org/core/">Hadoop</a> 0.16.3</li>
<li><a href="http://java.sun.com/j2se/">JDK</a> 1.6.0_05</li>
</ul>
<h3>手順</h3>
<h4>インストール</h4>
<ul>
<li><a href="http://cygwin.com/">Cygwin</a>をインストール</li>
<li><a href="http://cygwin.com/">Cygwin</a>の/binにパスを通す</li>
<li>JAVA_HOMEを設定しておく</li>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a>を任意の場所に展開</li>
</ul>
<h4>Standaloneサンプルの実行</h4>
<ul>
<li>conf/hadoop-site.xmlを以下のように空にする</li>
</ul>
<pre>&lt;configuration&gt;
&lt;/configuration&gt;
</pre>
<ul>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a>を展開したフォルダで以下のように実行</li>
</ul>
<pre>mkdir input
cp conf/*.xml input
bash bin/hadoop jar hadoop-0.16.1-examples.jar wordcount input output
cat output/*
</pre>
<h4>１台のPC上で、DFS, jobtrackerを使って実行</h4>
<ul>
<li>conf/hadoop-site.xmlを以下のように変更。</li>
</ul>
<p>複数マシンで実行する場合は、NameNode側の設定とDataNode側の設定を同じにすること。つまり、localhost等とはかかず、マシン名やIPアドレス指定にする。</p>
<pre>&lt;configuration&gt;
 &lt;property&gt;
   &lt;name&gt;fs.default.name&lt;/name&gt;
   &lt;value&gt;localhost:9000&lt;/value&gt;
 &lt;/property&gt;
 &lt;property&gt;
   &lt;name&gt;mapred.job.tracker&lt;/name&gt;
   &lt;value&gt;localhost:9001&lt;/value&gt;
 &lt;/property&gt;
 &lt;property&gt;
   &lt;name&gt;dfs.replication&lt;/name&gt;
   &lt;value&gt;1&lt;/value&gt;
 &lt;/property&gt;
&lt;/configuration&gt;
</pre>
<ul>
<li>以下のようにデーモンを起動。Vistaの場合は管理者権限で実行する必要がある。</li>
</ul>
<pre>bash bin/hadoop namenode -format
start bash bin/hadoop namenode
start bash bin/hadoop datanode
start bash bin/hadoop jobtracker
start bash bin/hadoop tasktracker
</pre>
<ul>
<li>以下のようにexampleを実行</li>
</ul>
<pre>bash bin/hadoop dfs -mkdir input
bash bin/hadoop dfs -put conf/hadoop-default.xml input
bash bin/hadoop jar hadoop-0.16.1-examples.jar wordcount input output
bash bin/hadoop dfs -cat output/*
</pre>
<p>以下のページから、DFSとMap/Reduceの実行状況が確認できる</p>
<pre>http://localhost:50070/
http://localhost:50030/
</pre>
<h4>複数台のPC上で実行</h4>
<p>複数台利用する場合は、マスタとするPC上で、</p>
<pre>start bash bin/hadoop namenode
start bash bin/hadoop jobtracker
</pre>
<p>と実行し、その他のデータノードを実行するPC上で、</p>
<pre>start bash bin/hadoop datanode
start bash bin/hadoop tasktracker
</pre>
<p>と実行する。</p>
<h3>サービス化</h3>
<h4>パッチを当てる</h4>
<p>Namenode, Jobtrackerはそのままではユーザ名の取得でエラーになってしまい起動できないので、</p>
<pre>org.apache.hadoop.security.UnixUserGroupInformation#getUnixUserName()
</pre>
<p>を、</p>
<pre> static String getUnixUserName() throws IOException {
   String[] result = executeShellCommand(
       new String[]{Shell.USER_NAME_COMMAND});
   return toString(result);
 }
</pre>
<p>のように変更して、jarにパッチを当てておく。＃以前のパッチは、ユーザ名に改行が入ってしまっていたので、修正。</p>
<h4>設定変更</h4>
<p>hadoop-site.xmlに以下の設定を追加。</p>
<pre>&lt;property&gt;
 &lt;name&gt;hadoop.tmp.dir&lt;/name&gt;
 &lt;value&gt;/tmp/hadoop&lt;/value&gt;
 &lt;description&gt;ユーザによって作業ディレクトリが変わらないように&lt;/description&gt;
&lt;/property&gt;
&lt;property&gt;
 &lt;name&gt;dfs.permissions&lt;/name&gt;
 &lt;value&gt;false&lt;/value&gt;
 &lt;description&gt;Jobをシステム以外のユーザが投入できるように&lt;/description&gt;
&lt;/property&gt;
</pre>
<h4>サービス登録</h4>
<p>master上で、以下のように実行して、サービスをインストールする。</p>
<pre>cygrunsrv --install HadoopNamenode --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop namenode&quot;
cygrunsrv --install HadoopJobtracker --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop jobtracker&quot;
</pre>
<p>slave上で、以下のようにサービスをインストールする。</p>
<pre>cygrunsrv --install HadoopDatanode --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop datanode&quot;
cygrunsrv --install HadoopTasktracker --path c:\cygwin\bin\bash.exe --chdir c:\hadoop --args &quot;bin/hadoop tasktracker&quot;
</pre>
<p>あとはそれぞれのサービスを起動すれば良い。</p>
<p>Windowsファイアウォール等が有効になっている場合は、ブロック確認を行う必要があるため、初回起動時はサービスではなく、コマンドラインから起動したほうが良い。</p>
