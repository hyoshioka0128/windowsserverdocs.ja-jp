---
title: detail disk
description: '[詳細ディスク] コマンドのリファレンストピックでは、選択したディスクのプロパティとそのディスク上のボリュームが表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 358d6762f382dc8461c73cbd557a906eb5189c6f
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993067"
---
# <a name="detail-disk"></a>detail disk

選択したディスクおよびそのディスク上のボリュームのプロパティを表示します。 開始する前に、この操作を成功させるには、ディスクを選択する必要があります。 使用して、 [select ディスク](select-disk.md) コマンド ディスクを選択し、それにフォーカスをします。 バーチャルハードディスク (VHD) を選択すると、このコマンドによってディスクのバスの種類が*仮想*として表示されます。

## <a name="syntax"></a>構文

```
detail disk
```

## <a name="examples"></a>例

選択したディスクのプロパティと、ディスク内のボリュームに関する情報を表示するには、次のように入力します。

```
detail disk
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [詳細コマンド](detail.md)
