---
title: ftp の削除
description: Ftp delete の Windows コマンドに関するトピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 067c45f3-e4e8-4450-b8b6-836994f6adfe vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4683e63700a22d8ac8016fb118475a341221e7f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843565"
---
# <a name="ftp-delete"></a>ftp: 削除

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートコンピューター上のファイルを削除します。   
## <a name="syntax"></a>構文  
```  
delete <remoteFile>  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |          説明          |
|--------------|-------------------------------|
| <remoteFile> | 削除するファイルを指定します。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモートコンピューター上のファイル test.txt を削除します。  
```  
delete test.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
