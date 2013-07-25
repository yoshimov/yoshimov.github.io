---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h4><a href="http://cygwin.com/">Cygwin</a>を入れる</h4>
<ul>
<li><a href="http://www.cygwin.com">http://www.cygwin.com</a></li>
</ul>
<h4>SourceForgeからバイナリをダウンロード</h4>
<ul>
<li><a href="http://sourceforge.net/projects/gnude">http://sourceforge.net/projects/gnude</a></li>
</ul>
<h4>インストール</h4>
<p>インストーラを実行してインストール。GNUDE/binにパスが自動的に通されます。</p>
<h4>cygwin1.dllのバージョンを確認</h4>
<pre>arm-elf-gcc
</pre>
<p>などを実行すると、</p>
<pre>You have multiple copies of cygwin1.dll on your system.
</pre>
<p>などと言われることがあります。この場合はGNUDE側のcygwin1.dllをリネームするなどすると、回避できます。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
