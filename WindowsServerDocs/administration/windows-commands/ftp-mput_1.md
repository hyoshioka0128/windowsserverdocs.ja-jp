---
title: ftp mput_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: dd19a97246aa6155182cb055deceb4b5a5019f6c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438581"
---
# <a name="ftp-mput1"></a>ftp: mput_1

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
コピー **Program1.exe**と**Program2.exe**現在のファイル転送の種類を使用してリモート コンピューターにします。  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>その他の参照  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
