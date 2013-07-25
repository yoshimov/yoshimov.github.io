---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.debian.org/">Debian</a>用のパッケージを使って、<a href="http://hadoop.apache.org/zookeeper/">ZooKeeper</a>を<a href="http://www.ubuntu.com/">Ubuntu</a>にインストールする方法です。（2010.2.5現在）</p>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10 (karmic) では既にaptでインストール可能になっていますので、下記の手順は不要です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10/9.04</li>
<li><a href="http://hadoop.apache.org/zookeeper/">ZooKeeper</a> 3.3.2</li>
</ul>
<h3>手順</h3>
<ul>
<li>以下のURLから、log4jの最新版のdebをダウンロード<ul>
<li><a href="http://ftp.debian.org/debian/pool/main/j/jakarta-log4j/">http://ftp.debian.org/debian/pool/main/j/jakarta-log4j/</a></li>
<li>liblog4j1.2-java_1.2.15-9_all.deb</li>
</ul>
<li><del>以下のURLから、zookeeper関連debをダウンロード。そのうちメインリポジトリに移動するかも。</del> 2010-2-11にmainに移動したようです。<ul>
<li><a href="http://ftp.debian.org/debian/pool/main/z/zookeeper/">http://ftp.debian.org/debian/pool/main/z/zookeeper/</a></li>
<li>libzookeeper-java_3.2.2+dfsg3-2_all.deb, zookeeper_3.2.2+dfsg3-2_all.deb, zookeeperd_3.2.2+dfsg3-2_all.deb</li>
<li>Cクライアントも必要であれば、i386のほうをインストールする。</li>
</ul>
<li>log4jをインストール</li>
</ul>
<pre>sudo dpkg -i liblog4j1.2-java_1.2.15-9_all.deb
</pre>
<ul>
<li>zookeeper関連debをインストール。dpkgで依存関係のエラーが出るが気にしない。</li>
</ul>
<pre>sudo dpkg -i libzookeeper*.deb zookeeper*.deb
sudo aptitude install libzookeeper-java zookeeper zookeeperd
</pre>
<ul>
<li>必要なディレクトリの作成</li>
</ul>
<pre>sudo mkdir -p /var/run/zookeeper
</pre>
<ul>
<li><a href="http://hadoop.apache.org/zookeeper/">ZooKeeper</a>の起動</li>
</ul>
<pre>sudo /etc/init.d/zookeeper start
</pre>
<h3>注意</h3>
<p>Jaunty (9.04) ではlibzookeeper-javaを入れる際にgcjが勝手に入ってしまうようです。</p>
<p>実害はなさそうですがちょっと無駄な感じです。</p>
<h3>各種ファイルの位置</h3>
<ul>
<li>設定ファイル等:  /etc/zookeeper/conf</li>
<li><a href="http://hadoop.apache.org/zookeeper/">ZooKeeper</a>本体のjar: /usr/share/java</li>
<li>サーバ、クライアントの起動スクリプト: /usr/share/zookeeper/bin</li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
