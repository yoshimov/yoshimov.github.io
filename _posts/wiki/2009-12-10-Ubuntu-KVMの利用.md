---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10でKVMを利用する際の手順のメモです。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.10</li>
<li>KVM 0.11.0-0ubuntu6.3</li>
</ul>
<h3>手順</h3>
<h4>環境の確認</h4>
<p>KVMを動かすにはハードウェアのサポートが必要ですのでまずはサポートされているか確認します。</p>
<pre>egrep &quot;(svm|vmx)&quot; /proc/cpuinfo
</pre>
<p>svmまたはvmxが含まれた行が表示されればサポートされています。</p>
<h4>KVMのインストール</h4>
<pre>sudo aptitude install qemu-kvm ubuntu-vm-builder libvirt-bin virt-manager
</pre>
<p>で一通り必要なパッケージがインストールできます。</p>
<h4>ブリッジの設定</h4>
<p>デフォルトではゲストOSはホストのNATを介してネットに繋がるので、ブリッジ接続ができるように設定します。</p>
<pre>sudo /etc/init.d/networking stop
</pre>
<p>でネットワークを止めてから、</p>
<pre>sudo vi /etc/network/interfaces
</pre>
<p>として、以下の内容を追記します。DHCPではない場合はbr0のほうをstaticとします。</p>
<pre>auto eth0
iface eth0 inet manual

auto br0
iface br0 inet dhcp
       bridge_ports eth0
       bridge_stp off
       bridge_fd 0
       bridge_maxwait 0
</pre>
<p>そして</p>
<pre>sudo /etc/init.d/networking start
</pre>
<p>としてネットワークを起動します。</p>
<h4>VMの設定</h4>
<p>VMは通常通りvirt-managerやvirshなどを使って設定します。この際にbr0をブリッジとして指定してやれば、ホストと同じネットワークにブリッジ接続できるようになります。</p>
<h3>課題</h3>
<p>どうもブリッジを設定すると、Gnome Desktopでネットワーク表示が未接続の状態になってしまう様子。実用上は特に問題なさそうですが、ちょっと気持ち悪いです。</p>
<h3>参考</h3>
<ul>
<li><a href="https://help.ubuntu.com/community/KVM/Networking">Ubuntu KVM Networking</a></li>
</ul>
