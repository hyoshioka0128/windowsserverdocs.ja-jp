---
title: offline disk
description: オフラインディスクコマンドの参照記事。オフライン状態に焦点を合わせてオンラインディスクを取得します。
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b570336bba8da402adb848c465148dabc49b0f6a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885282"
---
# <a name="offline-disk"></a>offline disk

オフラインの状態にフォーカスがあるオンライン ディスクを移動します。 ディスクグループのダイナミックディスクがオフラインになると、ディスクの状態が [**不足**] に変わり、グループにはオフラインのディスクが表示されます。 不足しているディスクは、無効なグループに移動されます。 ダイナミックディスクがグループ内の最後のディスクである場合、ディスクの状態は [**オフライン**] に変わり、空のグループは削除されます。

> [!NOTE]
> ディスクを選択する必要があります、 **オフライン ディスク** コマンドを正しく実行されます。 使用して、 [select ディスク](select-disk.md) コマンド ディスクを選択し、それにフォーカスをします。
>
> このコマンドは、san モードをオフラインに変更することで、SAN オンラインモードのディスクでも動作します。

## <a name="syntax"></a>構文

```
offline disk [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。

```
offline disk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
