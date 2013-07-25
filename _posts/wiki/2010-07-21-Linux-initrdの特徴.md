---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>概要</h3>
<p><a href="http://multiboot-usb.yoshimov.com/">これ</a>のためにいくつかinitrdにパッチを当ててきたので、それぞれのディストリビューション毎のinitrdの特徴をまとめてみます。</p>
<p><a href="http://www.slackware.com/">Slackware</a>とかがないですが、それは標準でisoブートに対応していたので、いじる必要がなかったためです。</p>
<h3><a href="http://www.debian.org/">Debian</a>系</h3>
<p><a href="http://www.debian.org/">Debian</a>とは言え、initrdはそれぞれまったく違います。ただ<a href="http://www.ubuntu.com/">Ubuntu</a>系は大体同じinitrdを使っているようで、標準でisoブートもできます。</p>
<h4><a href="http://www.ubuntu.com/">Ubuntu</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> 8.10以前はcpio+gz、9.04以降はcpio+lzma</dd>
</dl>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>は最初からISOブートをサポートしているので、基本的に手を入れる必要はありませんが、差分を保存するcasper-rw のファイル名の変更などに対応させるための簡単なパッチを提供しています。</p>
<p>基本的にはinitから、カーネルオプションで指定されたscripts/casperが呼び出される一般的なinitrdです。</p>
<h4><a href="http://live.debian.net/">Debian Live</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<p>本家のLiveCDですが、標準ではisoブートには対応していません。</p>
<p>最初にロードされるのはinitですが、そこからscriptsフォルダ以下のliveが読み込まれて、その中のfunctionが呼び出されます。</p>
<p>LiveCDのマウントはscripts/liveのis_live_path()の中で行われます。</p>
<h4><a href="http://www.backtrack-linux.org/">BackTrack</a> Linux</h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<p>これは、セキュリティ関係のツールが大量に詰まったLinuxですが、ベースは<a href="http://live.debian.net/">Debian Live</a>と同じで、initからscripts以下のcasperのfunctionが呼び出されます。LiveCDのマウントはcasperの中になります。</p>
<p>面白いのは、ローカルブート用のscripts/localにはisoファイルなどのループバックマウントを行うコードが入っているのに、casperには入っていない点です。おかげで同じloop=オプションを使って、簡単にパッチを当てることができました。</p>
<h4><a href="http://www.knoppix.net/">KNOPPIX</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<p><a href="http://www.knoppix.net/">KNOPPIX</a>は歴史のあるLiveCDだけあって、initスクリプトは１つで完結していますが、いろんな条件に対応できるように少々複雑になっています。</p>
<p>また、接続されている全てのストレージを検索する仕組みなので、最初に見つかった<a href="http://www.knoppix.net/">KNOPPIX</a>のイメージで起動するようになっているようです。</p>
<h4><a href="http://www.mepis.org/">MEPIS</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>ext2+gz</dd>
</dl>
<p>Simply<a href="http://www.mepis.org/">MEPIS</a>や、その派生のantiXはデフォルトでisoブート用のオプションfromiso=が用意されていますが、なぜか最近のバージョンではvfatのマウントには対応しておらず、そのままではVFAT(fat32)フォーマットのUSBメモリからはisoブートできません。</p>
<p>そこでマウント時に試すフォーマットにvfatを追加するだけで、isoブートできるようになりました。これは限りなくバグっぽいですが、誰も報告していないんでしょうか。</p>
<h4><a href="http://www2.mandriva.com/">Mandriva</a> One</h4>
<dl>
<dt>フォーマット</dt>
<dd>ext2+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd>/linuxrc</dd>
</dl>
<dl>
<dt>難易度</dt>
<dd>高</dd>
</dl>
<p><a href="http://www2.mandriva.com/">Mandriva</a>は珍しくinitrdでnashというshとは違うシェルでブートします。nashは非常に機能が限定されているので、通常shで使うような変数を使った動作の切り分けなどがしにくくなります。</p>
<p>実際、デフォルトのinitrdではCD-ROM限定、ラベル名限定でディスクをマウントするコードになっています。<a href="http://www2.mandriva.com/">Mandriva</a>の場合は、用途別にinitrdを分けるほうが良いかもしれません。</p>
<h4><a href="http://www.dreamlinux.com.br/">Dreamlinux</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> cpio+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> init.lua</dd>
</dl>
<p><a href="http://www.dreamlinux.com.br/">Dreamlinux</a>は、Luaというめずらしいシェルを使ってブートしています。ifを閉じるのにendと書くなど、若干Rubyのような感じです。ただ、コマンドを実行するのにわざわざos.executeと書かないといけないなど、普通のshに慣れた身としては非常に書きにくいです。</p>
<p>また、カーネルオプションの解析もややこしいので、私のパッチではfromiso=オプションは必ず最後に記述しないと動かないように簡略化しています。</p>
<h3><a href="http://www.gentoo.org/">Gentoo</a>系</h3>
<h4><a href="http://sabayonlinux.org/">Sabayon</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<p>これは、基本的に全てinitが処理しますが、functionは外部のファイルで定義されていて、実際のLiveCDのマウントは/etc/initrd.scriptsが行っています。</p>
<p>全体的に処理の流れが追いやすく、いじりやすいinitrdです。</p>
<h3>RedHat系</h3>
<h4><a href="http://www.centos.org/">CentOS</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /init</dd>
</dl>
<p><a href="http://www.centos.org/">CentOS</a>は、なんとなく全ての処理をinitスクリプトに詰め込んでいる感じで、<a href="http://www.knoppix.net/">KNOPPIX</a>に似ています。ただ処理の流れはわかりやすく、rootディスクのマウントも一箇所で行われているだけなので、比較的パッチは当てやすいです。</p>
<h4><a href="http://fedoraproject.org/">Fedora</a></h4>
<dl>
<dt>フォーマット</dt>
<dd>cpio+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /sbin/dmsquash-live-root</dd>
</dl>
<p><a href="http://fedoraproject.org/">Fedora</a>は同じRedHat系でもかなり機能毎にスクリプトが分割されていて、initから/sbin以下のスクリプトが順次呼び出されていきます。rootディスクは/sbin/dmsquash-live-root内でマウントされているので、ここにパッチを当てればisoブートできます。</p>
<h3>その他</h3>
<h4><a href="http://gobolinux.org/">GoboLinux</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> cramfs</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /Programs/InitRDScripts/20080330/bin/mount<a href="http://gobolinux.org/">GoboLinux</a></dd>
</dl>
<p>基本的にinit（の元ファイル）から、mount用のスクリプトを呼び出しているので構造は単純なんですが、Goboのポリシーで実行用のファイルは/Programs以下などと決まっているので、その実体を探して編集するのが結構大変です。</p>
<p>また、フォーマットがcramfsなので直接マウントしてもリードオンリーでパッチを当てられません。なので作業用フォルダーに一旦全てコピーしてから、新しいcramfsを生成するという手間が必要になります。</p>
<h4><a href="http://www.puppylinux.com/">Puppy Linux</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> cpio+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /init</dd>
</dl>
<dl>
<dt>難易度</dt>
<dd> 高</dd>
</dl>
<p>Puppyのスクリプトは、一旦全ドライブをスキャンして、見つかったファイルやオプションから起動方法を選択して起動する方法を採用しています。</p>
<p>これはこれで良いんですが、ISOブートに対応させようとするとスキャン時と実際にマウントする時の２箇所にパッチを当てなければならず、少々複雑になります。本当はISOが検出された場合の新しい起動方法を追加するのがよさそうです。</p>
<h4><a href="http://opensolaris.org/">OpenSolaris</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> ufs+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /lib/svc/method/live-fs-root</dd>
</dl>
<p><a href="http://opensolaris.org/">OpenSolaris</a>では、/boot/x86.microroot がRAMディスクとして使われます。これのマウントは、<a href="http://opensolaris.org/">OpenSolaris</a>上で</p>
<pre>lofiadm -a x86.microroot
</pre>
<p>とした後、表示されたデバイスを</p>
<pre>mkdir -p /mnt/microroot
mount /dev/lofi/1 /mnt/microroot
</pre>
<p>などとしてマウントします。</p>
<p><a href="http://www.ubuntu.com/">Ubuntu</a>上でzfsfuseなども試してみましたが、今のところ正しくマウントできません。</p>
<p>ファイルシステムのマウントは、</p>
<pre>/lib/svc/method/live-fs-root
</pre>
<p>というスクリプトで行われます。ここでlofiadmコマンドを使ってISOファイルをループバックマウントするように修正すればISOブート可能です。</p>
<p>ただし、デフォルトのmicrorootにはvfatをマウントするためのpcfsモジュールが含まれていないので、LiveCDなどから</p>
<pre>cp /usr/kernel/fs/pcfs kernel/fs
cp -r /usr/lib/fs/pcfs usr/lib/fs
</pre>
<p>などとして、関連するモジュール群をmicroroot内にコピーしておく必要があります。</p>
<h4><a href="http://www.opensuse.org/">openSUSE</a></h4>
<dl>
<dt>フォーマット</dt>
<dd> cpio+gz</dd>
</dl>
<dl>
<dt>パッチ対象</dt>
<dd> /init, /include</dd>
</dl>
<p>oenSUSEもPuppyと同じように、一旦全ドライブをスキャンした後で再度ファイルシステムをマウントする方式を採用しています。そのため、何ヶ所か手を入れる必要があって少々複雑になります。</p>
<h3>コメント</h3>
<p><span class="error">commentプラグインは存在しません。</span> </p>
