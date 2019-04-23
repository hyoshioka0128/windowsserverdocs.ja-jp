---
title: ftp ディレクトリ
description: Ftp ディレクトリの Windows コマンド」のトピック
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 78ac8ac5e9fc4894f55401bb234aa98de981adf7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835253"
---
# <a name="ftp-dir"></a>ftp: dir

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューター上のディレクトリのファイルとサブディレクトリの一覧を表示します。   
## <a name="syntax"></a>構文  
```  
dir [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<remotedirectory>]|一覧を表示するディレクトリを指定します。 ディレクトリが指定されていない場合は、リモート コンピューター上の現在の作業ディレクトリが使用されます。|  
|[<LocalFile>]|ディレクトリの一覧を格納するローカル ファイルを指定します。 ローカル ファイルが指定されていない場合は、結果が画面に表示されます。|  
## <a name="BKMK_Examples"></a>例  
ディレクトリの一覧を表示**dir1**リモート コンピューター。  
```  
dir dir1  
```  
ローカル ファイルにリモート コンピューターで、現在のディレクトリの一覧を保存**dirlist.txt**します。  
```  
dir . dirlist.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
