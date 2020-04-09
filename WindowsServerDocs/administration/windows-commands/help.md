---
title: ヘルプ
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7b6f3a563c59a55ff92b38f0854437b96478f6c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842345"
---
# <a name="help"></a>ヘルプ



システムコマンド (つまり、ネットワークに接続されていないコマンド) に関するオンライン情報を提供します。 パラメーターを指定せずに使用する場合は、すべてのシステムコマンドについての説明と**ヘルプ**が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
help [<Command>] 
[<Command>] /?
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<コマンド >|情報を表示するコマンドの名前を指定します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

**Robocopy**コマンドに関する情報を表示するには、次のいずれかを入力します。
```
help robocopy
robocopy /? 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)