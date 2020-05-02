---
title: select volume
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3885d5d40e35e975ebe1cc28ddc26d4c1e78e24
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721987"
---
# <a name="select-volume"></a>select volume

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたボリュームを選択し、それにフォーカスを移動します。 このコマンドは、選択したディスクにフォーカスが置かれているボリュームを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select volume={<n>|<d>}  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター |                                                                               [説明]                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <n>    | フォーカスを受け取るボリュームの数。 使用して現在選択されているディスク上のすべてのボリュームの番号を表示する、 **ボリュームを一覧表示** diskpart コマンドです。 |
|    <d>    |                                                 フォーカスを受け取るボリュームのドライブ文字またはマウント ポイントのパス。                                                 |
  
## <a name="remarks"></a>Remarks  
  
-   ボリュームが指定されていない場合、このコマンドは、選択したディスクに現在フォーカスがあるボリュームを表示します。  
  
-   ベーシック ディスクにボリュームを選択するともにフォーカスを対応するパーティション。  
  
-   ボリュームに対応するパーティションが選択されている場合は、パーティションが自動的に選択されます。  
  
-   対応するボリュームを持つパーティションを選択すると、ボリュームが自動的に選択されます。  
  
## <a name="examples"></a>例  
フォーカスをボリューム 2 に、次のように入力します。  
  
```  
select volume=2  
```  
  
フォーカスを C ドライブに、次のように入力します。  
  
```  
select volume=c  
```  
  
Mountpath という名前のフォルダーにマウントされているボリュームにフォーカスを移動するには、次のように入力します。  
  
```  
select volume=c:\mountpath  
```  
  
選択したディスクにフォーカスが置かれているボリュームを表示するには、次のように入力します。  
  
```  
select volume  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

