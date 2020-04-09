---
title: 取り込み
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4b9d2751-7637-4738-83b0-8c578eb28f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e098e7133bca18e1a6ba683e525783af17c3958
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842135"
---
# <a name="import"></a>取り込み



外部ディスクグループをローカルコンピューターのディスクグループにインポートします。

## <a name="syntax"></a>構文

```
import [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   Import コマンドは、フォーカスがあるディスクと同じグループにあるすべてのディスクをインポートします。
-   この操作を成功させるには、外部ディスクグループのダイナミックディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例

ローカルコンピューターのディスクグループにフォーカスがあるディスクと同じディスクグループにあるすべてのディスクをインポートするには、次のように入力します。
```
import
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

