---
layout: post
category: tips
tags: tips screen
title: ScreenにCPU使用率を表示する
---
{% include keywords.md %}

## 概要

GNU ScreenにCPU使用率を表示する方法です。

## 環境

* Ubuntu 13.04
* Screen 4.00.03

## 手順

ロードアベレージなら `%l` で表示することができますが、
ちょっとわかりにくいので、私は%表記のものを表示しています。
CPUの利用率は、/proc/statの差分を取るとわかるので、
awkで差分を計算するスクリプトを作って、
backtickとして流し込んでやります。

例えば、こんなスクリプトを作って、screenrc/cpuとして保存します。
ポイントは、前回の情報をprestatとして保存しておいて、
awkの計算時に利用する点です。

<pre>
#!/bin/bash
 
CUR=/proc/stat
USER=$(whoami)
PRE=/tmp/${USER}-prestat
 
if [ ! -f $PRE ]; then
  head -1 $CUR > $PRE
  exit 1
fi
 
awk '
  /cpu /{
	if (match(FILENAME,"prestat")) {
		pretotal = $2+$3+$4+$5; preidle = $5;
	} else {
		ctotal = $2+$3+$4+$5; cidle = $5;
	}
  }
  END {
	dtotal = ctotal - pretotal
	didle = cidle - preidle
	printf("%d%c",(((dtotal - didle) * 100) / dtotal),37)
  }
' $PRE $CUR
 
head -1 $CUR > $PRE
</pre>

そして、.screenrc 側で、

    hardstatus alwayslastline "%{=b by} %H %{= bg}%0`"
    backtick 0 10 10 bash $HOME/screenrc/cpu

こんな感じで指定すると、10秒に一回CPUの使用率が表示できます。
