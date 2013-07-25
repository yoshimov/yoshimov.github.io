---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>テレビ会議システムのdimdimがオープンソースで公開されていますので、そのインストール方法です。</p>
<h3>環境</h3>
<ul>
<li>Windows Server 2003</li>
<li><a href="http://ja.openoffice.org/">OpenOffice</a> 2.3.1日本語版</li>
<li>dimdim 3.0.0 beta<ul>
<li><a href="http://www.dimdim.com/">http://www.dimdim.com/</a></li>
</ul>
</ul>
<h3>インストール</h3>
<p>とりあえず、インストールはインストーラで簡単に終了します。</p>
<ul>
<li><a href="http://ja.openoffice.org/">OpenOffice</a> 2.3以降</li>
<li>dimdim</li>
</ul>
<p>という順でインストール。インストール先はデフォルトのままのほうが良いみたいです。また、サーバはIPアドレスで指定したほうが良いようです。</p>
<p>ポート80を使っているソフト（Apacheなど）が動作していた場合は、インストールの間だけ停止させておきます。</p>
<h3>設定の変更</h3>
<p>インストーラではメールサーバの指定などがうまく保存されていないようなので、この辺は手動で変更します。設定ファイルは以下の場所です。</p>
<pre>C:\Program Files\Dimdim\MeetingServer\Conference Server\Tomcat 5.5\webapps\dimdim\WEB-INF\classes\resources
</pre>
<p>ここのdimdim.propertiesを修正します。</p>
<h3>サーバのポート変更</h3>
<p>サーバのポート番号を変更したい場合は、上記の場所のdimdim.propertiesを以下のように編集します。</p>
<pre>dimdim.serverAddress=192.168.1.1
dimdim.serverPortNumber=10080
dimdim.dmsServerAddress=192.168.1.1:10080
</pre>
<p>また、lighttpdのポートも変える必要があるので、</p>
<pre>c:\lighttpd\etc\lighttpd.conf
</pre>
<p>を、以下のように編集します。</p>
<pre>server.port                = 10080
</pre>
<p>その後、lighttpdとdimdimを再起動すれば、新しいポートが有効になります。</p>
