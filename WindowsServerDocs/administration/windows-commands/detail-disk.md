---
title: detail disk
description: 選択したディスクのプロパティとそのディスク上のボリュームを表示する、詳細ディスクの参照トピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a746506d6c9609e3214dbd48e5fa91f52d16ab4d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82710513"
---
# <a name="detail-disk"></a>detail disk

選択したディスクおよびそのディスク上のボリュームのプロパティを表示します。

## <a name="syntax"></a>構文

```
detail disk
```

## <a name="remarks"></a>Remarks

-   この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
-   選択したディスクが仮想ハードディスク (VHD) の場合、**詳細ディスク**では、ディスクのバスの種類が仮想として報告されます。

## <a name="examples"></a>例

選択したディスクのプロパティと、ディスク内のボリュームに関する情報を表示するには、次のように入力します。
```
detail disk
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

