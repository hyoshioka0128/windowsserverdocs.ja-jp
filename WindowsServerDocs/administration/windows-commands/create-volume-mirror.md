---
title: ボリュームミラーの作成
description: ボリュームミラーの作成に関するリファレンストピックでは、2つの指定されたダイナミックディスクを使用してボリュームミラーを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eda0a6d799fc88c8382e128df1bd260b9e9426b7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716946"
---
# <a name="create-volume-mirror"></a>ボリュームミラーの作成

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 および Windows Server 2008 R2 でのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|         パラメーター         |                                                                                                                                     [説明]                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         幅\=<n>         |                 ボリュームが各ディスクで占有するディスク領域\(の\)量を mb 単位で指定します。 サイズを指定しないと、新しいボリュームは最小のディスクで残りの空き領域を占有し、それ以外のディスクでそれと同じ容量の空き領域を占有します。                 |
| ディスク\=<n><n>、\[、<n>,...\] |                       ミラーボリュームを作成するダイナミックディスクを指定します。 ミラーボリュームを作成するには、2つのダイナミックディスクが必要です。 **Size**パラメーターで指定したサイズと同じ容量の領域が、各ディスクに割り当てられます。                        |
|        位置\=<n>         | すべてのボリュームエクステントを最も近い配置境界に配置します。 このパラメータは通常、パフォーマンスを向上させるため\(に\) 、ハードウェア RAID 論理ユニット番号 LUN アレイと共に使用されます。 *n*は、ディスクの先頭\(から\)最も近いアラインメント境界までのキロバイト kb 数です。 |
|           noerr           |                                        スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターを指定しないと、エラーが発生して DiskPart が終了します。                                         |
  
## <a name="remarks"></a>Remarks  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a>例  
ディスク1と2で、サイズが 1000 mb のミラーボリュームを作成するには、次のように入力します。  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

