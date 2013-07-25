---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li>Java SE 6u10 (<a href="http://java.sun.com/j2se/">JDK</a>)</li>
<li>Apache Ant 1.7.1</li>
<li><a href="http://www.google.co.jp/">Google</a> App Engine for Java SDK 1.2.0</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.google.co.jp/">Google</a> App Engine for Java(以下GAEJ)にWebアプリを登録するまでの手順と注意点です。</p>
<h3>手順</h3>
<h4>環境のセットアップ</h4>
<ul>
<li><a href="http://java.sun.com/j2se/">JDK</a>のインストール<ul>
<li><a href="http://java.sun.com/javase/downloads/index.jsp">http://java.sun.com/javase/downloads/index.jsp</a></li>
</ul>
</ul>
<p>JREではなく<a href="http://java.sun.com/j2se/">JDK</a>が必要。また、<strong>\Windows\System32よりも先に<a href="http://java.sun.com/j2se/">JDK</a>のbinにPathを通しておくこと。</strong></p>
<p>現状のGAEJは、JAVA_HOME等を見てくれないようで、JREのJavaが先にあるとjavacが実行できなくなるようです。</p>
<ul>
<li>Apache Antのインストール<ul>
<li><a href="http://ant.apache.org/bindownload.cgi">http://ant.apache.org/bindownload.cgi</a></li>
</ul>
</ul>
<p>普通にzipを展開して、binにPathを通しておけば問題ありません。</p>
<ul>
<li>GAEJ SDKのインストール<ul>
<li><a href="http://code.google.com/intl/en/appengine/downloads.html">http://code.google.com/intl/en/appengine/downloads.html</a></li>
<li>2009/4/10現在では、英語のページからしかJava SDKはダウンロードできません。</li>
</ul>
</ul>
<p>これもzipを展開して、binにPathを通しておきます。</p>
<ul>
<li>Proxyの設定（オプション）</li>
</ul>
<p>Proxy越しに利用する場合は、以下のようにappcfg.cmdを編集します。<blockquote><p>@java -Dhttp.proxyHost=&lt;host&gt; -Dhttp.proxyPort=&lt;port&gt; -Dhttps.proxyHost=&lt;host&gt; -Dhttps.proxyPort=&lt;port&gt; -cp &quot;%~dp0\..\lib\appengine-tools-api.jar&quot; com.google.appengine.tools.admin.AppCfg %*</p>
</blockquote>
</p>
<h4>アプリIDの登録</h4>
<ul>
<li>App Engineダッシュボードにログイン<ul>
<li><a href="http://appengine.google.com/">http://appengine.google.com/</a></li>
</ul>
</ul>
<p><a href="http://www.google.co.jp/">Google</a>アカウントがなければ作成後、ダッシュボードにログインします。</p>
<ul>
<li>[Create an Application]ボタンを押す。</li>
<li>IDを入力して、[Save]ボタンを押す。</li>
</ul>
<h4>アプリIDの設定</h4>
<ul>
<li>作成したアプリの war/WEB-INF/appengine-web.xml を編集</li>
<li>以下の箇所にIDを記入する。</li>
</ul>
<pre>&lt;application&gt;hoge&lt;/application&gt;
</pre>
<h4>コマンドラインからのアプリのデプロイ</h4>
<ul>
<li>作成したアプリのルートに移動</li>
<li>以下のコマンドを実行</li>
</ul>
<pre>appcfg update war
</pre>
<p><a href="http://www.google.co.jp/">Google</a>のアカウントとパスワードを入力すると、アプリがデプロイされます。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
