---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.centos.org/">CentOS</a> 5.2</li>
<li>Eucalyptus 1.4.1</li>
</ul>
<h3>概要</h3>
<p><a href="http://www.amazon.co.jp/">Amazon</a> EC2互換APIを持つオープンソースのクラウドインフラのEucalyptusを、<a href="http://www.centos.org/">CentOS</a>にインストールする方法です。ここでは１台のサーバに全ての機能をインストールしています。</p>
<h3>準備</h3>
<h4>RPMのダウンロード</h4>
<ul>
<li>以下のサイトから、64bitまた32bit用RPMを全てダウンロードしておく。<ul>
<li><a href="http://eucalyptus.cs.ucsb.edu/downloads">http://eucalyptus.cs.ucsb.edu/downloads</a></li>
</ul>
</ul>
<h4><a href="http://www.centos.org/">CentOS</a>のインストール</h4>
<p>インストール時にgnome-desktopのチェックボックスを外して、virtualizationだけチェックを入れて<a href="http://www.centos.org/">CentOS</a>をインストールする。</p>
<p>以降はsudoを有効にしたと想定。</p>
<ul>
<li><a href="/?page=CentOS%2Fsudo%A4%F2%BB%C8%A4%A8%A4%EB%A4%E8%A4%A6%A4%CB%A4%B9%A4%EB" class="wikipage">CentOS/sudoを使えるようにする</a></li>
</ul>
<p>Proxyの設定をして、yum updateをかけておく</p>
<ul>
<li><a href="/?page=CentOS%2FProxy%B7%D0%CD%B3%A4%C7%A5%EA%A5%DD%A5%B8%A5%C8%A5%EA%A4%F2%CD%F8%CD%D1%A4%B9%A4%EB" class="wikipage">CentOS/Proxy経由でリポジトリを利用する</a></li>
</ul>
<p>ファイアウォールはひとまず無効にしておく。有効にしてしまった場合は、</p>
<pre>sudo system-config-securitylevel-tui
</pre>
<p>で変更する。</p>
<h3>手順</h3>
<h4><a href="http://java.sun.com/j2se/">JDK</a>のインストール</h4>
<ul>
<li>ここから最新の<a href="http://java.sun.com/j2se/">JDK</a>を選択して、wgetでダウンロード<ul>
<li><a href="http://java.sun.com/javase/downloads/index.jsp">http://java.sun.com/javase/downloads/index.jsp</a></li>
</ul>
</ul>
<pre>wget http://.../jdk-6u12-linux-x64-rpm.bin
</pre>
<ul>
<li><a href="http://java.sun.com/j2se/">JDK</a>をインストール</li>
</ul>
<pre>chmod +x jdk-6u12-linux-x64-rpm.bin
sudo ./jdk-6u12-linux-x64-rpm.bin
</pre>
<ul>
<li>インストールされたJavaをチェック</li>
</ul>
<pre>java -version
</pre>
<ul>
<li>JCEパッケージをダウンロード<ul>
<li><a href="https://cds.sun.com/is-bin/INTERSHOP.enfinity/WFS/CDS-CDS_Developer-Site/en_US/-/USD/ViewProductDetail-Start?ProductRef=jce_policy-6-oth-JPR@CDS-CDS_Developer">https://cds.sun.com/is-bin/INTERSHOP.enfinity/WFS/CDS-CDS_Developer-Site/en_US/-/USD/ViewProductDetail-Start?ProductRef=jce_policy-6-oth-JPR@CDS-CDS_Developer</a></li>
</ul>
</ul>
<pre>wget http://../jce_policy-6.zip
</pre>
<ul>
<li>インストール</li>
</ul>
<pre>unzip jce_policy-6.zip
cp jce/*.jar /usr/java/default/jre/lib/security/
</pre>
<h4>antのインストール</h4>
<ul>
<li>以下から最新のantのtar.gzをダウンロード<ul>
<li><a href="http://ant.apache.org/bindownload.cgi">http://ant.apache.org/bindownload.cgi</a></li>
</ul>
</ul>
<pre>wget http://www.meisei-u.ac.jp/mirror/apache/dist/ant/binaries/apache-ant-1.7.1-bin.tar.gz
</pre>
<ul>
<li>/optに展開</li>
</ul>
<pre>cd /opt
sudo tar zxvf ~/apache-ant-1.7.1-bin.tar.gz
ln -s apache-ant-1.7.1 apache-ant
</pre>
<p>yumでantを入れると、不要なgcjなどが入ってしまうため注意。</p>
<h4>必要パッケージのインストール</h4>
<pre>sudo yum -y install perl apr apr-devel apr-util rsync dhcp bridge-utils
</pre>
<h4>環境変数の設定</h4>
<pre>sudo vi /etc/profile.d/java.sh
</pre>
<p>として、以下の内容をファイルに記載して保存。</p>
<pre># for Java
JAVA_HOME=/usr/java/default
ANT_HOME=/opt/apache-ant
PATH=$PATH:$ANT_HOME/bin
export JAVA_HOME ANT_HOME
</pre>
<ul>
<li>再ログインして、antにパスが通っているか確認しておく</li>
</ul>
<pre>which ant
</pre>
<h4>RPMのインストール</h4>
<ul>
<li>全てを一度にインストール</li>
</ul>
<pre>rpm -Uvh euca-axis2c-1.4-1.x86_64.rpm \
        euca-httpd-1.4-1.x86_64.rpm \
        euca-libvirt-1.4-1.x86_64.rpm \
        eucalyptus-1.4-2.x86_64.rpm \
        eucalyptus-cloud-1.4-2.x86_64.rpm \
        eucalyptus-gl-1.4-2.x86_64.rpm \
        eucalyptus-cc-1.4-2.x86_64.rpm \
        eucalyptus-nc-1.4-2.x86_64.rpm
</pre>
<h4>設定の変更</h4>
<ul>
<li>サーバの役割設定</li>
</ul>
<pre>cd /opt/eucalyptus
./usr/sbin/euca_conf -cc Y -cloud Y -nc Y ./etc/eucalyptus/eucalyptus.conf
./usr/sbin/euca_conf -nodes &quot;localhost&quot; ./etc/eucalyptus/eucalyptus.conf
./usr/sbin/euca_conf -instances /images/instances ./etc/eucalyptus/eucalyptus.conf
mkdir /images/instances
</pre>
<ul>
<li>サーバの起動</li>
</ul>
<pre>./etc/init.d/eucalyptus start
</pre>
<h3>参考</h3>
<ul>
<li><a href="http://wiki.layerboom.com/installation">Installation</a></li>
</ul>
