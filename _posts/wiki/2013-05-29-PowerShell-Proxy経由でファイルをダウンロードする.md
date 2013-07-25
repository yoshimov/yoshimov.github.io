---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>WindowsのPowerShellで、Proxy経由でファイルなどをダウンロードする方法です。</p>
<h3>環境</h3>
<ul>
<li>Windows 7</li>
<li>PowerShell 2.0</li>
</ul>
<h3>手順</h3>
<h4>通常のProxy</h4>
<ul>
<li>IEのProxyを設定しておく</li>
<li>WebClientを取得</li>
</ul>
<pre>$wc = new-object System.Net.WebClient
</pre>
<ul>
<li>システムProxyを取得して設定</li>
</ul>
<pre>$proxy = [System.Net.WebRequest]::GetSystemWebProxy()
$proxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials
$wc.Proxy = $proxy
</pre>
<ul>
<li>ファイルをダウンロード</li>
</ul>
<pre>$wc.DownloadFile(&quot;http://hoge&quot;, &quot;hoge&quot;)
</pre>
<h4>認証付きProxy</h4>
<p>認証付きの場合はDefaultCredentialsではアクセスできない場合があるので、ステータスコードによって再度リクエストを出します。</p>
<ul>
<li>通常のProxyと同じように準備</li>
</ul>
<pre>$wc = new-object System.Net.WebClient
$proxy = [System.Net.WebRequest]::GetSystemWebProxy()
$proxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials
$wc.Proxy = $proxy
</pre>
<ul>
<li>407エラーをcatchして再度リクエスト</li>
</ul>
<pre>try \{
  $wc.DownloadFile(&quot;http://hoge&quot;, &quot;hoge&quot;)
\} catch [System.Net.WebException] \{
  if ($_.Exception -match &quot;.*\(407\).*&quot;) \{
    # ダイアログを表示してログイン情報を取得
    $cred = get-credential
    $wc.Proxy.Credentials = $cred.GetNetworkCredential()
    # 再度ダウンロード
    $wc.DownloadFile(&quot;http://hoge&quot;, &quot;hoge&quot;)
  \} else \{
    throw
  \}
\}
</pre>
<p>WebClientではなくWebRequestを使っている場合、１つのRequestから複数のリクエストは出せないため、再度通信を行うには新しくRequestを生成する必要があります。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
