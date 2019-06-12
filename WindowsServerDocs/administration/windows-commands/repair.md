---
title: 修復
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1e4b9cde10e11558aaa95edda94921144dac1f86
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441802"
---
# <a name="repair"></a>修復

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

修復、RAID\-指定されたダイナミック ディスクで障害が発生したディスク領域を置き換えることで、フォーカスのある 5 つのボリューム。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
repair disk=<n> [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                             説明                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ディスク\=<n>  |                                                                 失敗したディスク領域を置き換えるダイナミック ディスクを指定します。                                                                 |
| 配置\=<n> |          すべてのボリュームまたはパーティション範囲近いシリンダー境界に揃えて配置します。 *n*キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。           |
|   noerr    | スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>注釈  
  
-   指定されたダイナミック ディスクは、raid のディスク領域の合計サイズ以上の空き領域が必要\-5 ボリューム。  
  
-   Raid ボリューム\-を成功させるのには、この操作の 5 つの配列を選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
ボリュームをダイナミック ディスク 4 を置き換えることによりフォーカスに置き換えて、次のように入力します。  
  
```  
repair disk=4  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

