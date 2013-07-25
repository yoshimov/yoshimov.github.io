---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10ではUSBメモリに通常通りインストールが可能ですが、USBブートに対応していないPCではそのままでは起動しません。</p>
<p>USBメモリにインストールした<a href="http://www.ubuntu.com/">Ubuntu</a>を起動させるCDの作成方法です。</p>
<p>この方法では、パーティションのUUIDがCDに書き込まれるので、特定のUSBメモリ専用のCDイメージになりますのでご注意ください。</p>
<p>また、カーネルのバージョンアップや変更を行った場合はイメージも作る直す必要があります。</p>
<h3>手順</h3>
<ul>
<li>USBメモリに<a href="http://www.ubuntu.com/">Ubuntu</a>をインストール</li>
<li>CDから、ライブ版の<a href="http://www.ubuntu.com/">Ubuntu</a>を起動</li>
<li>USBメモリをマウントする<ul>
<li>ここでは /media/disk にマウントしたと想定</li>
</ul>
</ul>
<ul>
<li>作業用フォルダを作成</li>
</ul>
<pre>cd
mkdir -p boot-cd/boot/grub
</pre>
<ul>
<li>必要なファイルの用意</li>
</ul>
<pre>cp /usr/lib/grub/i386-pc/stage2_eltorito boot-cd/boot/grub
cp /media/disk/boot/grub/menu.lst boot-cd/boot/grub
cp /media/disk/boot/vmlinuz* boot-cd/boot
cp /media/disk/boot/initrd.img* boot-cd/boot
</pre>
<ul>
<li>menu.lstの編集</li>
</ul>
<pre>vi boot-cd/boot/grub/menu.lst
</pre>
<p>として、hiddenmenuとtimeoutをコメントアウトし、</p>
<pre>uuid xxxx
</pre>
<p>という行を</p>
<pre>root (cd)
</pre>
<p>に変更する。</p>
<ul>
<li>isoイメージの作成</li>
</ul>
<pre>mkisofs -R -b boot/grub/stage2_eltorito -no-emul-boot -boot-load-size 4 -boot-info-table -input-charset utf-8 -o boot-cd.iso boot-cd
</pre>
<ul>
<li>isoをCDに焼く</li>
</ul>
<p>Windowsとの共有ストレージにコピーしてWindowsで焼くか、<a href="http://www.ubuntu.com/">Ubuntu</a>のBraseroを使って焼きます。</p>
<h3>自動スクリプト</h3>
<ul>
<li><a href="http://gist.github.com/47362">http://gist.github.com/47362</a></li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://sato-si.at.webry.info/200810/article_2.html">VMwareを使ってUbuntu 8.04 をUSBメモリに安全にインストールする方法</a></li>
</ul>
