---
title: パーティション msr を作成します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79288fe90d037659f5e3934f1925dd8b7c21ad7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873433"
---
# <a name="create-partition-msr"></a>パーティション msr を作成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Microsoft の予約を作成します。 \(MSR\) GUID パーティション テーブルのパーティション\(gpt\)ディスク。  
  
> [!CAUTION]  
> このコマンドを使用する場合は十分に注意します。 Gpt ディスクには、特定のパーティション レイアウトが必要があります、ため Microsoft 予約パーティションを作成すると、ディスクが読みにくくなるがあります。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|サイズ\=<n>|メガバイト単位でのパーティションのサイズ\(MB\)します。 パーティションで指定された数 (バイト単位) を少なくとも限り<n>します。 サイズを指定しない場合、パーティションが現在の領域に空き領域があるまで続行されます。|  
|オフセット\=<n>|キロバイト単位のオフセットを指定します。 \(KB\)、でパーティションを作成します。 オフセットはセクター サイズの使用を完全に埋めるに丸めます。 オフセットを指定しない場合、パーティションは保持するのに十分な大きさである最初のディスク エクステントで配置されます。|  
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   Windows オペレーティング システム、拡張ファームウェア インターフェイスの起動に使用される gpt ディスク上で\(EFI\)システム パーティションは、Microsoft 予約パーティションが後に、ディスクの最初のパーティション。 データ ストレージに対してのみ使用される gpt ディスクの場合、Microsoft 予約パーティションが最初のパーティションは、EFI システム パーティションではありません。  
  
-   Windows では、Microsoft 予約パーティションをマウントしません。 データを格納することはできませんし、それらを削除することはできません。  
  
-   すべての gpt ディスク上に Microsoft 予約パーティションが必要です。 このパーティションのサイズは、gpt ディスクの合計サイズによって異なります。 Gpt ディスクのサイズは、Microsoft 予約パーティションを作成するには少なくとも 32 MB である必要があります。  
  
-   この操作を成功させるのには、基本的な gpt ディスクを選択してください。 使用して、 **select ディスク**コマンドを基本的な gpt ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
サイズをメガバイト数が 1000 の Microsoft 予約パーティションを作成するには、次のように入力します。  
  
```  
create partition msr size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照  
[コマンドライン構文キー](command-line-syntax-key.md)  
  

  

