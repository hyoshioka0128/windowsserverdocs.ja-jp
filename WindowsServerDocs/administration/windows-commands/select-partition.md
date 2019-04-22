---
title: パーティションを選択します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c7d5675aa6c33ddbe1e5e873e1a7cf7a2e8f8017
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824963"
---
# <a name="select-partition"></a>パーティションを選択します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したパーティションを選択し、それに、フォーカスを移動します。 このコマンドは、現在フォーカスが、選択したディスクのパーティションを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select partition=<n>  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|パーティション\=<n>|フォーカスを受け取るパーティションの数。 使用して現在選択されているディスク上のすべてのパーティションの番号を表示する、 **パーティションを一覧表示** diskpart コマンドです。|  
  
## <a name="remarks"></a>注釈  
  
-   使用して、ディスクを選択するパーティションを選択する前にまず必要があります、 **select ディスク** コマンドです。  
  
-   パーティションの数が指定されていない場合、このコマンドは、選択したディスクにフォーカスが置かれているパーティションを表示します。  
  
-   対応するパーティションを持つ、ボリュームを選択すると、パーティションが自動的に選択します。  
  
-   対応するボリュームにパーティションを選択すると、ボリュームが自動的に選択します。  
  
## <a name="BKMK_examples"></a>例  
フォーカスをパーティション 3 に、次のように入力します。  
  
```  
select partitition=3  
```  
  
現在フォーカスが、選択したディスクのパーティションを表示するには、次のように入力します。  
  
```  
select partition  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

