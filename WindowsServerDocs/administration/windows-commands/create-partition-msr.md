---
title: パーティション msr の作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 45cc215b097ce048b15f0e907f95f976e4941e28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378903"
---
# <a name="create-partition-msr"></a>パーティション msr の作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

GUID パーティションテーブル \(gpt @ no__t ディスクに Microsoft 予約 @no__t 0MSR @ no__t パーティションを作成します。  
  
> [!CAUTION]  
> このコマンドを使用する場合は注意が必要です。 Gpt ディスクには特定のパーティションレイアウトが必要であるため、Microsoft 予約パーティションを作成すると、ディスクが読み取り不能になる可能性があります。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                         説明                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ @ no__t-0 @ no__t-1  |               パーティションのサイズ (mb) \(MB @ no__t-1。 パーティションは、少なくとも <n> によって指定された数と同じ長さになるようにします。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。               |
| offset @ no__t-0 @ no__t-1 | パーティションが作成される、\(KB @ no__t のオフセット (kb 単位) を指定します。 オフセットは、使用されるセクターサイズを完全に埋めるために切り上げられます。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。 |
|    noerr    |                            スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                             |
  
## <a name="remarks"></a>コメント  
  
-   Windows オペレーティングシステムの起動に使用される gpt ディスクでは、拡張可能なファームウェアインターフェイス \(EFI @ no__t システムパーティションが、ディスク上の最初のパーティションであり、その後に Microsoft 予約パーティションが続きます。 データ記憶域にのみ使用される gpt ディスクには、EFI システムパーティションがありません。この場合、Microsoft 予約パーティションが最初のパーティションになります。  
  
-   Windows では、Microsoft 予約パーティションはマウントされません。 データを格納することはできません。削除することはできません。  
  
-   Microsoft 予約パーティションは、すべての gpt ディスクに必要です。 このパーティションのサイズは、gpt ディスクの合計サイズによって異なります。 Microsoft 予約パーティションを作成するには、gpt ディスクのサイズが 32 MB 以上である必要があります。  
  
-   この操作を成功させるには、ベーシック gpt ディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用して、ベーシック gpt ディスクを選択し、それにフォーカスを移動します。  
  
## <a name="BKMK_examples"></a>例  
サイズが 1000 mb の Microsoft 予約パーティションを作成するには、次のように入力します。  
  
```  
create partition msr size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

