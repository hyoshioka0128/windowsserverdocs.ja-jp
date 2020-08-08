---
title: Windows Server 2008 を実行し、動的メモリで構成された仮想マシンでは、メモリ設定に推奨値を使用する必要があります。
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: f4c05a2c-52d0-4fa2-987d-37a6ed667134
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 4fa6821e0fc4b26e697ad821be2eeb53d41da163
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946116"
---
# <a name="a-virtual-machine-running-windows-server-2008-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Windows Server 2008 を実行し、動的メモリで構成された仮想マシンでは、メモリ設定に推奨値を使用する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*1つまたは複数の仮想マシンが動的メモリを使用するように構成されていますが、Windows Server 2008 で推奨されるメモリ量よりも少なくなっています。*

## <a name="impact"></a>影響
*次の仮想マシン上のゲストオペレーティングシステムが実行されていないか、または信頼性の高い動作をしていない可能性があります。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*Hyper-v マネージャーまたは Windows PowerShell を使用して、最小メモリを 256 MB 以上、起動メモリと最大メモリを 512 MB 以上に増やします。*

#### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やす

1.  Hyper-V マネージャーを開きます。 (サーバーマネージャーから、[**ツール**  >  ] をクリックします。**Hyper-v マネージャー**)

2.  仮想マシンの一覧から目的のものを右クリックし、[**設定**] をクリックします。

3.  ナビゲーションウィンドウで、[**メモリ**] をクリックします。

4.  **RAM**を 512 MB 以上に変更します。

5.  [**動的メモリ**で、**最小 RAM**を 256 MB 以上、**最大 ram**を 512 mb 以上に変更します。

6.  **[OK]** をクリックします。

### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす

1.  Windows PowerShell を開きます。 (デスクトップから [**スタート**] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  次のようなコマンドを実行します。 MyVM は仮想マシンの名前に、メモリ値は少なくとも以下の値に置き換えてください。

```
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB
```



