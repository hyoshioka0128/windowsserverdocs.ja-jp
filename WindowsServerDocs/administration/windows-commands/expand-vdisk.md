---
title: vdisk を展開する
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8fb5d7b58b7aa4bc9557086c73020820cfa04284
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377293"
---
# <a name="expand-vdisk"></a>vdisk を展開する

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

仮想ハードディスク (VHD) を指定されたサイズに拡張します。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> expand vdisk maximum=<n>
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |  パラメーター  |                      説明                      |
> |-------------|-------------------------------------------------------|
> | 最大値 = <n> | VHD の新しいサイズをメガバイト (MB) 単位で指定します。 |
> 
> ## <a name="remarks"></a>コメント
> - この操作を成功させるには、VHD を選択してデタッチする必要があります。 **Select vdisk**コマンドを使用してボリュームを選択し、それにフォーカスを移動します。
>   ## <a name="BKMK_Examples"></a>例
>   選択した VHD を 20 GB まで拡張するには、次のように入力します。
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>その他の参照情報
> - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [Vdisk のデタッチ](detach-vdisk.md)
-   [詳細 vdisk](detail-vdisk.md)
-   [マージ vdisk](merge-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
