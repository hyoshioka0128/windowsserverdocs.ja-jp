---
title: nslookup set timeout
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f6c8863d0a9330fd3a8499b0e6dbc802bd95022
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436509"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

初期の参照要求に応答を待機する秒数を変更します。
## <a name="syntax"></a>構文
```
set timeout=<Number>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                           説明                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | 応答を待機する秒数を指定します。 既定を待機する秒数には 5 です。 |
| {help &#124; ?} |                      簡単な概要を表示します。 **nslookup**サブコマンドします。                       |

## <a name="remarks"></a>注釈
- 指定した期間中、要求への応答が受信していない場合は、タイムアウトが倍になり、要求を再送信します。 使用することができます、**セット再試行**再試行の回数を制御するコマンド。
  ## <a name="BKMK_examples"></a>例
  次の例は、2 秒への応答を取得するためのタイムアウトを設定します。
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup 再試行の設定](nslookup-set-retry.md)
