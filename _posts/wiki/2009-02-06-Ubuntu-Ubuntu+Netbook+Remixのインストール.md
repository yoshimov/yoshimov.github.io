---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li> <a href="http://www.ubuntu.com/">Ubuntu</a> 8.10</li>
</ul>
<h3>概要</h3>
<p>画面の狭いネットブック向けにカスタマイズされたデスクトップを導入する方法です。こんな感じのランチャーが使えるようになります。</p>
<p><a href="https://wiki.ubuntu.com/UNR?action=AttachFile&do=get&target=unr-desktop-small.png">https://wiki.ubuntu.com/UNR?action=AttachFile&amp;do=get&amp;target=unr-desktop-small.png</a></p>
<h3>手順</h3>
<h4>必要アプリのインストール</h4>
<ul>
<li>Synapticを起動</li>
<li>[設定]-[リポジトリ]を選択</li>
<li>[<a href="http://www.ubuntu.com/">Ubuntu</a>のソフトウェア]タブの「コミュニティによるメンテナンスされるオープンソースソフトウェア」にチェックを入れる。</li>
<li>[サードパーティのソフトウェア]タブを選ぶ</li>
<li>[追加]ボタンを押して、以下の内容を入力</li>
</ul>
<pre>deb http://ppa.launchpad.net/netbook-remix-team/ubuntu intrepid main
</pre>
<ul>
<li>再読み込みボタンを押す</li>
<li>クイック検査などで、以下のパッケージを選択して、適用ボタンを押す<ul>
<li>go-home-applet</li>
<li>human-netbook-theme</li>
<li>maximus</li>
<li>netbook-launcher</li>
<li>window-picker-applet</li>
</ul>
</ul>
<p>＃まだdesktop-switcherなどは用意されていない様子。</p>
<h4>設定の変更</h4>
<ul>
<li>[設定]-[外観の設定]を起動して[テーマ]タブで、human-netbook-themeを選ぶ</li>
<li>[視覚効果]タブで効果なしを選ぶ<ul>
<li>これをしておかないと、上のパネルがちらついたりしました</li>
</ul>
<li>[設定]-[セッション]を起動して、[自動起動するプログラム]タブを選ぶ</li>
<li>[追加]ボタンを押して以下のコマンドを自動起動するように追加<ul>
<li>netbook-launcher</li>
<li>maximus</li>
</ul>
</ul>
<p>＃ここで一旦ログインし直して、起動するか確認すると良いかもしれません</p>
<ul>
<li>画面下のパネルを削除</li>
<li>上のパネルのメニュー、アプリランチャー、右端のログアウトをバッサリ削除</li>
<li>上のパネルの左端に「ホームへ戻る」というアイテムを追加</li>
<li>上のパネルの中央に「ウィンドウピッカー」というアイテムを追加</li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="https://wiki.ubuntu.com/UNR">UNR - Ubuntu Wiki</a></li>
</ul>
