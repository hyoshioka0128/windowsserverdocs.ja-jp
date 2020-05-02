---
title: create volume stripe
description: ボリュームストライプの作成に関するリファレンストピックでは、2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 98ca692d27135aa8ba4da0ff85ecd3074cdd73c4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716876"
---
# <a name="create-volume-stripe"></a>create volume stripe

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows Vista では、この DiskPart コマンドは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition でのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|         パラメーター         |                                                                                                                            [説明]                                                                                                                            |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         幅\=<n>         |             ボリュームが各ディスクで占有するディスク\(領域\)の容量 (mb 単位)。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。             |
| ディスク\=<n><n>、\[、<n>,...\] |                                  ストライプボリュームを作成するダイナミックディスク。 ストライプ ボリュームを作成するには、少なくとも 2 台のダイナミック ディスクが必要です。 **サイズ\= **と同じ量の領域が各ディスクに割り当てられます。                                   |
|        位置\=<n>         | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるため\(に\) 、ハードウェア RAID 論理ユニット番号 LUN アレイと共に使用します。 *n*は、ディスクの先頭\(から\)最も近いアラインメント境界までのキロバイト kb 数です。 |
|           noerr           |                               スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>Remarks  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a>例  
ディスク1と2で、サイズが 1000 mb のストライプボリュームを作成するには、次のように入力します。  
  
```  
create volume stripe size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

