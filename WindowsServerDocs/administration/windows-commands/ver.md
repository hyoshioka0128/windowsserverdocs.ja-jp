---
title: ver
description: Ver のリファレンストピック。オペレーティングシステムのバージョン番号が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7050dddda6cc27c50980f2e44f40e1f682c1d375
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720309"
---
# <a name="ver"></a>ver



オペレーティング システムのバージョン番号を表示します。

このコマンドは、Windows コマンドプロンプト (Cmd.exe) ではサポートされていますが、PowerShell ではサポートされていません。



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


## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
