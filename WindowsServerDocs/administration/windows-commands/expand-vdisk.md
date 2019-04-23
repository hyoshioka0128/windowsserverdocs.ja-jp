---
title: vdisk を展開します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cf8fd0b05ca5baeeee4fadd670adb3169130d04e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837403"
---
# <a name="expand-vdisk"></a>vdisk を展開します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したサイズの仮想ハード_ディスク (VHD) を展開します。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
## <a name="syntax"></a>構文
```
expand vdisk maximum=<n>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|最大 =<n>|メガバイト (MB) 単位で VHD を新しいサイズを指定します。|
## <a name="remarks"></a>注釈
-   VHD の選択し、この操作を正常にデタッチする必要があります。 使用して、 **vdisk を選択**コマンドをボリュームを選択し、それにフォーカスをします。
## <a name="BKMK_Examples"></a>例
選択した VHD を展開し、20 GB に、次のように入力します。
```
expand vdisk maximum=20000
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [attach vdisk](attach-vdisk.md)
-   [vdisk を最適化します。](compact-vdisk.md)

-   [Vdisk をデタッチします。](detach-vdisk.md)
-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk をマージします。](merge-vdisk.md)
-   [vdisk を選択します。](select-vdisk.md)
-   [list_1](list_1.md)
