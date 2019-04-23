---
title: Get DriverPackageFile コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed9518fae07745502d01dc0084b7443a1332db83
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859803"
---
# <a name="using-the-get-driverpackagefile-command"></a>Get DriverPackageFile コマンドを使用してください。



ドライバーが含まれているファイルを含むドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/InfFile:\<Inf ファイルのパス >|ドライバー パッケージの .inf ファイルの完全パスとファイル名を指定します。|
|[/アーキテクチャ: {x86 | ia64 | x64}]|ドライバー パッケージのアーキテクチャを指定します。|
|[/Show: {ドライバー | ファイル | All}]|パッケージ情報を表示することを示します。 場合 **/show** が指定されていない、既定では、パッケージ メタデータ ドライバーのみを返します。 **ドライバー** パッケージのドライバーの一覧が表示されます。 **ファイル** パッケージにファイルの一覧が表示されます。 **すべて** ドライバーやファイルが表示されます。|

## <a name="BKMK_examples"></a>例

ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)