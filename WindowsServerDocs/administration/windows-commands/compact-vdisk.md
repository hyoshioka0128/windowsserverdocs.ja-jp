---
title: compact vdisk
description: Windows コマンドのトピック「compact vdisk」では、容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズが削減されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9691be21c188fbc2c3b2e782acde127270decf56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847425"
---
# <a name="compact-vdisk"></a>compact vdisk

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

容量可変の拡張バーチャルハードディスク (VHD) ファイルの物理サイズを小さくします。 このパラメーターは、ファイルを追加したときに Vhd のサイズが大きく増加するため便利ですが、ファイルを削除すると自動的にサイズが縮小されることはありません。

> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。

## <a name="syntax"></a>構文
```
compact vdisk
```

## <a name="remarks"></a>コメント

- この操作を成功させるには、動的に拡張された VHD を選択する必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。

- 動的に拡張された Vhd は、読み取り専用としてデタッチまたはアタッチされている場合にのみ圧縮できます。

## <a name="examples"></a><a name=BKMK_Examples></a>例
動的に拡張される VHD を圧縮するには、次のように入力します。
```
compact vdisk
```

## <a name="additional-references"></a>その他の参照情報
- - [コマンド ライン構文の記号](command-line-syntax-key.md)
- [vdisk のアタッチ](attach-vdisk.md)
- [詳細 vdisk](detail-vdisk.md)
- [Vdisk のデタッチ](detach-vdisk.md)
- [vdisk を展開する](expand-vdisk.md)
- [マージ vdisk](merge-vdisk.md)
- [vdisk の選択](select-vdisk.md)
- [list_1](list_1.md)
