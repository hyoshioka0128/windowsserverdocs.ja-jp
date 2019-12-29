---
title: ヘルプ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3d76a71ec287e5c874ae3e4dec34016c5c80336
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375580"
---
# <a name="help"></a>ヘルプ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用可能なコマンドの一覧、または指定したコマンドの詳細なヘルプ情報を表示します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
help [<command>]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター |                              説明                              |
|-----------|-----------------------------------------------------------------------|
| <command> | 詳細なヘルプ情報を表示するコマンドを指定します。 |
  
## <a name="remarks"></a>コメント  
  
-   コマンドが指定されていない場合、**ヘルプ**には使用可能なすべてのコマンドが表示されます。  
  
## <a name="BKMK_examples"></a>例  
DiskPart で使用可能なすべてのコマンドの一覧を表示するには、次のように入力します。  
  
```  
help  
```  
  
DiskPart で**create partition primary**コマンドを使用する方法に関する詳細なヘルプ情報を表示するには、次のように入力します。  
  
```  
help create partition primary  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

