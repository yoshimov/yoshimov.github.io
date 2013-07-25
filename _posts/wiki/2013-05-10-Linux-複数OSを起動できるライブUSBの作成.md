---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>USBメモリに格納したisoファイルから、直接複数のOSを起動する方法です。</p>
<p>一部のディストリビューションしかiso直接起動は対応していませんが、カーネルとinitrdだけを取り出してパッチをあてることで、isoファイルには手を加えずに直接起動できます。</p>
<p>この方法だと、同じOSの異なるバージョンを、起動可能な状態で複数インストールすることができます。また、isoファイルがあるので配布やCD作成にも使えます。</p>
<p>このツールの名前は isobooster としました。</p>
<p><a href="/?page=Keyword" class="wikipage">Keyword</a>: マルチブート, USBメモリ, Multiboot USB, Linux, LiveCD, ISO, isobooster</p>
<p>-&gt; <a href="http://multiboot-usb.yoshimov.com">English site is here</a></p>
<h3>環境</h3>
<p>作業環境</p>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 10.04</li>
</ul>
<p>おそらく、その他のディストリビューションでも大丈夫だと思います。</p>
<p>ただ、bootloaderにgrub2 1.98を使っているので、このバージョン以降が提供されているディストリビューションを利用してください。</p>
<h3>手順</h3>
<h4>USBメモリの準備</h4>
<p>ここでは、USBメモリが/dev/sdb1にあると仮定しています。PartedやWindows上でパーティションを作っても問題ありません。</p>
<ul>
<li>USBメモリをvfatで全て初期化</li>
</ul>
<pre>sudo umount /dev/sdb1
sudo mkfs.vfat /dev/sdb1
</pre>
<ul>
<li>領域をマウント</li>
</ul>
<pre>sudo mount /dev/sdb1 /mnt
</pre>
<p>一旦USBメモリを抜いて、挿し直すと /media の下にマウントされるのでそれでも問題ありません。</p>
<h4>各種ファイルの準備</h4>
<ul>
<li>以下のようにして<a href="https://github.com/">GitHub</a>にあるファイルをダウンロード</li>
</ul>
<pre>sudo aptitude install git mtools wget
cd /mnt
git init
git pull https://github.com/isobooster/isobooster.git
</pre>
<ul>
<li>ブートローダをインストール</li>
</ul>
<pre>sudo bash mkboot.sh bootloader /dev/sdb
</pre>
<p>この時はデバイス名が必要なので注意。マウントはしたままで問題ありません。grub2を採用したバージョンから、パーティションではなくデバイスそのものを指定する必要があります。</p>
<ul>
<li>必要なディストリビューションをインストール</li>
</ul>
<p>以下のようにcfg内にあるファイル名の.cfgの前までを指定してください。</p>
<pre>sudo bash mkboot.sh ubuntu-10.04
sudo bash mkboot.sh knoppix-6.0.1-jp
</pre>
<p>isoファイルのダウンロードから必要があればinitrdのパッチあて、menu.lstの編集まで自動的に終わります。isoファイルは別にダウンロードしてisoフォルダに入れておいても問題ありません。</p>
<h4>対応しているディストリビューション</h4>
<p>現在のリストはこちら。</p>
<ul>
<li><a href="http://multiboot-usb.yoshimov.com/supported">http://multiboot-usb.yoshimov.com/supported</a></li>
</ul>
<p>GNOME系が多いですが、単に私がGNOME好きなだけです。リクエストが有れば、メールなり<a href="http://www.twitter.com">Twitter</a>なりでどうぞ。うまくいけば対応します。</p>
<h3>トラブルシューティング</h3>
<h4>起動時にcontiguousなんちゃらというエラーがでる</h4>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>系はisoファイルが断片化していると起動できない場合があります。Windowsなどでディスクの最適化を実行してみてください。</p>
<h4>isoのダウンロードが遅い</h4>
<p>cfgフォルダ内にあるファイルにダウンロード元のURLがあるので、適当に変えてください。</p>
<h3>参考</h3>
<ul>
<li><a href="http://www.pendrivelinux.com/boot-multiple-iso-from-usb-multiboot-usb/">Boot Multiple ISO from USB (MultiBoot USB)</a></li>
<li><a href="http://www.boot-land.net">Boot Land</a></li>
</ul>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
