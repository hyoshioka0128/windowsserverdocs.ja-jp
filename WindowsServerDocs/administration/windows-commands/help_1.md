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
ms.openlocfilehash: 078c779e7813d2aa7499e515d9729edf92452237
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438202"
---
# <a name="help"></a>ヘルプ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したコマンドで使用可能なコマンドや詳細なヘルプ情報の一覧を表示します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
help [<command>]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター |                              説明                              |
|-----------|-----------------------------------------------------------------------|
| <command> | 詳細なヘルプ情報を表示するためのコマンドを指定します。 |
  
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
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

