---
title: ver
description: Ver の Windows コマンドに関するトピック。オペレーティングシステムのバージョン番号が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0d0676dcfa6546e4bbf74c4c58a24f51744d00f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830195"
---
# <a name="ver"></a>ver



オペレーティング システムのバージョン番号を表示します。

このコマンドは、Windows コマンドプロンプト (Cmd.exe) ではサポートされていますが、PowerShell ではサポートされていません。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ver
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

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
