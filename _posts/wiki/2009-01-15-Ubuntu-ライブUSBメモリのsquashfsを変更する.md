---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10 ライブUSB</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10ではUSBメモリにライブCDをインストールする機能がありますが、パッケージ等の追加を行うと、すぐに書き込み領域がいっぱいになってしまいます。</p>
<p>そこで、書き込み領域の一部をsquashfsに移動することで、領域を確保し直す方法です。</p>
<h3>新規作成手順</h3>
<p>差分用のsquashfsをまだ作っていない時はこんな感じで作業します。</p>
<ul>
<li>USBメモリに<a href="http://www.ubuntu.com/">Ubuntu</a> 8.10をインストール<ul>
<li>作業領域はめいっぱいとらず、空き領域を残しておくこと</li>
</ul>
<li>USBメモリから<a href="http://www.ubuntu.com/">Ubuntu</a>を起動して、パッケージのインストールなどを行う</li>
<li>不要なファイルを削除しておく</li>
</ul>
<pre>sudo aptitude clean
</pre>
<ul>
<li>USBメモリから persistent オプションを削除して<a href="http://www.ubuntu.com/">Ubuntu</a>を再起動</li>
<li>squashfsファイルを作成</li>
</ul>
<pre>sudo aptitude update
sudo aptitude install squashfs-tools
sudo mount /cdrom -o remount,rw
sudo mount -t ext3 -o loop /cdrom/casper-rw /mnt
sudo mksquashfs /mnt /cdrom/casper/update.squashfs -info -noappend -wildcards -e .wh* cdrom etc home lost+found media rofs root tmp* var/backups var/cache var/crash var/log var/run var/spool var/tmp
</pre>
<p>フォルダ名の複数指定だとどうもエラーになってしまうので、excludesを指定します。</p>
<ul>
<li>書き込み領域の整理</li>
</ul>
<pre>cd /mnt
sudo rm -rf bin sbin usr lib var/lib
cd /
sudo sync
sudo umount /mnt
</pre>
<ul>
<li>USBメモリから通常通り<a href="http://www.ubuntu.com/">Ubuntu</a>を起動する</li>
</ul>
<h3>ファイルの追加手順</h3>
<p>既にupdate.squashfsがある場合、追加はちょっとややこしくなります。</p>
<ul>
<li>USBメモリから persistent オプションを削除して<a href="http://www.ubuntu.com/">Ubuntu</a>を再起動</li>
<li>必要ツールをinstall</li>
</ul>
<pre>sudo aptitude update
sudo aptitude install squashfs-tools aufs-tools
</pre>
<ul>
<li>USBメモリを書き込み可にする</li>
</ul>
<pre>sudo mount /cdrom -o remount,rw
</pre>
<ul>
<li>前のsquashfsをくっつけて、新しいsquashfsを作る</li>
</ul>
<pre>sudo mkdir /tmpsqfs /tmprwfs
sudo mount -t squashfs -o loop /cdrom/casper/update.squashfs /tmpsqfs
sudo mount -t ext3 -o loop /cdrom/casper-rw /tmprwfs
sudo mount -t aufs -o br:/tmprwfs=ro:/tmpsqfs=ro none /mnt
sudo mksquashfs /mnt /cdrom/casper/update-new.squashfs -info -noappend -wildcards -e .wh* cdrom etc home lost+found media rofs root tmp* var/backups var/cache var/crash var/log var/run var/spool var/tmp
cd /cdrom/casper
sudo umount /mnt
sudo mv update.squashfs update.squashfs.old
sudo mv update-new.squashfs update.squashfs
</pre>
<ul>
<li>書き込み領域の整理</li>
</ul>
<pre>cd /tmprwfs
sudo rm -rf sbin usr lib var/lib
cd /
sudo sync
sudo umount /tmprwfs
</pre>
<ul>
<li>USBメモリから通常通り<a href="http://www.ubuntu.com/">Ubuntu</a>を起動する</li>
</ul>
<h3>備考</h3>
<ul>
<li>squashfsを作るのはpersistentオプションなし環境のほうがいいらしい。<ul>
<li>毎回installが必要なのは面倒ですが。</li>
</ul>
<li>umountの前にsyncをしたほうがトラブルは少なかった。</li>
<li>起動できなくなったら以下のファイルを削除する。</li>
</ul>
<pre>/cdrom/casper-rw
/cdrom/casper/update.squashfs
</pre>
<h3>自動スクリプト</h3>
<ul>
<li><a href="http://gist.github.com/36981">http://gist.github.com/36981</a></li>
</ul>
