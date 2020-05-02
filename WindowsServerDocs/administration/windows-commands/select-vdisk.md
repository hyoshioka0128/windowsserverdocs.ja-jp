---
title: vdisk の選択
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68f60f8f43a33d498c40daa3b9994887f12037bb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722002"
---
# <a name="select-vdisk"></a>vdisk の選択

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された仮想ハード\(ディスク\) VHD を選択し、それにフォーカスを移動します。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
select vdisk file=<full path> [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|[説明]|  
|-------|--------|  
|拡張子\=<full path>|既存の VHD ファイルの完全パスとファイル名を指定します。|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="examples"></a>例  
フォーカスを Test.vhd という名前の VHD に、次のように入力します。  
  
```  
select vdisk file=c:\test\test.vhd  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [Vdisk のデタッチ](detach-vdisk.md)  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [Vdisk をマージします。](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

