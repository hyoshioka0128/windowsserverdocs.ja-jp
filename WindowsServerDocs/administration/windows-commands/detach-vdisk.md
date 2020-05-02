---
title: vdisk のデタッチ
description: Detach vdisk のリファレンストピックでは、選択したバーチャルハードディスク (VHD) がホストコンピューター上のローカルハードディスクドライブとして表示されなくなります。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5e64559650597eb8d15e28075f74704fdf338a6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716668"
---
# <a name="detach-vdisk"></a>vdisk のデタッチ

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

選択した仮想ハードディスク (VHD) がホストコンピューター上のローカルハードディスクドライブとして表示されなくなります。 VHD をデタッチすると、他の場所に VHD をコピーできます。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
detach vdisk [noerr]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|[説明]|  
|-------|--------|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>Remarks  
  
-   この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。  
  
## <a name="examples"></a>例  
選択した VHD をデタッチするには、次のように入力します。  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  

-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [Vdisk をマージします。](merge-vdisk.md)  
  
-   [vdisk の選択](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

