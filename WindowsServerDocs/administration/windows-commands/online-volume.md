---
title: online volume
description: オンラインボリュームコマンドの参照記事。オフラインボリュームをオンライン状態にします。
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b09730d3cc0cfe758c90c3ca57fd039282ba3fce
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885221"
---
# <a name="online-volume"></a>online volume

オフラインボリュームをオンライン状態にします。 このコマンドは、障害が発生しているか、失敗したか、冗長状態になっているボリュームに対して機能します。

> [!NOTE]
> **オンラインボリューム**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 [ボリュームを選択して](select-volume.md) コマンドのボリュームを選択し、それにフォーカスをします。

> [!IMPORTANT]
> 読み取り専用ディスクで使用されている場合、このコマンドは失敗します。

## <a name="syntax"></a>構文

```
online volume [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

フォーカスがあるボリュームをオンラインにするには、次のように入力します。

```
online volume
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
