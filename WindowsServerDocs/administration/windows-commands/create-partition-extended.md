---
title: create partition extended
description: パーティションを拡張するための Windows コマンドに関するトピックでは、フォーカスがあるディスクに拡張パーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4ad7cb66-9c66-4153-b94e-1030a7225070
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7071ed16d8ddbd1e37c9dd49bac8bb2b032b0b24
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847075"
---
# <a name="create-partition-extended"></a>create partition extended

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクに拡張パーティションを作成します。 このコマンドは、マスターブートレコード (MBR) ディスクでのみ使用できます。

## <a name="syntax"></a>構文  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                             説明                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ\=<n>  |                                                  パーティションのサイズを mb \(MB\)単位で指定します。 サイズが指定されていない場合、パーティションは拡張パーティションの空き領域がなくなるまで続行されます。                                                  |
| オフセット\=<n> |                     パーティションが作成される\)\(KB 単位のオフセットを指定します。 オフセットが指定されていない場合、パーティションは、新しいパーティションを保持するのに十分な大きさのディスクの空き領域の先頭から開始されます。                      |
| \=<n> に揃える  | すべてのパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるために、LUN\) 配列 \(ハードウェア RAID 論理ユニット番号と共に使用します。 <n> は、ディスクの先頭から最も近いアラインメント境界までのキロバイト数 \(KB\) です。 |
|    noerr    |                                 スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                 |
  
## <a name="remarks"></a>コメント  
  
-   パーティションを作成すると、フォーカスは自動的に新しいパーティションに移動します。  
  
-   1 台のディスクには、1 つの拡張パーティションしか作成できません。  
  
-   別の拡張パーティション内に拡張パーティションを作成しようとすると、このコマンドは失敗します。  
  
-   論理ドライブを作成する前に、拡張パーティションを作成する必要があります。  
  
-   この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
サイズが 1000 mb の拡張パーティションを作成するには、次のように入力します。  
  
```  
create partition extended size=1000  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

