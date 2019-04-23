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
ms.openlocfilehash: 3307ba71e7b3c8b4113f9ed29ab06660dafa5f6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868743"
---
# <a name="ftp-put"></a>ftp: 配置

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
put <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<LocalFile>|コピーするローカル ファイルを指定します。|  
|[<remoteFile>]|リモート コンピューターで使用する名前を指定します。|  
## <a name="remarks"></a>注釈  
-   **配置** コマンドと同じ、 **送信** コマンドです。  
-   場合*remoteFile*が指定されていない、ファイルが指定された、*ローカルファイル*名。  
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
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
