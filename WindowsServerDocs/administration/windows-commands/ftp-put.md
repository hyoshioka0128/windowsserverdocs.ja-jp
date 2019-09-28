---
title: ftp put
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95cc1e3f-523d-4374-98b8-16e6c276b2ca vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15c1734322d3642ebc85891b71c6ad68100d514d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376074"
---
# <a name="ftp-put"></a>ftp: put

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、ローカルファイルをリモートコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  

|   パラメーター    |                    説明                    |
|----------------|---------------------------------------------------|
|  <LocalFile>   |         コピーするローカル ファイルを指定します。         |
| [<remoteFile>] | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>コメント  
- **配置** コマンドと同じ、 **送信** コマンドです。  
- *Remotefile*が指定されていない場合、ファイルには*LocalFile*という名前が付けられます。  
  ## <a name="BKMK_Examples"></a>例  
  ローカルファイル**test.txt**をコピーし、リモートコンピューター上に「 **test1** 」という名前を指定します。  
  ```  
  put test.txt test1.txt  
  ```  
  ローカルファイルの**setup.exe**をリモートコンピューターにコピーします。  
  ```  
  put program.exe  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [ftp: ascii](ftp-ascii.md)  
- [ftp: バイナリ](ftp-binary.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
