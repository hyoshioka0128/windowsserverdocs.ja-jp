---
title: ftp mdir
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0ac1e7cd50fe4d9325c272f74a7b81971c8bb12a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878213"
---
# <a name="ftp-mdir"></a>ftp: mdir

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。   
## <a name="syntax"></a>構文  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<remoteFile>|一覧を表示するディレクトリまたはファイルを指定します。|  
|<LocalFile>|一覧を格納するローカル ファイルを指定します。 このパラメーターは必須です。|  
## <a name="remarks"></a>注釈  
-   使用することができます**mdir**を複数のファイルを指定します。  
-   指定する*remoteFile*  
    ハイフンを入力 (**-**)、リモート コンピューター上の現在の作業ディレクトリを使用します。  
-   指定する、*ローカルファイル*  
    ハイフンを入力 (**-**) 画面の一覧を表示します。  
## <a name="BKMK_Examples"></a>例  
ディレクトリの一覧を表示**dir1**と**ディレクトリ 2**画面  
```  
mdir dir1 dir2 -  
```  
結合されたディレクトリの一覧を保存**dir1**と**ディレクトリ 2**ローカル ファイルと呼ばれる**dirlist.txt**  
```  
mdir dir1 dir2 dirlist.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
