---
title: ヘルプ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1d759c85c07d76811053ba0a4a938e07220c2648
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375587"
---
# <a name="help"></a>ヘルプ



システムコマンド (つまり、ネットワークに接続されていないコマンド) に関するオンライン情報を提供します。 パラメーターを指定せずに使用する場合は、すべてのシステムコマンドについての説明と**ヘルプ**が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
help [<Command>] 
[<Command>] /?
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Command >|情報を表示するコマンドの名前を指定します。|

## <a name="BKMK_examples"></a>例

**Robocopy**コマンドに関する情報を表示するには、次のいずれかを入力します。
```
help robocopy
robocopy /? 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)