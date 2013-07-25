---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>MavenなどAntのタスクでネットワーク接続が必要な場合に、Proxyを利用する方法のメモ。</p>
<h3>環境</h3>
<ul>
<li>Ant 1.7.1</li>
</ul>
<h3>手順</h3>
<ul>
<li>build.xmlにproxyターゲットを追加</li>
</ul>
<p>以下のようなターゲットを追加します。</p>
<pre>&lt;target name=&quot;proxy&quot;&gt;
 &lt;property name=&quot;proxy.host&quot; value=&quot;proxy.somewhere.com&quot; /&gt;
 &lt;property name=&quot;proxy.port&quot; value=&quot;8080&quot; /&gt;
 &lt;setproxy proxyhost=&quot;${proxy.host}&quot; proxyport=&quot;${proxy.port}&quot; /&gt;
&lt;/target&gt;
</pre>
<ul>
<li>必要なターゲットからdependsで指定</li>
</ul>
<p>他のターゲットから依存しているinitなどからdependsでproxyを指定しておきます。</p>
<p>あとは通常通りantのターゲットを実行すればProxy経由でネットワークにアクセスできます。</p>
<p>AntのマニュアルにはANT_OPTSで指定する方法も書いてありますが、setproxyを使うのが一番確実でした。</p>
<h3>参考</h3>
<ul>
<li><a href="http://ant.apache.org/manual/proxy.html">Proxy Configuration</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
