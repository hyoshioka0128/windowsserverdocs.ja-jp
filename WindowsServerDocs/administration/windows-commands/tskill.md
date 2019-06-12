---
title: tskill
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b582334d7b79b2badbb86818be1093b6a5f55080
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440815"
---
# <a name="tskill"></a>tskill

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のセッションで実行中のプロセスを終了します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|\<ProcessID>|終了するプロセスの ID を指定します。|
|\<ProcessName>|終了するプロセスの名前を指定します。 このパラメーターは、ワイルドカード文字を含めることができます。|
|/server:\<ServerName >|終了するプロセスがターミナル サーバーを指定します。 場合 **/server**が指定されていない、現在の RD セッション ホスト サーバーが使用されます。|
|/id:\<SessionID>|指定したセッションで実行されているプロセスを終了します。|
|/a|すべてのセッションで実行されているプロセスを終了します。|
|/v|実行する操作についての情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
- 使用することができます**tskill**管理者である場合を除きに属しているプロセスのみを終了します。 管理者は、すべてにフル アクセス権を持つ**tskill**関数およびその他のユーザーのセッションで実行されているプロセスを終了することができます。
- セッションで実行されているすべてのプロセスが終了すると、セッションが終了します。
- 使用する場合、 *ProcessName*と **/server:** <em>ServerName</em>パラメーター、いずれかを指定する必要があります、 **/id:** <em>SessionID</em>または **/a**パラメーター。

## <a name="BKMK_examples"></a>例
- 6543 プロセスを終了するには、次のように入力します。
  ```
  tskill 6543
  ```
- セッション 5 で実行されているプロセス"explorer"を終了するには、次のように入力します。
  ```
  tskill explorer /id:5
  ```
  #### <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービスと #40 です。ターミナル サービスと #41 です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
