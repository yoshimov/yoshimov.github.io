---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>Windows7環境で，NTPサーバと時刻を同期する方法のメモ．</p>
<h3>環境</h3>
<ul>
<li>Windows 7 Enterprise 64bit</li>
</ul>
<h3>手順</h3>
<p>時刻の同期設定を行うには，w32tmコマンドを使います．</p>
<ul>
<li><a href="http://technet.microsoft.com/en-us/library/bb491016.aspx">W32tm</a></li>
</ul>
<p>管理者権限のコマンドプロンプトをひらいて，</p>
<pre>w32tm /monitor
</pre>
<p>と実行すると，現在同期中のサーバの一覧と時刻の差が表示されます．</p>
<p>これが正しくない場合は，</p>
<pre>w32tm /resync /rediscover
</pre>
<p>などを実行して，新しいNTPサーバを発見します．</p>
<p>これでもうまくいかない場合，以下のようにNTPサーバを手動登録します．</p>
<pre>w32tm /config /manualpeerlist:&quot;ntp.jst.mfeed.ad.jp&quot;
</pre>
