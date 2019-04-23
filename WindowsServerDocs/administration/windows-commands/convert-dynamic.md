---
title: 動的変換します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 353c1e4558ab2b0c948ec78c0cd87b579c738ec8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841613"
---
# <a name="convert-dynamic"></a>動的変換します。



ベーシック ディスクをダイナミック ディスクに変換します。

このコマンドを使用する方法に関する手順については、次を参照してください。[ベーシック ディスクをダイナミック ディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207047)(https://go.microsoft.com/fwlink/?LinkId=207047)します。

## <a name="syntax"></a>構文

```
convert dynamic [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   ベーシック ディスク上の既存のパーティションでは、シンプル ボリュームになります。
-   この操作を成功させるのには、ベーシック ディスクを選択してください。 使用して、 **select ディスク**コマンドをベーシック ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ベーシック ディスクをダイナミック ディスクに変換するには、次のように入力します。
```
convert dynamic
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

