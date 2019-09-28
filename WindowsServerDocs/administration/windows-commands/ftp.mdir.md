---
title: ftp mdir
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08aa5bb216a3d0155c100c761e476bb963e59311
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375848"
---
# <a name="ftp-mdir"></a>ftp: mdir

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。   
## <a name="syntax"></a>構文  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                               説明                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   一覧を表示するディレクトリまたはファイルを指定します。   |
| <LocalFile>  | 一覧を格納するローカルファイルを指定します。 このパラメーターは必須です。 |

## <a name="remarks"></a>コメント  
- **Mdir**を使用して、複数のファイルを指定できます。  
- 指定 ( *Remotefile*を)  
  リモートコンピューター上の現在の作業ディレクトリを使用するには、ハイフン ( **-** ) を入力します。  
- *LocalFile*の指定  
  画面に一覧を表示するには、ハイフン ( **-** ) を入力します。  
  ## <a name="BKMK_Examples"></a>例  
  画面に**dir1**と**dir2**のディレクトリ一覧を表示する  
  ```  
  mdir dir1 dir2 -  
  ```  
  **Dir1**と**dir2**の結合されたディレクトリの一覧を**dirlist .txt**という名前のローカルファイルに保存します。  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
