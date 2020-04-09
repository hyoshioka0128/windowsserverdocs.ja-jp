---
title: detail volume
description: '[詳細] ボリュームの Windows コマンドトピック。現在のボリュームが存在するディスクが表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 38f2bc75-2ed6-4e80-aa74-ab83133db1cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f0441beba769066c593e77b55b9266918e5f778
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846323"
---
# <a name="detail-volume"></a>detail volume

現在のボリュームが存在するディスクを表示します。

## <a name="syntax"></a>構文

```
detail volume
```

## <a name="remarks"></a>コメント

-   この操作を正常に実行するには、ボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。
-   ボリュームの詳細は、DVD-ROM ドライブや CD-ROM ドライブなどの読み取り専用ボリュームには適用されません。

## <a name="examples"></a><a name=BKMK_examples></a>例

現在のボリュームが置かれているすべてのディスクを表示するには、次のように入力します。
```
detail volume
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

