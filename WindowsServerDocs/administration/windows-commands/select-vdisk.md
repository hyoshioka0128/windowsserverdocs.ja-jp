---
title: vdisk を選択します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a71a5c15c05a1e969d0720bc8e67e669d553f649
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852573"
---
# <a name="select-vdisk"></a>vdisk を選択します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した仮想ハード_ディスクを選択します。 \(VHD\)し、それに、フォーカスを移動します。  
  
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
|noerr|スクリプトのみに使用されます。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="BKMK_examples"></a>例  
フォーカスを Test.vhd という名前の VHD に、次のように入力します。  
  
```  
select vdisk file="c:\test\test.vhd"  
```  
  
#### <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
-   [attach vdisk](attach-vdisk.md)  
  
-   [vdisk を最適化します。](compact-vdisk.md)  
  
  
  
-   [Vdisk をデタッチします。](detach-vdisk.md)  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開します。](expand-vdisk.md)  
  
-   [Vdisk をマージします。](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

