---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p><a href="http://www.softether.com/jp/">SoftEther</a>はWindows XPのブリッジ接続機能を使うと、仮想LANに繋がったPCを、物理LANに接続したのと同じ状態にすることができます。</p>
<ul>
<li><a href="http://www.softether.com/jp/manual/bridge.aspx">物理ネットワークと仮想ネットワークのブリッジ接続</a></li>
</ul>
<p>ただ、このままの方法では、無線LANで接続されているマシンは仮想Hub兼ブリッジとして設定することができません。これを回避するには、netshコマンドを使って、以下のようにレイヤ３互換モードのブリッジ接続に変更する必要があります。</p>
<h4>ブリッジを設定する</h4>
<p><a href="http://www.softether.com/jp/">SoftEther</a>のページと同じように、ブリッジ接続したい仮想LANと無線LANを選択してブリッジ接続します。</p>
<p>うちの環境ではこれだけではブリッジされず、さらに仮想LANと無線LANを右クリックでブリッジに追加してやる必要がありました。</p>
<h4>IPアドレスを設定する</h4>
<p>作成されたブリッジに、IPアドレスを設定します。ここでは、仮想Hubがブリッジを設定するマシン上にあるため、固定のIPアドレスを設定しました。</p>
<h4>レイヤ３モードに設定を変更する</h4>
<p>まず下記のコマンドで、ブリッジ接続している無線LANのインタフェースの番号を調べます。</p>
<pre>netsh bridge show adapter
</pre>
<p>次に、以下のコマンドで、レイヤ３モードに設定を変更します。1の部分には、上記コマンドで調べたインタフェース番号を指定します。</p>
<pre>netsh bridge set adapter 1 forcecompatmode=enable
</pre>
<p>これで、無線LANインタフェースを通して他のマシン宛てにping等が通ればブリッジの設定は終了です。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
