---
title: ボリュームミラーの作成
description: ボリュームミラーの作成に関する Windows コマンドのトピックでは、指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa5ea72eb0edacb841f32126f31a257b0573dd6d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846975"
---
# <a name="create-volume-mirror"></a>ボリュームミラーの作成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 および Windows Server 2008 R2 でのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|         パラメーター         |                                                                                                                                     説明                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         サイズ\=<n>         |                 ボリュームが各ディスク上で占有するディスク領域の容量を mb \(MB\)単位で指定します。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。                 |
| ディスク\=<n>、<n>\[、<n>,...\] |                       ミラーボリュームを作成するダイナミックディスクを指定します。 ミラーボリュームを作成するには、2つのダイナミックディスクが必要です。 **Size**パラメーターで指定したサイズと同じ容量の領域が、各ディスクに割り当てられます。                        |
|        \=<n> に揃える         | すべてのボリュームエクステントを最も近い配置境界に配置します。 このパラメーターは、通常、パフォーマンスを向上させるために、LUN\) 配列 \(ハードウェア RAID 論理ユニット番号と共に使用されます。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。 |
|           noerr           |                                        スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターを指定しないと、エラーが発生して DiskPart が終了します。                                         |
  
## <a name="remarks"></a>コメント  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
ディスク1と2で、サイズが 1000 mb のミラーボリュームを作成するには、次のように入力します。  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

