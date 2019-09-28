---
title: convert mbr
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a635a4c0-af73-4330-b021-51d483424537
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 47001415158b3bdb0b06af9114b995a6f0634da1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379071"
---
# <a name="convert-mbr"></a>convert mbr



GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。

> [!IMPORTANT]
> MBR ディスクに変換するには、ディスクを空にする必要があります。 データをバックアップしてから、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。

このコマンドの使用方法については、「 [GUID パーティションテーブルディスクをマスターブートレコードディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207050)する」 (https://go.microsoft.com/fwlink/?LinkId=207050) を参照してください。

## <a name="syntax"></a>構文

```
convert mbr [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   この操作を成功させるには、ベーシックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

ベーシックディスクを GPT パーティションスタイルから MBR パーティションスタイルに変換するには > 次のように入力します。
```
convert mbr
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

