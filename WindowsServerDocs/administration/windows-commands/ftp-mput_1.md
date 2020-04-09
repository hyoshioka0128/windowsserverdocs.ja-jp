---
title: ftp mput_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 980f15e7-7cf1-4813-9946-a8cc4edfb198 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 489e18da937e12a1fc69e0ee84d9dda00309ccd6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843235"
---
# <a name="ftp-mput_1"></a>ftp: mput_1

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送の種類を現在のファイルを使用してリモート コンピューターにローカル ファイルをコピーします。   
## <a name="syntax"></a>構文  
```  
mput <LocalFile>[ ]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター  |                       説明                        |
|-------------|----------------------------------------------------------|
| <LocalFile> | リモート コンピューターにコピーするローカル ファイルを指定します。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例  
現在のファイル転送の種類を使用して、 **Program1**と**program2.c**をリモートコンピューターにコピーします。  
```  
mput Program1.exe Program2.exe  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
