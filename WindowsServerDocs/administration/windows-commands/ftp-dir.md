---
title: ftp ディレクトリ
description: Ftp ディレクトリの Windows コマンドに関するトピック
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a29a92a5-7b79-4e6e-95cf-2ccb38bb6fb2 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c47971c52135d79ce62f935bfed981f6eefcecaa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376443"
---
# <a name="ftp-dir"></a>ftp: ディレクトリ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のディレクトリファイルとサブディレクトリの一覧を表示します。   
## <a name="syntax"></a>構文  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<remotedirectory>]|一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモートコンピューター上の現在の作業ディレクトリが使用されます。|  
|[<LocalFile>]|ディレクトリの一覧を格納するローカルファイルを指定します。 ローカルファイルが指定されていない場合、結果は画面に表示されます。|  
## <a name="BKMK_Examples"></a>例  
リモートコンピューター上の**dir1**のディレクトリ一覧を表示します。  
```  
dir dir1  
```  
リモートコンピューター上の現在のディレクトリの一覧をローカルファイル**dirlist .txt**に保存します。  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
