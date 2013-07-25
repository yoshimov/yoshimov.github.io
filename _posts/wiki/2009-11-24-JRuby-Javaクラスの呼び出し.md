---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>JRubyからJavaクラスを呼び出す際にはまった点のまとめです。</p>
<h3>環境</h3>
<ul>
<li>JRuby 1.1.5</li>
<li>Java 1.6.0u16</li>
</ul>
<h3>基本</h3>
<p>基本的な呼び方は以下のようにします。</p>
<pre>include Java
include_class 'org.apache.xxx.SomeClass'

obj = SomeClass.new(args)
obj.method()
</pre>
<p>最初のinclude以外は、ほとんどRubyの流儀で呼び出すことができます。</p>
<h3>注意点</h3>
<h4>配列など</h4>
<p>byte配列が必要なメソッドにはrubyの配列は渡せませんので、</p>
<pre>bytes = &quot;abc&quot;.to_java_bytes
</pre>
<p>などとして、Javaのbyte配列に変換して渡します。</p>
<h4>定数</h4>
<p>定数は、</p>
<pre>CreateMode::PERSISTENT
</pre>
<p>などという風に参照します。</p>
<h4>内部クラス</h4>
<p>内部クラスは定数と同じように</p>
<pre>ZooDefs::Ids
</pre>
<p>などという感じで参照します。</p>
<h4>インタフェースの実装</h4>
<p>JavaではListenerオブジェクトをメソッドに渡すというようなことがよくありますが、このような場合は、</p>
<pre>class HogeListener
  include ActionListener
end
</pre>
<p>という感じで、インタフェースをincludeしたクラスを作って、このオブジェクトを渡してやります。</p>
<h3>参考</h3>
<ul>
<li><a href="http://kenai.com/projects/jruby/pages/CallingJavaFromJRuby">Scripting Java from JRuby</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
