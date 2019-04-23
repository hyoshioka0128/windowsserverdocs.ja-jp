---
title: PowerShell スクリプトのパフォーマンスに関する考慮事項
description: PowerShell でのパフォーマンスについての説明
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: JasonSh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: df406c7e382907ca32006ec4dae6537a140a91cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830373"
---
# <a name="powershell-scripting-performance-considerations"></a>PowerShell スクリプトのパフォーマンスに関する考慮事項

.NET を直接活用して、パイプラインを回避する PowerShell スクリプトは、慣用 PowerShell よりも高速にする傾向があります。 慣用 PowerShell は、通常、コマンドレットを使用し、PowerShell 関数、パイプラインを利用し、ドロップダウン表示に必要な場合にのみ .NET 頻度の高い、多くの場合、します。

>[!Note] 
> ここで説明した手法の多くは、慣用 PowerShell ではないと、PowerShell スクリプトの読みやすさを減らすことができます。 スクリプトの作成者はパフォーマンスがそれ以外の場合に指定しない限り、慣用 PowerShell を使用することをお勧めします。

## <a name="suppressing-output"></a>出力を抑制します。

オブジェクトをパイプラインに書き込まれないようにする多くの方法はあります。

```PowerShell
$null = $arrayList.Add($item)
[void]$arrayList.Add($item)
```

割り当てを`$null`をキャストまたは`[void]`はほぼ同等ですし、パフォーマンスが重要な優先一般にする必要があります。

```PowerShell
$arrayList.Add($item) > $null
```

ファイルにリダイレクト`$null`ほぼ同程度前の代替手段として最もスクリプトに違いがわかることはありません。
シナリオによってはのファイルのリダイレクトは、多少のオーバーヘッドをただしに紹介します。

```PowerShell
$arrayList.Add($item) | Out-Null
```

パイプ`Out-Null`選択肢を比較した場合に大幅なオーバーヘッドが発生します。
これは、パフォーマンスの重要なコードで回避する必要があります。

```PowerShell
$null = . {
    $arrayList.Add($item)
    $arrayList.Add(42)
}
```

スクリプト ブロックの概要と、呼び出し (ソーシングまたはそれ以外の場合、ドットを使用して) に結果を代入し、`$null`は、大きなブロック スクリプトの出力を抑制するための便利な手法です。
この手法を実行するパイプ処理とほぼ`Out-Null`と機密性の高いスクリプトのパフォーマンスに避ける必要があります。
この例では余分なオーバーヘッドの作成と、スクリプト ブロックされていたインライン スクリプトを呼び出すことに由来します。


## <a name="array-addition"></a>配列の追加

項目のリストを生成するときは多くの場合、加算演算子を含む配列を使用します。

```PowerShell
$results = @()
$results += Do-Something
$results += Do-SomethingElse
$results
```

配列は変更できないために、非常に inefficent ができます。
配列に追加されるたびには実際には左右両方のオペランドのすべての要素を保持するために十分な大きさの新しい配列を作成し、両方のオペランドの要素を新しい配列にコピーします。
小規模なコレクション、このオーバーヘッドは問題になりません。
大きなコレクションは、問題を明らかにこのことができます。

いくつかの選択肢があります。
配列が実際に必要なしない場合は、代わりに ArrayList の使用を検討してください。

```PowerShell
$results = [System.Collections.ArrayList]::new()
$results.AddRange((Do-Something))
$results.AddRange((Do-SomethingElse))
$results
```

配列が必要な場合は使用する独自`ArrayList`を呼び出すだけで、`ArrayList.ToArray`配列の場合します。
または、PowerShell の作成をさせることができます、`ArrayList`と`Array`できます。

```PowerShell
$results = @(
    Do-Something
    Do-SomethingElse
)
```

この例では PowerShell を作成、`ArrayList`配列式の内部でパイプラインに書き込まれた結果を保持します。
代入する前に`$results`、PowerShell によって変換されます、`ArrayList`を`object[]`します。

## <a name="processing-large-files"></a>大きなファイルの処理

PowerShell でのファイルを処理するための慣用方法はようになります可能性があります。

```PowerShell
Get-Content $path | Where-Object { $_.Length -gt 10 }
```

これはほぼ桁違い .NET Api を直接使用するよりも低速になります。

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

## <a name="avoid-write-host"></a>Write-host を避ける

一般に、コンソールに直接出力を記述することを不適切と見なされますが、多くのスクリプトを使用して検出するときに、`Write-Host`します。

場合は、コンソールに多数のメッセージを記述する必要があります`Write-Host`桁よりも低速にすることができます`[Console]::WriteLine()`します。 ただし、注意を`[Console]::WriteLine()`適切な代替のみは、特定のホストなどの powershell.exe または powershell_ise.exe - すべてのホストで作業とは限りません。

使用する代わりに`Write-Host`、使用を検討して[Write-output](/powershell/module/Microsoft.PowerShell.Utility/Write-Output?view=powershell-5.1)します。

