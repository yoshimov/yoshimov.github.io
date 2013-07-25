---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://opensolaris.org/">OpenSolaris</a>のブートアップ時に利用されるmicrorootの変更方法です。忘れないうちにメモ。<a href="http://opensolaris.org/">OpenSolaris</a>使いの人には当たり前の内容かもしれませんが。</p>
<h3>環境</h3>
<ul>
<li><a href="http://opensolaris.org/">OpenSolaris</a> 2009.06</li>
</ul>
<h3>手順</h3>
<ul>
<li>書き込み可能なディスクにmicrorootをコピー</li>
</ul>
<pre>mkdir work
cp /mnt/iso/boot/x86.microroot
</pre>
<ul>
<li>gz圧縮を解凍</li>
</ul>
<pre>mv x86.microroot x86.microroot.gz
gunzip x86.microroot.gz
</pre>
<ul>
<li>ufsとしてマウント</li>
</ul>
<pre>pfexec mkdir /mnt/microroot
pfexec lofiadm -a x86.microroot
</pre>
<p>表示されたループバックデバイスをマウント。ここでは/dev/lofi/4と想定。</p>
<pre>pfexec mount -F ufs /dev/lofi/4 /mnt/microroot
</pre>
<ul>
<li>/mnt/microroot以下のファイルを編集</li>
<li>アンマウント</li>
</ul>
<pre>pfexec umount /mnt/microroot
pfexec lofiadm -d /dev/lofi/4
</pre>
<ul>
<li>必要に応じて、再圧縮する</li>
</ul>
<pre>gzip x86.microroot
</pre>
<p>ディストリビューションによってはmicrorootの空きが少ない場合があるので、そのような時は以下のように新しいmicrorootファイルを作ってそちらに全ファイルをコピーします。</p>
<ul>
<li><a href="/?page=OpenSolaris%2Fufs%B7%C1%BC%B0%A4%CEloopback%A5%D5%A5%A1%A5%A4%A5%EB%A4%CE%BA%EE%C0%AE" class="wikipage">OpenSolaris/ufs形式のloopbackファイルの作成</a></li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://blogs.sun.com/sunwg11nprg/entry/changing_miniroot_in_opensolaris">Changing miniroot in OpenSolaris</a></li>
</ul>
