---
title: convert gpt
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3b1b747-0a7a-4be2-8487-2c4be16ee190
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a6392cbcff618c642b9d0f168fe555e8be9e759
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379093"
---
# <a name="convert-gpt"></a>convert gpt



マスターブートレコード (MBR) パーティションスタイルを持つ空のベーシックディスクを、GUID パーティションテーブル (GPT) パーティションスタイルを持つベーシックディスクに変換します。

このコマンドの使用方法については、「[マスターブートレコードディスクを GUID パーティションテーブルディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207049)する」 (https://go.microsoft.com/fwlink/?LinkId=207049) を参照してください。

## <a name="syntax"></a>構文

```
convert gpt [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!IMPORTANT]
> GPT ディスクに変換するには、ディスクを空にする必要があります。 データをバックアップしてから、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。
> -   GPT への変換に必要な最小ディスクサイズは 128 mb です。
> -   この操作を成功させるには、ベーシック MBR ディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

ベーシックディスクを MBR パーティションスタイルから GPT パーティションスタイルに変換するには、次のように入力します。
```
convert gpt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

