---
title: diskpart のインポート
description: インポートコマンドの参照記事。外部ディスクグループをローカルコンピューターのディスクグループにインポートします。
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c32ee8643beefa394451c83df08dcec7a565117
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888354"
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
