---
title: パーティション拡張の作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21620da46be0e1375f320172e7ccfe2edc338114
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378911"
---
# <a name="create-partition-extended"></a>パーティション拡張の作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクに拡張パーティションを作成します。 このコマンドは、マスターブートレコード \(MBR @ no__t ディスクでのみ使用できます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                             説明                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ @ no__t-0 @ no__t-1  |                                                  パーティションのサイズを mb 単位で指定します \(MB @ no__t-1。 サイズが指定されていない場合、パーティションは拡張パーティションの空き領域がなくなるまで続行されます。                                                  |
| offset @ no__t-0 @ no__t-1 |                     パーティションが作成される、\(KB @ no__t のオフセット (kb 単位) を指定します。 オフセットが指定されていない場合、パーティションは、新しいパーティションを保持するのに十分な大きさのディスクの空き領域の先頭から開始されます。                      |
| align\=<n>  | すべてのパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 \(LUN @ no__t アレイと共に使用します。 <n> は、ディスクの先頭から最も近いアラインメント境界までの kb @no__t 1 KB @ no__t の数です。 |
|    noerr    |                                 スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                 |
  
## <a name="remarks"></a>コメント  
  
-   パーティションが作成されると、フォーカスは自動的に新しいパーティションに移ります。  
  
-   ディスクごとに作成できる拡張パーティションは1つだけです。  
  
-   別の拡張パーティション内に拡張パーティションを作成しようとすると、このコマンドは失敗します。  
  
-   論理ドライブを作成する前に、拡張パーティションを作成する必要があります。  
  
-   この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
サイズが 1000 mb の拡張パーティションを作成するには、次のように入力します。  
  
```  
create partition extended size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

