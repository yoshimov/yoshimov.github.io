---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>上でdebパッケージを作る方法です。とりあえずバイナリパッケージのみを手っ取り早く作ります。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10</li>
</ul>
<h3>手順</h3>
<h4>必要ソフトのインストール</h4>
<pre>sudo aptitude install dpkg-dev dh-make debhelper fakeroot
</pre>
<p>以下は必要に応じて。</p>
<pre>sudo aptitude install devscripts gnupg lintian pbuilder devscripts
</pre>
<h4>インストールするソフトの用意</h4>
<p>本来は通常のオープンソースツールを<a href="http://www.debian.org/">Debian</a>用にパッケージするためのツールなので、決まった形式のファイルとフォルダを用意しておく必要があります。例えばツールの名前がhogeで、バージョン1.0だった場合、</p>
<pre>hoge-1.0.tar.gz
hoge-1.0/
  ソースやバイナリファイル群
</pre>
<p>という関係で、tar.gzファイルとフォルダを用意しておきます。元が<a href="http://bazaar-vcs.org/">Bazaar</a>リポジトリだった場合、フォルダの名前を上記のように変更してから、</p>
<pre>cd hoge-1.0
bzr export ../hoge-1.0.tar.gz
</pre>
<p>としてやるとtar.gzファイルを作れます。</p>
<h4>ひな型ファイルの生成</h4>
<p>上記の形式のフォルダを用意した後、</p>
<pre>dh_make -e hoge@gmail.com -c gpl -f ../hoge-1.0.tar.gz
</pre>
<p>と実行すると、debianというフォルダが作られてその中にcontrolなどの必要ファイルのひな型が生成されます。</p>
<p>ひな形ファイルが出来上がったら、上記tar.gzファイルは削除してしまっても問題ありません。</p>
<h4>設定ファイルの編集</h4>
<p>重要なのは、</p>
<ul>
<li>control</li>
<li>rules</li>
<li>postinst</li>
<li>changelog</li>
</ul>
<p>あたりです。</p>
<p>controlには主に依存関係と説明を記述します。</p>
<p>依存関係は</p>
<pre>Depends: python, ruby
</pre>
<p>という感じで列挙していきます。途中で改行しても大丈夫です。</p>
<p>説明は</p>
<pre>Description: 短い説明
 長い説明
</pre>
<p>と言う感じに記述します。もちろん英語です。</p>
<p>あとは、rulesファイルにmakefile形式でインストール方法を記述します。注意するのは、DESTDIRとして書かれている</p>
<pre>hoge-1.0/debian/hoge/
</pre>
<p>を、ルートディレクトリと見立ててインストールするという点です。</p>
<p>例えば、/usr/bin にインストールする hoge-exec であれば、</p>
<pre>hoge-1.0/debian/hoge/usr/bin/hoge-exec
</pre>
<p>にインストールします。またrulesに書かれたインストール処理はパッケージを作成する際に行われ、配布したパッケージを実際にインストールする際にはここからファイルがコピーされるだけです。</p>
<p>あとは、パッケージのインストール後に設定等が必要な場合は、postinstなどに必要な処理を記述しておきます。</p>
<p>changelogの最初の行には、作成するパッケージのバージョンを記述します。バージョンは、1.0-2のように、オリジナルのバージョンの後ろにパッケージのバージョンを付加する形にします。</p>
<p>changelogの編集には、以下のようにdevscriptsに含まれるdebchangeコマンドを使うと便利です。</p>
<pre>debchange -i
</pre>
<h4>パッケージの作成</h4>
<p>dpkg系のコマンドを使うとソースのパッケージの作成も同時に行われるので、バイナリパッケージだけを作成するには、</p>
<pre>cd hoge-1.0
fakeroot debian/rules binary
</pre>
<p>とすると、一個上のディレクトリにdebファイルができます。あとはこのdebファイルを配布すれば簡単にインストールができます。</p>
<h4>debファイルのインストール</h4>
<p>debファイルが依存関係を多く持っている場合は、apt用パッケージリストを作って、apt-getなどでインストールします。</p>
<ul>
<li><a href="/?page=Ubuntu%2Fdeb%A5%D5%A5%A1%A5%A4%A5%EB%A4%F2%B0%CD%C2%B8%A5%D1%A5%C3%A5%B1%A1%BC%A5%B8%A4%C8%C6%B1%BB%FE%A4%CB%A5%A4%A5%F3%A5%B9%A5%C8%A1%BC%A5%EB%A4%B9%A4%EB" class="wikipage">Ubuntu/debファイルを依存パッケージと同時にインストールする</a></li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://www.debian.org/doc/maint-guide/">Debian New Maintainers' Guide</a></li>
</ul>
