---
title: vdisk を最適化します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c4a95354bf041777e43a9eac5f16e693b02c185c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434306"
---
# <a name="compact-vdisk"></a>vdisk を最適化します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

容量可変の拡張仮想ハード_ディスク (VHD) ファイルの物理サイズを縮小します。 このパラメーターは、ファイルを追加するが、いくらか難しくない自動的にサイズでファイルを削除すると、Vhd サイズの増加を動的に拡張するために役立ちます。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> compact vdisk
> ```
> ## <a name="remarks"></a>注釈
> - この操作を成功させるのには、可変の VHD を選択してください。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
> - 可変の Vhd をデタッチまたは読み取り専用としてアタッチされている圧縮することのみできます。
>   ## <a name="BKMK_Examples"></a>例
>   可変の VHD を最適化するには、次のように入力します。
>   ```
>   compact vdisk
>   ```
>   ## <a name="additional-references"></a>その他の参照
> - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [attach vdisk](attach-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk をデタッチします。](detach-vdisk.md)
-   [vdisk を展開します。](expand-vdisk.md)
-   [Vdisk をマージします。](merge-vdisk.md)
-   [vdisk を選択します。](select-vdisk.md)
-   [list_1](list_1.md)
