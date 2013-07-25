---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>ライブラリなどを作る際に、ランタイムがJRubyかCRubyかを判定する方法です。</p>
<h3>環境</h3>
<ul>
<li>JRuby 1.2.0</li>
</ul>
<h3>手順</h3>
<pre>if defined? JRUBY_VERSION
</pre>
<p>で判定すれば、JRubyかどうかがわかります。</p>
<p>Rubyのバージョンの判定は、</p>
<pre>if RUBY_VERSION &lt; 1.9
</pre>
<p>などとします。</p>
