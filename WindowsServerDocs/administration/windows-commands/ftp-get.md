---
title: ftp get
description: Ftp get のリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 37423f81fd72e79cebcdf169160ad3e8033b69b2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725296"
---
# <a name="ftp-get"></a>ftp: get

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル転送の種類を使用して、リモートファイルをローカルコンピューターにコピーします。   
## <a name="syntax"></a>構文  
```  
get <remoteFile> [<LocalFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|   パラメーター   |                                                              [説明]                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   コピーするリモートファイルを指定します。                                                   |
| [<LocalFile>] | ローカルコンピューターで使用するファイルの名前を指定します。 *LocalFile*が指定されていない場合、ファイルには*remotefile*という名前が付けられます。 |

## <a name="remarks"></a>Remarks  
**Get**コマンドは、 **recv**コマンドと同じです。  
## <a name="examples"></a>例  
現在のファイル転送の種類を使用して、ローカルコンピューターに**test.txt**をコピーします。  
```  
get test.txt  
```  
現在のファイル転送の種類を使用して、 **test.txt**をローカルコンピューターに**test.txt**としてコピーします。  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: バイナリ](ftp-binary.md)  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
