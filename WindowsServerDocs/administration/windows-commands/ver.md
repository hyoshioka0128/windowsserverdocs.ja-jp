---
title: ver
description: オペレーティングシステムのバージョン番号を表示する ver のリファレンス記事です。
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de080395c2e26f03371e0b27609238b66d7317f5
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891884"
---
# <a name="ver"></a>ver



オペレーティング システムのバージョン番号を表示します。

このコマンドは、Windows コマンドプロンプト (Cmd.exe) でサポートされていますが、PowerShell ではサポートされていません。



## <a name="syntax"></a>構文

```
ver
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a>例

コマンドシェル (cmd.exe) からオペレーティングシステムのバージョン番号を取得するには、次のように入力します。

```
ver
```

Ver コマンドは PowerShell では機能しません。 PowerShell から OS バージョンを取得するには、次のように入力します。

```powershell
$PSVersionTable.BuildVersion
````


## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
