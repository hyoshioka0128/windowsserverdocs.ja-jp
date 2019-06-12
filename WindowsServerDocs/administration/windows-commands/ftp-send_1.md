---
title: ftp [send_1]
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 39423aff3c64f41c4fc0f8998484e6dcc38f822e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438443"
---
# <a name="ftp-send1"></a>ftp: [send_1]

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                    説明                    |
|--------------|---------------------------------------------------|
| <LocalFile>  |         コピーするローカル ファイルを指定します。         |
| <remoteFile> | リモート コンピューターで使用する名前を指定します。 |

## <a name="remarks"></a>注釈  
- **送信**コマンドと同じ、**配置**コマンド。  
- 場合*remoteFile*が指定されていない、ファイルが指定された、*ローカルファイル*名。  
  ## <a name="BKMK_Examples"></a>例  
  ローカル ファイルをコピー **test.txt**名前を付けます**test1.txt**リモート コンピューター。  
  ```  
  send test.txt test1.txt  
  ```  
  ローカル ファイルをコピー **program.exe**リモート コンピューターにします。  
  ```  
  send program.exe  
  ```  
  ## <a name="additional-references"></a>その他の参照  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
