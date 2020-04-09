---
title: ftp open_1
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8bd3063a52908d65f336afcda6b6982d5bc9bf94
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843185"
---
# <a name="ftp-open_1"></a>ftp: open_1

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された ftp サーバーに接続します。   
## <a name="syntax"></a>構文  
```  
open <computer> [<Port>]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                                           説明                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                接続を試みているリモート コンピューターを指定します。                 |
|  [<Port>]  | Ftp サーバーへの接続に使用する TCP ポート番号を指定します。 既定では、TCP ポート 21 を使用します。 |

## <a name="remarks"></a>コメント  
**コンピューター**を指定するには、IP アドレスまたはコンピューター名 (その場合は、DNS サーバーまたはホストファイルを使用できる必要があります) を使用できます。  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
**Ftp.microsoft.com**で ftp サーバーに接続します。  
```  
Open ftp.microsoft.com  
```  
TCP ポート755でリッスンしている**ftp.microsoft.com**で ftp サーバーに接続します。  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
