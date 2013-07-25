---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Windows上で、<a href="http://hive.apache.org/">Hive</a>を動かす方法のメモ。</p>
<h3>環境</h3>
<ul>
<li>Windows Vista</li>
<li><a href="http://cygwin.com/">Cygwin</a> 1.7.7</li>
<li><a href="http://java.sun.com/j2se/">JDK</a> 1.6.0_13</li>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.20.2</li>
<li><a href="http://hive.apache.org/">Hive</a> 0.5.0</li>
<li>Ant 1.7.1</li>
</ul>
<h3>手順</h3>
<h4><a href="http://hadoop.apache.org/core/">Hadoop</a>のインストール、起動</h4>
<p>まずは<a href="http://hadoop.apache.org/core/">Hadoop</a>をインストールして、HDFS, MapReduce共に起動します。</p>
<ul>
<li><a href="/?page=Hadoop%2FWindows%BE%E5%A4%C7%A4%CE%BC%C2%B9%D4%280%2E20%2E2%29" class="wikipage">Hadoop/Windows上での実行(0.20.2)</a></li>
</ul>
<p>今のところ、<a href="http://hadoop.apache.org/core/">Hadoop</a> 0.21系には対応していないので注意が必要です。</p>
<h4><a href="http://hive.apache.org/">Hive</a>の展開</h4>
<p><a href="http://hive.apache.org/">Hive</a>はソース付きのdevパッケージをダウンロードして、任意の場所に展開します。</p>
<h4>パッチを当てる</h4>
<p><a href="http://hive.apache.org/">Hive</a>の</p>
<pre>src/ql/src/java/org/apache/hadoop/hive/ql/exec/Utilities.java
</pre>
<p>を編集して、getMapRedWorkメソッドを以下のように修正します。</p>
<pre> public static mapredWork getMapRedWork (Configuration job) \{
   mapredWork gWork = null;
   try \{
     synchronized(gWorkMap) \{
       gWork = gWorkMap.get(getJobName(job));
     \}
     if(gWork == null) \{
       synchronized (Utilities.class) \{
         if(gWork != null)
           return (gWork);
	  Path planPath = new Path(HiveConf.getVar(job, HiveConf.ConfVars.PLAN));
	  FileSystem fs = planPath.getFileSystem(job);
	  InputStream in = fs.open(planPath);
//          InputStream in = new FileInputStream(&quot;HIVE_PLAN&quot;
//            +sanitizedJobId(job));
         mapredWork ret = deserializeMapRedWork(in, job);
         gWork = ret;
         gWork.initialize();
         gWorkMap.put(getJobName(job), gWork);
       \}
     \}
     return (gWork);
   \} catch (Exception e) \{
     e.printStackTrace();
     throw new RuntimeException (e);
   \}
 \}
</pre>
<p>要は、キャッシュへのシンボリックリンクを当てにせず、通常の方法でクエリプランを読み込むように修正します。</p>
<h4>antを実行</h4>
<p>srcフォルダ内で</p>
<pre>ant package
</pre>
<p>を実行して、修正したソースからjarを作成します。Proxyがある場合は、build.xmlを修正してProxyを設定します。</p>
<ul>
<li><a href="/?page=Java%2FAnt%A4%CE%BD%E8%CD%FD%A4%C7Proxy%A4%F2%CD%F8%CD%D1%A4%B9%A4%EB" class="wikipage">Java/Antの処理でProxyを利用する</a></li>
</ul>
<h4>jarをコピー</h4>
<p>src/build/dist/lib内にjarファイルができるので、</p>
<pre>cp src/build/dist/lib/* lib/
</pre>
<p>というように、lib内にコピーします。</p>
<h4><a href="http://hive.apache.org/">Hive</a>を利用</h4>
<p>あとは、以下のように<a href="http://hive.apache.org/">Hive</a>を起動すれば利用出来るようになります。</p>
<pre>HADOOP_HOME=c:\somewhere\hadoop-0.20.2 bash bin/hive
</pre>
<p>HADOOP_HOMEは環境変数に指定しておくと、毎回指定する必要はなくなります。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
