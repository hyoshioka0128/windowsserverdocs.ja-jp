---
title: 4つ以下の仮想プロセッサを搭載した Windows 7 を実行する仮想マシンを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8fcf0868-b543-4f94-aee7-35324346da55
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 21c6f9df66b1a537141842bf696a5e286cd05636
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968329"
---
# <a name="configure-virtual-machines-running-windows-7-with-no-more-than-4-virtual-processors"></a>4つ以下の仮想プロセッサを搭載した Windows 7 を実行する仮想マシンを構成する

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
*Windows 7 を実行している仮想マシンは、4つ以上の仮想プロセッサで構成されています。*

## <a name="impact"></a>**影響**
*Microsoft では、次の仮想マシンの構成をサポートしていません。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*仮想マシンをシャットダウンし、1つまたは複数の仮想プロセッサを削除します。*

#### <a name="to-remove-virtual-processors"></a>仮想プロセッサを削除するには

1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。

2.  結果ウィンドウで [ **仮想マシン**, 、構成する仮想マシンを選択します。 バーチャルマシンの状態は [**オフ (オフ**)」と表示されます。 そうでない場合は、バーチャルマシンを右クリックし、[**シャットダウン**] をクリックします。

3.  **[操作]** ウィンドウで、仮想マシン名の下の **[設定]** をクリックします。

4.  ナビゲーションウィンドウで、[**プロセッサ**] をクリックします。

5.  [**プロセッサ**] ページで、プロセッサ数を**3**以下に設定し、[ **OK]** をクリックします。



