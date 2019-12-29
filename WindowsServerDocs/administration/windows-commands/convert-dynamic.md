---
title: 動的変換
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 15c15d14aeb440c5d7862f0a304f223988f52bbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379098"
---
# <a name="convert-dynamic"></a>動的変換



ベーシックディスクをダイナミックディスクに変換します。

このコマンドの使用方法については、「[ベーシックディスクをダイナミックディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207047)する方法」 (https://go.microsoft.com/fwlink/?LinkId=207047) を参照してください。

## <a name="syntax"></a>構文

```
convert dynamic [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   ベーシックディスク上の既存のパーティションは、単純ボリュームになります。
-   この操作を成功させるには、ベーシックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

ベーシックディスクをダイナミックディスクに変換するには、次のように入力します。
```
convert dynamic
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

