---
title: ftp open_1
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15a27d2f7512da352a0f4ddf02fa2511ffce7c1d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725193"
---
# <a name="ftp-open_1"></a>ftp: open_1

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された ftp サーバーに接続します。   
## <a name="syntax"></a>構文  
```  
open <computer> [<Port>]  
```  
#### <a name="parameters"></a>パラメーター  

| パラメーター  |                                           [説明]                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                接続を試みているリモート コンピューターを指定します。                 |
|  [<Port>]  | Ftp サーバーへの接続に使用する TCP ポート番号を指定します。 既定では、TCP ポート 21 を使用します。 |

## <a name="remarks"></a>Remarks  
**コンピューター**を指定するには、IP アドレスまたはコンピューター名 (その場合は、DNS サーバーまたはホストファイルを使用できる必要があります) を使用できます。  
## <a name="examples"></a>例  
**Ftp.microsoft.com**で ftp サーバーに接続します。  
```  
Open ftp.microsoft.com  
```  
TCP ポート755でリッスンしている**ftp.microsoft.com**で ftp サーバーに接続します。  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
