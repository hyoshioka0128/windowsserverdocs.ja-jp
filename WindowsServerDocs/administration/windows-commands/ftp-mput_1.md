---
title: ftp mput_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6308f7b47d58bc25d964944f96fbc83a26350962
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376207"
---
# <a name="ftp-mput_1"></a>ftp: mput_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mput <LocalFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター  |                       説明                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | リモート コンピューターにコピーするローカル ファイルを指定します。 |

## <a name="BKMK_Examples"></a>例  
現在のファイル転送の種類を使用して、 **Program1**と**program2.c**をリモートコンピューターにコピーします。  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
