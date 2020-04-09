---
title: ftp mget
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72b45f84622fcd6abf7a743f606fb514def584cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843355"
---
# <a name="ftp-mget"></a>ftp: mget

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mget <remoteFile>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                        説明                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | ローカル コンピューターにコピーするリモート ファイルを指定します。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例  
現在のファイル転送の種類を使用して、リモートファイル**を**ローカル**コンピューターにコピーします。**  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
