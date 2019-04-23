---
title: ftp open_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: da7926914e2cbdbb4909093d90c33025ae5cd695
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882473"
---
# <a name="ftp-open1"></a>ftp: open_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された ftp サーバーに接続します。   
## <a name="syntax"></a>構文  
```  
open <computer> [<Port>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<computer>|接続を試みているリモート コンピューターを指定します。|  
|[<Port>]|Ftp サーバーへの接続に使用する TCP ポート番号を指定します。 既定では、TCP ポート 21 を使用します。|  
## <a name="remarks"></a>注釈  
(この場合、DNS サーバーまたはホスト ファイルがあります)、IP アドレスまたはコンピューター名を使用して、**コンピューター**します。  
## <a name="BKMK_Examples"></a>例  
Ftp サーバーに接続**専用**します。  
```  
Open ftp.microsoft.com  
```  
Ftp サーバーに接続**専用**755 の TCP ポートでリッスンします。  
```  
open ftp.microsoft.com 755  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
