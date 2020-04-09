---
title: vdisk を展開する
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 272714372a35f7f205b5a2e70cb2f2669b3a0634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844895"
---
# <a name="expand-vdisk"></a>vdisk を展開する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

仮想ハードディスク (VHD) を指定されたサイズに拡張します。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
> ## <a name="syntax"></a>構文
> ```
> expand vdisk maximum=<n>
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |  パラメーター  |                      説明                      |
> |-------------|-------------------------------------------------------|
> | 最大値 =<n> | VHD の新しいサイズをメガバイト (MB) 単位で指定します。 |
> 
> ## <a name="remarks"></a>コメント
> - この操作を成功させるには、VHD を選択してデタッチする必要があります。 **Select vdisk**コマンドを使用してボリュームを選択し、それにフォーカスを移動します。
>   ## <a name="examples"></a><a name=BKMK_Examples></a>例
>   選択した VHD を 20 GB まで拡張するには、次のように入力します。
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>その他の参照情報
> - - [コマンド ライン構文の記号](command-line-syntax-key.md)
> - [vdisk のアタッチ](attach-vdisk.md)
> - [compact vdisk](compact-vdisk.md)

-   [Vdisk のデタッチ](detach-vdisk.md)
-   [詳細 vdisk](detail-vdisk.md)
-   [マージ vdisk](merge-vdisk.md)
-   [vdisk の選択](select-vdisk.md)
-   [list_1](list_1.md)
