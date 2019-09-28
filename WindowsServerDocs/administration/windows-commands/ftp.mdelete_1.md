---
title: ftp mdelete_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6ffbb06cff9e177316ea60e281c25d7640a7f981
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375923"
---
# <a name="ftp-mdelete_1"></a>ftp: mdelete_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のファイルを削除します。   
## <a name="syntax"></a>構文  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |             説明              |
|--------------|--------------------------------------|
| <remoteFile> | 削除するリモートファイルを指定します。 |

## <a name="BKMK_Examples"></a>例  
リモートファイル**の .exe**と**b .exe**を削除します。  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
