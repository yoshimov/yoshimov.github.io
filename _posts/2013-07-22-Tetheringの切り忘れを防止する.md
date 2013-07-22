---
layout: post
title: Tetheringの切り忘れを防止する
category: Tasker
tags: [TaskerTips, AndroidTips]
---

概要
====
CASIO IS11CAではテザリングができますが、使った後にオフにし忘れてしまって、
バッテリが激減してしまうことがよくあるので、
それを防止する方法です。

タブレットとセットで設定します。

これでどんなことができるようになるかというと、
*スマホを取り出して、振るだけでテザリングを開始
*タブレットから操作不要ですぐネットが使える
*使い終わったらタブレットをスリープにするだけで、テザリングも勝手に切れる
という感じの使い勝手になります。

* 2013.7.19: Time Contextを使った設定に変更しました。
* 2013.7.22: 画面再表示時にメッセージを再送信するように変更しました。

環境
====
* CASIO IS11CA
* Google Nexus 7
* Tasker 1.6
* AutoRemote 2.0.6

準備
====
* スマートフォンとタブレット双方に、TaskerとAutoRemoteを入れておく。
* タブレット側のAutoRemoteに、スマートフォンのAutoRemoteを登録しておく。

設定
====
##スマートフォン側（テザリング提供側）
* 以下のようなタイマーでテザリングを切るタスクを作って、ジェスチャーなどから起動するようにしておく。以下は５分で切る例です。

```
 Task: Tether timer (22)
   A1: Notify LED [ Title:Tethering Text: Icon:<icon> Number:3 Colour:Blue Rate:525 Priority:3 ] 
   A2: WiFi Tether [ Set:On ] 
   A3: Variable Set [ Name:%keepTether To:5 Do Maths:Off Append:Off ]

 Task: stopTether (27)
   A1: WiFi Tether [ Set:Off ] 
   A2: Notify Cancel [ Title:Tethering Warn Not Exist:Off ] 
   A3: Variable Clear [ Name:%keepTether Pattern Matching:Off ]

 Task: countTether (36)
   A1: Variable Subtract [ Name:%keepTether Value:2 ] 
   A2: Perform Task [ Name:stopTether Stop:Off Priority:5 Parameter 1 (%par1): Parameter 2 (%par2): Return Value Variable: ] If [ %keepTether < 1 ]
```

* ジェスチャーでテザリングを開始するプロファイルの例です。
 * Time Contextを使って一定時間ごとに残り時間をカウントダウンするプロファイルも作っておきます。

```
    Profile: Tethering gesture (23)
    Event: Shake [ Axis:Left-Right Sensitivity:Medium Duration:Medium ]
    State: Orientation [ Is:Face Up ]
    State: Variable Value [ Name:%keepTether Op:Isn't Set Value:* ]
    Enter: Tether timer (22)
    
    Profile: Tethering off (28)
      Event: Shake [ Axis:Left-Right Sensitivity:Medium Duration:Medium ]
      State: Orientation [ Is:Face Up ]
      State: Variable Value [ Name:%keepTether Op:Is Set Value:* ]
      Enter: stopTether (27)
    
    Profile: Count Tethering (37)
      State: Variable Value [ Name:%keepTether Op:Maths: Greater Than Value:0 ]
      Time: Every 2m
      Enter: countTether (36)
```

* AutoRemoteのメッセージを受けて、テザリングタイマーの残り時間をクリアするようにする。以下では "kt" というメッセージでクリアしています。

```
    Profile: Keep Tethering (25)
      State: AutoRemoteLite [ Configuration:kt ]
      State: Variable Value [ Name:%keepTether Op:Is Set Value:* ]
      Enter: keepTether (26)
    
    Task: keepTether (26)
      A1: Variable Set [ Name:%keepTether To:5 Do Maths:Off Append:Off ]
```

##タブレット側（テザリング利用側）
* テザリング中は、一定時間毎にAutoRemoteのメッセージを送るタスクを作ります。
 * 以下はディスプレイがオンの間は２分おきにメッセージを送る例です。
 * Profileが２つあるのは、一度画面を消して再度表示させた際に、２分待つ間にテザリングが切れてしまうのを防止するためです。

```
   Profile: Mobile (9)
     State: Display State [ Is:On ]
     State: Wifi Connected [ SSID:xxxx MAC:xxxx IP:* ]
     Time: Every 2m
     Enter: Mobile (10)
    
    Profile: Mobile Display On
     Event: Display On
     State: Wifi Connected [ SSID:xxxx MAC:xxxx IP:* ]
     Enter: Mobile
    
    Task: Mobile (10)
     A1: AutoRemoteLite Message [ Configuration:Recipient: xxxx Message: kt Package:com.joaomgcd.autoremote.lite Name:AutoRemoteLite Message ]
```

これで、テザリングタイマーを使って普通にWifiを使って、使い終わったら
タブレット側のティスプレイを切るだけで、自動的にスマートフォン側のテザリングが
切れるようになります。
