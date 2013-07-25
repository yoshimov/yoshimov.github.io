---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>JRubyのSSL実装は色々問題を抱えていて、一筋縄ではいきません。私がうまくいった方法をメモしておきます。</p>
<h3>環境</h3>
<ul>
<li>JRuby 1.1.5</li>
<li>jruby-openssl 0.6</li>
<li>httpclient 2.1.5.2</li>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 9.04 (amd64)</li>
</ul>
<h3>手順</h3>
<h4>クライアント側</h4>
<p>クライアント側からSSLを利用する場合は、</p>
<ol>
<li>webrick/https を最初にrequireする</li>
<li>optionsを指定する</li>
</ol>
<p>の２点を気をつければ問題ありません。httpclientはgem installで入れておきます。</p>
<p>SOAP::RPC::Driverを使った接続はこんな感じで使います。</p>
<pre>require 'webrick/https'
require 'soap/rpc/driver'

conn = SOAP::RPC::Driver.new(&quot;https://localhost:443&quot;)
conn.options[&quot;protocol.http.ssl_config.verify_mode&quot;] = nil
conn.add_method(&quot;echo&quot;, &quot;message&quot;)
puts &quot;result=&quot;, conn.echo(&quot;test&quot;)
</pre>
<p>注意が必要なのは、optionsでssl_configを指定するやり方は、CRuby 1.8.7(オリジナルRuby)では動作しないという点です。これは私も何故だかわかりません。</p>
<h4>サーバ側</h4>
<p>サーバ側でクライアント認証をせずにSSLを使うには、JRuby内のwebrickのメソッドをオーバーライドします。</p>
<p>これはおそらくjruby-opensslのバグなので、そのうち修正されたら元に戻す必要があります。またバージョンによっては動作しない可能性もありますので、注意が必要です。</p>
<p>具体的にはこんな感じでparseメソッドをオーバーライドして、クライアントのcertificateを取得しないようにします。</p>
<pre>require 'webrick/https'
require 'soap/rpc/httpserver'
require 'soap/rpc/driver'

module WEBrick
 class HTTPRequest
   attr_reader :cipher, :server_cert, :client_cert
   def parse(socket=nil)
     if socket.respond_to?(:cert)
       @server_cert = socket.cert || @config[:SSLCertificate]
       @cipher      = socket.cipher
     end
     orig_parse(socket)
   end
 end
end
</pre>
<p>あとは通常どおり、</p>
<pre>class SOAPServer &lt; SOAP::RPC::HTTPServer
 def on_init
   add_method(self, 'echo', 'message')
 end
 def echo(message)
   return message
 end
end

server_cert = ..省略
server_key = ..省略
server = SOAPServer.new(
 :BindAddress =&gt; &quot;0.0.0.0&quot;,
 :Port =&gt; 443,
 :AccessLog =&gt; [],
 :SSLEnable =&gt; true,
 :SSLCertificate =&gt; server_cert,
 :SSLPrivateKey =&gt; server_key,
 :SSLVerifyClient =&gt; nil,
 :SSLCertName =&gt; nil
)
new_thread = Thread.new { server.start }
</pre>
<p>という感じでサーバを起動すれば使えます。気をつけないといけないのは、CRubyでは自己署名していないCertificateでもエラーは出ませんが、JRubyでは署名がないとエラーになってしまうという点です。</p>
<h3>組み合わせ毎の動作</h3>
<h4>JRuby server + JRuby 1.1 client</h4>
<ul>
<li>オプション指定なし<ul>
<li>エラー</li>
</ul>
</ul>
<blockquote><p>/usr/lib/jruby1.1/lib/ruby/1.8/soap/streamHandler.rb:183:in `send_post': certificate verify failed (OpenSSL::SSL::SSLError)</p>
</blockquote>
<ul>
<li>オプション指定あり<ul>
<li>正常動作</li>
</ul>
</ul>
<h4>JRuby server + Ruby 1.8.7 client</h4>
<ul>
<li>オプション指定なし<ul>
<li>warning</li>
</ul>
</ul>
<blockquote><p>warning: peer certificate won't be verified in this SSL session</p>
</blockquote>
<ul>
<li>オプション指定あり<ul>
<li>エラー</li>
</ul>
</ul>
<blockquote><p>/usr/lib/ruby/1.8/soap/httpconfigloader.rb:64:in `set_ssl_config': SSL not supported (NotImplementedError)</p>
</blockquote>
<h4>JRuby server + JRuby 1.2 client</h4>
<ul>
<li>オプション指定なし<ul>
<li>エラー</li>
</ul>
</ul>
<blockquote><p>/usr/lib/jruby1.2/lib/ruby/gems/1.8/gems/httpclient-2.1.5.2/lib/httpclient/session.rb:247:in `ssl_connect': certificate verify failed (OpenSSL::SSL::SSLError)</p>
</blockquote>
<ul>
<li>オプション指定あり<ul>
<li>正常動作</li>
</ul>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
