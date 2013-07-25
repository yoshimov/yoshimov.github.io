---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>のPythonでの、モジュールのローディングに関するメモです。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.04/9.10</li>
<li>Python 2.6</li>
</ul>
<h3>9.10 Karmicのモジュールのロード元</h3>
<p>何も指定しない状態でもロード可能なのが以下のフォルダ。</p>
<ul>
<li>/usr/lib/python2.6</li>
<li>/usr/lib/python2.6/plat-linux2</li>
<li>/usr/lib/python2.6/lib-tk</li>
<li>/usr/lib/python2.6/lib-old</li>
<li>/usr/lib/python2.6/lib-dynload</li>
</ul>
<p>その後、siteをimportすると、以下のフォルダがロード元として追加される。一段下になっているのが、pthファイルで指定されたフォルダ。</p>
<ul>
<li>/usr/lib/python2.6/dist-packages<ul>
<li>/usr/lib/python2.6/dist-packages/PIL</li>
<li>/usr/lib/python2.6/dist-packages/gst-0.10</li>
<li>/usr/lib/python2.6/dist-packages/gtk-2.0</li>
<li>/usr/lib/pymodules/python2.6<ul>
<li>/usr/lib/pymodules/python2.6/gtk-2.0</li>
</ul>
</li>
</ul>
<li>/usr/local/lib/python2.6/dist-packages</li>
</ul>
<p>/var/lib がなくなって、代わりに/usr/lib/pymodules というフォルダが追加されている。実際には、/var/lib/python-supportは、/usr/lib/pymodulesへのシンボリックリンクとして残っている。</p>
<p>また、/usr/lib/pymodules 内も多くがシンボリックリンクで、モジュールの実体は/usr/share/python-supportや、/usr/share/pysharedにあるものが多い。</p>
<h3>9.04 Jauntyのモジュールのロード元</h3>
<p>site無しの状態では、以下のフォルダのみ。</p>
<ul>
<li>/usr/lib/python2.6/</li>
<li>/usr/lib/python2.6/plat-linux2</li>
<li>/usr/lib/python2.6/lib-tk</li>
<li>/usr/lib/python2.6/lib-old</li>
<li>/usr/lib/python2.6/lib-dynload</li>
</ul>
<p>import site後は以下のフォルダ。/var/lib/python-supportがpthで追加される。</p>
<ul>
<li>/usr/lib/python2.6/dist-packages<ul>
<li>/var/lib/python-support/python2.6</li>
</ul>
<li>/usr/local/lib/python2.6/dist-packages</li>
</ul>
<h3>ロード元フォルダの調べ方</h3>
<ul>
<li>以下のようにPythonを起動</li>
</ul>
<pre>python -S
</pre>
<ul>
<li>sys.pathを調べる</li>
</ul>
<pre>&gt;&gt; import sys; sys.path
</pre>
<ul>
<li>import site後のsys.pathを調べる</li>
</ul>
<pre>&gt;&gt; import sys,site; sys.path
</pre>
<p><span class="error">commentプラグインは存在しません。</span> </p>
