---
title: delete disk
description: ディスクの削除コマンドの参照記事。ディスクの一覧から、不足しているダイナミックディスクを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55eabb19e10a7ca6fe4dd705ab91961919bb2b7c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958404"
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [delete コマンド](delete.md)
