---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>cronから送られてくるメールに、日本語などの２バイト文字があるとよく文字化けするので、その対処方法です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.5</li>
</ul>
<h3>手順</h3>
<p>要はメールヘッダに記載されているContent-Typeと、cronジョブからの出力の文字コードを一致させれば良いので、Content-Typeがcharset=UTF-8の場合は、</p>
<pre>LC_ALL=ja_JP.UTF-8 hoge.sh
</pre>
<p>という感じでロケールを明に指定してスクリプトなどを実行してやります。</p>
<p>メールの文字コードをJIS(iso-2022-jp)にしたければ、</p>
<pre>CONTENT_TYPE=&quot;text/plain; charset=iso-2022-jp&quot;
LC_ALL=ja_JP.jis hoge.sh
</pre>
<p>などとします。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
