---
title: nslookup set
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1fe5b36d-e93e-468b-abca-43b0204b32d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e416fb3bf8dafa72f0c46a018723aa75ae621de
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723514"
---
# <a name="nslookup-set"></a>nslookup set

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

参照の機能に影響する構成設定を変更します。
## <a name="syntax"></a>構文
```
set <KeyWord>[=<Value>]
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                    [説明]                                                                                                                    |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <KeyWord>    | **Set**サブコマンドから派生したサブコマンドを識別します。 たとえば、サブコマンド**set d2**には、[**no**]**d2**というキーワードがあります。 **Set**サブコマンドから派生したサブコマンドの一覧については、「その他の参照情報」を参照してください。 |
|     <Value>     |                                                                                      各サブコマンドの nslookup 構成設定値を指定します。                                                                                      |
| {help &#124;?} |                                                                                               **Nslookup**サブコマンドの簡単な概要を表示します。                                                                                               |

## <a name="remarks"></a>Remarks
現在の設定の一覧を表示するには、[**すべて設定**] を使用します。
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[nslookup set all](nslookup-set-all.md)
