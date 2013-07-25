---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>パッケージ</h3>
<p>postgres パッケージを選ぶと、自動的にインストールされます。</p>
<h3>設定</h3>
<h4>メモリ設定</h4>
<pre>/etc/sysctl.conf
</pre>
<p>を編集して、</p>
<pre>kernel.shmall = 134217728
kernel.shmmax = 134217728
</pre>
<p>という行を追加して、</p>
<pre>sysctl -w
</pre>
<p>と実行する。</p>
<h4>ローカルアクセス権設定</h4>
<pre>/var/lib/postgres/data/pg_hba.conf
</pre>
<p>を編集して、</p>
<pre>local all trust
</pre>
<p>という行を追加する。</p>
<h3>DB作成</h3>
<pre>createdb -U postgres [DB名]
</pre>
<p>としてDBを作成。</p>
<pre>psql -U postgres [DB名]
</pre>
<p>で接続できる。</p>
