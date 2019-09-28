---
title: bitsadmin rawreturn
description: '**Bitsadmin rawreturn**の Windows コマンドトピックは、解析に適したデータを返します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86d769de460538acda696194348980de5752d6d8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380877"
---
# <a name="bitsadmin-rawreturn"></a>bitsadmin rawreturn

解析に適したデータを返します。

## <a name="syntax"></a>構文

```
bitsadmin /RawReturn
```

## <a name="remarks"></a>コメント

改行文字と書式設定を出力から取り除きます。

通常、このコマンドを**Create**および**Get @ no__t*** スイッチと組み合わせて使用すると、値のみを受け取ることができます。 このスイッチは、他のスイッチの前に指定する必要があります。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態の生データを取得します。
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)