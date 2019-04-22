---
title: ボリュームのミラーを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48776917-783a-47ff-8da4-1cab77cea34b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c66f21f55201d9d784b1ab0d7b729bc272589e5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822973"
---
# <a name="create-volume-mirror"></a>ボリュームのミラーを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

2 つの指定されたダイナミック ディスクを使用してボリュームのミラーを作成します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 および Windows Server 2008 R2 で利用可能なだけです。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|ディスク領域の量をメガバイト単位で指定\(MB\)ボリュームが各ディスクで占有します。 サイズを指定しないと、新しいボリュームは最小のディスクと後続の各ディスクに同じメモリ領域の残りの空き領域を占有。|  
|ディスク\=<n>、<n>\[、<n>、.\]|ミラー ボリュームを作成するダイナミック ディスクを指定します。 2 つのダイナミック ディスク ミラー ボリュームを作成する必要があります。 指定されたサイズに相当する領域の量、**サイズ**パラメーターは、各ディスクに割り当てられます。|  
|配置\=<n>|すべてのボリュームのエクステント近いシリンダー境界に揃えて配置します。 このパラメーターは、通常、ハードウェア RAID の論理ユニット番号で使用\(LUN\)パフォーマンスを向上させるために配列。 *n*キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。|  
|noerr|スクリプトのみに使用されます。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターがない場合、エラーが原因で DiskPart はエラーで終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="BKMK_examples"></a>例  
1 と 2 は、ディスク上のサイズで 1000 メガバイトのミラー化されたボリュームを作成するには、次のように入力します。  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

