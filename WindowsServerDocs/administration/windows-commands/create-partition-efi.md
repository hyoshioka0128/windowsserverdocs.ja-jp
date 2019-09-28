---
title: パーティション efi の作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 76d97129fd67345f23eee2fc7b300493a1632cc6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379010"
---
# <a name="create-partition-efi"></a>パーティション efi の作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Itanium @ no__t ベースのコンピューターでは、拡張可能なファームウェアインターフェイス \(EFI @ no__t-2 システムパーティションを GUID パーティションテーブル \(gpt @ no__t ディスクに作成します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                             説明                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ @ no__t-0 @ no__t-1  |                         パーティションのサイズ (mb) \(MB @ no__t-1。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。                         |
| offset @ no__t-0 @ no__t-1 |             パーティションが作成されるオフセット (kb \(KB @ no__t-1)。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。              |
|    noerr    | スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>コメント  
  
-   パーティションが作成されると、新しいパーティションにフォーカスが割り当てられます。  
  
-   この操作を成功させるには、gpt ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="BKMK_examples"></a>例  
選択したディスクに 1000 mb の EFI パーティションを作成するには、次のように入力します。  
  
```  
create partition efi size=1000  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

