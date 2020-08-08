---
title: Windows 7 は、推奨されるメモリ量で構成する必要があります。
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: d77d648c-6e26-43fa-be0a-6eb4b28f9cb4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: e88f2e96c4862cb89caf328546488566ebd96c18
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992626"
---
# <a name="windows-7-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows 7 は、推奨されるメモリ量で構成する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*Windows 7 を実行する仮想マシンは、推奨される RAM 容量 (1 GB) 未満で構成されます。*

## <a name="impact"></a>影響

*ゲストオペレーティングシステムとアプリケーションが正常に動作しない可能性があります。複数のアプリケーションを同時に実行するのに十分なメモリがない可能性があります。これは、次の仮想マシンに影響します。*
```
<list of virtual machine names>
```
## <a name="resolution"></a>解決方法

*HYPER-V マネージャーを使用して、1 GB 以上にするには、この仮想マシンに割り当てるメモリを増やします。*

### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やすには

1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。

2.  結果ウィンドウで [ **仮想マシン**, 、構成する仮想マシンを選択します。 バーチャルマシンの状態は [**オフ (オフ**)」と表示されます。 そうでない場合は、バーチャルマシンを右クリックし、[**シャットダウン**] をクリックします。

3.  **[操作]** ウィンドウで、仮想マシン名の下の **[設定]** をクリックします。

4.  ナビゲーションウィンドウで、[**メモリ**] をクリックします。

5.  [**メモリ**] ページで、**スタートアップ RAM**を 1 GB 以上に設定し、[ **OK]** をクリックします。

### <a name="increase-the-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす

1.  Windows PowerShell を開きます。 (デスクトップから [**スタート**] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  交換した後にこのコマンドを実行 \<MyVM> 、仮想マシンの名前に置き換えます。

```
Set-VMMemory <MyVM> -StartupBytes 1GB
```

## <a name="see-also"></a>参照
[設定-VMMemory](/powershell/module/hyper-v/set-vmmemory?view=win10-ps)