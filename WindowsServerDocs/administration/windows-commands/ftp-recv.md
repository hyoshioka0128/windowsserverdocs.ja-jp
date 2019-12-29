---
title: ftp 受信
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f249ce61-247d-421b-9b93-48bce5108800 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ec35a2044945e3d39a2a78d39923de3a56eb18d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376129"
---
# <a name="ftp-recv"></a>ftp: 受信

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、リモートファイルをローカルコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
recv <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  

|   パラメーター   |                   説明                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        コピーするリモートファイルを指定します。        |
| [<LocalFile>] | ローカル コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>コメント  
- **Recv** コマンドと同じ、 **取得** コマンドです。  
- *LocalFile*が指定されていない場合、ファイルには*remotefile*という名前が付けられます。  
  ## <a name="BKMK_Examples"></a>例  
  現在のファイル転送の種類を使用して、ローカルコンピューターに**test.txt**をコピーします。  
  ```  
  recv test.txt  
  ```  
  現在のファイル転送の種類を使用して、 **test.txt**をローカルコンピューターに**test.txt**としてコピーします。  
  ```  
  recv test.txt test1.txt  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [ftp: ascii](ftp-ascii.md)  
- [ftp: バイナリ](ftp-binary.md)  
- [ftp: get](ftp-get.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
