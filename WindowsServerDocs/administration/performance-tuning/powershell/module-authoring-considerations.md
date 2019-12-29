---
title: PowerShell モジュールの作成に関する考慮事項
description: PowerShell モジュールの作成に関する考慮事項
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 8945339e7a7950d3cd722ab2af629b45e7f6dd5d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370359"
---
# <a name="powershell-module-authoring-considerations"></a>PowerShell モジュールの作成に関する考慮事項

このドキュメントには、最適なパフォーマンスを得るためにモジュールを作成する方法に関連するガイドラインがいくつか含まれています。

## <a name="module-manifest-authoring"></a>モジュールマニフェストの作成

次のガイドラインを使用しないモジュールマニフェストは、セッションでモジュールが使用されていない場合でも、一般的な PowerShell のパフォーマンスに大きな影響を与える可能性があります。

コマンドの自動検出では、各モジュールを分析して、モジュールがエクスポートするコマンドと、この分析に負荷がかかる可能性のあるコマンドを決定します。
モジュール分析の結果はユーザーごとにキャッシュされますが、最初の実行時にはキャッシュを使用できません。これは、コンテナーを使用した一般的なシナリオです。
モジュール分析中に、エクスポートされたコマンドをマニフェストから完全に判別できる場合は、そのモジュールの負荷の高い分析を回避できます。

### <a name="guidelines"></a>ガイドライン

* モジュールマニフェストでは、`AliasesToExport`、`CmdletsToExport`、`FunctionsToExport` の各エントリにワイルドカードを使用しないでください。

* モジュールが特定の種類のコマンドをエクスポートしない場合は、`@()` を指定することにより、マニフェストで明示的に指定します。
Missing または `$null` のエントリは、ワイルドカード `*` を指定した場合と同じです。

可能な限り、次のことを避ける必要があります。

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

## <a name="avoid-cdxml"></a>CDXML を避ける

モジュールを実装する方法を決定する際には、主に次の3つの選択肢があります。

* バイナリ (通常C#は)
* スクリプト (PowerShell)
* CDXML (CIM をラップする XML ファイル)

モジュールの読み込み速度が重要である場合、CDXML の次数は、バイナリモジュールよりもはるかに遅くなります。

バイナリモジュールは、事前にコンパイルされていて、NGen を使用してコンピューターごとに1回 JIT コンパイルできるため、最速のを読み込みます。

スクリプトモジュールの読み込みは、通常、バイナリモジュールよりも少し遅くなります。 PowerShell では、スクリプトをコンパイルして実行する前に解析する必要があるためです。

通常、CDXML モジュールは、スクリプトモジュールよりはるかに低速です。そのため、最初に XML ファイルを解析する必要があります。その後、解析とコンパイルが行われる PowerShell スクリプトが大量に生成されます。

