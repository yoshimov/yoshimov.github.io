---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>Windowsのアプリ上でEmacsキーバインディングを有効にする、<a href="http://www.cam.hi-ho.ne.jp/oishi/">Xkeymacs</a>の自分用設定のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.cam.hi-ho.ne.jp/oishi/">Xkeymacs</a> 3.47</li>
<li>Windows 7</li>
</ul>
<h3>設定</h3>
<h4>標準</h4>
<p>私はIMEのオンオフには Ctrl+o を使ってるので、<table>
<tr>
<th>機能</th>
<th>キー</th>
</tr>
<tr>
<td>[IMEの切り替え]-[toggle-input-method]</td>
<td>Ctrl+o</td>
</tr>
<tr>
<td>[移動]-[scroll-down]</td>
<td>Ctrl+z</td>
</tr>
<tr>
<td>[移動]-[beginning-of-buffer]</td>
<td>Ctrl+x [</td>
</tr>
<tr>
<td>[移動]-[end-of-buffer]</td>
<td>Ctrl+x ]</td>
</tr>
</table>
を割り当ててます。あとは大体そのまま。</p>
<p>忘れずに、同じ設定をダイアログの方にもしておきます。</p>
<h4><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a></h4>
<p><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a>では結構キーボードショートカットを使うので、独自設定を使うようにしてます。</p>
<p>以下のキーは、設定を解除。</p>
<ul>
<li>C-u</li>
<li>C-t</li>
<li>C-Space</li>
<li>C-r</li>
<li>C-s</li>
<li>C-g</li>
</ul>
<p>C-wは好みの分かれるところですが、私はFireGestureでタブを閉じることにして、<a href="http://www.cam.hi-ho.ne.jp/oishi/">Xkeymacs</a>を有効にしています。</p>
<h4><a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a></h4>
<p><a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a>はEmacsキーバインドで使えるテキストエディタなので基本的に設定は不要ですが、IMEのオンオフだけを<a href="http://www.cam.hi-ho.ne.jp/oishi/">Xkeymacs</a>で切り替えてます。siteinit.lに書いても良いですが、こちらのほうがお手軽なので。</p>
