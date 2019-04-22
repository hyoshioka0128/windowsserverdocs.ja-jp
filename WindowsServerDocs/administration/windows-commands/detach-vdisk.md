---
title: Vdisk をデタッチします。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f01dcb8-9237-4564-ad94-8a8dd0fd0cca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b6a1ecd3d787506c89f120bed204cc30e6d68d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822733"
---
# <a name="detach-vdisk"></a>Vdisk をデタッチします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

選択した仮想ハード_ディスクを停止する\(VHD\)ホスト コンピューター上のローカル ハード ディスク ドライブとして表示されないようにします。 VHD がデタッチされている場合は、他の場所にコピーできます。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
detach vdisk [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|noerr|スクリプトのみに使用されます。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   VHD の選択し、この操作を正常にデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。  
  
## <a name="BKMK_Examples"></a>例  
選択した VHD をデタッチするには、次のように入力します。  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
-   [attach vdisk](attach-vdisk.md)  
  
-   [vdisk を最適化します。](compact-vdisk.md)  
  
  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開します。](expand-vdisk.md)  
  
-   [Vdisk をマージします。](merge-vdisk.md)  
  
-   [vdisk を選択します。](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

