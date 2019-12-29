---
title: 属性のボリューム
description: '**Attributes volume**の Windows コマンドのトピック-ボリュームの属性を表示、設定、またはクリアします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e40e8284-3d57-4de8-a46c-e4ade34a0d53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 225a10307123763d1a024fcc08fbae536fd0b5df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382584"
---
# <a name="attributes-volume"></a>属性のボリューム

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ボリュームの属性を表示、設定、またはクリアします。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|set|フォーカスがあるボリュームの指定された属性を設定します。|  
|clear|フォーカスがあるボリュームの指定された属性をクリアします。|  
|readonly|ボリュームが読み取り専用\-ことを指定します。|  
|表示|ボリュームが非表示であることを指定します。|  
|nodefaultdriveletter|既定では、ボリュームがドライブ文字を受け取らないことを指定します。|  
|コピー|ボリュームがシャドウコピーボリュームであることを指定します。|  
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   ベーシックマスタブートレコード \(MBR\) disks では、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメータがディスク上のすべてのボリュームに適用されます。  
  
-   基本的な GUID パーティションテーブル \(gpt\) ディスク、動的 MBR および gpt ディスクでは、 **hidden**、 **readonly**、および**nodefaultdriveletter**各パラメーターは、選択したボリュームにのみ適用されます。  
  
-   **属性 volume**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
選択したボリュームの現在の属性を表示するには、次のように入力します。  
  
```  
attributes volume  
```  
  
選択したボリュームを非表示として設定し、読み取り\-のみにするには、次のように入力します。  
  
```  
attributes volume set hidden readonly  
```  
  
選択したボリュームの hidden 属性と read\-属性のみを削除するには、次のように入力します。  
  
```  
attributes volume clear hidden readonly  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

