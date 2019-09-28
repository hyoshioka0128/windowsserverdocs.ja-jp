---
title: ftp 追加
description: 'Ftp 追加の Windows コマンドに関するトピック '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 52d16b878ff5fb165fd851b227dcc361c9da3a80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376638"
---
# <a name="ftp-append"></a>ftp: 追加

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイルの種類の設定を使用して、リモートコンピューター上のファイルにローカルファイルを追加します。   
## <a name="syntax"></a>構文  
```  
append <LocalFile> [remoteFile]  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                               説明                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     追加するローカルファイルを指定します。                     |
| RemoteFile | @No__t-0 を追加するリモートコンピューター上のファイルを指定します。 |

## <a name="remarks"></a>コメント  
*Remotefile*を省略した場合、リモートファイル名の代わりに*LocalFile*名が使用されます。  
## <a name="BKMK_Examples"></a>例  
リモートコンピューターの file2 に file1 を追加します。  
```  
append file1.txt file2.txt  
```  
リモートコンピューター上の file1 という名前のファイルに、ローカルの file1 を追加します。  
```  
append file1.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
