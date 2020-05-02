---
title: ftp 追加
description: Ftp 追加のリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53228473b8ea16a0955c244d60fae77cf4f7d7f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725399"
---
# <a name="ftp-append"></a>ftp: 追加

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイルの種類の設定を使用して、リモートコンピューター上のファイルにローカルファイルを追加します。   
## <a name="syntax"></a>構文  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                               [説明]                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     追加するローカルファイルを指定します。                     |
| RemoteFile | を追加する<LocalFile>リモートコンピューター上のファイルを指定します。 |

## <a name="remarks"></a>Remarks  
*Remotefile*を省略した場合、リモートファイル名の代わりに*LocalFile*名が使用されます。  
## <a name="examples"></a>例  
リモートコンピューターの file2 に file1 を追加します。  
```  
append file1.txt file2.txt  
```  
リモートコンピューター上の file1 という名前のファイルに、ローカルの file1 を追加します。  
```  
append file1.txt  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
