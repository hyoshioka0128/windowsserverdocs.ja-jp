---
title: ver
description: オペレーティングシステムのバージョン番号を表示する ver のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd9b40fa526c2917b6cdcbc8d54da510eb40bc53
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931340"
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
