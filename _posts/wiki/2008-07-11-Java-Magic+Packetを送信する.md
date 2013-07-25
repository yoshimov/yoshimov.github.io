---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Wake On LAN用のMagic PacketをJavaから送信する。</p>
<p>Javaと言いながら、例によって<a href="http://groovy.codehaus.org/">Groovy</a>です。</p>
<h3>環境</h3>
<ul>
<li>Java SE 6u5</li>
<li><a href="http://groovy.codehaus.org/">Groovy</a> 1.5.4</li>
</ul>
<h3>コード</h3>
<p>まずはコマンドラインの解析。</p>
<pre>def int PORT = 9

def cli = new CliBuilder()
cli.h(longOpt: 'help', 'usage information')
cli.i(argName: 'networkInterface', longOpt: 'interface', args: 1, required: true, 'MAC address of network interface(IPv4)')
cli.b(argName: 'broadcast', longOpt: 'broadcast', args: 1, required: true, 'Broadcast address')

def opt = cli.parse(args)
if (!opt) return
if (opt.h) cli.usage()
</pre>
<p>MACアドレスを取得</p>
<pre>String mac = opt.i.replaceAll(&quot;-&quot;, &quot;&quot;).replaceAll(&quot;:&quot;, &quot;&quot;)
byte[] macBytes = new byte[6]
for (pos in 0..5) \{
    macBytes[pos] = Integer.valueOf(mac.substring(pos*2,pos*2+2), 16)
\}
</pre>
<p>パケットデータを構築</p>
<pre>byte[] data = new byte[6 + 16 * 6]
for (i in 0..5) \{
   data[i] = 0xff
\}
for (i in 1..16) \{
   System.arraycopy(macBytes, 0, data, i * 6, 6)
\}
</pre>
<p>データ送信</p>
<pre>InetAddress address = InetAddress.getByName(opt.b)
DatagramPacket packet = new DatagramPacket(data, data.length, address, PORT)
DatagramSocket socket = new DatagramSocket()
socket.send(packet)
socket.close()

println &quot;Wake-on-LAN packet sent.&quot;
</pre>
