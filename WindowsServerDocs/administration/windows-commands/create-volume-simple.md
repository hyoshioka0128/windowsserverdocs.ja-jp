---
title: 単純なボリュームを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a35d0de5110c0e1616c42921c8402ecc1aff8c41
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434051"
---
# <a name="create-volume-simple"></a>単純なボリュームを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたダイナミック ディスクにシンプル ボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows vista の場合、この DiskPart コマンドでは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition で提供のみ。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                                                            説明                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| サイズ\=<n>  |                                                                  メガバイト単位でボリュームのサイズ\(MB\)します。 サイズを指定しない場合、新しいボリュームをディスク上の残りの空き領域は。                                                                   |
| ディスク\=<n>  |                                                                                ボリュームが作成されたダイナミック ディスクです。 ディスクが指定されていない場合は、現在のディスクが使用されます。                                                                                |
| 配置\=<n> | すべてのボリュームのエクステント近いシリンダー境界に揃えて配置します。 ハードウェア RAID の論理ユニット番号で通常使用\(LUN\)パフォーマンスを向上させるために配列。 *n*キロバイト数は、 \(KB\)近いシリンダー境界にディスクの先頭から。 |
|   noerr    |                               スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>注釈  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="BKMK_examples"></a>例  
ディスク 1、上のサイズで 1000 メガバイトのボリュームを作成するには、次のように入力します。  
  
```  
create volume simple size=1000 disk=1  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

