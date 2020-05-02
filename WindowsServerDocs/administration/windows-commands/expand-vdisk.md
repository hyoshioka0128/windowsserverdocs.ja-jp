---
title: vdisk を展開する
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c2380045de45397888777f58e3420c75bb6915ae
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725692"
---
# <a name="expand-vdisk"></a>vdisk を展開する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

仮想ハードディスク (VHD) を指定されたサイズに拡張します。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> expand vdisk maximum=<n>
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |  パラメーター  |                      [説明]                      |
> |-------------|-------------------------------------------------------|
> | 最大 =<n> | VHD の新しいサイズをメガバイト (MB) 単位で指定します。 |
> 
> ## <a name="remarks"></a>Remarks
> - この操作を成功させるには、VHD を選択してデタッチする必要があります。 **Select vdisk**コマンドを使用してボリュームを選択し、それにフォーカスを移動します。
>   ## <a name="examples"></a>例
>   選択した VHD を 20 GB まで拡張するには、次のように入力します。
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
> - - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [Vdisk のデタッチ](detach-vdisk.md)
-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk をマージします。](merge-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
