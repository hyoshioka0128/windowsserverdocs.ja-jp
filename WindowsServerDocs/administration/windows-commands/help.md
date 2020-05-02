---
title: help
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c65b5ac3-711a-4368-95b8-ba82e2d00713
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d3a16c2534934a7bc8126b0a775ec7aa08462b3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724912"
---
# <a name="help"></a>help



システムコマンド (つまり、ネットワークに接続されていないコマンド) に関するオンライン情報を提供します。 パラメーターを指定せずに使用する場合は、すべてのシステムコマンドについての説明と**ヘルプ**が表示されます。



## <a name="syntax"></a>構文

```
help [<Command>] 
[<Command>] /?
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<コマンド>|情報を表示するコマンドの名前を指定します。|

## <a name="examples"></a>例

**Robocopy**コマンドに関する情報を表示するには、次のいずれかを入力します。
```
help robocopy
robocopy /? 
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)