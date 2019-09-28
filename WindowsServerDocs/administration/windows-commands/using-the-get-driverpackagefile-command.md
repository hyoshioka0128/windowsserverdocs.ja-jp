---
title: Get DriverPackageFile コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 21bbe17e56177da5cd2c1bf83c712d256cc794c8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363153"
---
# <a name="using-the-get-driverpackagefile-command"></a>Get DriverPackageFile コマンドを使用してください。



ドライバーが含まれているファイルを含むドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

## <a name="parameters"></a>パラメーター

|         パラメーター         |                              説明                               |
|---------------------------|------------------------------------------------------------------------|
| /Inffile: \<Inf ファイルのパス > | ドライバー パッケージの .inf ファイルの完全パスとファイル名を指定します。 |
|    [/アーキテクチャ: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 ファイル                                  |

## <a name="BKMK_examples"></a>例

ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-DriverPackageFile /InfFile:"C:\temp\1394.inf" /Architecture:x86
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)