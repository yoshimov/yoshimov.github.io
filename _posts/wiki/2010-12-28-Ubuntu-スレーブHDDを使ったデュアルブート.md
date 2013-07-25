---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>Windowsの入ったマスタHDDを全く変更せずに、スレーブHDDを使って<a href="http://www.ubuntu.com/">Ubuntu</a>とのデュアルブートにする方法のメモ。</p>
<p>この方法だと、マスタHDDのMBRも変更しなくてよいので、Windowsのアップデート時にMBRの上書きが起こってもデュアルブートには何の影響もありません。</p>
<h3>環境</h3>
<ul>
<li>Windows 7</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 10.10</li>
<li>grub2 1.98</li>
<li>HDD 2台</li>
</ul>
<h3>手順</h3>
<h4><a href="http://www.ubuntu.com/">Ubuntu</a>のインストール</h4>
<ul>
<li>スレーブHDDの接続<ul>
<li>普通に２台目のHDDをスレーブとして接続します。</li>
</ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a>インストーラの起動<ul>
<li>CDまたはUSBから<a href="http://www.ubuntu.com/">Ubuntu</a>をライブ起動して、インストーラを実行します。</li>
</ul>
<li>インストール先をスレーブHDDに指定して、<a href="http://www.ubuntu.com/">Ubuntu</a>をインストール<ul>
<li>通常通り<a href="http://www.ubuntu.com/">Ubuntu</a>をインストール</li>
<li>grubのインストール先もスレーブHDDになるように注意してください。</li>
</ul>
<li>再起動時に、BIOSの設定を変更してスレーブHDDから起動するように変更<ul>
<li>これでとりあえず<a href="http://www.ubuntu.com/">Ubuntu</a>が普通に起動するようになります。</li>
</ul>
</ul>
<h4>Windowsがデフォルトで起動するように変更</h4>
<p>マスタHDDのWindowsは勝手に検出されてgrubメニューに追加されますが、デフォルトでマスタHDDにあるWindowsが起動するようにするには、スレーブHDDの<a href="http://www.ubuntu.com/">Ubuntu</a>を起動後、</p>
<pre>/etc/default/grub
</pre>
<p>を編集して、</p>
<pre>GRUB_DEFAULT=5
</pre>
<p>または</p>
<pre>GRUB_DEFAULT=&quot;Windows 7 (loader) (on xxx)&quot;
</pre>
<p>というようにWindowsのメニュー項目を指定してから、</p>
<pre>sudo update-grub
</pre>
<p>でgrub.cfgを更新しておきます。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
