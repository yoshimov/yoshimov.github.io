---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>cronを頻繁に動かしていると、大量にメールが送られてくることがありますが、大事なときだけメールを送信するための設定方法のメモです。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.5</li>
</ul>
<h3>手順</h3>
<p>cronは標準出力をメールとしてユーザに送信するようになっているので、特定のキーワードが含まれる場合のみ標準出力するように設定すれば、重要なメールだけを送るようになります。</p>
<p>例えばExceptionというキーワードを含む場合だけメールを送信するようにするには、</p>
<pre>command &gt; /tmp/hoge.log; grep -q &quot;Exception&quot; /tmp/hoge.log &amp;&amp; cat /tmp/hoge.log
</pre>
<p>という感じで指定します。</p>
<p>またキーワードを複数指定したい場合は、</p>
<pre>command &gt; /tmp/hoge.log; grep -q &quot;Exception&quot; /tmp/hoge.log || grep -q &quot;Error&quot; /tmp/hoge.log &amp;&amp; cat /tmp/hoge.log
</pre>
<p>という感じに記述します。</p>
<p>crontabにこの指定を直接記述するとメールのタイトルが長くなるので、実際には同じ処理を行うシェルスクリプトを用意して、それを呼び出すのみにしたほうが記述もすっきりすると思います。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
