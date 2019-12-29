---
title: Vdisk をマージします。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7023f2a6669ea6f6801e25cbfc87c950ab95a3bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373730"
---
# <a name="merge-vdisk"></a>Vdisk をマージします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

差分仮想ハード_ディスク (VHD)、対応する親 VHD をマージします。 親 VHD は、差分 VHD からの変更を含めるように変更されます。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> merge vdisk depth=<n>
> ```
> ### <a name="parameters"></a>パラメーター
> 
> | パラメーター |                                                                                    説明                                                                                    |
> |-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | depth = <n> | マージする親 VHD ファイルの数を示します。 たとえば、 **深さ = 1** 差分チェーンの 1 つのレベルで差分 VHD をマージすることを示します。 |
> 
> ## <a name="remarks"></a>コメント
> - この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
> - このパラメーターは、親 VHD を変更します。 その結果、親に依存するその他の差分 Vhd は無効になります。
>   ## <a name="BKMK_Examples"></a>例
>   その親 VHD と差分 VHD をマージするには、次のように入力します。
>   ```
>   merge vdisk depth=1
>   ```
>   ## <a name="additional-references"></a>その他の参照情報
> - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk のデタッチ](detach-vdisk.md)
-   [vdisk を展開する](expand-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
