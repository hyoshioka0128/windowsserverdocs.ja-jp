---
title: convert gpt
description: Gpt の変換コマンドのリファレンス記事。マスターブートレコード (MBR) パーティションスタイルを持つ空のベーシックディスクを、GUID パーティションテーブル (GPT) パーティションスタイルを持つベーシックディスクに変換します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2384ea5a94de64051dc45caecd88e08960b567b0
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958534"
---
# <a name="convert-gpt"></a>convert gpt

マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。 この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 [[ディスクの選択] コマンド](select-disk.md)を使用してベーシックディスクを選択し、それにフォーカスを移動します。

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換するためには、そのディスクが空である必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。 GPT への変換に必要な最小ディスクサイズは 128 mb です。

> [!NOTE]
> このコマンドの使用方法については、「[マスターブートレコードディスクを GUID パーティションテーブルディスクに変更](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc725671(v=ws.11))する」を参照してください。

## <a name="syntax"></a>構文

```
convert gpt [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

ベーシックディスクを MBR パーティションスタイルから GPT パーティションスタイルに変換するには、次のように入力します。

```
convert gpt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [convert コマンド](convert.md)
