---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://code.google.com/intl/ja/googleapps/appsscript/">Google Apps Script</a>で、<a href="http://www.twitter.com">Twitter</a>に自動投稿する方法のメモ。簡単なbotはかなりこれで作れそうな感じです。ほとんどチュートリアルのまんまですが。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.google.co.jp/">Google</a> Docs Spreadsheet (2011.3時点)</li>
</ul>
<h3>手順</h3>
<h4><a href="http://www.twitter.com">Twitter</a> Developersでアプリを登録</h4>
<ul>
<li><a href="http://dev.twitter.com/">http://dev.twitter.com/</a></li>
</ul>
<p>にアクセスして、新規アプリを登録しておきます。この際に、以下の点を注意します。</p>
<ul>
<li>Application Typeは&quot;Browser&quot;とする。</li>
<li>Callback URLは &quot;<a href="https://spreadsheets.google.com/macros">https://spreadsheets.google.com/macros</a>&quot; とする。</li>
<li>Default access typeは &quot;Read &amp; Write&quot; とする。</li>
</ul>
<p>登録したら、Consumer KeyとConsumer Secretをメモしておきます。</p>
<h4>Spreadsheetを用意</h4>
<p>何でも良いので、<a href="http://www.google.co.jp/">Google</a> Docs上にSpreadsheetを用意しておきます。</p>
<h4>OAuth認証</h4>
<ul>
<li>[Tools]-[Scripts]-[Script Editor]からスクリプトエディタを起動します。</li>
<li>まずは以下のような認証用の関数を入力して、保存します。</li>
</ul>
<pre>function test_oauth() \{
 // Setup OAuthServiceConfig
 var oAuthConfig = UrlFetchApp.addOAuthService(&quot;twitter&quot;);
 oAuthConfig.setAccessTokenUrl(&quot;http://api.twitter.com/oauth/access_token&quot;);
 oAuthConfig.setRequestTokenUrl(&quot;http://api.twitter.com/oauth/request_token&quot;);
 oAuthConfig.setAuthorizationUrl(&quot;http://api.twitter.com/oauth/authorize&quot;);
 oAuthConfig.setConsumerKey(ScriptProperties.getProperty(&quot;twitterConsumerKey&quot;));
 oAuthConfig.setConsumerSecret(ScriptProperties.getProperty(&quot;twitterConsumerSecret&quot;));

 // Setup optional parameters to point request at OAuthConfigService.  The &quot;twitter&quot;
 // value matches the argument to &quot;addOAuthService&quot; above.
 var options =
   \{
     &quot;oAuthServiceName&quot; : &quot;twitter&quot;,
     &quot;oAuthUseToken&quot; : &quot;always&quot;,
     &quot;method&quot; : &quot;GET&quot;
   \};
 var result = UrlFetchApp.fetch(&quot;http://api.twitter.com/1/account/verify_credentials.json&quot;, options);
\}
</pre>
<ul>
<li>[File]-[Properties]を開いて、Script propertiesにtwitterConsumerKeyとして、前述のComsumer Keyを、twitterConsumerSecretとして、前述のConsumer Secretを追加します。</li>
<li>[Share]-[Publish as Service]を選んで、Enable ServiceのチェックをオンにしてSaveボタンを押します。</li>
<li>[Run]メニューから、test_oauthを選んで、上記スクリプトを実行します。</li>
<li>Authorizeボタンを押すと、通常のOAuthアプリ同様認証画面が出るのでAllowを選択します。</li>
</ul>
<h4><a href="http://www.twitter.com">Twitter</a>投稿関数を用意</h4>
<p>あとは、JavaScriptの関数で<a href="http://www.twitter.com">Twitter</a>への投稿を記述します。以下は投稿のための関数の例。</p>
<pre>function post_status(status) \{
 // Setup OAuthServiceConfig
 var oAuthConfig = UrlFetchApp.addOAuthService(&quot;twitter&quot;);
 oAuthConfig.setAccessTokenUrl(&quot;http://api.twitter.com/oauth/access_token&quot;);
 oAuthConfig.setRequestTokenUrl(&quot;http://api.twitter.com/oauth/request_token&quot;);
 oAuthConfig.setAuthorizationUrl(&quot;http://api.twitter.com/oauth/authorize&quot;);
 oAuthConfig.setConsumerKey(ScriptProperties.getProperty(&quot;twitterConsumerKey&quot;));
 oAuthConfig.setConsumerSecret(ScriptProperties.getProperty(&quot;twitterConsumerSecret&quot;));

 // Setup optional parameters to point request at OAuthConfigService.  The &quot;twitter&quot;
 // value matches the argument to &quot;addOAuthService&quot; above.
 var options =
   \{
     &quot;oAuthServiceName&quot; : &quot;twitter&quot;,
     &quot;oAuthUseToken&quot; : &quot;always&quot;,
     &quot;method&quot; : &quot;POST&quot;
   \};
 var result = UrlFetchApp.fetch(&quot;http://api.twitter.com/1/statuses/update.json?status=&quot; + encodeURIComponent(status), options);
\}
</pre>
<p>ポイントは以下の点。</p>
<ul>
<li>POSTを明示的に指定する。</li>
<li>ステータスはURLエンコードした文字列を利用して、Query stringとして埋め込む。</li>
</ul>
<p>あとは、トリガーなどを設定して一定時間毎に<a href="http://www.twitter.com">Twitter</a>への投稿を行うようにします。</p>
<ul>
<li><a href="/?page=GAS%2F%B3%B0%C9%F4%A5%C7%A1%BC%A5%BF%A4%F2Spreadsheet%A4%CB%BC%AB%C6%B0%BC%FD%BD%B8%A4%B9%A4%EB" class="wikipage">GAS/外部データをSpreadsheetに自動収集する</a></li>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://code.google.com/googleapps/appsscript/articles/twitter_tutorial.html">Tutorial: Twitter Approval Manager</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
