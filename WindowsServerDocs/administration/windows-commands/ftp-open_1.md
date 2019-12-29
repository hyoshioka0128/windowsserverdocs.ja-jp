---
title: ftp open_1
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b61926a-dc60-4b4c-96d3-64e5c91c18ba vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c5da1c73362c0396300f712b2e45b906d1652604
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376188"
---
# <a name="ftp-open_1"></a>ftp: open_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された ftp サーバーに接続します。   
## <a name="syntax"></a>構文  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>パラメーター  

| パラメーター  |                                           説明                                            |
|------------|--------------------------------------------------------------------------------------------------|
| <computer> |                接続を試みているリモート コンピューターを指定します。                 |
|  [<Port>]  | Ftp サーバーへの接続に使用する TCP ポート番号を指定します。 既定では、TCP ポート 21 を使用します。 |

## <a name="remarks"></a>コメント  
**コンピューター**を指定するには、IP アドレスまたはコンピューター名 (その場合は、DNS サーバーまたはホストファイルを使用できる必要があります) を使用できます。  
## <a name="BKMK_Examples"></a>例  
**Ftp.microsoft.com**で ftp サーバーに接続します。  
```  
Open ftp.microsoft.com  
```  
TCP ポート755でリッスンしている**ftp.microsoft.com**で ftp サーバーに接続します。  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
