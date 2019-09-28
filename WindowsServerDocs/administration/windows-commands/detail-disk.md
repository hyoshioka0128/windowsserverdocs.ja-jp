---
title: 詳細ディスク
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ff78a3f9e27cde35a7e19bdf1565c515a127261b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378576"
---
# <a name="detail-disk"></a>詳細ディスク



選択したディスクとそのディスク上のボリュームのプロパティを表示します。

## <a name="syntax"></a>構文

```
detail disk
```

## <a name="remarks"></a>コメント

-   この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
-   選択したディスクが仮想ハードディスク (VHD) の場合、**詳細ディスク**では、ディスクのバスの種類が仮想として報告されます。

## <a name="BKMK_examples"></a>例

選択したディスクのプロパティと、ディスク内のボリュームに関する情報を表示するには、次のように入力します。
```
detail disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

