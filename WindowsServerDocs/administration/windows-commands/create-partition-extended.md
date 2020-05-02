---
title: create partition extended
description: パーティション拡張の作成に関するリファレンストピック。フォーカスがあるディスクに拡張パーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b8af7247a9084b722f5b510df1d6af4622fc4ac2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719245"
---
# <a name="create-partition-extended"></a>create partition extended

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクに拡張パーティションを作成します。 このコマンドは、マスターブートレコード (MBR) ディスクでのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                             [説明]                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  幅\=<n>  |                                                  パーティションのサイズを mb \(単位で指定し\)ます。 サイズが指定されていない場合、パーティションは拡張パーティションの空き領域がなくなるまで続行されます。                                                  |
| 影\=<n> |                     パーティションが作成される\(オフセット\)をキロバイト kb 単位で指定します。 オフセットが指定されていない場合、パーティションは、新しいパーティションを保持するのに十分な大きさのディスクの空き領域の先頭から開始されます。                      |
| 位置\=<n>  | すべてのパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるため\(に\) 、ハードウェア RAID 論理ユニット番号 LUN アレイと共に使用します。 <n>ディスクの先頭から最も\(近い\)アラインメント境界までのキロバイト kb 数を指定します。 |
|    noerr    |                                 スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                 |
  
## <a name="remarks"></a>Remarks  
  
-   パーティションを作成すると、フォーカスは自動的に新しいパーティションに移動します。  
  
-   1 台のディスクには、1 つの拡張パーティションしか作成できません。  
  
-   別の拡張パーティション内に拡張パーティションを作成しようとすると、このコマンドは失敗します。  
  
-   論理ドライブを作成する前に、拡張パーティションを作成する必要があります。  
  
-   この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="examples"></a>例  
サイズが 1000 mb の拡張パーティションを作成するには、次のように入力します。  
  
```  
create partition extended size=1000  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

