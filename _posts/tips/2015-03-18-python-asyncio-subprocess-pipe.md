---
layout: post
category: tips
tags: tips python asyncio pipe
title: Python3のasyncioを使って非同期に標準出力を取得する
---

## 概要

Python3のasyncioを使って、サブプロセスとして起動したtailなどのコマンドから
非同期に出力を取得する方法です。

asyncioはスレッドより並列処理が書きやすいですが、
あんまりasyncioを使ったサンプルが見当たらなかったのでメモ。

## 環境

- Ubuntu 14.10
- Python 3.4.2

## コード

```
import asyncio

@asyncio.coroutine
def tailf():
  print("tail started")
  p = yield from asyncio.create_subprocess_shell("tail -F test", stdout=asyncio.subprocess.PIPE)
  while True:
    str = yield from p.stdout.readline()
    print(str.decode('utf-8'))

loop = asyncio.get_event_loop()
asyncio.async(tailf())

try:
  loop.run_forever()
finally:
  loop.close()
```

まず、サブプロセスを監視する処理はコルーチン関数である必要があるらしいので、
`@asyncio.coroutine`を付けた関数を定義します。

そして、asyncio.asyncで呼び出します。
call_soon, call_laterなどではないので気をつけてください。

プロセスの起動はyield fromを付けて`asyncio.create_subprocess_shell`を使います。
この際にstdoutをPIPEに設定すると、`stdout.readline()`で１行ずつ処理結果を受け取れます。
またreadlineにyield fromを付けることで、見た目上入力待ち状態になります。

## 参考

- [サブプロセスの作成: Process を使用した高レベル API](http://docs.python.jp/3/library/asyncio-subprocess.html#create-a-subprocess-high-level-api-using-process)

