---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="/?page=CASIO+IS11CA" class="wikipage">CASIO IS11CA</a>ではテザリングができますが、使った後にオフにし忘れてしまって、バッテリが激減してしまうことがよくあるので、それを防止する方法です。</p>
<p>タブレットとセットで設定します。</p>
<p>これでどんなことができるようになるかというと、</p>
<ul>
<li>スマホを取り出して、振るだけでテザリングを開始</li>
<li>タブレットから操作不要ですぐネットが使える</li>
<li>使い終わったらタブレットをスリープにするだけで、テザリングも勝手に切れる</li>
</ul>
<p>という感じの使い勝手になります。</p>
<ul>
<li>2013.7.19: Time Contextを使った設定に変更しました。</li>
<li>2013.7.22: 画面再表示時にメッセージを再送信するように変更しました。</li>
</ul>
<h3>環境</h3>
<ul>
<li><a href="/?page=CASIO+IS11CA" class="wikipage">CASIO IS11CA</a></li>
<li><a href="http://www.google.co.jp/">Google</a> Nexus 7</li>
<li><a href="http://tasker.dinglisch.net/">Tasker</a> 1.6</li>
<li><a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a> 2.0.6</li>
</ul>
<h3>準備</h3>
<ul>
<li>スマートフォンとタブレット双方に、<a href="http://tasker.dinglisch.net/">Tasker</a>と<a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a>を入れておく。</li>
<li>タブレット側の<a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a>に、スマートフォンの<a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a>を登録しておく。</li>
</ul>
<h3>設定</h3>
<h4>スマートフォン側（テザリング提供側）</h4>
<ul>
<li>以下のようなタイマーでテザリングを切るタスクを作って、ジェスチャーなどから起動するようにしておく。以下は５分で切る例です。</li>
</ul>
<pre>Task: Tether timer (22)
 A1: Notify LED [ Title:Tethering Text: Icon:&lt;icon&gt; Number:3 Colour:Blue Rate:525 Priority:3 ] 
 A2: WiFi Tether [ Set:On ] 
 A3: Variable Set [ Name:%keepTether To:5 Do Maths:Off Append:Off ] 

Task: stopTether (27)
 A1: WiFi Tether [ Set:Off ] 
 A2: Notify Cancel [ Title:Tethering Warn Not Exist:Off ] 
 A3: Variable Clear [ Name:%keepTether Pattern Matching:Off ] 

Task: countTether (36)
 A1: Variable Subtract [ Name:%keepTether Value:2 ] 
 A2: Perform Task [ Name:stopTether Stop:Off Priority:5 Parameter 1 (%par1): Parameter 2 (%par2): Return Value Variable: ] If [ %keepTether &lt; 1 ]
</pre>
<ul>
<li>ジェスチャーでテザリングを開始するプロファイルの例です。<ul>
<li>Time Contextを使って一定時間ごとに残り時間をカウントダウンするプロファイルも作っておきます。</li>
</ul>
</ul>
<pre>Profile: Tethering gesture (23)
 Event: Shake [ Axis:Left-Right Sensitivity:Medium Duration:Medium ]
 State: Orientation [ Is:Face Up ]
 State: Variable Value [ Name:%keepTether Op:Isn't Set Value:* ]
 Enter: Tether timer (22)

Profile: Tethering off (28)
 Event: Shake [ Axis:Left-Right Sensitivity:Medium Duration:Medium ]
 State: Orientation [ Is:Face Up ]
 State: Variable Value [ Name:%keepTether Op:Is Set Value:* ]
 Enter: stopTether (27)

Profile: Count Tethering (37)
 State: Variable Value [ Name:%keepTether Op:Maths: Greater Than Value:0 ]
 Time: Every 2m
 Enter: countTether (36)
</pre>
<ul>
<li><a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a>のメッセージを受けて、テザリングタイマーの残り時間をクリアするようにする。以下では &quot;kt&quot; というメッセージでクリアしています。</li>
</ul>
<pre>Profile: Keep Tethering (25)
 State: AutoRemoteLite [ Configuration:kt ]
 State: Variable Value [ Name:%keepTether Op:Is Set Value:* ]
 Enter: keepTether (26)

Task: keepTether (26)
    A1: Variable Set [ Name:%keepTether To:5 Do Maths:Off Append:Off ]
</pre>
<h4>タブレット側（テザリング利用側）</h4>
<ul>
<li>テザリング中は、一定時間毎に<a href="https://dl.dropboxusercontent.com/u/9787157/autoremotewelcome.html">AutoRemote</a>のメッセージを送るタスクを作ります。<ul>
<li>以下はディスプレイがオンの間は２分おきにメッセージを送る例です。</li>
<li>Profileが２つあるのは、一度画面を消して再度表示させた際に、２分待つ間にテザリングが切れてしまうのを防止するためです。</li>
</ul>
</ul>
<pre>Profile: Mobile (9)
 State: Display State [ Is:On ]
 State: Wifi Connected [ SSID:xxxx MAC:xxxx IP:* ]
 Time: Every 2m
 Enter: Mobile (10)

Profile: Mobile Display On
 Event: Display On
 State: Wifi Connected [ SSID:xxxx MAC:xxxx IP:* ]
 Enter: Mobile

Task: Mobile (10)
    A1: AutoRemoteLite Message [ Configuration:Recipient: xxxx Message: kt Package:com.joaomgcd.autoremote.lite Name:AutoRemoteLite Message ]
</pre>
<p>これで、テザリングタイマーを使って普通にWifiを使って、使い終わったらタブレット側のティスプレイを切るだけで、自動的にスマートフォン側のテザリングが切れるようになります。</p>
