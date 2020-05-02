---
title: select partition
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55b06f247c8e9f183a2971278a8f16ac237e9cfe
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722012"
---
# <a name="select-partition"></a>select partition

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたパーティションを選択し、そのパーティションにフォーカスを移動します。 このコマンドは、現在フォーカスが、選択したディスクのパーティションを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select partition=<n>  
```  
  
### <a name="parameters"></a>パラメーター  
  
|   パラメーター    |                                                                                    [説明]                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| partition\=<n> | フォーカスを受け取るパーティションの数。 使用して現在選択されているディスク上のすべてのパーティションの番号を表示する、 **パーティションを一覧表示** diskpart コマンドです。 |
  
## <a name="remarks"></a>Remarks  
  
-   使用して、ディスクを選択するパーティションを選択する前にまず必要があります、 **select ディスク** コマンドです。  
  
-   パーティション番号が指定されていない場合、このコマンドは、現在選択されているディスクにフォーカスがあるパーティションを表示します。  
  
-   ボリュームに対応するパーティションが選択されている場合は、パーティションが自動的に選択されます。  
  
-   対応するボリュームを持つパーティションを選択すると、ボリュームが自動的に選択されます。  
  
## <a name="examples"></a>例  
フォーカスをパーティション 3 に、次のように入力します。  
  
```  
select partitition=3  
```  
  
現在フォーカスが、選択したディスクのパーティションを表示するには、次のように入力します。  
  
```  
select partition  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

