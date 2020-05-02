---
title: ftp mput_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3fb654d5a2f44b9b63238abdbaee8d6a0294861
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725227"
---
# <a name="ftp-mput_1"></a>ftp: mput_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mput <LocalFile>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター  |                       [説明]                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | リモート コンピューターにコピーするローカル ファイルを指定します。 |

## <a name="examples"></a>例  
現在のファイル転送の種類を使用して、 **Program1**と**program2.c**をリモートコンピューターにコピーします。  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
