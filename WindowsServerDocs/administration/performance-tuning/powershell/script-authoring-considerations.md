---
title: PowerShell スクリプトのパフォーマンスに関する考慮事項
description: PowerShell でのパフォーマンスのスクリプト作成
ms.topic: article
ms.author: jasonsh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: f5ab7fbb1c993192f4626935d2adb73fc9401250
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896257"
---
# <a name="powershell-scripting-performance-considerations"></a>PowerShell スクリプトのパフォーマンスに関する考慮事項

.NET を直接利用してパイプラインを回避する PowerShell スクリプトは、慣用的な PowerShell よりも高速になる傾向があります。 慣用的な PowerShell は、通常、コマンドレットと PowerShell 関数を頻繁に使用します。多くの場合、パイプラインを利用し、必要な場合にのみ .NET にドロップします。

>[!Note]
> ここで説明する手法の多くは、PowerShell の慣用的なではないため、PowerShell スクリプトの読みやすさが低下する可能性があります。 スクリプト作成者は、それ以外の場合は、慣用的な PowerShell を使用することをお勧めします。

## <a name="suppressing-output"></a>出力の抑制

パイプラインへのオブジェクトの書き込みを回避するには、さまざまな方法があります。

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

への割り当て `$null` またはへのキャスト `[void]` はほぼ同じであり、通常はパフォーマンスが重要な場合に推奨されます。

```PowerShell
$arrayList.Add($item) > $null
```

へのファイルのリダイレクト `$null` は、前の方法とほとんど同じですが、ほとんどのスクリプトでは違いがわかりません。
このシナリオによっては、ファイルのリダイレクトによって若干のオーバーヘッドが生じます。

```PowerShell
$arrayList.Add($item) | Out-Null
```

パイプを別の方法と `Out-Null` 比較すると、大きなオーバーヘッドが発生します。
パフォーマンスに影響するコードでは、これを回避する必要があります。

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

スクリプトブロックを導入して (ドットソーシングまたはそれ以外の方法を使用して) 呼び出し、その結果をに割り当てること `$null` は、スクリプトの大きなブロックの出力を抑制するための便利な手法です。
この手法は、にパイプを使用して実行 `Out-Null` されるため、パフォーマンスに影響するスクリプトでは回避する必要があります。
この例の追加のオーバーヘッドは、以前インラインスクリプトであったスクリプトブロックを作成して呼び出すことから取得されます。


## <a name="array-addition"></a>配列の加算

多くの場合、項目のリストを生成するには、加算演算子を使用した配列を使用します。

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

配列は不変であるため、これは非常に inefficent になる可能性があります。
配列に追加するたびに、左側と右の両方のオペランドのすべての要素を保持するために十分な大きさの新しい配列が作成され、その後、両方のオペランドの要素が新しい配列にコピーされます。
小さいコレクションの場合、このオーバーヘッドは問題にならない可能性があります。
大規模なコレクションの場合、これは明らかに問題になる可能性があります。

代替手段がいくつかあります。
実際に配列を必要としない場合は、代わりに ArrayList を使用することを検討してください。

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

配列が必要な場合は、独自のを使用して、 `ArrayList` `ArrayList.ToArray` 配列が必要なときにを呼び出すだけで済みます。
または、PowerShell でとを作成することもでき `ArrayList` `Array` ます。

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

この例では、PowerShell によって、 `ArrayList` 配列式内のパイプラインに書き込まれた結果を保持するが作成されます。
をに割り当てる直前に、 `$results` PowerShell はをに変換し `ArrayList` `object[]` ます。

## <a name="processing-large-files"></a>大きなファイルの処理

PowerShell でファイルを処理する慣用的なの方法は、次のようになります。

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

これは、.NET Api を直接使用するよりもはるかに低い順序で実行できます。

```PowerShell
try
{
    $stream = [System.IO.StreamReader]::new($path)
    while ($line = $stream.ReadLine())
    {
        if ($line.Length -gt 10)
        {
            $line
        }
    }
}
finally
{
    $stream.Dispose()
}
```

## <a name="avoid-write-host"></a>書き込みホストを避ける

一般に、出力をコンソールに直接書き込むことは不適切であると考えられますが、意味がある場合は、多くのスクリプトでが使用さ `Write-Host` れます。

多くのメッセージをコンソールに書き込む必要がある場合は、 `Write-Host` よりもはるかに低い順序にすることができ `[Console]::WriteLine()` ます。 ただし、 `[Console]::WriteLine()` は powershell.exe や powershell_ise.exe などの特定のホストに適した代替手段であることに注意してください。すべてのホストで動作する保証はありません。

を使用する代わり `Write-Host` に、[書き込み出力](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1)の使用を検討してください。

