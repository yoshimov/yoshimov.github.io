---
layout: post
category: tips
tags: powershell tips classid windows
title: PowerShellでアプリのクラスIDを検索する
---
{% include keywords.md %}

## 概要

WindowsのPowerShellで、インストールされているアプリのクラスIDを検索する方法です。

## 環境

- Windows 8
- PowerShell 1.0

## 手順

MSI形式でインストールするアプリの場合、アンインストール時にアプリのクラスIDが必要になります。
クラスIDは以下のレジストリの下に格納されています。

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

ここから、特定のクラスIDを検索する場合、
まずGet-ChildItemでリストを取得して、foreachでループします。

    $croot = "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall"
    Get-ChildItem -Path $croot | foreach {

それぞれのアイテムから、プロパティを取得します。

      $CurrentKey = (Get-ItemProperty -Path $_.PsPath)

取得したプロパティの中に、特定の文字列がないかを -match で判定します。
見つかればそこから、PsChildName を取ると
クラスIDが取得できます。

      if ($CurrentKey -match 'gSyncIt' -and $CurrentKey -match '3.9') {
        $CurrentKey.PsChildName
      }
    }

## 参考

* [レジストリエントリの操作](http://technet.microsoft.com/ja-jp/library/dd315394.aspx)
