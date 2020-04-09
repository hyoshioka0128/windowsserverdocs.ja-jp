---
title: convert gpt
description: Gpt の変換に関する Windows コマンドのトピックでは、マスターブートレコード (MBR) パーティションスタイルを持つ空のベーシックディスクを、GUID パーティションテーブル (GPT) パーティションスタイルを持つベーシックディスクに変換します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c1ffe61245f7752ccc81d21d513fa00acd7b68b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847285"
---
# <a name="convert-gpt"></a>convert gpt

マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。

このコマンドの使用方法については、「[マスターブートレコードディスクを GUID パーティションテーブルディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207049)する」 (https://go.microsoft.com/fwlink/?LinkId=207049)を参照してください。

## <a name="syntax"></a>構文

```
convert gpt [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!IMPORTANT]
> GPT ディスクに変換するには、ディスクを空にする必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。
> -   GPT への変換に必要な最小ディスクサイズは 128 mb です。
> -   この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

ベーシックディスクを MBR パーティションスタイルから GPT パーティションスタイルに変換するには、次のように入力します。
```
convert gpt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

