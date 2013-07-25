---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.cyanogenmod.com/">CyanogenMod</a>などのカスタムROMでは、Apps2SDを使ってSDカードにアプリをインストールすることができますが、そのためのパーティションの作り方のメモ。</p>
<p>Linuxマシンから操作するのが一番簡単です。環境がなければCDやUSBからブートして使うのもありです。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.cyanogenmod.com/">CyanogenMod</a> 4.2.13</li>
<li>cm-recovery 1.4</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10</li>
</ul>
<h3>手順</h3>
<h4>パーティション作成</h4>
<ul>
<li>USBケーブルで、<a href="http://www.ubuntu.com/">Ubuntu</a>マシンに接続</li>
<li><a href="http://www.android.com/">Android</a>の上のバーにUSB connectedと出るので、そこを選んでMountボタンを押す。</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a>マシン上でSDカードが認識されたら、gpartedを起動。なければaptitudeなどで入れておく</li>
</ul>
<pre>sudo aptitude install gparted
sudo gparted
</pre>
<ul>
<li>右上から/dev/sdcなどSDカードデバイスを選択</li>
<li>[partition]-[Unmount]からunmountする</li>
<li>FAT32のパーティションがあれば、[Resize/Move]ボタンでサイズを変更</li>
<li>空いた部分に[New]でext3パーティションを作成する</li>
<li>[Apply]ボタンを押して作業を終了</li>
<li>gpartedを終了後、USBケーブルを抜く</li>
</ul>
<h4>パーティションのアップグレード</h4>
<p>どうも<a href="http://www.android.com/">Android</a>側でパーティションのアップグレードをしないと、ext3として認識しないようなので、以下の作業も必要です。</p>
<p>この作業には、cm-recoveryなどのカスタムリカバリROMが必要になります。</p>
<ul>
<li>Homeボタンを押しながら<a href="http://www.android.com/">Android</a>を起動して、リカバリモードに入る。</li>
<li>go to consoleを選択して、以下のコマンドを実行する。PC側にadbがあれば、adb shellからでもできます。</li>
</ul>
<pre>upgrade_fs
tune2fs -O extents,uninit_bg,dir_index /dev/block/mmcblk0p2
e2fsck -fpDC0 /dev/block/mmcblk0p2
reboot
</pre>
<p><span class="error">commentプラグインは存在しません。</span> </p>
