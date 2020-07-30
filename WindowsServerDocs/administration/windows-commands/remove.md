---
title: remove
description: 削除コマンドの参照記事。ボリュームからドライブ文字またはマウントポイントを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b0886140-da8b-4231-8cb2-f280874d99c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7fba062945effd49efa9987d2c7d23fc90552fd4
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409683"
---
# <a name="remove"></a>remove

フォーカスがあるボリュームからドライブ文字とマウント ポイントを削除します。 all パラメーターを使用すると、現在のドライブ文字とマウント ポイントがすべて削除されます。 ドライブ文字またはマウントポイントが指定されていない場合は、DiskPart によって検出された最初のドライブ文字またはマウントポイントが削除されます。

また、[削除] コマンドを使用して、リムーバブルドライブに関連付けられているドライブ文字を変更することもできます。 システムボリューム、ブートボリューム、またはページングボリュームのドライブ文字を削除することはできません。 さらに、OEM パーティションのドライブ文字、認識されていない GUID を持つ GPT パーティション、または特殊なデータではない GPT パーティション (EFI システムパーティションなど) のいずれかを削除することはできません。

> [!NOTE]
> [**削除**] コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 [ボリュームを選択して](select-volume.md) コマンド ディスクを選択し、それにフォーカスをします。

## <a name="syntax"></a>構文

```
remove [{letter=<drive> | mount=<path> [all]}] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 文字 =`<drive>` | 削除するドライブ文字。 |
| mount =`<path>` | 削除するマウントポイントのパス。 |
| all | 現在のドライブ文字とマウント ポイントをすべて削除します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

D! を削除するにはドライブ、次のように入力します。

```
remove letter=d
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
