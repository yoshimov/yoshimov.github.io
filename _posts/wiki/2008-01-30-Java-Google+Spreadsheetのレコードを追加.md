---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<ul>
<li>Java SE 6</li>
<li><a href="http://groovy.codehaus.org/">Groovy</a> 1.0</li>
<li>GData API 1.15.2</li>
</ul>
<h3>コード</h3>
<p><a href="http://groovy.codehaus.org/">Groovy</a>での記述例です。最近そればっかり。</p>
<pre>import java.text.SimpleDateFormat
import com.google.gdata.client.*
import com.google.gdata.client.spreadsheet.*
import com.google.gdata.data.spreadsheet.*

SpreadsheetService service = new SpreadsheetService(&quot;hoge-1&quot;)
service.setUserCredentials(&quot;gmailuser&quot;, &quot;gmailpass&quot;)

URL metafeedUrl = new URL(&quot;http://spreadsheets.google.com/feeds/spreadsheets/private/full&quot;)
</pre>
<p>まず、レコードを追加するSpreadsheetを特定。</p>
<pre>SpreadsheetFeed feed = service.getFeed(metafeedUrl, SpreadsheetFeed.class)
SpreadsheetEntry sheet = feed.getEntries().find {
  it.getTitle().getPlainText().equals(&quot;家計簿&quot;)
}
</pre>
<p>次にワークシートを特定。</p>
<pre>WorksheetEntry work = sheet.getWorksheets().find {
  it.getTitle().getPlainText().equals(&quot;明細&quot;)
}
</pre>
<p>ListFeedにレコードを追加。</p>
<pre>ListFeed list = service.getFeed(work.getListFeedUrl(), ListFeed.class)
ListEntry row = new ListEntry()
String time = new SimpleDateFormat(&quot;yyyy/MM/dd H:m:s&quot;).format(new Date())
row.getCustomElements().setValueLocal(&quot;項目名&quot;, &quot;食費&quot;)
row.getCustomElements().setValueLocal(&quot;金額&quot;, &quot;-1000&quot;)
row.getCustomElements().setValueLocal(&quot;日付&quot;, time)
row.getCustomElements().setValueLocal(&quot;入力日&quot;, time)
list.insert(row)
</pre>
