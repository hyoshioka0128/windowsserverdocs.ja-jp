---
title: bdehdcfg quiet
description: Bdehdcfg quiet の Windows コマンドに関するトピックでは、すべてのアクションとエラーを表示しないように bdehdcfg に指示しています。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f75b702-890b-4ff9-805c-edf5cadd8822
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d59a14e34200e3fa8e18e36e166ef62ceca1afe7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382221"
---
# <a name="bdehdcfg-quiet"></a>bdehdcfg: quiet



Bdehdcfg コマンドラインツールに、すべてのアクションとエラーがコマンドラインインターフェイスに表示されないことを通知します。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -quiet
```

### <a name="parameters"></a>パラメーター

このコマンドは、追加のパラメーターを受け取りません。

## <a name="remarks"></a>コメント

ドライブの準備中に "yes/No (Y/N)" プロンプトが表示された場合は、"Yes" という答えが想定されます。 ドライブの準備中に発生したエラーを表示するには、 **DrivePreparationTool**イベントプロバイダーの下にあるシステムイベントログを確認します。

## <a name="BKMK_Examples"></a>例

次の例は、 **quiet**コマンドの使用方法を示しています。
```
bdehdcfg -target default -quiet
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)