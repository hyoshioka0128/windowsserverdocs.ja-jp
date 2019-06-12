---
title: ftp の配置
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4d602c685b7eac5d18c88bc0f6709b189cc61a77
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438467"
---
# <a name="ftp-put"></a>ftp: 配置

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  

|   パラメーター    |                    説明                    |
|----------------|---------------------------------------------------|
|  <LocalFile>   |         コピーするローカル ファイルを指定します。         |
| [<remoteFile>] | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>注釈  
- **配置** コマンドと同じ、 **送信** コマンドです。  
- 場合*remoteFile*が指定されていない、ファイルが指定された、*ローカルファイル*名。  
  ## <a name="BKMK_Examples"></a>例  
  ローカル ファイルをコピー **test.txt**名前を付けます**test1.txt**リモート コンピューター。  
  ```  
  put test.txt test1.txt  
  ```  
  ローカル ファイルをコピー **program.exe**リモート コンピューターにします。  
  ```  
  put program.exe  
  ```  
  ## <a name="additional-references"></a>その他の参照  
- [ftp: ascii](ftp-ascii.md)  
- [ftp: バイナリ](ftp-binary.md)  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
