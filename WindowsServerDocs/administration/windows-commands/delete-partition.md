---
title: パーティションを削除します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b47338b74cf71a4754b7320d6b3842f342d324d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436142"
---
# <a name="delete-partition"></a>パーティションを削除します。



フォーカスのあるパーティションを削除します。

## <a name="syntax"></a>構文

```
delete partition [noerr] [override]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|上書き|Diskpart で種類に関係なくすべてのパーティションを削除します。 通常、DiskPart のみを許可する既知のデータのパーティションを削除します。|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

> [!CAUTION]
> ダイナミック ディスク上のパーティションを削除するため、任意のデータは破棄され、ディスクは破損状態のままになります、ディスク上のすべてのダイナミック ボリュームを削除できます。 ダイナミック ボリュームを削除するには、常に使用して、**ボリュームを削除する**コマンドを代わりにします。 パーティションはダイナミック ディスクから削除できますが、作成する必要がありますされません。 たとえば、ダイナミック GPT ディスク上の認識されない GUID パーティション テーブル (GPT) パーティションを削除することです。 このようなパーティションを削除しても、空き領域を使用可能になるには発生しません。 このコマンドは、緊急の場合に、破損したオフライン ダイナミック ディスク上の reclame 領域には、場所、**クリーン**diskpart コマンドを使用することはできません。
> -   システム パーティション、ブート パーティション、またはアクティブなページング ファイルやクラッシュ ダンプ情報を含むパーティションを削除することはできません。
> -   この操作を成功させるのには、パーティションを選択してください。 使用して、**パーティションを選択**コマンドをパーティションを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

フォーカスのあるパーティションを削除するには、次のように入力します。
```
delete partition
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

