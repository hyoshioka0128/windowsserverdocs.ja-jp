---
title: diskpart のインポート
description: ローカルコンピューターのディスクグループに外部ディスクグループをインポートするインポートコマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6912aa9698d484501cad5f3cdfb5b19955bb4931
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818452"
---
# <a name="import-diskpart"></a>インポート (diskpart)

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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [diskpart コマンド](diskpart.md)
