---
title: ftp mdelete_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f578a50207439f9bfb21c2607f0aa60a20fad292
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725037"
---
# <a name="ftp-mdelete_1"></a>ftp: mdelete_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のファイルを削除します。   
## <a name="syntax"></a>構文  
```  
mdelete <remoteFile>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |             [説明]              |
|--------------|--------------------------------------|
| <remoteFile> | 削除するリモートファイルを指定します。 |

## <a name="examples"></a>例  
リモートファイル**の .exe**と**b .exe**を削除します。  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
