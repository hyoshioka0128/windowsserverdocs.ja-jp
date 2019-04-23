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
ms.openlocfilehash: 3dca11f0d534eb875a71fa2c39cdd4dc674ad788
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862123"
---
# <a name="ftp-send1"></a>ftp: [send_1]

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
send <LocalFile> [<remoteFile>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<LocalFile>|コピーするローカル ファイルを指定します。|  
|<remoteFile>|リモート コンピューターで使用する名前を指定します。|  
## <a name="remarks"></a>注釈  
-   **送信**コマンドと同じ、**配置**コマンド。  
-   場合*remoteFile*が指定されていない、ファイルが指定された、*ローカルファイル*名。  
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
-   [コマンドライン構文キー](command-line-syntax-key.md)  
