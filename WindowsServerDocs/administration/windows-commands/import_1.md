---
title: import
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca0a15e73e4aa913ece34e083a8070be3b4b190d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375410"
---
# <a name="import"></a>import



外部ディスクグループをローカルコンピューターのディスクグループにインポートします。

## <a name="syntax"></a>構文

```
import [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   Import コマンドは、フォーカスがあるディスクと同じグループにあるすべてのディスクをインポートします。
-   この操作を成功させるには、外部ディスクグループのダイナミックディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ローカルコンピューターのディスクグループにフォーカスがあるディスクと同じディスクグループにあるすべてのディスクをインポートするには、次のように入力します。
```
import
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

