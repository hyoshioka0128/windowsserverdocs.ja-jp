---
title: nslookup set timeout
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8506511fc203f94d395851471f6a981ef0765928
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838275"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

検索要求への応答を待機する秒数の初期値を変更します。
## <a name="syntax"></a>構文
```
set timeout=<Number>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                           説明                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | 応答を待機する秒数を指定します。 待機する既定の秒数は5です。 |
| {ヘルプ&#124; ?} |                      **Nslookup**サブコマンドの簡単な概要を表示します。                       |

## <a name="remarks"></a>コメント
- 指定された期間内に要求への応答が受信されない場合、タイムアウトは2倍になり、要求は再度送信されます。 **[再試行の設定]** コマンドを使用して、再試行回数を制御できます。
  ## <a name="examples"></a><a name=BKMK_examples></a>例
  次の例では、応答を2秒に取得するためのタイムアウトを設定します。
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup](nslookup-set-retry.md)による再試行の設定
