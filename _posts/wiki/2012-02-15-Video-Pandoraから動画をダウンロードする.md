---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>Pandora.TVからの動画のダウンロードは、リファラーチェックやアクセス元IPのチェックが入ったおかげで少々コツが必要になりました。</p>
<p>2012.2現在うまく行っている手順をメモしておきます。Vid-DLを使うとだいぶ簡単になりました。</p>
<h3>環境</h3>
<ul>
<li>Windows Vista</li>
<li><a href="http://www.orbitdownloader.com/">Orbit</a> V4.1.0.2</li>
</ul>
<h3>2012.2手順</h3>
<ul>
<li>Pandoraでダウンロードしたい動画を開く。</li>
<li>CMが終わったぐらいのところで一旦停止する。</li>
<li>別のタブで以下のサイトを開く。<ul>
<li><a href="http://www.vid-dl.net/">http://www.vid-dl.net/</a></li>
</ul>
<li>Pandoraの動画のURLをペーストして、ダウンロードボタンを押す。</li>
<li>Downloadという下向き矢印のついた黄色いボタンのリンク先を調べて、trans-idxから始まっていないURLだった場合は、もう一度URLのペーストからやり直す。</li>
<li><a href="http://www.orbitdownloader.com/">Orbit</a>のNewで、Downloadリンクをダウンロードする。</li>
</ul>
<p>ダウンロードしたFLVファイルは、<a href="http://www.videolan.org/vlc/">VLC</a> Playerなどで再生できますし、<a href="http://www.dvdstyler.de/">DVDStyler</a>などを使えば簡単にDVDにできます。</p>
<h3>2010.8手順</h3>
<h4>準備</h4>
<p>ダウンロードに使う<a href="http://www.orbitdownloader.com/">Orbit</a>をインストールしておきます。また、ダウンロードしたい動画のあるPandora.TVのURLも必要です。</p>
<h4><a href="http://www.orbitdownloader.com/">Orbit</a>の設定</h4>
<p>ダウンロードには韓国のProxyを利用する必要があるので、以下のサイトなどで利用可能な韓国のHTTP Proxyを調べます。</p>
<ul>
<li>以下のサイトを開く<ul>
<li><a href="http://www.cybersyndrome.net/country.html">http://www.cybersyndrome.net/country.html</a></li>
</ul>
<li>韓国(KR)のProxyボタンを押す</li>
<li>検索結果の１番目をメモ</li>
</ul>
<p>ここで得られたIPアドレスとポートを、<a href="http://www.orbitdownloader.com/">Orbit</a>に設定します。</p>
<ul>
<li><a href="http://www.orbitdownloader.com/">Orbit</a>で Tools-&gt;Preferences-&gt;Proxy を開く</li>
<li>Internet Explorer Default Proxyのチェックを外す</li>
<li>Proxy Typeから HTTP&lt;Get&gt;を選択</li>
<li>HostとPortに韓国ProxyのIPアドレスとポートを入れる</li>
</ul>
<h4>動画のダウンロード</h4>
<p>まずはFLVファイルのURLを調べます。</p>
<ul>
<li>以下のサイトを開く<ul>
<li><a href="http://mm-video.net/">http://mm-video.net/</a></li>
</ul>
<li>ダウンロードしたいPandora.TVの動画のURLを貼り付けて、ダウンロードボタンをクリック</li>
<li>保存用のURLが表示されるので、これをコピー</li>
<li><a href="http://www.orbitdownloader.com/">Orbit</a>のNewボタンを押す</li>
<li>Save asに入力されたファイル名を分かりやすい名前に変更</li>
<li>More-&gt;Browser Contextタブを開いて、Referer: にPandora.TVの動画のURLを貼り付け</li>
<li>Download ボタンを押す</li>
</ul>
<p>あとはダウンロードが終わるまで待つだけです。エラーになってしまう場合は、違うProxyを設定しなおして試してみてください。</p>
<p>ダウンロードしたFLVファイルは、<a href="http://www.videolan.org/vlc/">VLC</a> Playerなどで再生できますし、<a href="http://www.dvdstyler.de/">DVDStyler</a>などを使えば簡単にDVDにできます。</p>
