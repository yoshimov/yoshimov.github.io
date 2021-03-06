---
layout: post
category: tips
tags: [tasker, android, tips]
title: 電波が弱い時に一定時間機内モードにする
---
{% include keywords.md %}

## 概要

携帯電話は電波が弱いと出力を上げるので電池が早く減りますが、
一定時間機内モードにすることで、電池の消費を抑える設定です。

* 2013-7-19 Time Contextを使った設定に変更しました。

## 環境

* [CASIO IS11CA][]
* [Google Nexus 7][]
* [Tasker][] 1.6
* [AutoRemote][] 2.0.6

## 手順

* 一定時間機内モードに設定するタスクを作る。
以下は６分間機内モードに設定するタスクの例です。
    * 電波状況の揺れを考えて、５秒間待って電波が改善しなければ
機内モードにしています。
    * Countdownと機内モードを解除するResumeを別にしましたが、１つでも良いです。

<pre>Task: Suspend cell network (31)
 A1: Wait [ MS:0 Seconds:5 Minutes:0 Hours:0 Days:0 ] If [ %CELLSIG = 0 ]
 A2: Return [ Value:0 Stop:On ] If [ %CELLSIG &gt; 0 ]
 A3: Airplane Mode [ Set:On ] 
 A4: Auto-Sync [ Set:Off ] 
 A5: Variable Set [ Name:%suspendMinute To:6 Do Maths:Off Append:Off ] If [ %suspendMinute ! Set ]

Task: Resume cell network (33)
 A1: Airplane Mode [ Set:Off ] 
 A2: Auto-Sync [ Set:On ] 
 A3: Variable Clear [ Name:%suspendMinute Pattern Matching:Off ] 

Task: Countdown cell network (34)
 A1: Variable Subtract [ Name:%suspendMinute Value:3 ] 
 A2: Return [ Value:0 Stop:On ] If [ %suspendMinute &gt; 0 ]
 A3: Variable Clear [ Name:%suspendMinute Pattern Matching:Off ] 
 A4: Perform Task [ Name:Resume cell network Stop:Off Priority:5 Parameter 1 (%par1): Parameter 2 (%par2): Return Value Variable: ] 
</pre>

* 携帯の電波が弱くなった時に、Wifi接続なし、電源なし、機内モードではなければ、
一定時間機内モードに設定するプロファイルを作ります。
    * Time Stateのrepeatを使って、一定時間ごとに残り時間をカウントダウンする
タスクを呼び出します。

<pre>Profile: Weak Cell Network (32)
 State: Not Airplane Mode
 State: Not Wifi Connected [ SSID:* MAC:* IP:* ]
 Event: Variable Set [ Variable:%CELLSIG Value:0 ]
 State: Not Power [ Source:Any ]
 Enter: Suspend cell network (31)

Profile: Keep airplane (35)
 State: Variable Value [ Name:%suspendMinute Op:Maths: Greater Than Value:0 ]
 Time: Every 3m
 State: Airplane Mode
 Enter: Countdown cell network (34)
</pre>

これで、一定時間機内モードにして、復帰した時にまだ電波状況が
改善していなければ、再度機内モードに入ります。

もう１つ変数を導入すれば、機内モードに設定する時間を徐々に延ばしていく
スロットリングが入れられますね。そのへんはまたおいおい。
