---
layout: post
category: tips
tags: tips emacs evernote
title: Emacsでお手軽Markdownメモ帳
---
{% include keywords.md %}

## 概要

[Emacs]を使って、キー操作ですぐにMarkdownでメモができるファイルを作成、
保存したファイルをキー操作ですぐに[Evernote]に送信する方法です。

## 環境

* Windows 7
* [Emacs] 24.3

## 手順

まずはMarkdown modeをインストールします。
以下のサイトから`markdown-mode.el`をダウンロードして、
ロードパスに置いてください。
わからなければ、Emacsのsite-lisp内で良いです。

* [Markdown mode](http://jblevins.org/projects/markdown-mode/)

次に、Markdownファイルを置くフォルダを作成します。
普通のフォルダで良いですが、Gitのリポジトリなどにすると
より保存などもやりやすくなります。

    > mkdir c:\markdown-memo

Evernoteクライアントを入れている場合は、インポートフォルダを
設定しておきます。ここでは `c:\evernote` と仮定しています。

そして、`~/.emacs.d/init.el`に以下の記述を追加します。

<pre>
;; Markdown mode
;;  <http://jblevins.org/projects/markdown-mode/>

(autoload 'markdown-mode "markdown-mode"
       "Major mode for editing Markdown files" t)
(add-to-list 'auto-mode-alist '("\\.text\\'" . markdown-mode))
(add-to-list 'auto-mode-alist '("\\.markdown\\'" . markdown-mode))
(add-to-list 'auto-mode-alist '("\\.md\\'" . markdown-mode))

;; Markdown memo

(defun markdown-memo-sendto-evernote ()
  "Copy markdown file into evernote folder as text file."
  (interactive)
  (let* ((orgbuf (current-buffer))
	 (orgname (buffer-file-name))
	 (memonameorg (file-name-nondirectory orgname))
	 (memoname (concat (file-name-sans-extension memonameorg) ".txt"))
	 (destname (concat markdown-memo-evernote-dir memoname)))
    (with-temp-buffer
      (insert memonameorg)
      (insert "\n")
      (insert-buffer orgbuf)
      (setq buffer-file-coding-system 'cp932)
      (write-region (point-min) (point-max) destname)
      )
    )
  )
(defun markdown-memo-create-memo ()
  "Create new markdown memo file into specified folder."
  (interactive)
  (let* ((defaultfilename (format-time-string "%Y-%m-%d.md" (current-time)))
	 (orgname (read-string "memo file: " defaultfilename))
	 (memofile (concat markdown-memo-root-dir orgname)))
    (find-file memofile))
  )
(setq markdown-memo-root-dir "c:/markdown-memo/")
(setq markdown-memo-evernote-dir "c:/evernote/")
(global-set-key "\C-xce" 'markdown-memo-sendto-evernote)
(global-set-key "\C-xcc" 'markdown-memo-create-memo)
</pre>

あとはEmacsを起動なおして、`Ctrl+x c c` で新しいメモファイルの作成、
編集が終わったら `Ctrl+x c e` でEvernoteにテキストとして送信することが
できるようになります。

## 参考

* [Parsing and Formatting Times](http://www.gnu.org/software/emacs/manual/html_node/elisp/Time-Parsing.html)
* [File Name Components](http://www.gnu.org/software/emacs/manual/html_node/elisp/File-Name-Components.html#File-Name-Components)
