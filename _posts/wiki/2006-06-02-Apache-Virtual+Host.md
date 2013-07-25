---
layout: post
---
<h2>ApacheでのVirtual Host設定</h2>
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<p>Apacheを使って、１台のマシンに複数のドメインを割り当てる場合、httpd.confを以下のように編集する。</p>
<h4>Virtual Hostモジュールを有効にする</h4>
<pre>LoadModule vhost_alias_module /usr/lib/apache/1.3/mod_vhost_alias.so
</pre>
<p>という行のコメントを外す。</p>
<h4>Virtual Host設定をするIPアドレスを指定</h4>
<p>通常は、</p>
<pre>NameVirtualHost *
</pre>
<p>とする。複数のIPが割り当てられている場合は、どちらかに設定するなどできる。</p>
<h4>ホスト名毎の設定を追加する</h4>
<pre>&lt;VirtualHost *&gt;
 ServerName hoge.example.org
 DocumentRoot /usr/www/hoge
&lt;/VirtualHost&gt;
</pre>
<p>などと記述する。ServerName部分に設定したいホスト名を指定する。</p>
<p>あるホスト名へのリクエストのみ、他のホストに転送したい場合、</p>
<pre>&lt;VirtualHost *&gt;
 ServerName hoge.example.org
 Redirect / http://redirect.org
&lt;/VirtualHost&gt;
</pre>
<p>などとする。</p>
<p>指定したディレクトリへのリクエストを、他のホストに転送したい場合、</p>
<pre>&lt;VirtualHost *&gt;
 ServerName example.org
 Redirect /who http://who.example.org
&lt;/VirtualHost&gt;
</pre>
<p>などとする。</p>
<p>NameVirtualHostを*にしている場合、ServerNameが一致する設定がない場合は自動的に一番最初のVirtualHost設定が利用される。</p>
<h3>参考</h3>
<ul>
<li><a href="http://nekojita.org/debian/apache.html">DebianでApache</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
