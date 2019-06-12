---
title: ftp の受信
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5bfd68dcb745ebf7ef239883aa1c5322241b32df
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438435"
---
# <a name="ftp-recv"></a>ftp: recv

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
recv <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  

|   パラメーター   |                   説明                    |
|---------------|--------------------------------------------------|
| <remoteFile>  |        コピーするリモート ファイルを指定します。        |
| [<LocalFile>] | ローカル コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>注釈  
- **Recv** コマンドと同じ、 **取得** コマンドです。  
- 場合*ローカルファイル*が指定されていない、ファイルが指定された、 *remoteFile*名。  
  ## <a name="BKMK_Examples"></a>例  
  コピー **test.txt**現在のファイル転送の種類を使用してローカル コンピューターにします。  
  ```  
  recv test.txt  
  ```  
  コピー **test.txt**として、ローカル コンピューターに**test1.txt**転送の種類を現在のファイルを使用します。  
  ```  
  recv test.txt test1.txt  
  ```  
  ## <a name="additional-references"></a>その他の参照  
- [ftp: ascii](ftp-ascii.md)  
- [ftp: バイナリ](ftp-binary.md)  
- [ftp: get](ftp-get.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
