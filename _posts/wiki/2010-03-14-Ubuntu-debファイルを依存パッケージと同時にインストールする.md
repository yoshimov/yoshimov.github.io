---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>依存パッケージが多いdebファイルは、dpkgでインストールしようとしてもエラーになってしまいます。aptを使って依存するパッケージをインストールする手順のメモ。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10</li>
</ul>
<h3>aptを使う方法</h3>
<h4>必要ツールのインストール</h4>
<pre>sudo aptitude install dpkg-dev
</pre>
<h4>お手軽な方法</h4>
<ul>
<li>ローカルリポジトリを作成</li>
</ul>
<p>debファイルを１つのディレクトリに集めて</p>
<pre>mkdir -p /home/debs
cd /home
cp /somewhere/hoge.deb debs
</pre>
<p>パッケージリストを作ります。</p>
<pre>dpkg-scanpackages debs /dev/null | gzip &gt; debs/Packages.gz
</pre>
<ul>
<li>aptの設定ファイル追加</li>
</ul>
<p>aptの設定ファイルにリポジトリの場所を登録します。</p>
<pre>sudo cat &gt; /etc/apt/source.conf.d/hoge-local.list
deb file:/home debs/
^d
</pre>
<p>最後の/がないとうまくいかないので注意。</p>
<ul>
<li>パッケージのインストール</li>
</ul>
<p>あとは通常どおり、aptitudeなどでインストールすれば依存関係にあるパッケージを含めてインストールができます。</p>
<pre>sudo aptitude update
sudo aptitude install hoge
</pre>
<h4>バージョンやアーキテクチャ毎に違うリポジトリを用意する場合</h4>
<ul>
<li>ローカルリポジトリの作成</li>
</ul>
<p>スキャンがやりやすいよう、jaunty, karmicなど<a href="http://www.ubuntu.com/">Ubuntu</a>のバージョン毎にフォルダを分けてdebファイルを置きます。アーキテクチャ(32bit, 64bitなど)は混在していても大丈夫です。</p>
<pre>mkdir -p /home/debs/pool/jaunty-hoge
cp xxxx.deb /home/debs/pool/jaunty-hoge
</pre>
<p>次に、パッケージリストを置く場所を作ります。これはアーキテクチャ毎に別です。</p>
<pre>mkdir -p /home/debs/dists/jaunty/main/binary-amd64
</pre>
<p>スキャンしてパッケージリストを作ります。</p>
<pre>cd /home/debs
dpkg-scanpackages --arch amd64 pool/jaunty-hoge | gzip &gt; dists/jaunty/main/binary-amd64/Packages.gz
</pre>
<ul>
<li>APTからの指定</li>
</ul>
<p>あとは、</p>
<pre>deb file:/home/debs jaunty main
</pre>
<p>などと指定すれば、パッケージが使えるようになります。</p>
<h3>強制的に入れる方法</h3>
<p>dpkgでインストールに失敗しても、aptitudeなどで再度インストールすれば依存関係を含めてインストールできます。</p>
<pre>sudo dpkg -i hoge.deb
sudo aptitude install hoge
</pre>
<p>これが一番簡単です。</p>
<h3>参考</h3>
<ul>
<li><a href="http://www.debian.org/doc/manuals/apt-howto/ch-basico.en.html#s-dpkg-scanpackages">How to use APT locally</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
