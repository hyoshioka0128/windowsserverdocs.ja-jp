---
title: convert gpt
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 433e30efeecec4e4ec51d67c40c14cacf986d12e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434227"
---
# <a name="convert-gpt"></a>convert gpt



マスター ブート レコード (MBR) パーティション スタイルに空のベーシック ディスクを GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。

このコマンドを使用する方法に関する手順については、次を参照してください。[マスター ブート レコード ディスクを GUID パーティション テーブル ディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207049)(https://go.microsoft.com/fwlink/?LinkId=207049)します。

## <a name="syntax"></a>構文

```
convert gpt [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

> [!IMPORTANT]
> ディスクを GPT ディスクに変換する空にする必要があります。 データのバックアップし、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。
> -   GPT への変換の必要な最小ディスク サイズは、128 メガバイトです。
> -   この操作を成功させるのには、ベーシック MBR ディスクを選択してください。 使用して、 **select ディスク**コマンドをベーシック ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ベーシック ディスクを MBR パーティション スタイルを GPT パーティション スタイルに変換するには、次のように入力します。
```
convert gpt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

