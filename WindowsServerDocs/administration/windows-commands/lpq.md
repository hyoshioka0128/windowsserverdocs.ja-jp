---
title: lpq
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 18ff1ff3ecbc2df0a437ec8a465dec9a12123ede
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437511"
---
# <a name="lpq"></a>lpq

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ライン プリンタ デーモン (LPD) を実行しているコンピューター上の印刷キューの状態を表示します。  

## <a name="syntax"></a>構文  
```  
lpq -S <ServerName> -P <printerName> [-l]  
```  
## <a name="parameters"></a>パラメーター  

|    パラメーター     |                                                                        説明                                                                        |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| -S <ServerName>  | コンピューターまたはプリンターの共有状態を表示したい LPD 印刷キューをホストしているデバイス (名前または IP アドレス) を指定します。 必須。 |
| -P <printerName> |                           表示する状態で印刷キューのプリンターを (名) を指定します。 必須。                           |
|        -l        |                                      印刷キューの状態に関する詳細を表示することを指定します。                                      |
|        /?        |                                                           コマンド プロンプトにヘルプを表示します。                                                            |

## <a name="remarks"></a>注釈  
**-S**と **-p**パラメーターは大文字と小文字、大文字で入力する必要があります。  
## <a name="BKMK_examples"></a>例  
この例では、LPD 10.0.0.45 にホスト上の Laserprinter1 プリンター キューの状態を表示する方法を示します。  
```  
lpq -S 10.0.0.45 -P Laserprinter1  
```  
#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
[印刷コマンドのリファレンス](print-command-reference.md)  
