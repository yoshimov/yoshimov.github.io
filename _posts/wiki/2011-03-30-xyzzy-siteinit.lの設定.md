---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a>はEmacs風のテキストエディタですが、起動が高速なので重宝してます。以下はその設定ファイルの設定内容です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a> 0.2.2.235</li>
</ul>
<h3>設定</h3>
<ul>
<li>以下の内容をsite-lisp/siteinit.lに保存。</li>
</ul>
<pre>; キーバインドの変更
(global-set-key '(#\C-x #\u) 'undo)
;; [ツール]-[共通設定]-[さまざま]のクリップボード同期
;(global-set-key '(#\M-w) 'copy-region-to-clipboard)
;(global-set-key '(#\C-w) 'kill-region-to-clipboard)
;(global-set-key '(#\C-y) 'paste-from-clipboard)
(global-set-key '(#\C-x #\j) 'goto-line)
(global-set-key '(#\C-x #\l) 'fill-region)
(global-set-key #\C-o 'toggle-ime)

; インクリメンタルサーチ (C-s, C-r)
(require &quot;isearch&quot;)

; バックアップを特定ディレクトリに保存する
(require &quot;backup&quot;)
(setq *backup-directory* &quot;/tmp/&quot;)
(setq *hierarchic-backup-directory* nil)

;;インデントレベルの設定
(setq java-indent-level 4)
;;インデントをタブで指定 
(setq ed::*java-indent-tabs-mode* t)

;;.groovyをJavaモードで開く
(push '(&quot;\\.groovy$&quot; . java-mode) *auto-mode-alist*)
</pre>
<ul>
<li> <a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a>.wxpを削除するか、Ctrl+Shiftを押しながら<a href="http://www.jsdlab.co.jp/~kamei/">xyzzy</a>を起動する。</li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://xyzzy.s53.xrea.com/wiki/">xyzzy Wiki</a></li>
</ul>
