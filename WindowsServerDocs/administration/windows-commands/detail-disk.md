---
title: detail disk
description: '[詳細ディスク] コマンドの参照記事。選択したディスクのプロパティとそのディスク上のボリュームが表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b09cf40-8d93-452b-b449-5242e62a4102
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5bb5ec5a51f16aecf1b8ee35c78736f1791d3106
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929467"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [詳細コマンド](detail.md)
