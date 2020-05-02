---
title: ftp 受信
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ece259f2d48e18f6a789d51b1df7089490f2fa1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725127"
---
# <a name="ftp-recv"></a>ftp: 受信

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、リモートファイルをローカルコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
recv <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|   パラメーター   |                   [説明]                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        コピーするリモートファイルを指定します。        |
| [<LocalFile>] | ローカル コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>Remarks  
- **Recv** コマンドと同じ、 **取得** コマンドです。  
- *LocalFile*が指定されていない場合、ファイルには*remotefile*という名前が付けられます。  
  ## <a name="examples"></a>例  
  現在のファイル転送の種類を使用して、ローカルコンピューターに**test.txt**をコピーします。  
  ```  
  recv test.txt  
  ```  
  現在のファイル転送の種類を使用して、 **test.txt**をローカルコンピューターに**test.txt**としてコピーします。  
  ```  
  recv test.txt test1.txt  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- [ftp: ascii](ftp-ascii.md)  
- [ftp: バイナリ](ftp-binary.md)  
- [ftp: get](ftp-get.md)  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
