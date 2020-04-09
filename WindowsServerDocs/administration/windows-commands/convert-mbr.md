---
title: convert mbr
description: Mbr の変換に関する Windows コマンドのトピックでは、GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルのベーシックディスクに変換します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eeaf79a380fb5f1074d2bbef004537804caa0d8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847205"
---
# <a name="convert-mbr"></a>convert mbr

GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。

> [!IMPORTANT]
> MBR ディスクに変換するには、ディスクを空にする必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。

このコマンドの使用方法については、「 [GUID パーティションテーブルディスクをマスターブートレコードディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207050)する」 (https://go.microsoft.com/fwlink/?LinkId=207050)を参照してください。

## <a name="syntax"></a>構文

```
convert mbr [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   この操作を成功させるには、ベーシックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

ベーシックディスクを GPT パーティションスタイルから MBR パーティションスタイルに変換するには > 次のように入力します。
```
convert mbr
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

