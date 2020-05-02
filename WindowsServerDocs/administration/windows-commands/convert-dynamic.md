---
title: convert dynamic
description: ベーシックディスクをダイナミックディスクに変換する [動的変換] コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05d507fb5a1f8ac3ca8d8899249a26dee496ed2a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720776"
---
# <a name="convert-dynamic"></a>convert dynamic

ベーシック ディスクをダイナミック ディスクに変換します。 この操作を成功させるには、ベーシックディスクを選択する必要があります。 [[ディスクの選択] コマンド](select-disk.md)を使用してベーシックディスクを選択し、それにフォーカスを移動します。

> [!NOTE]
> このコマンドの使用方法については、「[ダイナミックディスクをベーシックディスクに戻す](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文

```
convert dynamic [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

#### <a name="remarks"></a>Remarks

- ベーシックディスク上の既存のパーティションは、単純ボリュームになります。

## <a name="examples"></a>例

ベーシックディスクをダイナミックディスクに変換するには、次のように入力します。

```
convert dynamic
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [convert コマンド](convert.md)
