---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.2</li>
<li><a href="http://git-scm.com/">Git</a> 1.5.6.1</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.centos.org/">CentOS</a> 5.2の標準リポジトリには<a href="http://git-scm.com/">Git</a>がないので、yum等ではインストールできません。</p>
<p>kernel.orgとRPMForgeを指定してインストールする手順です。</p>
<h3>手順</h3>
<ul>
<li><a href="http://git-scm.com/">Git</a>のリポジトリを追加</li>
</ul>
<pre>sudo vi /etc/yum.repo.d/git.repo
</pre>
<p>として、以下の内容を保存。</p>
<pre>[git]
name=Base git repository
baseurl=http://www.kernel.org/pub/software/scm/git/RPMS/$basearch
enabled=1
gpgcheck=0
</pre>
<ul>
<li>RPMForgeを追加</li>
</ul>
<pre>sudo vi /etc/yum.repo.d/rpmforge.repo
</pre>
<p>として、以下の内容を保存。</p>
<pre>[rpmforge]
name = Red Hat Enterprise $releasever - RPMforge.net - dag
mirrorlist = http://apt.sw.be/redhat/el5/en/mirrors-rpmforge
enabled = 0
gpgcheck = 0
</pre>
<ul>
<li>yumでバージョンを指定してインストール</li>
</ul>
<p>最新の1.6は<a href="http://fedoraproject.org/">Fedora</a>用のパッケージしかないので、以下のように実行。</p>
<pre>sudo yum install -y git-1.5.6.1 --enablerepo=rpmforge
</pre>
