---
title: convert basic
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4b81126f4a623d841bb5868f786678d7b093581
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379132"
---
# <a name="convert-basic"></a>convert basic



空のダイナミックディスクをベーシックディスクに変換します。

このコマンドの使用方法については、「[ダイナミックディスクをベーシックディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207048)する方法」 (https://go.microsoft.com/fwlink/?LinkId=207048) を参照してください。

## <a name="syntax"></a>構文

```
convert basic [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!IMPORTANT]
> ベーシックディスクに変換するには、ディスクを空にする必要があります。 データをバックアップしてから、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。
> -   この操作を成功させるには、ダイナミックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してダイナミックディスクを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

選択したダイナミックディスクをベーシックに変換するには、次のように入力します。
```
convert basic
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

