---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>TableType は，</p>
<pre>TblSetRowHeight()
</pre>
<p>で行を任意の高さに設定した場合，callback には正しい RectangleType が渡されるが，テーブルが持っている Highlight 処理が，フォントの高さを基準にしている（らしい）ため，表示がおかしくなる．</p>
<p>このため，<a href="http://www.sony.jp/CLIE/">CLIE</a> のハイレゾなどに対応しようとすると，標準のテーブルの Highlight 処理は使えない．</p>
<p>これを回避するには，自前でタップをハンドリングするようなHighlight 処理を作ってやる必要がある．</p>
<p><em>OS 5 では直るんでしょうか？まぁ直っても，OS 3.x じゃ動かないから意味ないか．</em></p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
