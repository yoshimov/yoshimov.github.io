---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.04</li>
<li>KVMなど</li>
</ul>
<h3>概要</h3>
<p>VM内で<a href="http://www.ubuntu.com/">Ubuntu</a>を利用する場合などに、ハイパーバイザーの設定でMACアドレスを変更したりすることがありますが、そのMACアドレスを認識しなくなってしまった場合の対処です。</p>
<p>なかなかわからなくてはまりました。</p>
<h3>手順</h3>
<ul>
<li>以下のファイルを削除する</li>
</ul>
<pre>/etc/udev/rules.d/70-persistent-net.rules
</pre>
<ul>
<li>MACアドレスを変更</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a>を再起動</li>
</ul>
<pre>restart
</pre>
