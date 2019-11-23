---
title: repair
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 88293422519488405d94e32596c81dbe4a697dee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371530"
---
# <a name="repair"></a>repair

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

障害が発生したディスク領域を指定されたダイナミックディスクに交換することによって、フォーカスがある RAID\-5 ボリュームを修復します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                             説明                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| disk\=<n>  |                                                                 障害が発生したディスク領域を置き換えるダイナミックディスクを指定します。                                                                 |
| align\=<n> |          すべてのボリュームまたはパーティションエクステントを最も近いアラインメント境界に配置します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。           |
|   noerr    | スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>注釈  
  
-   指定されたダイナミックディスクには、RAID\-5 ボリュームの障害が発生したディスク領域の合計サイズ以上の空き領域が必要です。  
  
-   この操作を成功させるには、RAID\-5 アレイのボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
ダイナミックディスク4に置き換えることによって、フォーカスのあるボリュームを置き換えるには、次のように入力します。  
  
```  
repair disk=4  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

