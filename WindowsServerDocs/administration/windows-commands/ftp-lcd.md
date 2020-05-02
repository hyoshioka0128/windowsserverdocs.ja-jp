---
title: ftp lcd
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60a25808-6abb-408b-8373-0bbdcd0994b4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 646cbfe3feadb63388694218758dae165ffb49c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725263"
---
# <a name="ftp-lcd"></a>ftp: lcd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカルコンピューター上の作業ディレクトリを変更します。 既定では、作業ディレクトリは**ftp**が開始されたディレクトリです。   
## <a name="syntax"></a>構文  
```  
lcd [<directory>]  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|[説明]|  
|-------|--------|  
|[<directory>]|変更するローカルコンピューター上のディレクトリを指定します。 *Directory*が指定されていない場合は、現在の作業ディレクトリが既定のディレクトリに変更されます。|  
## <a name="examples"></a>例  
ローカルコンピューター上の作業ディレクトリを**C:\ dir1**に変更します。  
```  
lcd C:\dir1  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
