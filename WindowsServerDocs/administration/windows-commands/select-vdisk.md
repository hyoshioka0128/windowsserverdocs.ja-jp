---
title: vdisk の選択
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bfa6450d1704cde1e5ff2a50a8e3b61a30d0766
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384191"
---
# <a name="select-vdisk"></a>vdisk の選択

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたバーチャルハードディスク \(VHD\) を選択し、それにフォーカスを移動します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
select vdisk file=<full path> [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|ファイル\=<full path>|既存の VHD ファイルの完全パスとファイル名を指定します。|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="BKMK_examples"></a>例  
フォーカスを Test.vhd という名前の VHD に、次のように入力します。  
  
```  
select vdisk file="c:\test\test.vhd"  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [Vdisk のデタッチ](detach-vdisk.md)  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [マージ vdisk](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

