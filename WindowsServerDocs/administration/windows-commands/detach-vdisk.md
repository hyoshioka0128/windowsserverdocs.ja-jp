---
title: Vdisk のデタッチ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4850f9f17218178f210820dd4c6ca96fd918accc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378693"
---
# <a name="detach-vdisk"></a>Vdisk のデタッチ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

選択したバーチャルハードディスク \(VHD\) が、ホストコンピューターのローカルハードディスクドライブとして表示されなくなります。 VHD をデタッチすると、他の場所に VHD をコピーできます。  
  
> [!NOTE]  
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。  
  
## <a name="syntax"></a>構文  
  
```  
detach vdisk [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|noerr|スクリプト作成にのみ使用されます。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|  
  
## <a name="remarks"></a>注釈  
  
-   この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。  
  
## <a name="BKMK_Examples"></a>例  
選択した VHD をデタッチするには、次のように入力します。  
  
```  
detach vdisk  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [vdisk のアタッチ](attach-vdisk.md)  
  
-   [compact vdisk](compact-vdisk.md)  
  
  
  
-   [詳細 vdisk](detail-vdisk.md)  
  
-   [vdisk を展開する](expand-vdisk.md)  
  
-   [マージ vdisk](merge-vdisk.md)  
  
-   [vdisk の選択](select-vdisk.md)  
  
-   [list_1](list_1.md)  
  

