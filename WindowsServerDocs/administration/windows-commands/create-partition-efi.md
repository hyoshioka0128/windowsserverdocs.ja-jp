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
ms.openlocfilehash: 3714cfe52aafd4a602346139552b6712dbbc98c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878223"
---
# <a name="create-partition-efi"></a>efi のパーティションを作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Itanium\-ベースのコンピューターは、拡張ファームウェア インターフェイスを作成します。 \(EFI\) GUID パーティション テーブルのシステム パーティション\(gpt\)ディスク。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|メガバイト単位でのパーティションのサイズ\(MB\)します。 サイズを指定しない場合、パーティションが現在の領域に空き領域があるまで続行されます。|  
|オフセット\=<n>|キロバイト単位のオフセット\(KB\)でパーティションを作成します。 オフセットを指定しない場合、パーティションは保持するのに十分な大きさである最初のディスク エクステントで配置されます。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   パーティションが作成された後は、新しいパーティションにフォーカスが与えられます。  
  
-   この操作を成功させるのには、gpt ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
選択したディスクを 1000 メガバイトの EFI パーティションを作成するには、次のように入力します。  
  
```  
create partition efi size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

