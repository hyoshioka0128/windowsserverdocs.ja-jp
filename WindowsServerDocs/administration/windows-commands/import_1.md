---
title: diskpart のインポート
description: インポートコマンドの参照記事。外部ディスクグループをローカルコンピューターのディスクグループにインポートします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 072c012e5e2cc8d49811fbfa1cff5140b2c745a1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924420"
---
# <a name="import-diskpart"></a>import (diskpart)

外部ディスクグループをローカルコンピューターのディスクグループにインポートします。 このコマンドは、フォーカスがあるディスクと同じグループにあるすべてのディスクをインポートします。

> :このコマンドを使用する前に、 [[ディスクの選択] コマンド](select-disk.md)を使用して、外部ディスクグループ内のダイナミックディスクを選択し、そのディスクにフォーカスを移動する必要があります。

## <a name="syntax"></a>構文

```
import [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

ローカルコンピューターのディスクグループにフォーカスがあるディスクと同じディスクグループにあるすべてのディスクをインポートするには、次のように入力します。

```
import
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [diskpart コマンド](diskpart.md)
