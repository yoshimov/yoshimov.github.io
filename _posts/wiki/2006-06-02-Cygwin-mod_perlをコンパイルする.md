---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p><a href="http://cygwin.com/">Cygwin</a>でmod_perlのコンパイルはできたんですが、動作しませんでした。とりあえずコンパイルのしかたをまとめておきます。</p>
<h3>環境</h3>
<ul>
<li><a href="http://cygwin.com/">Cygwin</a> 1.5.16-1</li>
<li>Apache 1.3.33-1 (<a href="http://cygwin.com/">Cygwin</a>)</li>
<li>gcc 3.3.3-3 (cygwin special)</li>
<li>perl v5.8.6-4 built for cygwin-thread-multi-64int</li>
<li>mod_perl 1.29</li>
</ul>
<h3>手順</h3>
<h4>apxsを編集</h4>
<p>/usr/sbin/apxsを編集して、</p>
<pre>my $CFG_LD_SHLIB      = q(gcc);
my $CFG_LDFLAGS_SHLIB = q(-g -shared); 
my $CFG_LIBS_SHLIB    = q(/bin/libhttpd.dll);
</pre>
<p>と変更する。</p>
<h4>mod_perlを展開</h4>
<p><a href="http://perl.apache.org">http://perl.apache.org</a> よりmod_perlをダウンロードして展開する。</p>
<h4>Makefile作成</h4>
<pre>perl Makefile.PL USE_APXS=1 WITH_APXS=/usr/sbin/apxs EVERYTHING=1
</pre>
<p>と実行。</p>
<h4>Makefileを編集</h4>
<p>apaci/Makefileを編集して、</p>
<pre>LIBEXT=dll
PERL_LD=gcc
PERL_LDDLFLAGS= -s -shared -L/usr/local/lib
</pre>
<p>PERL_LIBSに/bin/libhttpd.dllを追加。libperl.soとなっているところを、libperl.$(LIBEXT)と変更。</p>
<h4>makeを実行</h4>
<pre>make
make install
</pre>
<p>と実行すると、libperl.dllが作られてインストールされる。ただし、これを使うように設定するとApacheが起動しない。</p>
<p>＃いまいち使えない情報かも。(^^;</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> <span class="error">trackbackプラグインは存在しません。</span> </p>
