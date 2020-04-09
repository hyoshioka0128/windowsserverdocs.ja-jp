---
title: lpq
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 051b1983fcc0fddd7b69e561c0a27a120f78d998
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840395"
---
# <a name="lpq"></a>lpq

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ラインプリンターデーモン (LPD) を実行しているコンピューター上の印刷キューの状態を表示します。  

## <a name="syntax"></a>構文  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
### <a name="parameters"></a>パラメーター  

|    パラメーター     |                                                                        説明                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S <ServerName>  | (名前または IP アドレスを使用して) LPD 印刷キューをホストするコンピューターまたはプリンターの共有デバイスが、表示する状態であることを指定します。 必須。 |
| -P <printerName> |                           表示するステータスを持つ印刷キューのプリンタを (名前で) 指定します。 必須。                           |
|        -l        |                                      印刷キューの状態に関する詳細を表示するように指定します。                                      |
|        /?        |                                                           コマンド プロンプトでヘルプを表示します。                                                            |

## <a name="remarks"></a>コメント  
**-S**パラメーターと **-P**パラメーターは大文字と小文字が区別され、大文字で入力する必要があります。  
## <a name="examples"></a><a name=BKMK_examples></a>例  
この例では、10.0.0.45 にある LPD ホストの Laserprinter1 プリンターキューの状態を表示する方法を示します。  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
