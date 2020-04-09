---
title: nslookup set retry
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 615fdfa2-fa29-47a8-8c9e-a6c5b45b3b71
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b95c4c8af2d7960270fd43f7a766b313ddbc07a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838345"
---
# <a name="nslookup-set-retry"></a>nslookup set retry

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

再試行回数を設定します。
## <a name="syntax"></a>構文
```
set retry=<Number>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                      説明                                       |
|-----------------|----------------------------------------------------------------------------------------|
|    <Number>     | 再試行回数の新しい値を指定します。 既定の再試行回数は4です。 |
| {ヘルプ&#124; ?} |                 **Nslookup**サブコマンドの簡単な概要を表示します。                  |

## <a name="remarks"></a>コメント
- 一定の時間内に要求に対する応答が受信されない場合、タイムアウト期間は2倍になり、要求は再送信されます。 再試行の値は、要求を再送信する回数を制御します。 タイムアウト期間は、 **set timeout**サブコマンドを使用して変更できます。
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup set timeout](nslookup-set-timeout.md)
