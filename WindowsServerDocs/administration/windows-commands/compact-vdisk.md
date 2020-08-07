---
title: compact vdisk
description: Compact vdisk コマンドの参照記事。容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズが削減されます。
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e8f29cf7188d2630f15bee9bde2910c64f325b5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892626"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [vdisk コマンドのアタッチ](attach-vdisk.md)

- [detail vdisk コマンド](detail-vdisk.md)

- [Detach vdisk コマンド](detach-vdisk.md)

- [vdisk コマンドを展開する](expand-vdisk.md)

- [Merge vdisk コマンド](merge-vdisk.md)

- [vdisk コマンドを選択する](select-vdisk.md)

- [list コマンド](list.md)
