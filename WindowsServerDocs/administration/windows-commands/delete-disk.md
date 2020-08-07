---
title: delete disk
description: ディスクの削除コマンドの参照記事。ディスクの一覧から、不足しているダイナミックディスクを削除します。
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85657e571fb5f0f4e0a55cf54065056a8f28c385
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891445"
---
# <a name="delete-disk"></a>delete disk

ディスクの一覧から不足しているダイナミックディスクを削除します。

> [!NOTE]
> このコマンドの使用方法の詳細については、「不足している[ダイナミックディスクを削除する](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc753029(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文

```
delete disk [noerr] [override]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
| override | DiskPart でディスク上のすべてのシンプル ボリュームを削除できるようにします。 ミラー ボリュームを構成する領域がディスクに格納されている場合、ディスク上のそのミラー領域は削除されます。 ディスクが RAID-5 ボリュームのメンバーの場合、delete disk override コマンドは失敗します。 |

## <a name="examples"></a>例

ディスクの一覧から不足しているダイナミックディスクを削除するには、次のように入力します。

```
delete disk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [delete コマンド](delete.md)
