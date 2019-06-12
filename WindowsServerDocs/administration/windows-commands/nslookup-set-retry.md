---
title: nslookup set retry
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 876d8332e778aa0b3049354a21fbe01adb883729
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436653"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

再試行の回数を設定します。
## <a name="syntax"></a>構文
```
set retry=<Number>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                      説明                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | 再試行の回数の新しい値を指定します。 既定の再試行回数には 4 です。 |
| {help &#124; ?} |                 簡単な概要を表示します。 **nslookup**サブコマンドします。                  |

## <a name="remarks"></a>注釈
- 一定の時間内で、要求への応答が受信していない場合は、タイムアウト期間が倍になり、要求が再送信してもらいます。 再試行の値渡す前に、要求が再送信回数を制御します。 タイムアウト期間を変更することができます、**タイムアウト設定**サブコマンドします。
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup のタイムアウトを設定します。](nslookup-set-timeout.md)
