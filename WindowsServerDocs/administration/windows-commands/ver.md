---
title: ver
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a9c6cd4-b67d-4b30-8c56-5f9798eafd2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 384a5e8adb6c8304033f7dc645184ff2b674ae39
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887173"
---
# <a name="ver"></a>ver



オペレーティング システムのバージョン番号を表示します。

このコマンドには、PowerShell ではなく、Windows コマンド プロンプト (Cmd.exe) ではサポートされています。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ver
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

コマンド シェル (cmd.exe) からオペレーティング システムのバージョン番号を取得するには、次のように入力します。

```
ver
```

Ver コマンドは、PowerShell では機能しません。 PowerShell からの OS バージョンを取得するには、次のように入力します。

```powershell
$PSVersionTable.BuildVersion
````


#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
