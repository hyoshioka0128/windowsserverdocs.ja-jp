---
title: ヘルプ
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 29ec2da9d383985d62931ce1cee9bd4a83a0fb1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869593"
---
# <a name="help"></a>ヘルプ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したコマンドで使用可能なコマンドや詳細なヘルプ情報の一覧を表示します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
help [<command>]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|<command>|詳細なヘルプ情報を表示するためのコマンドを指定します。|  
  
## <a name="remarks"></a>注釈  
  
-   コマンドが指定されていない場合**ヘルプ**可能なすべてのコマンドが表示されます。  
  
## <a name="BKMK_examples"></a>例  
DiskPart で使用できるすべてのコマンドの一覧を表示するには、次のように入力します。  
  
```  
help  
```  
  
使用する方法についての詳細なヘルプ情報を表示する、**プライマリ パーティションを作成**型である DiskPart コマンドです。  
  
```  
help create partition primary  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

