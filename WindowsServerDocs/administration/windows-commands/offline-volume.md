---
title: offline volume
description: オフラインボリュームコマンドの参照記事。オフライン状態に焦点を合わせてオンラインボリュームを取得します。
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e8a6bbebb88f97c4e4b04afccedeb05c4a1392a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885263"
---
# <a name="offline-volume"></a>offline volume

オフラインの状態に、オンラインのボリュームがフォーカスを移動します。

> [!NOTE]
> **オフラインボリューム**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 [ボリュームを選択して](select-volume.md) コマンド ディスクを選択し、それにフォーカスをします。

## <a name="syntax"></a>構文

```
offline volume [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。

```
offline volume
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
