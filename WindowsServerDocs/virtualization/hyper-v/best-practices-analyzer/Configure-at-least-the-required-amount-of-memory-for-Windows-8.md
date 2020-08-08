---
title: Windows 8 を実行し、動的メモリに対して有効にする仮想マシンに対して、少なくとも必要なメモリ容量を構成します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 1dab6af6-852f-4243-9600-afe541a0f4cd
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 353acbeae1b7941425258a645f109241e012b87a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971029"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-8-and-enabled-for-dynamic-memory"></a>Windows 8 を実行し、動的メモリに対して有効にする仮想マシンに対して、少なくとも必要なメモリ容量を構成します。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*1つ以上の仮想マシンが、Windows 8 に必要なメモリ容量を下回る動的メモリを使用するように構成されています。*

## <a name="impact"></a>**影響**
*次の仮想マシン上のゲストオペレーティングシステムが実行されていないか、または信頼性の高い動作をしていない可能性があります。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*Hyper-v マネージャーを使用して最小メモリを 256 MB 以上に増やし、起動メモリと最大メモリをこの仮想マシンに対して少なくとも 512 MB に増やします。*

### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やす

1.  Hyper-V マネージャーを開きます。 (サーバーマネージャーから、[**ツール**  >  ] をクリックします。**Hyper-v マネージャー**)

2.  仮想マシンの一覧から目的のものを右クリックし、[**設定**] をクリックします。

3.  ナビゲーションウィンドウで、[**メモリ**] をクリックします。

4.  **RAM**を 512 MB 以上に変更します。

5.  [**動的メモリ**で、**最小 RAM**を 256 mb 以上、 **ram の最大値**を 512 mb に変更します。

6.  **[OK]** をクリックします。

### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす

1.  Windows PowerShell を開きます。 (デスクトップから [**スタート**] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  次のようなコマンドを実行します。 MyVM は仮想マシンの名前に、メモリ値は少なくとも以下の値に置き換えてください。

```
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512 GB -MinimumBytes 256MB -StartupBytes 512MB
```



