---
title: ftp get
description: Ftp get の Windows コマンドに関するトピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c0b4dc41ec29edfb94661176a5ccaf651584fc43
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843485"
---
# <a name="ftp-get"></a>ftp: get

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、リモートファイルをローカルコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
get <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|   パラメーター   |                                                              説明                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   コピーするリモートファイルを指定します。                                                   |
| [<LocalFile>] | ローカルコンピューターで使用するファイルの名前を指定します。 *LocalFile*が指定されていない場合、ファイルには*remotefile*という名前が付けられます。 |

## <a name="remarks"></a>コメント  
**Get**コマンドは、 **recv**コマンドと同じです。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
現在のファイル転送の種類を使用して、ローカルコンピューターに**test.txt**をコピーします。  
```  
get test.txt  
```  
現在のファイル転送の種類を使用して、 **test.txt**をローカルコンピューターに**test.txt**としてコピーします。  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
