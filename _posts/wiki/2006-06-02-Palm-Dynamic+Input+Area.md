---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Tungsten T3以降では、Palm OSのAPIで標準で仮想シルクがサポートされている。ドキュメント内ではDynamic Input Areaと呼んでいる。</p>
<p>ドキュメントは、以下のPDF。</p>
<ul>
<li>DynamicInputAreas.pdf</li>
</ul>
<p>Tungsten T3でこれを有効にするには、Palmの<a href="http://pluggedin.palm.com/">Plugged.in</a>から&quot;Tungsten T3 DIA Compatibility PRCs&quot;をダウンロードしてインストールする必要がある。これらのprcは、各アプリケーションにバンドルすることが推奨されている。</p>
<p>導入された仮想シルクの有無は、以下のコードで判定する。</p>
<pre>err = FtrGet(pinCreator, pinFtrAPIVersion, &amp;version);
if (!err &amp;&amp; version) \{
 //PINS exists
\}
</pre>
<p>仮想シルクに関する設定は、frmLoadFormイベントが発行される毎に設定する。</p>
<p>まずは、以下のコードでDynamic Input Areaのポリシーを設定する。</p>
<pre>err = FrmSetDIAPolicyAttr(frmP, frmDIAPolicyCustom);
</pre>
<p>次に、以下のコードでユーザによるInput Areaのopen,close操作を許可する。</p>
<pre>err = PINSetInputTriggerState(pinInputTriggerEnabled);
</pre>
<p>Input Areaに対する操作が行われると、sysNotifyDisplayResizedEventのNotifyが発生し、あらかじめ登録しているアプリケーション全てに通知される。</p>
<p>Pen Input Manager のバージョンによっては、NotifyではなくwinDisplayChangedEventが発生するため、Notifyを受け取った際に以下のようにwinDisplayChangedEventを発生させ、イベントのハンドラでリサイズ処理を行ったほうが良い。</p>
<pre>EventType e;
e.eType = winDisplayChangedEvent;
EvtAddEventToQueue(&amp;e);
</pre>
<p>リサイズ後のウィンドウのサイズは、以下のように取得する。</p>
<pre>WinGetBounds(WinGetDisplayWindow(), &amp;displayBounds);
</pre>
<p>この時点ではActiveFormのサイズは変化しないので注意。</p>
<p>プログラムからInput Areaをコントロールするには、以下のようにする。</p>
<pre>err = PINSetInputAreaState(pinInputAreaOpen);
</pre>
<p>フォームを切り替えた際にシルクの状態を保持するには、</p>
<pre>PINSetInputAreaState(pinInputAreaUser);
</pre>
<p>を実行しておく。逆にこれを実行しておかないと、フォームを切り替えた際に無条件でInput Areaが表示状態になる、らしい。</p>
<ul>
<li><a href="http://www.palmsource.com/developers/newsletter/20031016.html#bullet1">Supporting Dynamic Input Areas (PalmSource)</a></li>
</ul>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
