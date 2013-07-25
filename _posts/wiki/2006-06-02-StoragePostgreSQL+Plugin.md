---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://fswiki.poi.jp/">FSWiki</a>でストレージにPostgreSQLを使うプラグインです。これを導入することで以下のメリットが期待できます。</p>
<ul>
<li> ページ数が増えても、一定のレスポンス速度を保てる（はず）</li>
<li> 過去の編集履歴が全て保存されるため、全てのバージョンとの差分表示が可能。</li>
<li> Farmを含めたページのバックアップが、RDBのdump一発で取れる（添付ファイルを除く）</li>
</ul>
<p>まだ、ページ一覧、更新履歴などは正しく動作しません。くれぐれも、<strong>正式運用には使わないでください。</strong></p>
<h3>対応バージョン</h3>
<p><a href="http://fswiki.poi.jp/">FSWiki</a>の 3.5.1のみで、動作確認しています。</p>
<p>少なくとも3.5.5以降ではAPIが異なるため動作しません。ご注意ください。</p>
<h3>ダウンロード</h3>
<ul>
<li>2003.9.24β版:<span class="error">refプラグインは存在しません。</span><ul>
<li>ページの削除処理に対応。</li>
<li>ページ管理の際、参照権限が正しく表示されない障害を修正。</li>
</ul>
<li>2003.9.22α版:<span class="error">refプラグインは存在しません。</span><ul>
<li>ファイルストアからの移行スクリプトを追加。</li>
<li>ページのバックアップにトランザクションを利用するように変更。</li>
</ul>
<li>2003.9.21α版:<span class="error">refプラグインは存在しません。</span></li>
</ul>
<h3>インストール</h3>
<p>PostgreSQLの他に、<a href="/?page=Perl%2FPg+%2D+Perl+extension+for+PostgreSQL" class="wikipage">Perl/Pg - Perl extension for PostgreSQL</a>が必須です。インストールしていない場合は、まずインストールしてください。</p>
<p>ZIPを展開して、</p>
<pre>createdb -D [DBの格納先] -E EUC_JP fswiki
</pre>
<p>とDBを作成。</p>
<pre>psql -f create-db.sql fswiki
</pre>
<p>として、テーブルを作成。</p>
<p><a href="http://fswiki.poi.jp/">FSWiki</a>から、storage_postgres プラグインを有効にする。</p>
<p>DBの名前、接続形態が違う場合は、</p>
<pre>StoragePostgreSQL.pm
</pre>
<p>にある接続オプションを編集してください。</p>
<h3>ファイルストレージからの移行</h3>
<p>ファイルストレージのページをDBに移行するには、file2db.pl の接続オプションを正しく編集して、</p>
<pre>perl file2db.pl
</pre>
<p>と実行すると移行できます。一応Farmも含めて移行されます。</p>
<h3>問題点</h3>
<h4>mod_perl使用時にconnectionが切断されないまま残る</h4>
<p>これは、</p>
<pre>undef $wiki-&gt;\{storage\};
</pre>
<p>という記述を、</p>
<ul>
<li>wiki.cgi の最後</li>
<li>Wiki.pm の redirect の exit の前</li>
<li>AttachHandler.pm の do_action の exit の前</li>
<li>RSSMaker10.pm の exit の前</li>
</ul>
<p>に追加すると大丈夫のようです。</p>
<h4>一覧、更新履歴が正しく並ばない</h4>
<pre>data/
</pre>
<p>内のファイルを削除すると順序は正しくなります。ただし、Farmのフォルダは削除しないでください。</p>
<p>更新履歴は、RecentCache.pm の update_cache で $modtime を取得する部分を</p>
<pre>my $modtime = $wiki-&gt;get_last_modified($_);
</pre>
<p>と変更すると、正しく表示されるようになります。</p>
<h4>コメントが反映されない</h4>
<p>PostgreSQLに入れたときに、本文の改行が\r\nになってしまって、コメントプラグインの正規表現に引っかからなくなってしまうみたいです。</p>
<p>とりあえず、CommentHandler.pm 内の二箇所ある</p>
<pre>if(/^\{\{comment\s*.*\}\}$/ &amp;&amp; $flag==0)\{
</pre>
<p>という行を</p>
<pre>if(/^\{\{comment\s*.*\}\}/ &amp;&amp; $flag==0)\{
</pre>
<p>と変更すると動きます。（$を取る）</p>
<h3>コメント</h3>
<ul>
<li>以前PostgreSQLのインストに失敗したものです。どのようなメリットがあるのか説明があると嬉しいです。 - 名無しさん (2003年10月02日 12時56分26秒)</li>
<li>メリットを書いてみました。やはり大きいのは過去バージョンが残るところですかね。 - <a href="/?page=Yoshimov" class="wikipage">Yoshimov</a> (2003年10月02日 17時16分21秒)</li>
<li>なんかめっちゃすごそうですね、設置サイトでひとつ上のものです、いずれはプラグインにお世話になりたいです。その前にインストしないと・・・ - 名無しさん (2003年10月07日 11時34分13秒)</li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
