---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">HTC Android Dev Phone 1</a>に<a href="http://www.cyanogenmod.com/">CyanogenMod</a>を入れた時の手順のメモ。と言っても、ほとんどWikiに載っているのと同じです。</p>
<h3>参考</h3>
<ul>
<li><a href="http://wiki.cyanogenmod.com/index.php/Full_Update_Guide_-_ADP1_Firmware_to_CyanogenMod">Full Update Guide - ADP1 Firmware to CyanogenMod</a></li>
</ul>
<h3>環境</h3>
<ul>
<li><a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">HTC Android Dev Phone 1</a> 1.6ファーム</li>
<li>Windows Vista SP2</li>
<li><a href="http://www.cyanogenmod.com/">CyanogenMod</a> 4.2.13</li>
</ul>
<h3>手順</h3>
<h4>USBドライバのインストール</h4>
<p>まずは作業するWindowsマシンにUSBドライバを入れます。</p>
<ul>
<li>以下のSDKをダウンロードして、適当な場所に展開<ul>
<li><a href="http://developer.android.com/sdk/index.html">Download the Android SDK</a></li>
</ul>
<li>SDK Setup.exeを実行</li>
<li>Settingsの &quot;Force <a href="https://">https://</a> sources to be fetched using <a href="http://">http://</a>&quot; を選択</li>
<li>Available PackagesからUsb driver packageを選択して、&quot;Install Selected&quot; ボタンを押す</li>
</ul>
<h4>リカバリイメージの書き換え</h4>
<ul>
<li>以下の場所から、cm-recovery-1.4.imgをダウンロードして、SDKのtoolsフォルダに置く<ul>
<li><a href="http://cyanogenmod.com/download/recovery/">http://cyanogenmod.com/download/recovery/</a></li>
</ul>
<li>バックボタンを押しながら、<a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>の電源を入れる<ul>
<li>fastbootと画面に表示されるのを確認</li>
</ul>
<li>USBケーブルでPCと接続</li>
<li>コマンドラインからfastbootでデバイス一覧を表示してみる</li>
</ul>
<pre>cd \android-sdk-windows\tools
fastboot devices
</pre>
<ul>
<ul>
<li>USBマスストレージとして繋がってしまう場合は、デバイスマネージャから一旦削除するとうまくいく</li>
</ul>
<li>カスタムリカバリイメージをブート</li>
</ul>
<pre>fastboot boot cm-recovery-1.4.img
</pre>
<ul>
<li>シェルスクリプトを無効にする</li>
</ul>
<pre>adb shell mount -a
adb shell
cd /system/etc
mv install-recovery.sh install-recovery.sh.disabled
exit
</pre>
<ul>
<li>再度、バックボタンを押しながらfastbootモードで<a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>を起動</li>
<li>カスタムリカバリイメージを書き込む</li>
</ul>
<pre>fastboot flash recovery cm-recovery-1.4.img
</pre>
<ul>
<li>以下のコマンドを実行して、<a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>を再起動。USBケーブルは抜いておく</li>
</ul>
<pre>fastboot reboot
</pre>
<h4>ROMファイルの転送</h4>
<ul>
<li>以下の場所から<a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>用の1.6の<strong>リカバリイメージ</strong>をダウンロード。他はダウンロードしなくて良い<ul>
<li><a href="http://developer.htc.com/adp.html#s3">http://developer.htc.com/adp.html#s3</a></li>
</ul>
<li>以下の場所から<a href="http://www.cyanogenmod.com/">CyanogenMod</a> Romの最新版をダウンロード<ul>
<li><a href="http://wiki.cyanogenmod.com/index.php/Latest_version">http://wiki.cyanogenmod.com/index.php/Latest_version</a></li>
</ul>
<li>それぞれSDKのtoolsフォルダに置いておく</li>
</ul>
<ul>
<li><a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>の設定-アプリケーションからUSB debuggingを有効にして、USBケーブルで接続</li>
<li>以下のコマンドで接続していることを確認する</li>
</ul>
<pre>cd \android-sdk-windows\tools
adb devices
</pre>
<ul>
<li>ROMファイルを転送</li>
</ul>
<pre>adb push signed-dream_devphone_userdebug-ota-14721.zip /sdcard
adb push update-cm-4.2.13-signed.zip /sdcard
adb shell sync
</pre>
<h4>ROMの適用</h4>
<ul>
<li>ホームを押しながら<a href="/?page=HTC+Android+Dev+Phone+1" class="wikipage">ADP1</a>を再起動して、リカバリモードにする。以下のコマンドでも良い。</li>
</ul>
<pre>adb reboot recovery
</pre>
<ul>
<li>&quot;wipe data/factory reset&quot;を選択して、データをクリア</li>
<li>&quot;apply any zip from sd&quot;を選択して、上記のzipを順番に適用する。<strong>この間再起動はしない。</strong></li>
</ul>
<p>あとはホームとバックボタンを同時押しして、正常起動するのを待つだけです。途中でリカバリモードに入ったら、再度再起動します。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
