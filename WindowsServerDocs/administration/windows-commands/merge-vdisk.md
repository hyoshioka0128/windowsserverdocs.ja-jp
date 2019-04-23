---
title: Vdisk をマージします。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 159e307912cb06bc3ea5e452f735e786c0cf9965
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847013"
---
# <a name="merge-vdisk"></a>Vdisk をマージします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

差分仮想ハード_ディスク (VHD)、対応する親 VHD をマージします。 親 VHD は、差分 VHD からの変更を含めるように変更されます。
> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。
## <a name="syntax"></a>構文
```
merge vdisk depth=<n>
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|深さ =<n>|マージする親 VHD ファイルの数を示します。 たとえば、 **深さ = 1** 差分チェーンの 1 つのレベルで差分 VHD をマージすることを示します。|
## <a name="remarks"></a>注釈
-   VHD の選択し、この操作を正常にデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。
-   このパラメーターは、親 VHD を変更します。 その結果、親に依存するその他の差分 Vhd は無効になります。
## <a name="BKMK_Examples"></a>例
その親 VHD と差分 VHD をマージするには、次のように入力します。
```
merge vdisk depth=1
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [attach vdisk](attach-vdisk.md)
-   [vdisk を最適化します。](compact-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)
-   [Vdisk をデタッチします。](detach-vdisk.md)
-   [vdisk を展開します。](expand-vdisk.md)
-   [vdisk を選択します。](select-vdisk.md)
-   [list_1](list_1.md)
