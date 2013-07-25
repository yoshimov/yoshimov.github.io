---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p><a href="http://www.vmware.com/jp/products/player/">VMware</a> player上のVMに<a href="http://www.debian.org/">Debian</a>4をインストールする手順のメモ。</p>
<h4><a href="http://www.vmware.com/jp/products/player/">VMware</a> playerをダウンロード</h4>
<p>以下のページから<a href="http://www.vmware.com/jp/products/player/">VMware</a> playerをダウンロードしてインストール。</p>
<ul>
<li><a href="http://www.vmware.com/download/player">http://www.vmware.com/download/player</a></li>
</ul>
<h4>VMX Builderをダウンロード</h4>
<p>以下のページからVMX Builderをダウンロードしてインストール。</p>
<ul>
<li><a href="http://petruska.stardock.net/Software/VMware.html">http://petruska.stardock.net/Software/VMware.html</a></li>
</ul>
<h4><a href="http://www.debian.org/">Debian</a>をダウンロード</h4>
<p>以下の場所からnetinst.isoをダウンロード。</p>
<ul>
<li><a href="http://cdimage.debian.org/debian-cd/4.0_r1/i386/iso-cd/">http://cdimage.debian.org/debian-cd/4.0_r1/i386/iso-cd/</a></li>
</ul>
<h4><a href="http://www.vmware.com/jp/products/player/">VMware</a>のイメージを作成</h4>
<ul>
<li>VMX Builderで新しいイメージを作成</li>
<li>SCSI Controllerを無効にする</li>
<li>Floppyを接続していなければ無効にする</li>
<li>Hard Diskを追加<ul>
<li>Disk fileをCreate Newで作成する</li>
<li>容量は任意</li>
<li>IDEタイプを選択</li>
</ul>
<li>CD-ROMを追加<ul>
<li><a href="http://www.debian.org/">Debian</a>のイメージを選択する</li>
</ul>
<li>USB Controllerを追加</li>
<li>Ethernetを追加<ul>
<li>Network ConnectionはNATとする</li>
</ul>
</ul>
<h4><a href="http://www.debian.org/">Debian</a>の基本インストール</h4>
<ul>
<li><a href="http://www.vmware.com/jp/products/player/">VMware</a> playerを起動</li>
<li>ネットワークには接続せずに、そのまま<a href="http://www.debian.org/">Debian</a>の基本部分をインストール</li>
</ul>
<h4>デスクトップ環境のインストール</h4>
<ul>
<li>rootでログインする。</li>
<li>/etc/apt/sources.listを編集して、以下の行を追加。</li>
</ul>
<pre>deb http://ftp.jp.debian.org/debian stable main contrib non-free
</pre>
<ul>
<li>Proxyを利用している場合は、以下のコマンドを実行。</li>
</ul>
<pre>export http_proxy=http://[proxyserver]:[port]
</pre>
<ul>
<li>以下のコマンドを実行</li>
</ul>
<pre>apt-get update
</pre>
<ul>
<li>taskselを起動して、デスクトップを選択してインストール。</li>
</ul>
