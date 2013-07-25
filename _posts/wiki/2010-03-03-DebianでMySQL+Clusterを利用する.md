---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>構成</h3>
<dl>
<dt>ndb1</dt>
<dd> mysqld, ndb manager, ndbd</dd>
</dl>
<dl>
<dt>ndb2</dt>
<dd> ndbd</dd>
</dl>
<p>をそれぞれ起動すると仮定しています。</p>
<p>使用したバージョンは以下の通り。</p>
<ul>
<li><a href="http://www.debian.org/">Debian</a> 4.0</li>
<li>MySQL 5.0.34</li>
</ul>
<h3>MySQLのインストール</h3>
<p>以下のパッケージをインストールする。</p>
<pre>apt-get install mysql-server
</pre>
<h3>設定ファイル編集</h3>
<p>ndb1, ndb2の/etc/mysql/my.cnfを以下のように編集。</p>
<pre>[mysqld]
ndbcluster
ndb-connectstring=ndb1
[MYSQL_CLUSTER]
ndb-connectstring=ndb1
</pre>
<p>/etc/hostsに</p>
<pre>192.168.0.x ndb1
</pre>
<p>などと、名前解決のためのエントリを追加。</p>
<h3>管理用設定ファイル作成</h3>
<p>ndb1でサンプルをコピー。</p>
<pre>cp /usr/share/mysql/ndb-config-2-node.ini /etc/mysql/ndb_mgmd.cnf
</pre>
<p>/etc/mysql/ndb_mgmd.cnfを以下のように編集。</p>
<pre>NoOfReplicas=1
[ndb_mgmd]
id=1
HostName=ndb1
[ndbd]
id=2
HostName=ndb1
[ndbd]
id=3
HostName=ndb2
[mysqld]
HostName=ndb1
</pre>
<p>その他はそのままで可。</p>
<h3>各サービスを起動</h3>
<h4>初回の場合</h4>
<p>ndb1で以下を実行</p>
<pre>/etc/init.d/mysql-ndb-mgm start
/etc/init.d/mysql-ndb start-initial
</pre>
<p>ndb2で以下を実行</p>
<pre>/etc/init.d/mysql-ndb start-initial
</pre>
<p>各ndbが起動した後、ndb1でSQLサーバを起動。</p>
<pre>/etc/init.d/mysql start
</pre>
<h4>２回目以降</h4>
<p>ndb1で以下を実行</p>
<pre>/etc/init.d/mysql-ndb-mgm start
/etc/init.d/mysql-ndb start
</pre>
<p>ndb2で以下を実行</p>
<pre>/etc/init.d/mysql-ndb start
</pre>
<p>各ndbが起動した後、ndb1でSQLサーバを起動。</p>
<pre>/etc/init.d/mysql start
</pre>
<h3>状態を確認</h3>
<p>ndb1で以下を実行</p>
<pre>ndb_mgm -e show
</pre>
<p>ndbd 2nodes、ndb_mgmd 1node、mysqld 1nodeが表示されれば起動成功。</p>
<h3>停止</h3>
<p>MySQL Clusterを停止する場合は、以下のコマンドで停止させる。</p>
<pre>ndb_mgm -e shutdown
</pre>
