---
title: ftp ls_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0dd661742288bdd43299f379f4eb04016b2ac799
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725241"
---
# <a name="ftp-ls_1"></a>ftp: ls_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
> 
> 
> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューターのファイルとサブディレクトリの省略形の一覧を表示します。   
## <a name="syntax"></a>構文  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
#### <a name="parameters"></a>パラメーター  

|      パラメーター      |                                                                       [説明]                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | 一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモートコンピューター上の現在の作業ディレクトリが使用されます。 |
|    [<LocalFile>]    |               一覧を格納するローカル ファイルを指定します。 ローカルファイルが指定されていない場合、結果は画面に表示されます。               |

## <a name="examples"></a>例  
リモートコンピューターのファイルとサブディレクトリの省略形の一覧を表示します。  
```  
ls  
```  
リモートコンピューター上の**dir1**の省略形のディレクトリ一覧を取得し、dirlist という名前のローカルファイルに保存し**ます。**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
