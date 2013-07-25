---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://cygwin.com/">Cygwin</a>のApache2は、インストールしただけでは動作しないため、動作させるための設定方法です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://cygwin.com/">Cygwin</a> 1.5.25</li>
<li>Apache 2.2.6</li>
</ul>
<h3>手順</h3>
<ul>
<li>cygserverのセットアップ</li>
</ul>
<pre>cygserver-config
net start cygserver
</pre>
<p>Vistaの場合、管理者権限のコマンドプロンプトから実行する。</p>
<ul>
<li>環境設定の追加</li>
</ul>
<pre>vi /etc/profile.d/cygwin-server.sh
</pre>
<p>として</p>
<pre>export CYGWIN=server
</pre>
<p>という行を保存。</p>
<ul>
<li>Apacheの起動</li>
</ul>
<pre>/usr/sbin/apachectl2 start
</pre>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
