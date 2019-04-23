---
title: ftp を追加します。
description: 'Ftp の Windows コマンド」のトピックを追加します。 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 23fa04b86d9c26fb30b74eebe8caef8498b90a12
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879033"
---
# <a name="ftp-append"></a>ftp: 追加

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイル種類の設定を使用してリモート コンピューター上のファイルをローカル ファイルを追加します。   
## <a name="syntax"></a>構文  
```  
append <LocalFile> [remoteFile]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<LocalFile>|追加するローカル ファイルを指定します。|  
|[remoteFile]|リモート コンピューターにファイルを指定します<LocalFile>が追加されます。|  
## <a name="remarks"></a>注釈  
場合*remoteFile*を省略すると、*ローカルファイル*名前は、リモート ファイル名の代わりに使用されます。  
## <a name="BKMK_Examples"></a>例  
file1.txt を file2.txt、リモート コンピューター上に追加します。  
```  
append file1.txt file2.txt  
```  
ローカル file1.txt をリモート コンピューター上の file1.txt という名前のファイルに追加します。  
```  
append file1.txt  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
