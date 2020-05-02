---
title: Vdisk をマージします。
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bfcdde34d2c7dd6146222d04e982aa1ec8009c2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723990"
---
# <a name="merge-vdisk"></a>Vdisk をマージします。

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

差分仮想ハード_ディスク (VHD)、対応する親 VHD をマージします。 親 VHD は、差分 VHD からの変更を含めるように変更されます。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> merge vdisk depth=<n>
> ```
> #### <a name="parameters"></a>パラメーター
> 
> | パラメーター |                                                                                    [説明]                                                                                    |
> |-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | 深さ =<n> | マージする親 VHD ファイルの数を示します。 たとえば、 **深さ = 1** 差分チェーンの 1 つのレベルで差分 VHD をマージすることを示します。 |
> 
> ## <a name="remarks"></a>Remarks
> - この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
> - このパラメーターは、親 VHD を変更します。 その結果、親に依存するその他の差分 Vhd は無効になります。
>   ## <a name="examples"></a>例
>   その親 VHD と差分 VHD をマージするには、次のように入力します。
>   ```
>   merge vdisk depth=1
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
> - - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk のデタッチ](detach-vdisk.md)
-   [vdisk を展開する](expand-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
