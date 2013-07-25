---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Java Conduitから HTTP の Cookie をハンドリングするには、リクエストに使った URLConnection から</p>
<pre>getHeaderField(&quot;Set-Cookie&quot;)
</pre>
<p>で Cookie を取り出し、次のリクエストで、</p>
<pre>setRequestProperty(&quot;Cookie&quot;, string)
</pre>
<p>とする。</p>
<p>ただし、HTTP Redirect されるページでは、Cookie が取得できないことがある。（はてなダイアリーがこれにあたる）</p>
<p>この場合は、最初のリクエストを発行する前に、</p>
<pre>HttpURLConnection#connection.setInstanceFollowRedirects(false)
</pre>
<p>を呼んでおくと redirect されなくなるため、ただしく Cookie が取得できる。</p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
