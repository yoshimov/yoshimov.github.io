---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h2>Pg - Perl5 extension for PostgreSQL</h2>
<p>Perlから、PostgreSQLに接続するためのライブラリ。</p>
<h3>ダウンロード</h3>
<p><a href="http://search.cpan.org/">CPAN</a>からダウンロード。</p>
<p><a href="http://search.cpan.org/~mergl/pgsql_perl5-1.9.0/">http://search.cpan.org/~mergl/pgsql_perl5-1.9.0/</a></p>
<h3>インストール</h3>
<p>解凍して、</p>
<pre>perl Makefile.PL
make
make install
</pre>
<p>でインストール。</p>
<p><a href="http://cygwin.com/">Cygwin</a>では、何故か typemap ファイルが読み込めない場合があるので、<a href="http://cygwin.com/">Cygwin</a>のルートディレクトリにコピーして、Makefile中のtypemapファイルのパスを</p>
<pre>/typemap
</pre>
<p>などと書き換えるとうまくいく。</p>
<h3>接続</h3>
<p>PostgreSQLに接続するには、</p>
<pre>use Pg;
my $conn = Pg::connectdb(&quot;dbname=template1&quot;);
</pre>
<p>とする。ローカルのDBを利用する場合は、dbnameのみ指定すれば接続できる。</p>
<p>指定できるオプションは、以下の通り。</p>
<table>
<tr>
<th>パラメータ</th>
<th>デフォルト</th>
<th>内容</th>
</tr>
<tr>
<td>dbname</td>
<td>current userid</td>
<td>接続するデータベース名</td>
</tr>
<tr>
<td>host</td>
<td>localhost</td>
<td>接続先ホスト</td>
</tr>
<tr>
<td>port</td>
<td>5432</td>
<td>接続先ポート番号</td>
</tr>
<tr>
<td>user</td>
<td>current userid</td>
<td>接続に利用するユーザID</td>
</tr>
<tr>
<td>password</td>
<td></td>
<td>パスワード</td>
</tr>
</table>
<h3>SQL実行</h3>
<p>SQLは、</p>
<pre>my $result = $conn-&gt;exec(&quot;SELECT * FROM table&quot;);
</pre>
<p>と実行する。成功すれば、</p>
<pre>$conn-&gt;status
</pre>
<p>が0になる。</p>
<p>SELECTの検索結果を取得する場合は、</p>
<pre>my @row = $result-&gt;fetchrow
</pre>
<p>とすると、SELECT で指定したフィールドが $row[0] などで取得できる。</p>
<p>fetchrow を繰り返すことで、結果を順番に取得できる。それ以上のレコードがない場合は、@rowがnullになる。</p>
<dl>
<dt>$result-&gt;ntuples</dt>
<dd> レコード数を取得する。</dd>
</dl>
<dl>
<dt>$result-&gt;nfields</dt>
<dd> フィールド数を取得する。</dd>
</dl>
<dl>
<dt>$result-&gt;fnumber($field_name)</dt>
<dd> フィールド番号に対応するフィールド名を取得する。</dd>
</dl>
<dl>
<dt>$result-&gt;getvalue($tup_num, $field_num)</dt>
<dd> 検索結果の$tup_num番目のレコードの$field_num番目のフィールドの値を取得する。バイナリデータの場合は動作しない。</dd>
</dl>
<dl>
<dt>$result-&gt;resultStatus</dt>
<dd> SQLの実行結果を取得する。</dd>
</dl>
<table>
<tr>
<th>実行結果</th>
</tr>
<tr>
<td>PGRES_EMPTY_QUERY</td>
</tr>
<tr>
<td>PGRES_COMMAND_OK</td>
</tr>
<tr>
<td>PGRES_TUPLES_OK</td>
</tr>
<tr>
<td>PGRES_COPY_OUT</td>
</tr>
<tr>
<td>PGRES_COPY_IN</td>
</tr>
<tr>
<td>PGRES_BAD_RES<a href="/?page=PostnoteSync+Conduit" class="wikipage">PONS</a>E</td>
</tr>
<tr>
<td>PGRES_NONFATAL_ERROR</td>
</tr>
<tr>
<td>PGRES_FATAL_ERROR</td>
</tr>
</table>
<h3>参考リンク</h3>
<ul>
<li><a href="http://www.hpc.cs.ehime-u.ac.jp/~aman/linux/SQL/Pg.html">perl スクリプトで PostgreSQL サーバにアクセスする</a></li>
</ul>
