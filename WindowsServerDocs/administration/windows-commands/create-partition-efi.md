---
title: efi のパーティションを作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99970fba41a747a6bb4b1ca6cc4b7f603c547790
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434163"
---
# <a name="create-partition-efi"></a>efi のパーティションを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Itanium\-ベースのコンピューターは、拡張ファームウェア インターフェイスを作成します。 \(EFI\) GUID パーティション テーブルのシステム パーティション\(gpt\)ディスク。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                             説明                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ\=<n>  |                         メガバイト単位でのパーティションのサイズ\(MB\)します。 サイズを指定しない場合、パーティションが現在の領域に空き領域があるまで続行されます。                         |
| オフセット\=<n> |             キロバイト単位のオフセット\(KB\)でパーティションを作成します。 オフセットを指定しない場合、パーティションは保持するのに十分な大きさである最初のディスク エクステントで配置されます。              |
|    noerr    | スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>注釈  
  
-   パーティションが作成された後は、新しいパーティションにフォーカスが与えられます。  
  
-   この操作を成功させるのには、gpt ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
選択したディスクを 1000 メガバイトの EFI パーティションを作成するには、次のように入力します。  
  
```  
create partition efi size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

