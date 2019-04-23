---
title: ftp mdelete_1
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a80a8f5-e880-40a8-abc9-29a41836844f vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9390f8e5b0bded92a553b3057d122dace3fc665a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851613"
---
# <a name="ftp-mdelete1"></a>ftp: mdelete_1

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート コンピューター上のファイルを削除します。   
## <a name="syntax"></a>構文  
```  
mdelete <remoteFile>[ ]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|<remoteFile>|削除するリモート ファイルを指定します。|  
## <a name="BKMK_Examples"></a>例  
リモート ファイルの削除**a.exe**と**b.exe**します。  
```  
mdelete a.exe b.exe  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
