---
title: ftp ls_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6abf8466f90ac29846f2e1ee7d305e7e4280231e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438630"
---
# <a name="ftp-ls1"></a>ftp: ls_1

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
> 
> 
> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイルと、リモート コンピューターからのサブディレクトリの省略版リストを表示します。   
## <a name="syntax"></a>構文  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  

|      パラメーター      |                                                                       説明                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | 一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモート コンピューター上の現在の作業ディレクトリが使用されます。 |
|    [<LocalFile>]    |               一覧を格納するローカル ファイルを指定します。 ローカル ファイルが指定されていない場合は、結果が画面に表示されます。               |

## <a name="BKMK_Examples"></a>例  
ファイルと、リモート コンピューターからのサブディレクトリの省略版リストを表示します。  
```  
ls  
```  
ディレクトリの省略形にリスト**dir1**と呼ばれるリモート コンピューターとローカル ファイルに保存**dirlist.txt**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
