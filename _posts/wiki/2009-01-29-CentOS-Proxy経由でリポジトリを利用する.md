---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.2</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.centos.org/">CentOS</a>は、メニューからProxyを設定しただけでは、リポジトリにアクセスできない。Red Hat系はみんな同じ？</p>
<h3>手順</h3>
<ul>
<li>yum.confを編集</li>
</ul>
<pre>sudo vi /etc/yum.conf
</pre>
<p>以下の行を追加する</p>
<pre>proxy=http://proxy.somehost:port/
</pre>
<ul>
<li>[システム]-[設定]-[ネットワークのプロキシ]でプロキシを設定しておく</li>
<li>公開鍵のインポート</li>
</ul>
<pre>wget http://www.centos.org/centos/RPM-GPG-KEY-CentOS-5
sudo rpm --import RPM-GPG-KEY-CentOS-5
</pre>
<ul>
<li>yumでリポジトリをアップデート</li>
</ul>
<pre>sudo yum update
</pre>
<h3>参考</h3>
<ul>
<li><a href="http://linux.hayarimon.com/proxy.html">プロキシ設定（yumによるアップデート）</a></li>
<li><a href="http://take-blizzard.cocolog-nifty.com/blog/2008/07/proxyyumwget_e798.html">proxy経由のyumとwget</a></li>
</ul>
