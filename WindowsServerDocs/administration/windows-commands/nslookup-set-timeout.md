---
title: nslookup set timeout
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 07afdaf4-ffec-496f-a188-4e91cf1a28f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68e9630b9690c9b6c9d4c316f8b328897289362c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723541"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

検索要求への応答を待機する秒数の初期値を変更します。
## <a name="syntax"></a>構文
```
set timeout=<Number>
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                           [説明]                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | 応答を待機する秒数を指定します。 待機する既定の秒数は5です。 |
| {help &#124;?} |                      **Nslookup**サブコマンドの簡単な概要を表示します。                       |

## <a name="remarks"></a>Remarks
- 指定された期間内に要求への応答が受信されない場合、タイムアウトは2倍になり、要求は再度送信されます。 [**再試行の設定**] コマンドを使用して、再試行回数を制御できます。
  ## <a name="examples"></a>例
  応答の取得のタイムアウトを2秒に設定するには、次のようにします。
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文キー](command-line-syntax-key.md)
  [nslookup set retry](nslookup-set-retry.md)
