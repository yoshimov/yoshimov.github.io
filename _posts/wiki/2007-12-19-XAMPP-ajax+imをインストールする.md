---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>簡単ですが、ajax imのインストール手順です。</p>
<p>利用バージョンは以下の通り。</p>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a> 1.6.0a</li>
<li>ajax im 3.2</li>
</ul>
<h3><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>のインストール</h3>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>のサイトからApache, PHP, MySQLを含んだパッケージを選んでダウンロード。</li>
<li>setup_xampp.batなどを実行して、適宜インストールする。インストーラなら不要。</li>
</ul>
<h3>ajax imのダウンロード、展開</h3>
<ul>
<li>以下の場所からajax imをダウンロード<ul>
<li><a href="http://www.ajaxim.com/">http://www.ajaxim.com/</a></li>
</ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>のhtdocs以下にajaximなどのフォルダを作ってファイルを展開する。</li>
</ul>
<h3>インストール作業</h3>
<ul>
<li>xampp_control.exeから、MySQLを起動</li>
<li>以下のようにMySQLクライアントを起動</li>
</ul>
<pre>XAMPPパス\mysql\bin\mysql.exe -u root mysql
</pre>
<ul>
<li>以下のようにDBを作成</li>
</ul>
<pre>create database ajaxim charset utf8;
exit
</pre>
<ul>
<li>install.phpをメモ帳等で開いて、</li>
</ul>
<pre>INDEX ( `user` , `group` )
</pre>
<p>となっている２箇所を、</p>
<pre>INDEX ( `user`(20) , `group`(20) )
</pre>
<p>などと編集する。</p>
<ul>
<li>xampp_control.exeから、Apacheを起動</li>
<li>以下のURLを開く。</li>
</ul>
<pre>http://localhost/ajaxim/install.php
</pre>
<ul>
<li>管理者名、パスワード等を入力してInstallボタンを押す。</li>
<li>成功したら、以下のURLを開いてログイン</li>
</ul>
<pre>http://localhost/ajaxim/
</pre>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
