---
title: vdisk の選択
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65e186413bebbf467cd4c2033d274badd1fbea80
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834745"
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
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|ファイル\=<full path>|既存の VHD ファイルの完全パスとファイル名を指定します。|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
フォーカスを Test.vhd という名前の VHD に、次のように入力します。  
  
```  
select vdisk file=c:\test\test.vhd  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [Vdisk のデタッチ](detach-vdisk.md)  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [マージ vdisk](merge-vdisk.md)  
  
-   [list_1](list_1.md)  
  

