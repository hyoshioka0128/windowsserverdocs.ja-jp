---
title: ftp mget
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c85ae96-ec51-48a9-a227-7f02c7332c69 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 666025c92b6fb1a612cbe7b83833557a8a7d5017
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376301"
---
# <a name="ftp-mget"></a>ftp: mget

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してローカル コンピューターにリモート ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mget <remoteFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                        説明                        |
|--------------|-----------------------------------------------------------|
| <remoteFile> | ローカル コンピューターにコピーするリモート ファイルを指定します。 |

## <a name="BKMK_Examples"></a>例  
現在のファイル転送の種類を使用して、リモートファイル**を**ローカル**コンピューターにコピーします。**  
```  
mget a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
