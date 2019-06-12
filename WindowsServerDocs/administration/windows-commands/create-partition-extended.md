---
title: 拡張パーティションを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0a1cca93a064cfb6e5c18f4a472ea837b922d07b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434192"
---
# <a name="create-partition-extended"></a>拡張パーティションを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスのあるディスクに拡張パーティションを作成します。 このコマンドを使用するにはマスター ブート レコードにのみ\(MBR\)ディスク。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition extended [size=<n>] [offset=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                             説明                                                                                                                              |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ\=<n>  |                                                  パーティションのサイズをメガバイト単位で指定\(MB\)します。 サイズを指定しない場合、パーティションが拡張パーティションの空き領域があるまで続行されます。                                                  |
| オフセット\=<n> |                     キロバイト単位のオフセットを指定します。 \(KB\)、でパーティションを作成します。 オフセットを指定しない場合、パーティションは、新しいパーティションを保持するのに十分な大きさであるディスクの空き領域の先頭に開始されます。                      |
| 配置\=<n>  | すべてのパーティション エクステント近いシリンダー境界に揃えて配置します。 ハードウェア RAID の論理ユニット番号で通常使用\(LUN\)パフォーマンスを向上させるために配列。 <n> キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。 |
|    noerr    |                                 スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                 |
  
## <a name="remarks"></a>注釈  
  
-   パーティションが作成された後、フォーカスは自動的に新しいパーティションに移動します。  
  
-   ディスクあたり 1 つの拡張パーティションを作成できます。  
  
-   別の拡張パーティション内に拡張パーティションを作成しようとした場合、このコマンドは失敗します。  
  
-   論理ドライブを作成する前に、拡張パーティションを作成する必要があります。  
  
-   この操作を成功させるのには、ベーシック MBR ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
サイズをメガバイト数が 1000 の拡張パーティションを作成するには、次のように入力します。  
  
```  
create partition extended size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

