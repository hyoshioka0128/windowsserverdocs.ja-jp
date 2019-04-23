---
title: ボリュームを属性します。
description: Windows コマンド」のトピック**属性ボリューム**-表示、設定、またはボリュームの属性をクリアします。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 37af55ee2a041fbcf8068e0def72147732d3a687
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846583"
---
# <a name="attributes-volume"></a>ボリュームを属性します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示、設定、またはボリュームの属性をクリアします。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
attributes volume [{set | clear}] [{hidden | readonly | nodefaultdriveletter | shadowcopy}] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|セット (set)|フォーカスがあるボリュームの指定した属性を設定します。|  
|クリア|フォーカスがあるボリュームの指定した属性をクリアします。|  
|読み取り専用|ボリュームが読み込まれることを指定します。\-のみです。|  
|非表示|ボリュームが非表示になっているを指定します。|  
|nodefaultdriveletter|ボリュームが既定でドライブ文字を受信しないことを指定します。|  
|シャドウ コピー|シャドウ コピー ボリュームにボリュームを指定します。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   ベーシック マスター ブート レコードに\(MBR\) 、ディスク、**隠し**、 **readonly**と**nodefaultdriveletter**パラメーターは、上のすべてのボリュームに適用されます。ディスク。  
  
-   ベーシック GUID パーティション テーブルで\(gpt\)ディスク、および動的 MBR と gpt ディスクでは、**隠し**、 **readonly**と**nodefaultdriveletter**パラメーターは、選択したボリュームにのみ適用されます。  
  
-   ボリュームを選択する必要があります、**ボリュームを属性**コマンドは成功します。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
を、選択したボリューム上の現在の属性を表示するには、次のように入力します。  
  
```  
attributes volume  
```  
  
非表示と読み取りとして、選択したボリュームを設定する\-のみを入力します。  
  
```  
attributes volume set hidden readonly  
```  
  
非表示と読み取りを削除する\-、選択されたボリューム上の属性のみを入力します。  
  
```  
attributes volume clear hidden readonly  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

