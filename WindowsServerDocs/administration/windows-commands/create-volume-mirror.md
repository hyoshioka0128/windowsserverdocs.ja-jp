---
title: ボリュームミラーの作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 72ecc4e0ede163857c47c5b7013aacdd49719ac8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378871"
---
# <a name="create-volume-mirror"></a>ボリュームミラーの作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 および Windows Server 2008 R2 でのみ使用できます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume mirror [size=<n>] disk=<n>,<n>[,<n>,...] [align=<n>] [noerr] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|         パラメーター         |                                                                                                                                     説明                                                                                                                                     |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         サイズ @ no__t-0 @ no__t-1         |                 ボリュームが各ディスクで占有するディスク領域の容量をメガバイト @no__t 0MB @ no__t で指定します。 サイズが指定されていない場合、新しいボリュームでは、最小のディスクの残りの空き領域と、それ以降の各ディスクの容量が同じになります。                 |
| disk @ no__t-0 @ no__t、<n> @ no__t-3、<n>,... \] |                       ミラーボリュームを作成するダイナミックディスクを指定します。 ミラーボリュームを作成するには、2つのダイナミックディスクが必要です。 **Size**パラメーターで指定したサイズと同じ容量の領域が、各ディスクに割り当てられます。                        |
|        align\=<n>         | すべてのボリュームエクステントを最も近い配置境界に配置します。 このパラメータは通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 \(LUN @ no__t アレイで使用されます。 *n*は、ディスクの先頭から最も近いアラインメント境界までの 1 kb @ no__t の @no__t 単位数です。 |
|           noerr           |                                        スクリプト作成にのみ使用されます。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターを指定しないと、エラーが発生して DiskPart が終了します。                                         |
  
## <a name="remarks"></a>コメント  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移ります。  
  
## <a name="BKMK_examples"></a>例  
ディスク1と2で、サイズが 1000 mb のミラーボリュームを作成するには、次のように入力します。  
  
```  
create volume mirror size=1000 disk=1,2  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

