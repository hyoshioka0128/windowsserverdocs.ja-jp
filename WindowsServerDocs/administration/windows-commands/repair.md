---
title: repair
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46b98938394c10e31d4999ff0e060e10f7da9bdc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835935"
---
# <a name="repair"></a>repair

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

障害が発生したディスク領域を指定されたダイナミックディスクに交換することによって、フォーカスがある RAID\-5 ボリュームを修復します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                             説明                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ディスク\=<n>  |                                                                 障害が発生したディスク領域を置き換えるダイナミックディスクを指定します。                                                                 |
| \=<n> に揃える |          すべてのボリュームまたはパーティションエクステントを最も近いアラインメント境界に配置します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。           |
|   noerr    | スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>コメント  
  
-   指定されたダイナミックディスクには、RAID\-5 ボリュームの障害が発生したディスク領域の合計サイズ以上の空き領域が必要です。  
  
-   この操作を成功させるには、RAID\-5 アレイのボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
ダイナミックディスク4に置き換えることによって、フォーカスのあるボリュームを置き換えるには、次のように入力します。  
  
```  
repair disk=4  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

