---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.2</li>
</ul>
<h3>概要</h3>
<p>デフォルトではsudoが使えるのはrootだけになっているので、一般のユーザもsudoを使えるように設定します。</p>
<p>ただ、システムの設定を変更しようとした時はrootのパスワードが必要なので、<a href="http://www.ubuntu.com/">Ubuntu</a>のように全てsudoで済むわけではありません。</p>
<h3>手順</h3>
<ul>
<li>sudoersを編集</li>
</ul>
<pre>su
</pre>
<p>ルートのパスワードを入れる。</p>
<pre>/usr/sbin/visudo
</pre>
<p>以下の行のコメントを削除して、有効にする。</p>
<pre>%wheel ALL=(ALL) ALL
</pre>
<ul>
<li>対象のユーザをwheelに入れる<ul>
<li>[システム]-[管理]-[ユーザとグループ]を実行。ルートのパスワードを入れる</li>
<li>対象のユーザのプロパティを表示</li>
<li>グループタブでwheelグループにチェックを入れてOKを押す</li>
</ul>
</ul>
<h3>参考</h3>
<ul>
<li><a href="http://d.hatena.ne.jp/a__z/20071011">CentOS:sudo を設定する</a></li>
</ul>
