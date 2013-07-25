---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://opensolaris.org/">OpenSolaris</a>上でufs形式のループバックマウント可能なファイルを作る方法です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://opensolaris.org/">OpenSolaris</a> 2009.06</li>
</ul>
<h3>手順</h3>
<ul>
<li>ddで空のファイルを作る</li>
</ul>
<pre>dd if=/dev/zero of=loopback bs=1M count=128
</pre>
<ul>
<li>lofiadmでデバイスとして登録</li>
</ul>
<pre>pfexec lofiadm -a loopback
</pre>
<ul>
<li>ufs形式でフォーマット</li>
</ul>
<p>lofiadmを実行した際に表示される /dev/lofi/4 などのデバイス名を指定して、</p>
<pre>pfexec /usr/lib/fs/ufs/newfs /dev/lofi/4
</pre>
<p>と実行。</p>
<ul>
<li>通常通りマウント</li>
</ul>
<pre>pfexec mkdir -p /mnt/loopback
pfexec mount /dev/lofi/4 /mnt/loopback
</pre>
<p>マウント出来れば成功です。</p>
<p>一旦lofiadmで登録しないといけないのがちょっと面倒ですね。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
