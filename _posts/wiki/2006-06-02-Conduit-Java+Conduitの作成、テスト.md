---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>HotSync 時にアプリを実行できる Java Conduit は手軽に作れて良いです。<a href="http://java.sun.com/j2se/">JDK</a>+ant で十分開発できるし。以下は私がつまずいた注意点。</p>
<ul>
<li><a href="/?page=JSync" class="wikipage">JSync</a>Installer.exe で、まず Java VM をインストールすること。既存の<a href="http://java.sun.com/j2se/">JDK</a>はHotSync時には使えません。</li>
<li>Palm 側に、Conduit 登録時に指定した Creator ID を持ったアプリがないと、Conduit は動作しない。</li>
<li><a href="/?page=JSync" class="wikipage">JSync</a>は<a href="http://java.sun.com/j2se/">JDK</a> 1.3ベースなので、1.4で変更、追加されたクラスやメソッドは使えない。</li>
</ul>
<p>Conduit は、<a href="http://www.palmos.com/dev/tech/conduits/">CDK</a> に付属してくる Conduit Configuration (Common\Bin\CondCfg.exe)を使うと、簡単に追加、削除ができる。まずこれでテストを行う。</p>
<p>Conduit のインストーラは、<a href="http://www.handx.net/">handX</a> の<a href="http://www.handx.net/devtool/pInstaller/">pInstaller</a> を使うと非常に簡単に作れる。</p>
<p>pInstaller でインストーラを作る場合は、以下のファイルを揃えて、pInstaller.exe を自動実行する自己解凍圧縮ファイルを作れば良い。</p>
<ul>
<li>condmgr.dll</li>
<li>pInstaller.exe</li>
<li>settings.xml</li>
<li>その他jar, dllなど必要ファイル</li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
