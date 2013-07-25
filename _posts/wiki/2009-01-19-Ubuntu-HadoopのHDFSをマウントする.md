---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10</li>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a> 0.18.0</li>
</ul>
<h3>概要</h3>
<p><a href="http://hadoop.apache.org/core/">Hadoop</a>のcontribに、HDFSをfuseを使ってマウントするツールがありますので、これを使う方法です。</p>
<h3>準備</h3>
<ul>
<li>必要なツールのインストール</li>
</ul>
<pre>sudo aptitude install default-jdk ant
sudo aptitude install automake autoconf libfuse-dev
</pre>
<ul>
<li>環境変数を設定</li>
</ul>
<pre>cd
vi .bashrc
</pre>
<p>として、以下の行を追記</p>
<pre>export JAVA_HOME=/usr/lib/jvm/default-java
</pre>
<p>環境変数を有効にする</p>
<pre>source .bashrc
</pre>
<ul>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a>を展開</li>
</ul>
<pre>cd
tar zxvf hadoop-0.19.0.tar.gz
</pre>
<ul>
<li>fusedfsをビルド</li>
</ul>
<pre>cd hadoop-0.19.0
ant compile-libhdfs -Dlibhdfs=1
cp build/libhdfs/* libhdfs/
ant compile-contrib -Dlibhdfs=1 -Dfusedfs=1
</pre>
<ul>
<li>wrapperを編集</li>
</ul>
<pre>mkdir -p contrib/fuse-dfs
cp src/contrib/fuse-dfs/src/fuse_dfs contrib/fuse-dfs/
cp src/contrib/fuse-dfs/src/fuse_dfs_wrapper.sh contrib/fuse-dfs/
cd contrib/fuse-dfs
vi fuse_dfs_wrapper.sh
</pre>
<p>として、HADOOP_HOMEを展開先パスに修正して、以下のようにexportを行の先頭に追加。</p>
<pre>export HADOOP_HOME=/home/hoge/hadoop-0.18.0
export CLASSPATH=$CLASSPATH:$f
</pre>
<p>OS_ARCH, JAVA_HOME, LD_LIBRARY_PATHの行を以下のように変更する。</p>
<pre>export OS_ARCH=i386
export JAVA_HOME=/usr/lib/jvm/default-java
export LD_LIBRARY_PATH=$JAVA_HOME/jre/lib/$OS_ARCH/server:$HADOOP_HOME/libhdfs:/usr/local/lib
</pre>
<ul>
<li>HDFSを起動<ul>
<li><a href="http://hadoop.apache.org/core/">Hadoop</a>をインストールした環境を立ち上げる</li>
</ul>
<li>HDFSをマウント</li>
</ul>
<pre>cd ~/hadoop-0.18.0/contrib/fuse-dfs
sudo mkdir -p /mnt/hdfs
sudo ./fuse_dfs_wrapper.sh dfs://hadoopserver:9000 /mnt/hdfs
</pre>
