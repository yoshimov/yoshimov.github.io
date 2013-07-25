---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>私が行った方法をメモしておきます。</p>
<h3>準備</h3>
<p>以下のソフトをダウンロードして用意します。</p>
<ul>
<li><a href="http://www.dvdshrink.org/what_jp.html">DVD Shrink</a></li>
<li><a href="http://www.xvidmovies.com/codec/">XviD</a> Codec</li>
<li><a href="http://mitiok.ma.cx/">Lame</a> MP3 Codec</li>
<li><a href="http://flaskmpeg.sourceforge.net/">FlaskMPEG</a> 0.58</li>
<li><a href="http://download.microsoft.com/download/7/b/6/7b6abd84-7841-4978-96f5-bd58df02efa2/winxpvirtualcdcontrolpanel_21.exe">Virtual CD-ROM Control Panel for Windows XP</a></li>
</ul>
<h3>インストール</h3>
<p>上記ソフトを全てインストールします。<a href="http://flaskmpeg.sourceforge.net/">FlaskMPEG</a>以外は、最新版でよいと思います。<a href="http://flaskmpeg.sourceforge.net/">FlaskMPEG</a>は最新版だと不安定なので、１つ前の0.58をインストールします。</p>
<h3>作成手順</h3>
<h4><a href="http://www.dvdshrink.org/what_jp.html">DVD Shrink</a>でISOイメージ作成</h4>
<p><a href="http://www.dvdshrink.org/what_jp.html">DVD Shrink</a>を使って、DVDからISOイメージを作成します。</p>
<h4>ISOイメージをドライブにマウント</h4>
<p>Virtual CD-ROM Control Panel for Windowsを使って、ISOイメージをZ:ドライブ等にマウントします。これで、内部のVOBファイルが読み込み可能になります。</p>
<h4><a href="http://flaskmpeg.sourceforge.net/">FlaskMPEG</a>からDVDを開く</h4>
<p>VOBファイルのうち、一番容量の大きそうなものを選んで開きます。またこの際、字幕をどれにするかもあらかじめ選んでおきます。字幕が正しいかどうかはプレビューしてみるとわかります。たまに字幕を正しく読み込めないDVDもあります。（スターウォーズエピソード２など）</p>
<h4><a href="http://flaskmpeg.sourceforge.net/">FlaskMPEG</a>を設定</h4>
<p>全体の設定</p>
<ul>
<li>解像度を320x240とする。</li>
<li>アスペクト比（Aspect ratio）を変更しないようにする。</li>
<li>音声のサンプリングレートを44.1kHzに変更する。</li>
</ul>
<p>出力設定</p>
<ul>
<li>Videoは<a href="http://www.xvidmovies.com/codec/">XviD</a>を選んで、Portable Profileを選択する。</li>
<li>AudioはMP3 64k Mono等を選んでおく。</li>
</ul>
<h4>変換を開始</h4>
<p>変換を実行して、しばらく待つ。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
