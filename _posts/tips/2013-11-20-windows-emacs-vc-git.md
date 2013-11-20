---
layout: post
category: tips
tags: tips emacs windows git
title: Windows版Emacsでvc-gitを使う
---
{% include keywords.md %}

## 概要

Windows版[Emacs]は動作も速くなってかなり使えるようになりましたが、
vc-gitが日本語ファイル名でうまく動作しないという問題があったので、
その解決方法です。

## 環境

* Windows 7
* [Emacs] 24.3
* [Cygwin] 1.7.20
* [Git] for Win 1.8.4

## インストール

Emacsは、[Chocolatey]を使うと

    > cinst emacs

でインストールできます。

ここでは、

	set LANG=ja_JP.UTF-8

となっていて、Gitは全てUTF-8を前提にしています。

## 設定

環境変数 `HOME` を設定した後、`~/.emacs.d/init.el`に、
以下の設定を追加します。

<pre>
(prefer-coding-system 'utf-8-dos)
(set-default-coding-systems 'utf-8-dos)
(set-keyboard-coding-system 'utf-8-dos)
(setq file-name-coding-system 'cp932)
(setq default-process-coding-system '(utf-8 . cp932))
(setq git-commits-coding-system 'utf-8)
</pre>

要はgitコマンドを実行する際に、引数に渡すファイル名やらを
cp932(WindowsのシフトJIS)に文字コード変換してやります。

これで`vc-print-log`や`vc-diff`もうまく動くようになりました。

## おまけ

どうも`file-name-coding-system`を指定しただけでは、そもそも
日本語のファイルをGitに入っていると認識してくれない。

そこで、`lisp/vc/vc-git.el`の`vc-git-registered`あたりを追っていくと、

	(vc-git--out-ok "ls-files" "-c" "-z" "--" name)

でチェックしていることがわかる。

そこで試しに、`*scratch*`モードで

	(cd "hoge")
	(vc-git--out-ok "ls-files" "-c" "-z" "--" "日本語ファイル")

とすると、ファイル名が返ってこない。
どうも`vc-git--out-ok`は`process-file`を使っているようなので、
`default-process-coding-system`あたりが怪しい感じがする。

Emacsのマニュアルを見るとcons cellを設定しろというので、

	(setq default-process-coding-system '(utf-8 . cp932))

としてから、

	(vc-git--out-ok "ls-files" "-c" "-z" "--" "日本語ファイル")

を実行すると、無事ファイル名が返ってきた。

## 参考

* [NTEmacs の vc-git で Cygwin の git を使う](http://d.hatena.ne.jp/tsntsumi/20100913/UsingCygwinsGitOnNTEmacsVC)
* [NTEmacs で git.el を使ってコミットするときに日本語が使えない](http://d.hatena.ne.jp/toshiharu_z/20091216/1260938098)
* [NTEmacs 23.1.Xを使ってみる](http://moimoitei.blogspot.jp/2010/05/use-ntemacs-231x.html)
* [Default Coding Systems](http://www.gnu.org/software/emacs/manual/html_node/elisp/Default-Coding-Systems.html)
