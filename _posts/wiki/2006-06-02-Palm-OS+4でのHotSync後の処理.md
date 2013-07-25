---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>OS 4.0 以降では HotSync 後の処理は，Notify で行う．具体的には SysNotifyRegister 関数で Notify を受け取る関数，またはアプリケーションを指定する．</p>
<p>この際に指定する LocalIDは，Palm デバイス内でのデータベースファイル名などから DmFindDatabase で検索するなどして取得する．</p>
<pre>LocalID dbID = DmFindDatabase(0, &quot;Addrex&quot;);
SysNotifyRegister(0, dbID, sysNotifySyncFinishEvent, NULL, 96, NULL);
</pre>
<p>Notify は，sysAppLaunchCmdNotify イベントとしてアプリケーションに渡される．この中で ((SysNotifyParamType*)cmdPBP)-&gt;notifyType を見て，処理を振り分ける．</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
