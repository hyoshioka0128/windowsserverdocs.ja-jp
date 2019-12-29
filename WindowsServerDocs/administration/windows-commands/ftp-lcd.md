---
title: ftp lcd
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47058cc62e4e87d1fcd951ec3b4a7885eeef2ae2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376310"
---
# <a name="ftp-lcd"></a>ftp: lcd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルコンピューター上の作業ディレクトリを変更します。 既定では、作業ディレクトリは**ftp**が開始されたディレクトリです。   
## <a name="syntax"></a>構文  
```  
lcd [<directory>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<directory>]|変更するローカルコンピューター上のディレクトリを指定します。 *Directory*が指定されていない場合は、現在の作業ディレクトリが既定のディレクトリに変更されます。|  
## <a name="BKMK_Examples"></a>例  
ローカルコンピューター上の作業ディレクトリを**C:\ dir1**に変更します。  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
