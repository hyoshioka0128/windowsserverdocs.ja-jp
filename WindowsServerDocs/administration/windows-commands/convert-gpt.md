---
title: convert gpt
description: '[Gpt の変換] コマンドのリファレンストピック。マスターブートレコード (MBR) パーティションスタイルを持つ空のベーシックディスクを、GUID パーティションテーブル (GPT) パーティションスタイルを持つベーシックディスクに変換します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25b28473716037235a70e05835e23790f93164a1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720775"
---
# <a name="convert-gpt"></a>convert gpt

マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。 この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 [[ディスクの選択] コマンド](select-disk.md)を使用してベーシックディスクを選択し、それにフォーカスを移動します。

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換するためには、そのディスクが空である必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。 GPT への変換に必要な最小ディスクサイズは 128 mb です。

> [!NOTE]
> このコマンドの使用方法については、「[マスターブートレコードディスクを GUID パーティションテーブルディスクに変更](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc725671(v=ws.11))する」を参照してください。

## <a name="syntax"></a>構文

```
convert gpt [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
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
