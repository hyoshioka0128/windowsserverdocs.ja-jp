---
title: ftp send_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 000aa80a-60a0-4b51-815f-3237a4f3e0f4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df6ea9eda6fced91babca37639cd6efe981ba7de
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843005"
---
# <a name="ftp-send_1"></a>ftp: send_1

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
send <LocalFile> [<remoteFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                    説明                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         コピーするローカル ファイルを指定します。         |
| <remoteFile> | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>コメント  
- **Send**コマンドは、 **put**コマンドと同じです。  
- *Remotefile*が指定されていない場合、ファイルには*LocalFile*という名前が付けられます。  
  ## <a name="examples"></a><a name=BKMK_Examples></a>例  
  ローカルファイル**test.txt**をコピーし、リモートコンピューター上に「 **test1** 」という名前を指定します。  
  ```  
  send test.txt test1.txt  
  ```  
  ローカルファイルの**setup.exe**をリモートコンピューターにコピーします。  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
