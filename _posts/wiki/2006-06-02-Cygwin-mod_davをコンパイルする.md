---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://cygwin.com/">Cygwin</a> 1.5.16</li>
<li>Apache 1.3.33 (<a href="http://cygwin.com/">Cygwin</a>)</li>
<li>mod_dav 1.0.3-1.3.6</li>
<li>gcc 3.3.3 (cygwin special)</li>
</ul>
<h3>手順</h3>
<h4>apxsを編集</h4>
<p>/usr/sbin/apxsを以下のように編集する。</p>
<pre>my $CFG_LD_SHLIB      = q(gcc);
my $CFG_LDFLAGS_SHLIB = q(-g -shared);
my $CFG_LIBS_SHLIB    = q(/bin/libhttpd.dll); 
</pre>
<h4>mod_davを展開</h4>
<p><a href="http://www.webdav.org/mod_dav/">http://www.webdav.org/mod_dav/</a> よりソースをダウンロードして展開。</p>
<h4>configureを実行</h4>
<p>bashから</p>
<pre>./configure
</pre>
<p>と実行する。</p>
<h4>Makefileを編集</h4>
<p>以下の箇所を変更</p>
<pre>BINNAME = libdav.dll
INSTALL_IT = mkdir -p /usr/lib/apache &amp;&amp; $(APXS) -i -a -n dav libdav.dll
LIBS = -lexpat
libdav.dll: $(OBJS)
</pre>
<h4>make</h4>
<pre>make
make install
</pre>
<p>でインストールされる。</p>
<h3>設定</h3>
<ul>
<li><a href="http://webdav.todo.gr.jp/">WebDAV Resources JP</a></li>
</ul>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> <span class="error">trackbackプラグインは存在しません。</span> </p>
