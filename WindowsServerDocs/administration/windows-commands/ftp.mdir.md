---
title: ftp mdir
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90eec45b-558b-4b8d-bbe4-b56d98e1ca70 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afb024d063761f1e817f02fdd7301376dd167846
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842715"
---
# <a name="ftp-mdir"></a>ftp: mdir

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。   
## <a name="syntax"></a>構文  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>パラメーター  

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
  ## <a name="examples"></a><a name=BKMK_Examples></a>例  
  画面に**dir1**と**dir2**のディレクトリ一覧を表示する  
  ```  
  mdir dir1 dir2 -  
  ```  
  **Dir1**と**dir2**の結合されたディレクトリの一覧を**dirlist .txt**という名前のローカルファイルに保存します。  
  ```  
  mdir dir1 dir2 dirlist.txt  
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
