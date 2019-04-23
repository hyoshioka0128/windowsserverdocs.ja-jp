---
title: select volume
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d70d776-80ad-4f20-8288-a7997fb1df28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0ebf9896621268c384ea8129d32c985028054d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890733"
---
# <a name="select-volume"></a>select volume

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたボリュームを選択し、それに、フォーカスを移動します。 このコマンドは、選択したディスクにフォーカスが置かれているボリュームを表示することもできます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
select volume={<n>|<d>}  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|<n>|フォーカスを受け取るボリュームの数。 使用して現在選択されているディスク上のすべてのボリュームの番号を表示する、 **ボリュームを一覧表示** diskpart コマンドです。|  
|<d>|フォーカスを受け取るボリュームのドライブ文字またはマウント ポイントのパス。|  
  
## <a name="remarks"></a>注釈  
  
-   ボリュームが指定されていない場合、このコマンドは、選択したディスクにフォーカスが置かれているボリュームを表示します。  
  
-   ベーシック ディスクにボリュームを選択するともにフォーカスを対応するパーティション。  
  
-   対応するパーティションを持つ、ボリュームを選択すると、パーティションが自動的に選択します。  
  
-   対応するボリュームにパーティションを選択すると、ボリュームが自動的に選択します。  
  
## <a name="BKMK_examples"></a>例  
フォーカスをボリューム 2 に、次のように入力します。  
  
```  
select volume=2  
```  
  
フォーカスを C ドライブに、次のように入力します。  
  
```  
select volume=c  
```  
  
フォーカスを"mountpath"という名前のフォルダーにマウントされたボリュームに、次のように入力します。  
  
```  
select volume=c:\mountpath  
```  
  
選択したディスクにフォーカスが置かれているボリュームを表示するには、次のように入力します。  
  
```  
select volume  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

