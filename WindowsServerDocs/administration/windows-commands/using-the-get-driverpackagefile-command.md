---
title: get DriverPackageFile
description: ドライバーパッケージについての情報を表示する get DriverPackageFile のリファレンストピック。これには、ドライバーパッケージに含まれるドライバーとファイルが含まれます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f01a2c67-7e9c-4aad-b625-383f5a1fca25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71fc38e31471a1deb9d6be29b04d3cd911be1bd6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719932"
---
# <a name="get-driverpackagefile"></a>get DriverPackageFile

ドライバーが含まれているファイルを含むドライバー パッケージについての情報を表示します。

## <a name="syntax"></a>構文

```
WDSUTIL /Get-DriverPackageFile /InfFile:<Inf File path> [/Architecture:{x86 | ia64 | x64}] [/Show:{Drivers | Files | All}]
```

### <a name="parameters"></a>パラメーター

|         パラメーター         |                              [説明]                               |
|---------------------------|------------------------------------------------------------------------|
| /Inffile:\<Inf ファイルのパス> | ドライバー パッケージの .inf ファイルの完全パスとファイル名を指定します。 |
|    [/アーキテクチャ: {x86    |                                  ia64                                  |
|     [/Show: {Drivers      |                                 ファイル                                  |

## <a name="examples"></a>例

ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-DriverPackageFile /InfFile:C:\temp\1394.inf /Architecture:x86
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)