---
title: compact vdisk
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7efd40fa4b822636eda9f4082b5f561b452d3846
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379304"
---
# <a name="compact-vdisk"></a>compact vdisk

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズを小さくします。 このパラメーターは、ファイルを追加したときに Vhd のサイズが大きく増加するため便利ですが、ファイルを削除すると自動的にサイズが縮小されることはありません。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> compact vdisk
> ```
> ## <a name="remarks"></a>コメント
> - この操作を成功させるには、動的に拡張された VHD を選択する必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
> - 動的に拡張された Vhd は、読み取り専用としてデタッチまたはアタッチされている場合にのみ圧縮できます。
>   ## <a name="BKMK_Examples"></a>例
>   動的に拡張される VHD を圧縮するには、次のように入力します。
>   ```
>   compact vdisk
>   ```
>   ## <a name="additional-references"></a>その他の参照情報
> - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk のデタッチ](detach-vdisk.md)
-   [vdisk を展開する](expand-vdisk.md)
-   [マージ vdisk](merge-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
