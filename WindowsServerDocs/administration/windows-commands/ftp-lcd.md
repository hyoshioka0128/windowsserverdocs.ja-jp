---
title: lcd を ftp します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: eac028c8aa675e680dedefcfe9f0b8da18ce7179
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826893"
---
# <a name="ftp-lcd"></a>ftp: lcd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカル コンピューター上の作業ディレクトリを変更します。 既定では、作業ディレクトリには、ディレクトリを**ftp**開始されました。   
## <a name="syntax"></a>構文  
```  
lcd [<directory>]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<directory>]|変更をローカル コンピューター上のディレクトリを指定します。 場合*ディレクトリ*が指定されていない、現在の作業ディレクトリが既定のディレクトリに変更されます。|  
## <a name="BKMK_Examples"></a>例  
ローカル コンピューター上の作業ディレクトリを変更する**C:\dir1**  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
