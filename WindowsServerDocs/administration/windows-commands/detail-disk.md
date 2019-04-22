---
title: ディスクの詳細
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 2c7a5063edf3cb2e190e8aec957e1b571c1f15bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819103"
---
# <a name="detail-disk"></a>ディスクの詳細



選択したディスクとそのディスク上のボリュームのプロパティを表示します。

## <a name="syntax"></a>構文

```
detail disk
```

## <a name="remarks"></a>注釈

-   この操作を成功させるのには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
-   選択したディスクが仮想ハード_ディスク (VHD) の場合**詳細ディスク**として仮想ディスクのバスの種類を報告します。

## <a name="BKMK_examples"></a>例

選択したディスクとディスクのボリュームに関する情報のプロパティを表示するには、次のように入力します。
```
detail disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

