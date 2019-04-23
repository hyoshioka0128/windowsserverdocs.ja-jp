---
title: ストライプのボリュームを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20dce735-5f7c-4f83-a580-d087e2913a00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 197864c6908645af0c0fa47ac811186207c2f247
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853883"
---
# <a name="create-volume-stripe"></a>ストライプのボリュームを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した 2 つ以上のダイナミック ディスクを使用してストライプ ボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows vista の場合、この DiskPart コマンドでは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition で提供のみ。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume stripe [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|メガバイト単位でのディスク領域の量\(MB\)ボリュームが各ディスクで占有します。 サイズを指定しないと、新しいボリュームは最小のディスクと後続の各ディスクに同じメモリ領域の残りの空き領域を占有。|  
|ディスク\=<n>、<n>\[、<n>、.\]|ストライプ ボリュームを作成するダイナミック ディスクです。 少なくとも 2 つのダイナミック ディスクをストライプ ボリュームを作成する必要があります。 等しい領域の量**サイズ\=<n>** が各ディスクに割り当てられます。|  
|配置\=<n>|すべてのボリュームのエクステント近いシリンダー境界に揃えて配置します。 ハードウェア RAID の論理ユニット番号で通常使用\(LUN\)パフォーマンスを向上させるために配列。 *n*キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="BKMK_examples"></a>例  
1 と 2 は、ディスク上のサイズで 1000 メガバイトのストライプ ボリュームを作成するには、次のように入力します。  
  
```  
create volume stripe size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

