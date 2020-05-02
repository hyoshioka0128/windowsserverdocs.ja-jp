---
title: lpq
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2d7a013ad9481780873cd57be4fa15732fc6196
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724254"
---
# <a name="lpq"></a>lpq

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ラインプリンターデーモン (LPD) を実行しているコンピューター上の印刷キューの状態を表示します。  

## <a name="syntax"></a>構文  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
### <a name="parameters"></a>パラメーター  

|    パラメーター     |                                                                        [説明]                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S<ServerName>  | (名前または IP アドレスを使用して) LPD 印刷キューをホストするコンピューターまたはプリンターの共有デバイスが、表示する状態であることを指定します。 必須。 |
| -P<printerName> |                           表示するステータスを持つ印刷キューのプリンタを (名前で) 指定します。 必須。                           |
|        -l        |                                      印刷キューの状態に関する詳細を表示するように指定します。                                      |
|        /?        |                                                           コマンド プロンプトにヘルプを表示します。                                                            |

## <a name="remarks"></a>Remarks  
**-S**パラメーターと **-P**パラメーターは大文字と小文字が区別され、大文字で入力する必要があります。  
## <a name="examples"></a>例  
この例では、10.0.0.45 にある LPD ホストの Laserprinter1 プリンターキューの状態を表示する方法を示します。  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
