---
title: nslookup set retry
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1baeeaefedc211434f46bd0cfad713f093a873bf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723584"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

再試行回数を設定します。
## <a name="syntax"></a>構文
```
set retry=<Number>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                      [説明]                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | 再試行回数の新しい値を指定します。 既定の再試行回数は4です。 |
| {help &#124;?} |                 **Nslookup**サブコマンドの簡単な概要を表示します。                  |

## <a name="remarks"></a>Remarks
- 一定の時間内に要求に対する応答が受信されない場合、タイムアウト期間は2倍になり、要求は再送信されます。 再試行の値は、要求を再送信する回数を制御します。 タイムアウト期間は、 **set timeout**サブコマンドを使用して変更できます。
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set timeout](nslookup-set-timeout.md)
