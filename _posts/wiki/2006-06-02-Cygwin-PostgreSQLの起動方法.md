---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<ul>
<li> <a href="http://cygwin.com/">Cygwin</a> v2.78</li>
<li> PostgreSQL v7.3.4</li>
</ul>
<p>の使い方。</p>
<h4><a href="http://cygwin.com/">Cygwin</a>でPostgreSQLを選択</h4>
<p><a href="http://cygwin.com/">Cygwin</a>のsetup.exeから、PostgreSQLとIPCを選択してインストールする。</p>
<h4>IPCの起動</h4>
<p>Shared Memory, Semaphore を利用するためにIPCを起動する必要がある。</p>
<pre>/usr/bin/ipc-daemon2 &amp;
</pre>
<p>として起動。</p>
<pre>/usr/bin/ipcs
</pre>
<p>を実行すると、何やら情報が出る。</p>
<h4>DBの作成</h4>
<p>DBフォルダは、</p>
<pre>/usr/bin/createdb -D c:/Work/db
</pre>
<p>などとして作成する。マシンの管理者権限が必要。</p>
<h4>PostgreSQLの起動</h4>
<pre>/usr/bin/postmaster -D c:/Work/db
</pre>
<p>として起動する。外部マシンから接続して利用する場合は、</p>
<pre>/usr/bin/postmaster -i -D c:/Work/db
</pre>
<p>とする。</p>
<h4>SQL利用</h4>
<pre>/usr/bin/psql
</pre>
<p>を実行すると、SQL文が使える。</p>
<p>元ネタ：<a href="http://www.aspect-sys.co.jp/etc/win/xp_db/postgresql/install.html">http://www.aspect-sys.co.jp/etc/win/xp_db/postgresql/install.html</a></p>
<p><span class="error">trackbackプラグインは存在しません。</span> </p>
