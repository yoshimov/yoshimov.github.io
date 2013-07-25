---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<p>GSI には，FrmGetObjectIndex が使えないため，以下のようなコードで index を取得する．</p>
<pre>UInt16 i, numObjects;
numObjects = FrmGetNumberOfObjects(frmP);
for (i=0; i&lt;numObjects; i++) \{
  if (FrmGetObjectType(frmP, i) == frmGraffitiStateObj)
    return(i);
\}
return(-1);
</pre>
<p>後は，他の Object と同じように，</p>
<pre>FrmGetObjectBounds(formP, index, &amp;r);
r.topLeft.y += extent;
FrmSetObjectBounds(formP, index, &amp;r);
</pre>
<p>で位置を移動させる．</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
<p><a href="/?page=Palm+Tips" class="wikipage">目次</a></p>
