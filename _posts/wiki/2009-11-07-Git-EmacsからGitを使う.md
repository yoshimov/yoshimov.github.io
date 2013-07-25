---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>最近のEmacsは標準で<a href="http://git-scm.com/">Git</a>に対応していて非常に便利なんですが、<a href="http://git-scm.com/">Git</a>の場合は通常のvcと違って若干使い方が違うので、まとめてみました。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10</li>
<li>Emacs 22.2.1</li>
</ul>
<h3>操作</h3>
<h4>pull, push</h4>
<p>どうも標準の<a href="http://git-scm.com/">Git</a>モードではpush, pullはできないようです。これは通常通りコマンドラインから実行してやります。</p>
<h4>ファイルの追加、削除</h4>
<p>ファイルをリポジトリに追加する場合は、</p>
<pre>M-x vc-register
</pre>
<p>から登録できます。また削除は、</p>
<pre>M-x vc-delete-file
</pre>
<p>です。</p>
<p>＃念のため、M-x はEscを押してからxです。Emacs使いには当たり前ですね。</p>
<h4>差分表示</h4>
<p>個人的にはもっとも良く使う機能ですが、リポジトリと作業中のファイルとの差分を表示するには、</p>
<pre>M-x vc-diff
</pre>
<p>です。CVSなどと同じですね。</p>
<h4>commit, log表示</h4>
<p>この辺は<a href="http://git-scm.com/">Git</a>独自の操作になりますが、commitする場合は、まず</p>
<pre>M-x git-status
</pre>
<p>でフォルダ内の変更点を表示します。ここでn,pで対象のファイルを選択して、lを押すとログ表示、=を押すとdiff表示ができます。</p>
<p>またMを押すとすべてのファイルに*が付きますので、その状態でcを押すとcommitモードになり、コメントを入力してからC-c C-cでcommitできます。</p>
<p>巷には独自の<a href="http://git-scm.com/">Git</a>モードがたくさんあるようですが、とりあえずEmacs 22.2.1に付いていた<a href="http://git-scm.com/">Git</a>モードの簡単な使い方でした。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
