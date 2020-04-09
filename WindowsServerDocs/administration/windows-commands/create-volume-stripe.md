---
title: create volume stripe
description: ボリュームストライプの作成に関する Windows コマンドのトピックでは、2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8123d2b5852f606398e3be7161ef0341698b7fb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846905"
---
# <a name="create-volume-stripe"></a>create volume stripe

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows Vista では、この DiskPart コマンドは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition でのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|         パラメーター         |                                                                                                                            説明                                                                                                                            |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         サイズ\=<n>         |             ボリュームが各ディスク上で占有するディスク領域の容量 (mb \(MB\))。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。             |
| ディスク\=<n>、<n>\[、<n>,...\] |                                  ストライプボリュームを作成するダイナミックディスク。 ストライプ ボリュームを作成するには、少なくとも 2 台のダイナミック ディスクが必要です。 **\=<n>サイズ**と同じ大きさの領域が各ディスクに割り当てられます。                                   |
|        \=<n> に揃える         | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、LUN\) 配列 \(ハードウェア RAID 論理ユニット番号と共に使用します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。 |
|           noerr           |                               スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>コメント  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
ディスク1と2で、サイズが 1000 mb のストライプボリュームを作成するには、次のように入力します。  
  
```  
create volume stripe size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

