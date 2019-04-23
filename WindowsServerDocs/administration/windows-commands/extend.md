---
title: extend
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2414e21d-fc0b-40e8-9e33-3e072f8ad76b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 84047c690006bf727bc12855576960bbf67d1617
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857933"
---
# <a name="extend"></a>extend

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ボリュームを拡張して空きにフォーカスとそのファイル システム パーティション\(未割り当て\)ディスク上の領域。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
extend [size=<n>] [disk=<n>] [noerr]  
extend filesystem [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|領域の量をメガバイト単位で指定\(MB\)現在のボリュームまたはパーティションを追加します。 サイズを指定しない場合、ディスクで利用可能な連続した空き領域のすべてに使用されます。|  
|ディスク\=<n>|ボリュームまたはパーティションが拡張されて、ディスクを指定します。 ディスクが指定されていない場合は、現在のディスク上にボリュームまたはパーティションが拡張されます。|  
|ファイル システム|フォーカスがあるボリュームのファイル システムを拡張します。 ファイル システムがボリュームで拡張されていない、ディスク上にのみ使用できます。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   ベーシック ディスクで、ボリュームまたはフォーカスのあるパーティションと同じディスクに空き領域があります。 ボリュームまたはフォーカスのあるパーティションにもすぐに従う必要があります\([次へ] のセクター オフセットで開始する必要がありますが、\)します。  
  
-   シンプル ボリュームまたはスパン ボリュームをダイナミック ディスク上にある空き領域のダイナミック ディスク上にボリュームを拡張できます。 このコマンドを使用して、シンプル ダイナミック ボリュームをスパン ダイナミック ボリュームに変換できます。 ミラー化された RAID\-5 とストライプ ボリュームを拡張することはできません。  
  
-   パーティションは、NTFS ファイル システムでフォーマットされました以前、ファイル システムはより大きなパーティションが自動的に拡張し、データの損失は発生しません。  
  
-   パーティションが NTFS 以外のファイル システムでフォーマットされたでコマンドは、パーティションに変更なしで失敗します。  
  
-   パーティションはファイル システムで以前にフォーマットされていない場合、パーティションが引き続き拡張されます。  
  
-   パーティションは、拡張できる前に、関連付けられているボリュームが必要です。  
  
## <a name="BKMK_examples"></a>例  
ディスク 3 に、500 メガバイト単位でボリュームまたはフォーカスのあるパーティションを拡張するには、次のように入力します。  
  
```  
extend size=500 disk=3  
```  
  
拡張された後は、ボリュームのファイル システムを拡張するに次のように入力します。  
  
```  
extend filesystem  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

