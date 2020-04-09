---
title: ftp lcd
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d7e2e6fc9f6af7655381bfb802dc190e79365bd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80843405"
---
# <a name="ftp-lcd"></a>ftp: lcd

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルコンピューター上の作業ディレクトリを変更します。 既定では、作業ディレクトリは**ftp**が開始されたディレクトリです。   
## <a name="syntax"></a>構文  
```  
lcd [<directory>]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|[<directory>]|変更するローカルコンピューター上のディレクトリを指定します。 *Directory*が指定されていない場合は、現在の作業ディレクトリが既定のディレクトリに変更されます。|  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
ローカルコンピューター上の作業ディレクトリを**C:\ dir1**に変更します。  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>その他の参照情報  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
