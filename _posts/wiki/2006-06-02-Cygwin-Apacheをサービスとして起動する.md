---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p><a href="http://cygwin.com/">Cygwin</a>で、Apacheをサービス化するには、cygrunsrv コマンドを使う。ただし、httpdは実行するとデーモンプロセスを起動してしまうため、-Fオプションを付けて、フォアグラウンド動作をさせる必要がある。</p>
<h4>インストール</h4>
<pre>cygrunsrv -I Apache -p /usr/sbin/httpd.exe -a &quot;-F&quot;
</pre>
<p>とする。</p>
<p><a href="http://cygwin.com/">Cygwin</a>をadministratorとしてインストールしている場合、サービスもadministrator権限で起動しないと正しく動作しない。</p>
<h4>起動</h4>
<pre>cygrunsrv -S Apache
</pre>
<h4>停止</h4>
<pre>cygrunsrv -E Apache
</pre>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
