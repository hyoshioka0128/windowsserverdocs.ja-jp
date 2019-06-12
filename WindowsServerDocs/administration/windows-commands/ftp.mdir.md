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
ms.openlocfilehash: c4ec445c3e367a46dc40d10a37c0b3b8e53a10e3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438330"
---
# <a name="ftp-mdir"></a>ftp: mdir

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート ディレクトリ内のファイルとサブディレクトリのディレクトリ一覧を表示します。   
## <a name="syntax"></a>構文  
```  
mdir <remoteFile>[ ] <LocalFile>  
```  
### <a name="parameters"></a>パラメーター  

|  パラメーター   |                               説明                                |
|--------------|--------------------------------------------------------------------------|
| <remoteFile> |   一覧を表示するディレクトリまたはファイルを指定します。   |
| <LocalFile>  | 一覧を格納するローカル ファイルを指定します。 このパラメーターは必須です。 |

## <a name="remarks"></a>注釈  
- 使用することができます**mdir**を複数のファイルを指定します。  
- 指定する*remoteFile*  
  ハイフンを入力 ( **-** )、リモート コンピューター上の現在の作業ディレクトリを使用します。  
- 指定する、*ローカルファイル*  
  ハイフンを入力 ( **-** ) 画面の一覧を表示します。  
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
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
