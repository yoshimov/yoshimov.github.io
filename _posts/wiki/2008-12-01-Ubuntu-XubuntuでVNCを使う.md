---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>の軽量ディストリビューションのXubuntuでVNCサーバを利用する方法です。</p>
<h3>環境</h3>
<ul>
<li>Xubuntu 8.10</li>
</ul>
<h3>手順</h3>
<ul>
<li>通常どおりXubuntuをインストールする</li>
<li>Synapticでx11vncをインストールする</li>
<li>以下のようにパスワードを設定</li>
</ul>
<pre>x11vnc -storepasswd
</pre>
<ul>
<li>以下のようにパスワード付きでVNCサーバを起動</li>
</ul>
<pre>x11vnc -usepw -display :0
</pre>
<ul>
<li>他のPCからVNCクライアントでつなぐ</li>
</ul>
