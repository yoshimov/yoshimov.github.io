---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 10.10に<a href="http://www.google.co.jp/">Google</a> <a href="http://sketchup.google.co.jp/">SketchUp</a> 8を入れる方法のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="/?page=Lenovo+IdeaPad+S9e" class="wikipage">Lenovo IdeaPad S9e</a></li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 10.10</li>
<li>Wine 1.3.6</li>
<li><a href="http://www.google.co.jp/">Google</a> <a href="http://sketchup.google.co.jp/">SketchUp</a> 8</li>
</ul>
<h3>手順</h3>
<ul>
<li>最新のWineをインストール<ul>
<li><a href="/?page=Ubuntu%2FWine1%2E3%A4%CE%A5%A4%A5%F3%A5%B9%A5%C8%A1%BC%A5%EB" class="wikipage">Ubuntu/Wine1.3のインストール</a></li>
</ul>
</ul>
<p>標準のWine 1.2だとうまく行かなかったので、PPAから最新版を入れておきます。</p>
<ul>
<li><a href="http://www.google.co.jp/">Google</a> <a href="http://sketchup.google.co.jp/">SketchUp</a> 8をインストール<ul>
<li><a href="http://sketchup.google.com/">http://sketchup.google.com/</a></li>
</ul>
</ul>
<p>通常通り、<a href="http://www.google.co.jp/">Google</a>のサイトからダウンロードしてインストールすると、Wineから起動可能な状態になります。インストール先はデフォルトのままで良いです。</p>
<ul>
<li>一旦<a href="http://sketchup.google.co.jp/">SketchUp</a>を起動</li>
</ul>
<p>起動すると、OpenGLのエラーが表示されて、強制終了します。終了しなければそのまま使ってかまいません。</p>
<ul>
<li>レジストリを編集</li>
</ul>
<pre>wine regedit
</pre>
<p>としてレジストリエディタを起動して、</p>
<pre>HKEY_CURRENT_USER\Software\Google\SketchUp8\GLConfig\Display
</pre>
<p>のHW_OKを、1に変更します。</p>
<ul>
<li>ショートカットを初期化</li>
</ul>
<p>最初に起動した状態だと、キーボードショートカットが使えないので、</p>
<pre>Window-&gt;Preferences-&gt;Shortcuts
</pre>
<p>を開いて、Reset Allボタンを押すと、ショートカットが使えるようになります。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
