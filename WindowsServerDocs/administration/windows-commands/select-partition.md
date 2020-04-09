---
title: select partition
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 25f70083-b8f7-4a8e-9b34-4b3ffbe06670
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 97145d73cbbe1bdc9b27e545b047b78fe89e4984
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834805"
---
# <a name="select-partition"></a>select partition

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたパーティションを選択し、そのパーティションにフォーカスを移動します。 このコマンドは、現在フォーカスが、選択したディスクのパーティションを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select partition=<n>  
```  
  
### <a name="parameters"></a>パラメーター  
  
|   パラメーター    |                                                                                    説明                                                                                    |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| パーティション\=<n> | フォーカスを受け取るパーティションの数。 使用して現在選択されているディスク上のすべてのパーティションの番号を表示する、 **パーティションを一覧表示** diskpart コマンドです。 |
  
## <a name="remarks"></a>コメント  
  
-   使用して、ディスクを選択するパーティションを選択する前にまず必要があります、 **select ディスク** コマンドです。  
  
-   パーティション番号が指定されていない場合、このコマンドは、現在選択されているディスクにフォーカスがあるパーティションを表示します。  
  
-   ボリュームに対応するパーティションが選択されている場合は、パーティションが自動的に選択されます。  
  
-   対応するボリュームを持つパーティションを選択すると、ボリュームが自動的に選択されます。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
フォーカスをパーティション 3 に、次のように入力します。  
  
```  
select partitition=3  
```  
  
現在フォーカスが、選択したディスクのパーティションを表示するには、次のように入力します。  
  
```  
select partition  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

