---
title: detail disk
description: '[詳細ディスク] の Windows コマンドのトピック。選択したディスクのプロパティとそのディスク上のボリュームが表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d0768d45c0f56ba549ff54064c4e74ae3048e41
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846455"
---
# <a name="detail-disk"></a>detail disk

選択したディスクおよびそのディスク上のボリュームのプロパティを表示します。

## <a name="syntax"></a>構文

```
detail disk
```

## <a name="remarks"></a>コメント

-   この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
-   選択したディスクが仮想ハードディスク (VHD) の場合、**詳細ディスク**では、ディスクのバスの種類が仮想として報告されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

選択したディスクのプロパティと、ディスク内のボリュームに関する情報を表示するには、次のように入力します。
```
detail disk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

