---
title: convert basic
description: '[基本の変換] コマンドの参照記事では、空のダイナミックディスクをベーシックディスクに変換します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a61c3d9fd8d708a41347f0bcf46aa627e960153c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928987"
---
# <a name="convert-basic"></a>convert basic

空のダイナミックディスクをベーシックディスクに変換します。 この操作を成功させるには、ダイナミックディスクを選択する必要があります。 [[ディスクの選択] コマンド](select-disk.md)を使用してダイナミックディスクを選択し、それにフォーカスを移動します。

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換するためには、そのディスクが空である必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。

> [!NOTE]
> このコマンドの使用方法については、「[ダイナミックディスクをベーシックディスクに戻す](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755238(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文

```
convert basic [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

選択したダイナミックディスクをベーシックに変換するには、次のように入力します。

```
convert basic
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [convert コマンド](convert.md)
