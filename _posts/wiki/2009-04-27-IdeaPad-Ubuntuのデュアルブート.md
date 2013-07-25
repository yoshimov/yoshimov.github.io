---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li>IdeaPad S9e</li>
<li>WindowsXP Home Edition</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.04 Netbook Remix</li>
</ul>
<h3>概要</h3>
<p><a href="/?page=Lenovo+IdeaPad+S9e" class="wikipage">Lenovo IdeaPad S9e</a>には最初からWindowsXP Homeが入っていますが、MBRにはリカバリ用のパーティションのローダがあったり、WindowsXPのパーティションにはInstant On(Splashtop)のイメージが入っていたりするので、その辺の環境を残しつつ<a href="http://www.ubuntu.com/">Ubuntu</a>を入れる方法です。</p>
<p>起動の順序は、<blockquote><p>Instant On-&gt;MBR-&gt;Windows NTLDR-&gt;grub-&gt;<a href="http://www.ubuntu.com/">Ubuntu</a></p>
</blockquote>
となって、少々ややこしいですが、既存の機能は全て使える状態で残すことができます。</p>
<h3>準備</h3>
<h4>HDDのバックアップを取る</h4>
<p>まずはHDDをまるごとバックアップをとっておきます。<a href="http://clonezilla.org/">Clonezilla</a>を使うと、6GBほどで全HDDイメージのバックアップが取れました。</p>
<ul>
<li><span class="nopage">Linux/HDDイメージのバックアップ、リストア</span><a href="/?page=Linux%2FHDD%A5%A4%A5%E1%A1%BC%A5%B8%A4%CE%A5%D0%A5%C3%A5%AF%A5%A2%A5%C3%A5%D7%A1%A2%A5%EA%A5%B9%A5%C8%A5%A2">?</a></li>
</ul>
<h4>ライブUSBの用意</h4>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>のサイトから、インストールに使うイメージをダウンロードして、ライブUSBを作っておきます。ここでは、Netbook Remixを使っています。</p>
<ul>
<li><a href="http://www.ubuntu.com/getubuntu/download-netbook">Download Ubuntu Netbook Remix</a></li>
</ul>
<h4>ツールのインストール</h4>
<p>WindowsXPの入っているパーティションに、<a href="http://www.winimage.com/bootpart.htm">BootPart</a>をダウンロードして展開しておきます。</p>
<ul>
<li><a href="http://www.winimage.com/bootpart.htm">BootPart</a></li>
</ul>
<h3>手順</h3>
<h4><a href="http://www.ubuntu.com/">Ubuntu</a>のインストール</h4>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>のライブUSBでブートして、HDDに<a href="http://www.ubuntu.com/">Ubuntu</a>をインストールします。この際に、既存のWindowsパーティションのサイズを変更して、そこにできた空き領域に<a href="http://www.ubuntu.com/">Ubuntu</a>をインストールするようにします。</p>
<p>私は、以下のようにしました。</p>
<pre>/dev/sda1 .. NTFS。既存のWindowsパーティション
/dev/sda3 .. ext4。Ubuntuのルート
/dev/sda4 .. swap用領域
/dev/sda2 .. vfat。IdeaPadのリカバリ用領域
</pre>
<p>sda3に120GBほど割り当てました。</p>
<p>また、ブートローダーは/dev/sdaではなく、<a href="http://www.ubuntu.com/">Ubuntu</a>のインストール先パーティション、ここでは/dev/sda3にインストールするようにします。</p>
<h4><a href="http://www.winimage.com/bootpart.htm">BootPart</a>の設定</h4>
<ul>
<li>Windowsを通常通り起動</li>
<li>現在のパーティションリストを表示</li>
</ul>
<pre>cd c:\bootpart
bootpart
</pre>
<p>などとして、パーティションリストを表示した後、<a href="http://www.ubuntu.com/">Ubuntu</a>のルートパーティションの番号を</p>
<pre>bootpart 2 ubuntuboot.lnx Ubuntu 9.04 Netbook Remix
</pre>
<p>のように実行すると、Windows起動時に<a href="http://www.ubuntu.com/">Ubuntu</a>が出てくるようになる。</p>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a>が起動するか確認</li>
</ul>
<h4>OSの起動順序の変更</h4>
<ul>
<li>Windowsを通常通り起動</li>
<li>[コントロールパネル]-[システム]から、起動と回復の設定を選んで、<a href="http://www.ubuntu.com/">Ubuntu</a>を既定のオペレーティングシステムとして設定する。</li>
</ul>
