---
title: ftp mls_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27f74d4c1d03cb4d9f665566f69485e80f8eccdc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725208"
---
# <a name="ftp-mls_1"></a>ftp: mls_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリにファイルとサブディレクトリの省略版リストを表示します。   
## <a name="syntax"></a>構文  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                       [説明]                       |
|--------------|---------------------------------------------------------|
| <remoteFile> | 一覧を表示するファイルを指定します。 |
| <LocalFile>  |  一覧を格納するローカル ファイルを指定します。  |

## <a name="remarks"></a>Remarks  
- *Remotefiles*の指定  
  リモートコンピューター上の**-** 現在の作業ディレクトリを使用するには、ハイフン () を入力します。  
- 指定する *転送しています*  
  画面に一覧を**-** 表示するには、ハイフン () を入力します。  
  ## <a name="examples"></a>例  
  **Dir1**と**dir2**のファイルとサブディレクトリの省略形の一覧を表示します。  
  ```  
  mls dir1 dir2 -  
  ```  
  **Dir1**と**dir2**のファイルとサブディレクトリの省略された一覧をローカルファイルの**dirlist .txt**に保存します。  
  ```  
  mls dir1 dir2 dirlist.txt   
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
- - [コマンド ライン構文の記号](command-line-syntax-key.md)  
