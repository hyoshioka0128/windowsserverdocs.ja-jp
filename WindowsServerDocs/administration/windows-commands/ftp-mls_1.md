---
title: ftp mls_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca3b8e04dd4a152b2d1bf8ce1ca8006d70186116
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843295"
---
# <a name="ftp-mls_1"></a>ftp: mls_1

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリにファイルとサブディレクトリの省略版リストを表示します。   
## <a name="syntax"></a>構文  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                       説明                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | 一覧を表示するファイルを指定します。 |
| <LocalFile>  |  一覧を格納するローカル ファイルを指定します。  |

## <a name="remarks"></a>コメント  
- *Remotefiles*の指定  
  リモートコンピューター上の現在の作業ディレクトリを使用するには、ハイフン ( **-** ) を入力します。  
- 指定する *転送しています*  
  画面に一覧を表示するには、ハイフン ( **-** ) を入力します。  
  ## <a name="examples"></a><a name=BKMK_Examples></a>例  
  **Dir1**と**dir2**のファイルとサブディレクトリの省略形の一覧を表示します。  
  ```  
  mls dir1 dir2 -  
  ```  
  **Dir1**と**dir2**のファイルとサブディレクトリの省略された一覧をローカルファイルの**dirlist .txt**に保存します。  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>その他の参照情報  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
