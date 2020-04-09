---
title: ヘルプ
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 404cefe879e8f63678f2cba90516fad9c216eb23
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842315"
---
# <a name="help"></a>ヘルプ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用可能なコマンドの一覧、または指定したコマンドの詳細なヘルプ情報を表示します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
help [<command>]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター |                              説明                              |
|-----------|-----------------------------------------------------------------------|
| <command> | 詳細なヘルプ情報を表示するコマンドを指定します。 |
  
## <a name="remarks"></a>コメント  
  
-   コマンドが指定されていない場合、**ヘルプ**には使用可能なすべてのコマンドが表示されます。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
DiskPart で使用可能なすべてのコマンドの一覧を表示するには、次のように入力します。  
  
```  
help  
```  
  
DiskPart で**create partition primary**コマンドを使用する方法に関する詳細なヘルプ情報を表示するには、次のように入力します。  
  
```  
help create partition primary  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

