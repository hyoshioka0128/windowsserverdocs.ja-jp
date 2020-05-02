---
title: ftp ディレクトリ
description: Ftp ディレクトリのリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f2b9c610abe50bf662439a84d9bcbcb17b1a5bb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725313"
---
# <a name="ftp-dir"></a>ftp: ディレクトリ

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のディレクトリファイルとサブディレクトリの一覧を表示します。   
## <a name="syntax"></a>構文  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|[説明]|  
|-------|--------|  
|[<remotedirectory>]|一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモートコンピューター上の現在の作業ディレクトリが使用されます。|  
|[<LocalFile>]|ディレクトリの一覧を格納するローカルファイルを指定します。 ローカルファイルが指定されていない場合、結果は画面に表示されます。|  
## <a name="examples"></a>例  
リモートコンピューター上の**dir1**のディレクトリ一覧を表示します。  
```  
dir dir1  
```  
リモートコンピューター上の現在のディレクトリの一覧をローカルファイル**dirlist .txt**に保存します。  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
