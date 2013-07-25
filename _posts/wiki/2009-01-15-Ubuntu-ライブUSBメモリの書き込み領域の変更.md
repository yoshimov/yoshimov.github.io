---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10で作成したライブUSBメモリの書き込み領域の操作方法です。</p>
<h3>容量の変更</h3>
<ul>
<li>persistent オプションを削除して、USBメモリを起動</li>
<li>USBメモリを書き込み可能にする</li>
</ul>
<pre>sudo mount /cdrom -o remount,rw
</pre>
<ul>
<li>新しいファイルを作成。countでサイズを調整する</li>
</ul>
<pre>sudo dd if=/dev/zero of=/cdrom/casper-rw bs=1M count=512
</pre>
<p>作成したら以下と同じように初期化する。</p>
<h3>初期化</h3>
<ul>
<li>persistent オプションを削除して、USBメモリを起動</li>
<li>USBメモリを書き込み可能にする</li>
</ul>
<pre>sudo mount /cdrom -o remount,rw
</pre>
<ul>
<li>領域をフォーマット</li>
</ul>
<pre>sudo mkfs.ext3 -j -F /cdrom/casper-rw
</pre>
<ul>
<li>通常通りUSBメモリから<a href="http://www.ubuntu.com/">Ubuntu</a>を起動する</li>
</ul>
