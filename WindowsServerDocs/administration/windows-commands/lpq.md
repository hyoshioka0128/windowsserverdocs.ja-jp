---
title: lpq
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb6abcc4-310a-4fa4-927b-4084b62ca02e vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a3755c010c9bb4549deed08f26b5a0670fe7318
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374203"
---
# <a name="lpq"></a>lpq

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ラインプリンターデーモン (LPD) を実行しているコンピューター上の印刷キューの状態を表示します。  

## <a name="syntax"></a>構文  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
## <a name="parameters"></a>パラメーター  

|    パラメーター     |                                                                        説明                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S <ServerName>  | (名前または IP アドレスを使用して) LPD 印刷キューをホストするコンピューターまたはプリンターの共有デバイスが、表示する状態であることを指定します。 必須。 |
| -P <printerName> |                           表示するステータスを持つ印刷キューのプリンタを (名前で) 指定します。 必須。                           |
|        -l        |                                      印刷キューの状態に関する詳細を表示するように指定します。                                      |
|        /?        |                                                           コマンド プロンプトにヘルプを表示します。                                                            |

## <a name="remarks"></a>コメント  
**-S**パラメーターと **-P**パラメーターは大文字と小文字が区別され、大文字で入力する必要があります。  
## <a name="BKMK_examples"></a>例  
この例では、10.0.0.45 にある LPD ホストの Laserprinter1 プリンターキューの状態を表示する方法を示します。  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
