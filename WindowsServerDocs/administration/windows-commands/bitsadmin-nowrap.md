---
title: bitsadmin nowrap
description: '**Bitsadmin nowrap**の Windows コマンドトピックでは、コマンドウィンドウの右端からはみ出た出力テキストの行を切り捨てます。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3806ec51161eeae498e3c9b367b2aacf0bd32c99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381052"
---
# <a name="bitsadmin-nowrap"></a>bitsadmin nowrap

コマンドウィンドウの右端からはみ出た出力テキストの行をすべて切り捨てます。

## <a name="syntax"></a>構文

```
bitsadmin /NoWrap
```

## <a name="remarks"></a>コメント

既定では、**モニター**スイッチを除くすべてのスイッチが出力をラップします。 他のスイッチの前に、 **NoWrap**スイッチを指定します。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態を取得し、出力をラップしません。
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)