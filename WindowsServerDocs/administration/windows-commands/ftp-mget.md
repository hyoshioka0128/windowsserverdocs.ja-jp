---
title: ftp mget
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a71fbfb60ae012b5e65af04e6f3e21ec796996a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725234"
---
# <a name="ftp-mget"></a>ftp: mget

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mget <remoteFile>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                        [説明]                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | ローカル コンピューターにコピーするリモート ファイルを指定します。 |

## <a name="examples"></a>例  
現在のファイル転送の種類を使用して、リモートファイル**を**ローカル**コンピューターにコピーします。**  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
