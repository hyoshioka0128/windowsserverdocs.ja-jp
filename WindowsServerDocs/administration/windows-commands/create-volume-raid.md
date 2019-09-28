---
title: ボリューム raid の作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f257950-9240-4d5f-9537-8ad653d48ebf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a3c13cb5b78ae3e771b461a35a7130a48e7ec01
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378863"
---
# <a name="create-volume-raid"></a>ボリューム raid の作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された3つ以上のダイナミックディスクを使用して、RAID @ no__t-05 ボリュームを作成します。  
  
> [!IMPORTANT]  
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume raid [size=<n>] disk=<n>,<n>,<n>[,<n>,...] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|           パラメーター           |                                                                                                                                                                                                                                              説明                                                                                                                                                                                                                                              |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           サイズ @ no__t-0 @ no__t-1           | ボリュームが各ディスク上で占有するディスク領域の容量 (mb @no__t 0MB @ no__t)。 サイズが指定されていない場合は、可能な限り最大の RAID @ no__t-05 ボリュームが作成されます。 使用可能な連続する空き領域が最も小さいディスクによって、RAID @ no__t-05 ボリュームのサイズが決まり、各ディスクから同じ容量の領域が割り当てられます。 RAID @ no__t-05 ボリュームの実際の使用可能なディスク領域が、ディスク領域の合計容量を下回っています。これは、ディスク領域の一部がパリティに必要なためです。 |
| disk @ no__t-0 @ no__t-1、<n>、<n> @ no__t、<n>,... \] |                                                                                                                                               RAID @ no__t-05 ボリュームを作成するダイナミックディスク。 RAID @ no__t-05 ボリュームを作成するには、少なくとも3つのダイナミックディスクが必要です。 **サイズ @ no__t-1 @ no__t**と同じサイズの領域が各ディスクに割り当てられます。                                                                                                                                                |
|          align\=<n>           |                                                                                                                   すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 \(LUN @ no__t アレイと共に使用します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの 1 kb @ no__t の @no__t 単位数です。                                                                                                                   |
|             noerr             |                                                                                                                                                 スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                                                                                                                                  |
  
## <a name="remarks"></a>コメント  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移ります。  
  
## <a name="BKMK_examples"></a>例  
ディスク1、2、3を使用して、サイズが 1000 mb の RAID @ no__t ボリュームを作成するには、次のように入力します。  
  
```  
create volume raid size=1000 disk=1,2,3  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

