---
layout: post
---
<p><span class="error">categoryプラグインは存在しません。</span></p>
<h3>環境</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a> 8.10</li>
<li><a href="http://www.vmware.com/jp/products/player/">VMware</a> Player 1.0.3</li>
</ul>
<h3>概要</h3>
<p>USB起動の<a href="http://www.ubuntu.com/">Ubuntu</a>を<a href="http://www.vmware.com/jp/products/player/">VMware</a>上で動作させる方法です。</p>
<p>これができると<a href="http://www.vmware.com/jp/products/player/">VMware</a>上でカスタマイズした<a href="http://www.ubuntu.com/">Ubuntu</a>を、実マシン上で動作させるということが非常に簡単にできます。</p>
<h3>手順</h3>
<ul>
<li><a href="http://www.ubuntu.com/">Ubuntu</a>をライブCDから起動</li>
<li>USBメモリへのインストールを行う<ul>
<li>[システム]-[システム管理]-[Create a USB startup disk]から</li>
</ul>
</ul>
<ul>
<li><a href="http://www.vmware.com/jp/products/player/">VMware</a>のホストPCからUSBメモリを抜いておく</li>
<li>以下のサイトから、起動用CDイメージをダウンロード<ul>
<li><a href="http://www.pendrivelinux.com/2008/11/15/usb-boot-cd-for-ubuntu-810/">http://www.pendrivelinux.com/2008/11/15/usb-boot-cd-for-ubuntu-810/</a></li>
</ul>
</ul>
<ul>
<li><a href="http://www.vmware.com/jp/products/player/">VMware</a> PlayerのVMXファイルを作成して、以下のように変更<ul>
<li>作成は<a href="http://petruska.stardock.net/Software/VMware.html">VMX Builder</a>がお勧め</li>
</ul>
</ul>
<pre>ide0:0.present = &quot;TRUE&quot;
ide0:0.fileName = &quot;C:\somewhere\USBCD810.iso&quot;
ide0:0.autodetect = &quot;TRUE&quot;
ide0:0.deviceType = &quot;cdrom-image&quot;
ide0:0.startConnected = &quot;TRUE&quot;
usb.present = &quot;TRUE&quot;
usb.generic.autoconnect = &quot;TRUE&quot;
</pre>
<ul>
<li>VMXファイルをダブルクリックして<a href="http://www.vmware.com/jp/products/player/">VMware</a> Playerを起動</li>
<li>grubのメニューが出たら、USBメモリを挿入</li>
<li><a href="http://www.vmware.com/jp/products/player/">VMware</a> Playerのウィンドウ上にUSBメモリが現れて選択状態になったら、<a href="http://www.ubuntu.com/">Ubuntu</a>を起動する</li>
</ul>
<h3>備考</h3>
<p>カーネルのバージョンをアップデートしていたりするとこの方法は使えませんので、以下のページを参考にCDイメージを作り直す必要があります。</p>
<ul>
<li><a href="/?page=Ubuntu%2FUSB%A5%E1%A5%E2%A5%EA%A4%AB%A4%E9%B5%AF%C6%B0%A4%B9%A4%EBCD%A5%A4%A5%E1%A1%BC%A5%B8%A4%CE%BA%EE%C0%AE" class="wikipage">Ubuntu/USBメモリから起動するCDイメージの作成</a></li>
<li><a href="http://www.pendrivelinux.com/2008/12/17/create-a-cd-to-boot-ubuntu-from-usb/">http://www.pendrivelinux.com/2008/12/17/create-a-cd-to-boot-ubuntu-from-usb/</a></li>
</ul>
