---
title: ftp mdelete_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7b342f9d728e91085d5edf2f8e1ece00b48bec8d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438319"
---
# <a name="ftp-mdelete1"></a>ftp: mdelete_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューター上のファイルを削除します。   
## <a name="syntax"></a>構文  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |             説明              |
|--------------|--------------------------------------|
| <remoteFile> | 削除するリモート ファイルを指定します。 |

## <a name="BKMK_Examples"></a>例  
リモート ファイルの削除**a.exe**と**b.exe**します。  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
