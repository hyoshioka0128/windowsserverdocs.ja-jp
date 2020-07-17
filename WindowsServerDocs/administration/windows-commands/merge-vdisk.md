---
title: merge vdisk
description: Merge vdisk コマンドの参照記事。差分仮想ハードディスク (VHD) とそれに対応する親 VHD をマージします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41201885861b7084fa7b49be8b5bf5a0e7394981
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925037"
---
# <a name="merge-vdisk"></a>merge vdisk

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

差分仮想ハード_ディスク (VHD)、対応する親 VHD をマージします。 親 VHD は、差分 VHD からの変更を含めるように変更されます。 このコマンドは、親 VHD を変更します。 その結果、親に依存するその他の差分 Vhd は無効になります。

> [!IMPORTANT]
> この操作を成功させるには、VHD を選択してデタッチする必要があります。 使用して、 **vdisk を選択して** コマンド、VHD を選択し、それにフォーカスをします。

## <a name="syntax"></a>構文

```
merge vdisk depth=<n>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 深さ =`<n>` | マージする親 VHD ファイルの数を示します。 たとえば、は差分 `depth=1` VHD が差分チェーンの1つのレベルにマージされることを示します。 |

### <a name="examples"></a>例

その親 VHD と差分 VHD をマージするには、次のように入力します。

```
merge vdisk depth=1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [vdisk コマンドのアタッチ](attach-vdisk.md)

- [compact vdisk コマンド](compact-vdisk.md)

- [detail vdisk コマンド](detail-vdisk.md)

- [detach vdisk コマンド](detach-vdisk.md)

- [vdisk コマンドを展開する](expand-vdisk.md)

- [vdisk コマンドを選択する](select-vdisk.md)

- [list コマンド](list.md)
