---
title: compact vdisk
description: Compact vdisk コマンドのリファレンストピックでは、容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズを削減します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4ae5c653645c9f6f3ef97501a59932682c24be3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711148"
---
# <a name="compact-vdisk"></a>compact vdisk

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズを小さくします。 このパラメーターは、ファイルを追加したときに Vhd のサイズが大きく増加するため便利ですが、ファイルを削除すると自動的にサイズが縮小されることはありません。

## <a name="syntax"></a>構文

```
compact vdisk
```

### <a name="remarks"></a>Remarks

- この操作を成功させるには、動的に拡張された VHD を選択する必要があります。 [Select vdisk コマンド](select-vdisk.md)を使用して VHD を選択し、それにフォーカスを移動します。

- 圧縮解除された、または読み取り専用としてアタッチされている、動的に拡張された Vhd のみを使用できます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [vdisk コマンドのアタッチ](attach-vdisk.md)

- [detail vdisk コマンド](detail-vdisk.md)

- [Detach vdisk コマンド](detach-vdisk.md)

- [vdisk コマンドを展開する](expand-vdisk.md)

- [Merge vdisk コマンド](merge-vdisk.md)

- [vdisk コマンドを選択する](select-vdisk.md)

- [list コマンド](list.md)
