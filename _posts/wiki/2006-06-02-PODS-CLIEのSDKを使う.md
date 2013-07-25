---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>ヘッダファイル書き換え</h3>
<p>Palm OS Developer Suiteで<a href="http://www.sony.jp/CLIE/">CLIE</a>のSDKを使用するには、PRC-Toolsで使う時と同じように、ヘッダファイルを書き換える必要があります。</p>
<ul>
<li><a href="http://homepage1.nifty.com/abby/PalmTech/DvPr/sony-sdk.html">PRC-Tools for CLIE</a></li>
</ul>
<p>ヘッダファイルを書き換えるPerl Scriptがダウンロードできなくなってるみたいなので、作ってみました。</p>
<ul>
<li><span class="error">refプラグインは存在しません。</span></li>
</ul>
<p><a href="http://www.sony.jp/CLIE/">CLIE</a> SDKを展開して出来る Incs/Libraries にこのファイルをコピーして、</p>
<pre>perl convert-gcc.pl
</pre>
<p>と実行してください。</p>
<p>実行結果については責任は持ちませんので、あくまで自己責任でお願いします。</p>
<h3>include追加</h3>
<p>Sony SDKのincludeにはFileStream.hが足りないようで、コンパイルするとFileHandleがありません、というエラーが出ます。</p>
<p>Sony<a href="http://www.sony.jp/CLIE/">CLIE</a>.hを編集して、各ヘッダファイルをincludeする前の部分に</p>
<pre>#include &lt;FileStream.h&gt;
</pre>
<p>を入れておくと、エラーが出なくなります。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
