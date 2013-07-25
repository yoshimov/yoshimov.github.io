---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>initrdにパッチをあてて、自前オプションなどを処理できるようにする方法です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.5</li>
<li><a href="http://www.knoppix.net/">KNOPPIX</a> 6.0.1</li>
</ul>
<h3>手順</h3>
<p>通常、initrdはcpioという形式のファイルがgz圧縮されたものなので、以下のようにして中のファイルを取り出すことができます。</p>
<pre>mkdir cpio
cd cpio
zcat /somewhere/initrd.gz | sudo cpio -i H newc --no-absolute-filenames
</pre>
<p>rootではないユーザで作業している場合、sudoしないとファイルの所有者が正しく反映されません。</p>
<p>initrdは、起動時にinitというスクリプトが実行される際のディスクイメージになります。通常はinitスクリプトを編集すれば、自前オプションの処理などが可能になります。</p>
<p>修正後にinitrdを作り直す場合は、以下のようにします。</p>
<pre>find . | sudo cpio -o -H newc | gzip - &gt; /somewhere/initrd-mod.gz
</pre>
<p><span class="error">commentプラグインは存在しません。</span> </p>
