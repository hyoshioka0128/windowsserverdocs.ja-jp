---
title: ftp 追加
description: Ftp 追加の Windows コマンドに関するトピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 44ce1d6e7259dc8745da35ed462e6378f0fce8ba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843825"
---
# <a name="ftp-append"></a>ftp: 追加

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイルの種類の設定を使用して、リモートコンピューター上のファイルにローカルファイルを追加します。   
## <a name="syntax"></a>構文  
```  
append <LocalFile> [remoteFile]  
```  
#### <a name="parameters"></a>パラメーター  

|  パラメーター   |                               説明                                |
|--------------|--------------------------------------------------------------------------|
| <LocalFile>  |                     追加するローカルファイルを指定します。                     |
| RemoteFile | <LocalFile> を追加するリモートコンピューター上のファイルを指定します。 |

## <a name="remarks"></a>コメント  
*Remotefile*を省略した場合、リモートファイル名の代わりに*LocalFile*名が使用されます。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
リモートコンピューターの file2 に file1 を追加します。  
```  
append file1.txt file2.txt  
```  
リモートコンピューター上の file1 という名前のファイルに、ローカルの file1 を追加します。  
```  
append file1.txt  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
