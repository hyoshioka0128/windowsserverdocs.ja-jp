---
title: ftp send_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 04617246c05edde127db01ce1a0fe692eb0aceb1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725106"
---
# <a name="ftp-send_1"></a>ftp: send_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
send <LocalFile> [<remoteFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                    [説明]                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         コピーするローカル ファイルを指定します。         |
| <remoteFile> | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>Remarks  
- **Send**コマンドは、 **put**コマンドと同じです。  
- *Remotefile*が指定されていない場合、ファイルには*LocalFile*という名前が付けられます。  
  ## <a name="examples"></a>例  
  ローカルファイル**test.txt**をコピーし、リモートコンピューター上に「 **test1** 」という名前を指定します。  
  ```  
  send test.txt test1.txt  
  ```  
  ローカルファイルの**setup.exe**をリモートコンピューターにコピーします。  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
