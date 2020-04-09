---
title: nslookup set
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1fe5b36d-e93e-468b-abca-43b0204b32d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3883e6b032c5a4542711ad14a4e45b31fb605485
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838145"
---
# <a name="nslookup-set"></a>nslookup set

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

参照の機能に影響する構成設定を変更します。
## <a name="syntax"></a>構文
```
set <KeyWord>[=<Value>]
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                    説明                                                                                                                    |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <KeyWord>    | **Set**サブコマンドから派生したサブコマンドを識別します。 たとえば、サブコマンド**set d2**には、 **[no]** **d2**というキーワードがあります。 **Set**サブコマンドから派生したサブコマンドの一覧については、「その他の参照情報」を参照してください。 |
|     <Value>     |                                                                                      各サブコマンドの nslookup 構成設定値を指定します。                                                                                      |
| {ヘルプ&#124; ?} |                                                                                               **Nslookup**サブコマンドの簡単な概要を表示します。                                                                                               |

## <a name="remarks"></a>コメント
現在の設定の一覧を表示するには、 **[すべて設定]** を使用します。
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[nslookup set all](nslookup-set-all.md)
