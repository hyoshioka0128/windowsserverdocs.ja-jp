---
title: convert mbr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: da8d62567863bc38a5aa0b35a8f3fe4ee24cc888
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834613"
---
# <a name="convert-mbr"></a>convert mbr



GUID パーティション テーブル (GPT) パーティション スタイルを持つ空のベーシック ディスクをマスター ブート レコード (MBR) パーティション スタイルを持つベーシック ディスクに変換します。

> [!IMPORTANT]
> ディスクを MBR ディスクに変換する空にする必要があります。 データのバックアップし、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。

このコマンドを使用する方法に関する手順については、次を参照してください。 [GUID パーティション テーブル ディスクをマスター ブート レコード ディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207050)(https://go.microsoft.com/fwlink/?LinkId=207050)します。

## <a name="syntax"></a>構文

```
convert mbr [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   この操作を成功させるのには、ベーシック ディスクを選択してください。 使用して、 **select ディスク**コマンドをベーシック ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

MBR パーティション スタイルを GPT パーティション スタイルからベーシック ディスクに変換する入力 >:
```
convert mbr
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

