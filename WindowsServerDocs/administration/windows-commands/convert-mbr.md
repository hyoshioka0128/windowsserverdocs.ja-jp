---
title: convert mbr
description: Mbr の変換コマンドのリファレンストピック。 GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 178384ff63267c6ca22069f49b980a316b7695aa
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720758"
---
# <a name="convert-mbr"></a>convert mbr

GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。 この操作を成功させるには、ベーシックディスクを選択する必要があります。 [[ディスクの選択] コマンド](select-disk.md)を使用してベーシックディスクを選択し、それにフォーカスを移動します。

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換するためには、そのディスクが空である必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。

> [!NOTE]
> このコマンドの使用方法については、「 [GUID パーティションテーブルディスクをマスターブートレコードディスクに変更](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725797(v=ws.11))する」を参照してください。

## <a name="syntax"></a>構文

```
convert mbr [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

ベーシックディスクを GPT パーティションスタイルから MBR パーティションスタイルに変換するには> 次のように入力します。

```
convert mbr
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [convert コマンド](convert.md)
