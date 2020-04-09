---
title: vdisk のデタッチ
description: Detach vdisk の Windows コマンドに関するトピックでは、選択したバーチャルハードディスク (VHD) がホストコンピューター上のローカルハードディスクドライブとして表示されなくなります。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14eb66031841624156afb03f492e2afce5bc56f0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846505"
---
# <a name="detach-vdisk"></a>vdisk のデタッチ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

選択した仮想ハードディスク (VHD) がホストコンピューター上のローカルハードディスクドライブとして表示されなくなります。 VHD をデタッチすると、他の場所に VHD をコピーできます。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
detach vdisk [noerr]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>コメント  
  
-   この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。  
  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
選択した VHD をデタッチするには、次のように入力します。  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  

-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [マージ vdisk](merge-vdisk.md)  
  
-   [vdisk の選択](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

