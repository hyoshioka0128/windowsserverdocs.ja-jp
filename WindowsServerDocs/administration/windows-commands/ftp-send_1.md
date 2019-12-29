---
title: ftp send_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd9f658b4fbfa5f6c9fa9a58fb0c524ad53627bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376001"
---
# <a name="ftp-send_1"></a>ftp: send_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                    説明                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         コピーするローカル ファイルを指定します。         |
| <remoteFile> | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>コメント  
- **Send**コマンドは、 **put**コマンドと同じです。  
- *Remotefile*が指定されていない場合、ファイルには*LocalFile*という名前が付けられます。  
  ## <a name="BKMK_Examples"></a>例  
  ローカルファイル**test.txt**をコピーし、リモートコンピューター上に「 **test1** 」という名前を指定します。  
  ```  
  send test.txt test1.txt  
  ```  
  ローカルファイルの**setup.exe**をリモートコンピューターにコピーします。  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
