---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.openbsd.org/">OpenBSD</a>は、minirootをカーネルイメージ内に抱えているので、minirootを変更、特にサイズを変更したいときはカーネルの再構築が必要です。その手順のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a> 4.7</li>
</ul>
<h3>手順</h3>
<ul>
<li>USBから<a href="http://kaw.ath.cx/openbsd/index.php?LiveCD">FuguIta</a>をブート<ul>
<li><a href="/?page=OpenBSD%2FFuguIta%A4%CE%A5%E9%A5%A4%A5%D6USB%A4%F2%BA%EE%A4%EB" class="wikipage">OpenBSD/FuguItaのライブUSBを作る</a></li>
</ul>
<li>USBメモリを読み書き可で再マウント</li>
</ul>
<pre>mount -f -o update,rw /sysmedia
</pre>
<ul>
<li>作業用ディレクトリを作って、toolsとsysのソースを持ってくる。</li>
</ul>
<p>別のマシンでダウンロードしたものを、別のUSBメモリで受け渡すと楽です。</p>
<ul>
<ul>
<li>tools: <a href="http://kaw.ath.cx/dl/pub/OpenBSD/LiveCD/tools/tools-4.7.tar.gz">http://kaw.ath.cx/dl/pub/OpenBSD/LiveCD/tools/tools-4.7.tar.gz</a></li>
<li>sys: <a href="http://ftp5.usa.openbsd.org/pub/OpenBSD/4.7/sys.tar.gz">http://ftp5.usa.openbsd.org/pub/OpenBSD/4.7/sys.tar.gz</a></li>
</ul>
</ul>
<pre>mkdir -p /sysmedia/work
cd /sysmedia/work
cp /somewhere/tools-4.7.tar.gz .
tar zxvf tools-4.7.tar.gz
cp /somewhere/sys.tar.gz .
tar zxvf sys.tar.gz
</pre>
<ul>
<li>/usr/srcからリンク</li>
</ul>
<pre>ln -s /sysmedia/work/sys /usr/src/sys
</pre>
<ul>
<li>パラメータを変更</li>
</ul>
<pre>cd tools-4.7/sys/arch/i386/conf
vi RDROOT
</pre>
<p>minirootのサイズは512バイトのブロックの数。</p>
<ul>
<li>カーネルをコンパイル</li>
</ul>
<pre>config RDROOT
cd ../compile/RDROOT
make clean
make depend
make
</pre>
<p>コンパイルしたカーネルは、tools-4.7の下にコピーしておきます。</p>
<pre>cp bsd /sysmedia/work/tools-4.7/bsd.orig
</pre>
<ul>
<li>minirootのカスタマイズ</li>
</ul>
<p>tools-4.7以下にあるrdroot.imgをループバックマウントしてカスタマイズします。</p>
<pre>cd /sysmedia/work/tools-4.7
vnconfig svnd2 rdroot.img
mount /dev/svnd2a /mnt
</pre>
<p>容量が足りない場合は、</p>
<pre>cd /sysmedia/work/tools-4.7
mv rdroot.img rdroot-org.img
dd if=/dev/zero of=rdroot.img bs=512 count=8192
vnconfig svnd2 rdroot.img
disklabel -E svnd2 (aパーティションを作成)
newfs svnd2a
mount /dev/svnd2a /mnt
</pre>
<p>などとします。</p>
<ul>
<li>カーネルイメージの作成</li>
</ul>
<p>あとは、makeでカーネルとminirootをくっつくれば完成です。</p>
<pre>make bsd.rdcd
</pre>
<p>完成したカーネルイメージ(bsd-fi)は、mediaの中にできます。</p>
<h3>参考</h3>
<ul>
<li><a href="http://kaw.ath.cx/openbsd/index.php?%B2%B6CD%A4%F2%BA%EE%A4%EB">OpenBSD - 俺CDを作る</a></li>
</ul>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
