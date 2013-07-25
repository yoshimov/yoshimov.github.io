---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>PowerPoint, Word, ExcelのOfficeアプリのファイルを、エクスプローラから直接読み取り専用で開く方法のメモ。</p>
<p>Windows Vista/7向けです。</p>
<h3>環境</h3>
<ul>
<li>Windows 7 Enterprise</li>
</ul>
<h3>手順</h3>
<ul>
<li>以下のページにあるWindows Scriptを、Office_readonly.vbsなどのファイル名で適当な場所に保存する。ここでは C:\App\VBS\Office_readonly.vbs としています。<ul>
<li><a href="https://gist.github.com/1253177">https://gist.github.com/1253177</a></li>
</ul>
<li>エクスプローラで C:\Users\&lt;自分のアカウント名&gt;\AppData\Roaming\Microsoft\Windows\SendTo を開く。</li>
<li>以下の内容で新しいショートカットを作成<ul>
<li>名前: 読み取り専用で開く</li>
<li>リンク先: wscript.exe &quot;C:\App\VBS\Office_readonly.vbs&quot;</li>
</ul>
<li>あとは、エクスプローラからPPTファイルなどを選んで、右クリックから [送る]-[読み取り専用で開く] で、読み取り専用で開けるようになります。</li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://www.alato.ne.jp/kazu-/vb/etc_tip01.htm">Microsoft Officeファイルの「読み取り専用で開く」をショートカット化</a></li>
</ul>
