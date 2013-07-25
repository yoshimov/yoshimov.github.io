---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p>一定時間毎に<a href="http://www.json.org">JSON</a>などで取得したデータを<a href="http://www.google.co.jp/">Google</a> DocsのSpreadsheetに追記していく方法です。</p>
<h3>環境</h3>
<ul>
<li><a href="http://www.google.co.jp/">Google</a> Docs Spreadsheet (2011.3時点)</li>
</ul>
<h3>手順</h3>
<h4>Spreadsheetを用意</h4>
<p><a href="http://www.google.co.jp/">Google</a> Docs上で通常通りSpreadsheetを用意します。</p>
<h4>収集用の関数を用意</h4>
<ul>
<li>[Tools]-[Script]-[Script Editor]を選んで、スクリプトエディタを開きます。</li>
<li>データ収集関数を記述します。以下はその例です。</li>
</ul>
<pre>function fetch_json() \{
 var url=&quot;http://tepco-usage-api.appspot.com/latest.json&quot;;
 var result= UrlFetchApp.fetch(url);
 var obj = Utilities.jsonParse(result.getContentText());
</pre>
<p>ここまでで、<a href="http://www.json.org">JSON</a>で取得したデータをオブジェクトに変換しています。</p>
<pre> var sheet = SpreadsheetApp.getActiveSpreadsheet();
 var cell = sheet.getRange('a1');
 var index = 0;
 cell.offset(index, 0).setValue(obj.entryfor);
 cell.offset(index, 1).setValue(obj.year);
 cell.offset(index, 2).setValue(obj.month);
 cell.offset(index, 3).setValue(obj.day);
 cell.offset(index, 4).setValue(obj.hour);
 cell.offset(index, 5).setValue(obj.usage);
 cell.offset(index, 6).setValue(obj.capacity);
 cell.offset(index, 7).setValue(obj.saving);
\}
</pre>
<p>このあたりで、取得したデータをシート内のセルに入力しています。重複を避ける場合は、入力する前にシートをスキャンするなどの工夫が必要です。</p>
<h4>トリガーを設定</h4>
<ul>
<li>[Triggers]-[Current Script's triggers]を選んで、新しいトリガを設定します。</li>
<li>実行する上記関数名と、実行間隔を指定してSaveボタンを押すと、一定時間毎に収集関数が実行されるようになります。</li>
<li>必要に応じて、<a href="http://www.twitter.com">Twitter</a>などへの自動投稿もここから行う。<ul>
<li><a href="/?page=GAS%2FTwitter%A4%D8%A4%CE%BC%AB%C6%B0%C5%EA%B9%C6" class="wikipage">GAS/Twitterへの自動投稿</a></li>
</ul>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
