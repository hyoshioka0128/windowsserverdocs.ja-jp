---
title: ftp mls_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4738fd49-0e80-4bdf-a773-0f973db3a710 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6cf81018fa590d38e55778d60b0cb0e849ab83de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835703"
---
# <a name="ftp-mls1"></a>ftp: mls_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリにファイルとサブディレクトリの省略版リストを表示します。   
## <a name="syntax"></a>構文  
```  
mls <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<remoteFile>|一覧を表示するファイルを指定します。|  
|<LocalFile>|一覧を格納するローカル ファイルを指定します。|  
## <a name="remarks"></a>注釈  
-   指定する*remoteFiles*  
    ハイフンを入力 (**-**)、リモート コンピューター上の現在の作業ディレクトリを使用します。  
-   指定する *転送しています*  
    ハイフンを入力 (**-**) 画面の一覧を表示します。  
## <a name="BKMK_Examples"></a>例  
ファイルとサブディレクトリの省略版リストを表示**dir1**と**ディレクトリ 2**します。  
```  
mls dir1 dir2 -  
```  
ファイルとサブディレクトリの省略版リストを保存**dir1**と**ディレクトリ 2**ローカル ファイルに**dirlist.txt**  
```  
mls dir1 dir2 dirlist.txt   
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
