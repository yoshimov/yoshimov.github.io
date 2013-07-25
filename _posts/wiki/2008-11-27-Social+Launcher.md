---
layout: post
---
<h2><a href="/?page=Social+Launcher" class="wikipage">Social Launcher</a> （ベータ）</h2>
<p><span class="error">categoryプラグインは存在しません。</span><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="/?page=Social+Launcher" class="wikipage">Social Launcher</a>（と勝手に名付けた）という、ソーシャルネットワークにまたがって同一人物のページを行き来できるツールを作ってみました。</p>
<h3>インストール</h3>
<p>以下のBookmarkletをブックマークしてください。</p>
<ul>
<li><span class="error">不正なリンクです。</span></li>
</ul>
<p><a href="http://labs.mozilla.com/projects/ubiquity/">Ubiquity</a>から利用する場合は、以下のページからSubscribeしてください。</p>
<ul>
<li><a href="http://gist.github.com/29316">http://gist.github.com/29316</a></li>
</ul>
<h3>使い方</h3>
<p>個人のプロフィールページなどで起動させると、他のサイトでのその人のページのリストが表示されます。</p>
<p>例えば以下のページを表示してブックマークを起動すると、他のサイトでの私の個人ページがリストで表示されます。</p>
<ul>
<li><a href="http://yoshimov.com/">http://yoshimov.com/</a></li>
</ul>
<p>元にしているのは<a href="http://delicious.com/">delicious</a>のブックマークで、同じ人のプロフィールをブックマークする際にタグに</p>
<pre>id:yoshimov
</pre>
<p>などと、id:付きで同じ名前のタグを付けておくと、その情報を拾ってリスト表示します。</p>
<p>公開されているブックマークは全て検索対象になりますので、誰かがid:付きのブックマークを登録していればそこからリンクを取得してきてくれます。</p>
<h3>動作環境</h3>
<p>今のところ確認が取れているのは以下の環境です。</p>
<ul>
<li><a href="http://www.mozilla-japan.org/products/firefox/">Firefox</a> 3.0.4</li>
<li><a href="http://labs.mozilla.com/projects/ubiquity/">Ubiquity</a> 0.1.2</li>
<li><a href="http://www.google.com/chrome">Google Chrome</a> 0.3.154.9</li>
</ul>
<h3>課題</h3>
<p>今のところ、以下のような問題があるので、他の人が同じid:タグで違う人のページをブックマークしていたりすると違う人のリンクも表示されてしまいます。</p>
<ul>
<li><a href="http://support.delicious.com/forum/comments.php?DiscussionID=791">Developer tree house: Please fix: XML returns user IDs while JSON does not</a></li>
</ul>
<p>この機能が<a href="http://delicious.com/">delicious</a>に実装されたら、ぼちぼち直していきます。</p>
<p>あと、各サイトに特化した正規化をまだ入れていないので、ブックマークと完全一致したURLからでないと利用できません。あしからず。</p>
<h3>Copyright</h3>
<p>このツールでは、<a href="http://www.onicos.com/staff/iz/amuse/javascript/expert/">Masanao Izumo</a>さんのMD5, UTF JavaScriptライブラリを利用させていただいてます。ありがとうございます。</p>
<p><span class="error">commentプラグインは存在しません。</span> </p>
