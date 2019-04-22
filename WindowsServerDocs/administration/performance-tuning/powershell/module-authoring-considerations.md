---
title: PowerShell モジュールの作成に関する考慮事項
description: PowerShell モジュールの作成に関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 37dd860019b91daf70947dba93d20274048487a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818723"
---
# <a name="powershell-module-authoring-considerations"></a>PowerShell モジュールの作成に関する考慮事項

このドキュメントには、最適なパフォーマンス モジュールを作成する方法に関連するいくつかのガイドラインが含まれています。

## <a name="module-manifest-authoring"></a>モジュール マニフェストの作成

モジュール マニフェストでは、次のガイドラインを使用しない、モジュールがセッションで使用されていない場合でも PowerShell の全般的パフォーマンスの顕著な影響を受けることができます。

コマンドの自動検出では、モジュールがエクスポートして、この分析は、高価なコマンドを判断するには、各モジュールを分析します。
モジュール分析の結果が、ユーザーごとにキャッシュされますが、キャッシュは、コンテナーでの一般的なシナリオは、初回起動時に使用できません。
モジュールの分析中に、エクスポートしたコマンドは、マニフェストから完全に決定できる場合、モジュールのより高価な分析を回避できます。

### <a name="guidelines"></a>ガイドライン

* モジュール マニフェストでワイルドカードを使用しないでで、 `AliasesToExport`、 `CmdletsToExport`、および`FunctionsToExport`エントリ。

* モジュールが特定の種類のコマンドをエクスポートされない場合はこれを明示的に指定マニフェストで指定することによって`@()`します。
存在しないか、`$null`エントリは、ワイルドカードを指定すると同じ`*`します。

次は避ける必要があります可能な場合。

```PowerShell
@{
    FunctionsToExport = '*'

    # Also avoid omitting an entry, it is equivalent to using a wildcard
    # CmdletsToExport = '*'
    # AliasesToExport = '*'
}
```

代わりに、次のように使用します。

```PowerShell
@{
    FunctionsToExport = 'Format-Hex', 'Format-Octal'
    CmdletsToExport = @()  # Specify an empty array, not $null
    AliasesToExport = @()  # Also ensure all three entries are present
}
```

## <a name="avoid-cdxml"></a>CDXML を回避します。

モジュールを実装する方法を決定する際に、次の 3 つの主要な選択肢があります。

* バイナリ (通常はC#)
* スクリプト (PowerShell)
* CDXML (ラッピング CIM XML ファイル)

モジュールの読み込みの速度が重要な場合は、CDXML はほぼ桁違いバイナリ モジュールよりも遅くなります。

事前にコンパイルし、マシンごとに 1 回の JIT コンパイルを NGen を使用できるため、バイナリ モジュールを高速で読み込みます。

スクリプト モジュール通常読み込みますバイナリ モジュールよりも少し時間がかかるため、PowerShell は、コンパイルして、実行する前にスクリプトを解析する必要があります。

CDXML モジュールは、生成し、解析およびコンパイルする PowerShell スクリプトの XML ファイルを解析する必要がありますまずためスクリプト モジュールよりも通常かなり遅くなります。

