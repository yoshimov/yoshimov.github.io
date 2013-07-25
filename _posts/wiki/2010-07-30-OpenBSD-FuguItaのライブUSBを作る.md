---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.openbsd.org/">OpenBSD</a>がライブCDから利用できる<a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>を、USBメモリにインストールする方法です。インストールスクリプトがうまく動かなかったので、手動でのインストールメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a> 4.7</li>
</ul>
<h3>手順</h3>
<ul>
<li>CDなどから<a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>を起動</li>
</ul>
<p>最初はどうしても<a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>を起動する必要があるので、CDを焼くか、qemuなどを使って</p>
<pre>qemu -cdrom FuguIta-4.7.iso -hda /dev/sdb -boot d -m 512
</pre>
<p>などとして、起動する。起動方法などは公式Wikiなどを参照のこと。</p>
<ul>
<li>USBメモリをフォーマット</li>
</ul>
<p><a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>を起動後にUSBメモリを差すと、CD-ROM起動ならsd0, qemuからならwd0などにUSBメモリが接続されるので、</p>
<pre>fdisk -i sd0
</pre>
<p>などとすると、<a href="http://www.openbsd.org/">OpenBSD</a>のMBRが書き込まれる。デフォルトのままでは、cパーティション１つ。</p>
<ul>
<li>パーティションを作成</li>
</ul>
<pre>disklabel -E sd0
</pre>
<p>と起動して、以下のようにa,dパーティションを作る。aのサイズはCD-ROMより大きければ良い。</p>
<pre>&gt; a a
offset: [63] &lt;enter&gt;
size: [???] 2g&lt;enter&gt;
&gt; a d
offset: [???] &lt;enter&gt;
size: [???] &lt;enter&gt;
&gt; w &lt;enter&gt;
&gt; q &lt;enter&gt;
</pre>
<ul>
<li>フォーマット</li>
</ul>
<pre>newfs sd0a
newfs sd0d
</pre>
<p>として、それぞれffsでフォーマットする。</p>
<ul>
<li>システムファイルをコピー</li>
</ul>
<pre>mount /dev/sd0a /mnt
</pre>
<p>とaパーティションをマウントした後、</p>
<pre>cp -R /sysmedia/* /mnt
</pre>
<p>として、必要なファイルをすべてUSBメモリにコピー。</p>
<ul>
<li>ブートローダのインストール</li>
</ul>
<pre>/usr/mdec/installboot -v /mnt/boot /usr/mdec/biosboot sd0
</pre>
<p>として、ブートローダをインストール。</p>
<p>あとは通常通りUSBメモリからブートすれば<a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>がブートする（はず）。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
