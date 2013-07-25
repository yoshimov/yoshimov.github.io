---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>Java Conduit で次回の HotSync の動作は、</p>
<pre>ConfigureConduitInfo#syncTemporary
</pre>
<p>から取得する。</p>
<p>また、次回の HotSync の動作を変える場合は、</p>
<pre>ConfigureConduitInfo#syncNew
</pre>
<p>を書き換える。</p>
<p>書き換えた設定を、標準の設定として保存する場合は、</p>
<pre>ConfigureConduitInfo#syncPermanent
</pre>
<p>を書き換え、</p>
<pre>ConfigureConduitInfo#syncPref
</pre>
<p>に</p>
<pre>ConfigureConduitInfo.PREF_PERMANENT
</pre>
<p>を指定する。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
