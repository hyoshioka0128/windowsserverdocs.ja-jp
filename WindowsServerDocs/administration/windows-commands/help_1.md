---
title: help
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6887edfd41895bb151c5aaebb88d8b72198f4dbf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724906"
---
# <a name="help"></a>help

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用可能なコマンドの一覧、または指定したコマンドの詳細なヘルプ情報を表示します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
help [<command>]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター |                              [説明]                              |
|-----------|-----------------------------------------------------------------------|
| <command> | 詳細なヘルプ情報を表示するコマンドを指定します。 |
  
## <a name="remarks"></a>Remarks  
  
-   コマンドが指定されていない場合、**ヘルプ**には使用可能なすべてのコマンドが表示されます。  
  
## <a name="examples"></a>例  
DiskPart で使用可能なすべてのコマンドの一覧を表示するには、次のように入力します。  
  
```  
help  
```  
  
DiskPart で**create partition primary**コマンドを使用する方法に関する詳細なヘルプ情報を表示するには、次のように入力します。  
  
```  
help create partition primary  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

