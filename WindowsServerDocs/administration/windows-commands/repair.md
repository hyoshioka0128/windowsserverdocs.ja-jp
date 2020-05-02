---
title: 修復
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89c09608e64b408db9c7c79269046195e005c187
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722391"
---
# <a name="repair"></a>修復

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

障害が発生\-したディスク領域を指定されたダイナミックディスクに交換することで、フォーカスのある RAID 5 ボリュームを修復します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                             [説明]                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ディスク\=<n>  |                                                                 障害が発生したディスク領域を置き換えるダイナミックディスクを指定します。                                                                 |
| 位置\=<n> |          すべてのボリュームまたはパーティションエクステントを最も近いアラインメント境界に配置します。 *n*は、ディスクの先頭\(から\)最も近いアラインメント境界までのキロバイト kb 数です。           |
|   noerr    | スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>Remarks  
  
-   指定されたダイナミックディスクには、RAID\-5 ボリューム内の障害が発生したディスク領域の合計サイズ以上の空き領域が必要です。  
  
-   この操作を成功さ\-せるには、RAID 5 アレイのボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="examples"></a>例  
ダイナミックディスク4に置き換えることによって、フォーカスのあるボリュームを置き換えるには、次のように入力します。  
  
```  
repair disk=4  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

