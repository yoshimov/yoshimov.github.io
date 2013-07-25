---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.centos.org/">CentOS</a>でWindows共有フォルダを自動マウントする方法です。</p>
<h3>環境</h3>
<ul>
<li>Windows Vista</li>
<li><a href="http://www.centos.org/">CentOS</a> 5.5</li>
</ul>
<h3>手順</h3>
<ul>
<li>必要なパッケージのインストール</li>
</ul>
<pre>sudo yum install autofs samba-client
</pre>
<ul>
<li>auto.masterを編集</li>
</ul>
<pre>sudo vi /etc/auto.master
</pre>
<p>として、</p>
<pre>/smb /etc/auto.smb
</pre>
<p>という行を有効にするか追記する。</p>
<ul>
<li>auto.smbを編集</li>
</ul>
<p>ユーザ認証が必要な場合、</p>
<pre>sudo vi /etc/auto.smb
</pre>
<p>として、opts=の行に、</p>
<pre>opts=&quot;-fstype=cifs,iocharset=utf8,username=hoge,password=pass&quot;
</pre>
<p>などと指定して、$SMB<a href="http://www.sony.jp/CLIE/">CLIE</a>NTから始まる行を、</p>
<pre>$SMBCLIENT -U hoge%pass -gL
</pre>
<p>などと変更する。</p>
<ul>
<li>automountの起動</li>
</ul>
<pre>sudo /etc/init.d/autofs start
</pre>
<p>としてautomountを起動。あとは、</p>
<pre>ls /smb/hostname/shared
</pre>
<p>などとすれば、共有フォルダにアクセス出来る。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
