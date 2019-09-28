---
title: パーティションの選択
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9a186e2678fde64396a8b4b57a2d14e4b0b7bf26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371068"
---
# <a name="select-partition"></a>パーティションの選択

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたパーティションを選択し、そのパーティションにフォーカスを移動します。 このコマンドは、現在フォーカスが、選択したディスクのパーティションを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select partition=<n>  
```  
  
## <a name="parameters"></a>パラメーター  
  
|   パラメーター    |                                                                                    説明                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| パーティション @ no__t-0 @ no__t-1 | フォーカスを受け取るパーティションの数。 使用して現在選択されているディスク上のすべてのパーティションの番号を表示する、 **パーティションを一覧表示** diskpart コマンドです。 |
  
## <a name="remarks"></a>コメント  
  
-   使用して、ディスクを選択するパーティションを選択する前にまず必要があります、 **select ディスク** コマンドです。  
  
-   パーティション番号が指定されていない場合、このコマンドは、現在選択されているディスクにフォーカスがあるパーティションを表示します。  
  
-   ボリュームに対応するパーティションが選択されている場合は、パーティションが自動的に選択されます。  
  
-   対応するボリュームを持つパーティションを選択すると、ボリュームが自動的に選択されます。  
  
## <a name="BKMK_examples"></a>例  
フォーカスをパーティション 3 に、次のように入力します。  
  
```  
select partitition=3  
```  
  
現在フォーカスが、選択したディスクのパーティションを表示するには、次のように入力します。  
  
```  
select partition  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

