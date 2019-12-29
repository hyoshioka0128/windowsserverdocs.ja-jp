---
title: nslookup set timeout
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 32fcfcaeccb6599e9aaca21f9c085bb00857479c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372758"
---
# <a name="nslookup-set-timeout"></a>nslookup set timeout

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

検索要求への応答を待機する秒数の初期値を変更します。
## <a name="syntax"></a>構文
```
set timeout=<Number>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                                           説明                                            |
|-----------------|--------------------------------------------------------------------------------------------------|
|    <Number>     | 応答を待機する秒数を指定します。 待機する既定の秒数は5です。 |
| {ヘルプ&#124; ?} |                      **Nslookup**サブコマンドの簡単な概要を表示します。                       |

## <a name="remarks"></a>注釈
- 指定された期間内に要求への応答が受信されない場合、タイムアウトは2倍になり、要求は再度送信されます。 **[再試行の設定]** コマンドを使用して、再試行回数を制御できます。
  ## <a name="BKMK_examples"></a>例
  次の例では、応答を2秒に取得するためのタイムアウトを設定します。
  ```
  set timeout=2
  ```
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup](nslookup-set-retry.md)による再試行の設定
