---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<p>Windowsサーバに、<a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>を使ってBugzillaをインストールする手順のメモ。</p>
<h3>利用バージョン</h3>
<ul>
<li>Bugzilla 3.0.1</li>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a> 1.6.0a</li>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a> perl addon 5.8.8-2.2.4</li>
</ul>
<h3><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>インストール</h3>
<h4>ダウンロード</h4>
<ul>
<li><a href="http://www.apachefriends.org/jp/xampp-windows.html">http://www.apachefriends.org/jp/xampp-windows.html</a></li>
</ul>
<p>から<a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>とperl add-onをダウンロード。</p>
<h4><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>パッケージを展開</h4>
<p>任意のディレクトリに<a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>を展開する</p>
<h4>Perl add-onを展開</h4>
<p>Perl add-onを<a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>のディレクトリに上書き展開する。</p>
<h4><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>セットアップ</h4>
<ul>
<li>以下のバッチを実行する。</li>
</ul>
<pre>XAMPPルート\setup_xampp.bat
</pre>
<ul>
<li>Proxyを利用している場合は、環境変数に以下の記述を追加する。</li>
</ul>
<pre>HTTP_proxy=http://proxyサーバ:proxyポート番号
</pre>
<h3>Bugzillaのインストール</h3>
<h4>ダウンロード</h4>
<ul>
<li><a href="http://www.bugzilla.org/download/">http://www.bugzilla.org/download/</a></li>
</ul>
<p>からtar.gzをダウンロード。</p>
<h4>展開</h4>
<p><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>直下あたりにBugzillaを展開。</p>
<h4>Perlモジュールを用意する</h4>
<ul>
<li>コマンドプロンプトから以下を実行する。</li>
</ul>
<pre>XAMPPフルパス\perl\bin\perl.exe checksetup.pl --check-modules
</pre>
<ul>
<li>エクスプローラから以下のbatを実行する。</li>
</ul>
<pre>XAMPPフルパス\perl\bin\ppm-shell.bat
</pre>
<ul>
<li>以下のコマンドを実行する。</li>
</ul>
<pre>repo add theory58S http://theoryx5.uwinnipeg.ca/ppms
repo add landfill http://www.landfill.bugzilla.org/ppm/
install Email-Send
install Template-Toolkit
install Email-MIME-Modifier
remove File-Spec
install PathTools
</pre>
<ul>
<li>以下はオプション</li>
</ul>
<pre>install GD
install Template-GD
install Chart
install GDGraph
install MIME-tools
install Email-Reply
install Email-MIME-Attachment-Stripper
install PatchReader
</pre>
<ul>
<li>もう一度、checksetupを実行して、モジュールがインストールされていることを確認する。</li>
</ul>
<pre>XAMPPフルパス\perl\bin\perl.exe checksetup.pl
</pre>
<p>メールサーバや管理者情報は適宜入力する。</p>
<h4>MySQL設定</h4>
<ul>
<li>bugzillaルート\localconfig を以下のように編集する。</li>
</ul>
<pre>$db_driver='mysql'
$db_user='root'
$db_pass=''
</pre>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>ルート\mysql\bin\my.cnf を以下のように編集する。</li>
</ul>
<pre>[mysqld]
max_allowed_packet=512M
ft_min_word_len=2
</pre>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>ルート\xampp-control.exeを実行する。</li>
<li>MySQLのstartボタンを押す。</li>
<li>コマンドプロンプトから以下のコマンドを実行する。</li>
</ul>
<pre>XAMPPルート\mysql\bin\mysql.exe -u root mysql
</pre>
<ul>
<li>以下のSQLを実行する。</li>
</ul>
<pre>create database bugs charset utf8;
</pre>
<ul>
<li>checksetupを再実行して、DBスキーマを構築する。</li>
</ul>
<pre>XAMPPフルパス\perl\bin\perl.exe checksetup.pl
</pre>
<ul>
<li>mod_perl.plを編集して、以下の３行をコメントアウトする。</li>
</ul>
<pre>#use Apache2::SizeLimit;
#$Apache2::SizeLimit::MAX_UNSHARED_SIZE = 70000;
#    PerlCleanupHandler  Apache2::SizeLimit
</pre>
<h4>Apacheの設定</h4>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a>ルート\apache\conf\httpd.conf を、以下のように編集する。</li>
</ul>
<pre>Alias /bugs &quot;XAMPPフルパス\bugzilla-3.0.1&quot;
PerlSwitches -IXAMPPフルパス\bugzilla-3.0.1 -w -T (ダブルクオートは付けない)
PerlConfigRequire &quot;XAMPPフルパス\bugzilla-3.0.1\mod_perl.pl&quot;
</pre>
<p>以下は必要に応じて。bugzillaをhtdocs以下に置いていれば不要。</p>
<pre>&lt;Directory /&gt;
# AllowOverride None
# Deny from all
&lt;/Directory&gt;
</pre>
<ul>
<li><a href="http://www.apachefriends.org/en/xampp.html">XAMPP</a> ControlからApacheを起動する。</li>
</ul>
<p>これで</p>
<pre>http://localhost/bugs/
</pre>
<p>でBugzillaのスタートページが見れれば、インストール成功。</p>
<h3>課題</h3>
<ul>
<li>パラメータの変更がうまくいかない。<ul>
<li>とりあえずdata\paramsを手動で編集する。</li>
</ul>
</ul>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
