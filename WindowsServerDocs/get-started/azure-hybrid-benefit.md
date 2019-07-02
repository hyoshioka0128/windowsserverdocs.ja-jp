---
title: Windows Server 向け Azure ハイブリッド特典
description: オンプレミスの Windows Server ライセンスを使用して、Azure VM の料金を節約できます
ms.prod: windows-server
ms.date: 11/10/2017
ms.technology: server-general
ms.topic: article
author: greg-lindsay
ms.author: greg-lindsay
ms.localizationpriority: high
ms.openlocfilehash: 62821abc6c9eec660fa6af832bb1aba151708021
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63686444"
---
# <a name="azure-hybrid-benefit-for-windows-server"></a>Windows Server 向け Azure ハイブリッド特典

>適用先:Windows Server

## <a name="benefit-description-rules-and-use-cases"></a>特典の説明、ルール、使用事例

Windows Server 向け Azure ハイブリッド特典を利用すると、オンプレミスのソフトウェア アシュアランス付き Windows Server ライセンスを使用して、Azure で Windows Server VM のコストを最大 40% 節減できます。  この特典では、Windows Server のライセンス料金がソフトウェア アシュアランス特典でカバーされるため、お客様が支払うのは仮想マシンの基本コンピューティング料金のみです。  この特典は、Windows Server 2008R2、2012、2012R2、2016 リリースの Standard エディションと Datacenter エディションの両方に適用されます。  この特典は、すべての地域とソブリン クラウドで利用できます。


![画像 1](media/ahb01.png)

この特典は、アクティブなソフトウェア アシュアランスまたは EAS、SCE サブスクリプション、Open Value Subscription などのサブスクリプション ライセンスの付いた Windows Server ライセンスを持つすべてのお客様にご利用いただけます。  

アクティブな SA/サブスクリプション付きの Windows Server の 2 プロセッサ ライセンス、および SA/サブスクリプション付きの Windows Server の 16 コア ライセンス セットごとに、最大 16 個の仮想コアを最大 2 台の Azure ベース インスタンス (仮想マシン) に割り当てて、Microsoft Azure で Windows Server を使用できます。 SA/サブスクリプション付きの 8 コア ライセンスの追加セットごとに、最大 8 個の仮想コアと 1 台のベース インスタンス (VM) を使用できます。

| SA/サブスクリプション付きのライセンス            | 付与される VM およびコア            | 使用方法                                |
|-----------------------------------------|----------------------------------|-----------------------------------------------------|
| WS Datacenter (16 コアまたは 2 プロセッサ ライセンス)  | 最大 2 台の VM および最大 16 個のコア | オンプレミスと Azure 内の両方で仮想マシンを実行  |
| WS Standard (16 コアまたは 2 プロセッサ ライセンス)    | 最大 2 台の VM および最大 16 個のコア | オンプレミスまたは Azure 内のいずれかで仮想マシンを実行 |

Azure ハイブリッド特典を利用した VM は、SA/サブスクリプション期間中のみ Azure で実行できます。 SA/サブスクリプションの有効期限が近づいた場合、お客様は、SA/サブスクリプションを更新するか、その VM のハイブリッド特典機能をオフにするか、ハイブリッド特典を使用してその VM をプロビジョニング解除するかを選択できます。 

### <a name="savings-examples"></a>節約額の例 

![画像 2](media/ahb02.png)
 
次の参照テーブルでは、特典のルールをさらに詳しく示します。 緑の列は同じ種類の VM の数を示し、青の行は各 VM のコア密度を示します。 黄色のセルは、特定のコア密度で特定の数の VM をデプロイするために必要な 2 プロセッサ ライセンス (または 16 コアのセット) の数を示します。 

SA 付き Windows Server 要件参照テーブル:

![画像 3](media/ahb03.png)
 
Windows Server 向け Azure ハイブリッド特典は、ニーズに応じた構成での実行や、さまざまな種類の VM の組み合わせに対応する優れた柔軟性を備えています。

さまざまなライセンス位置を使用した構成例

![画像 4](media/ahb04.png)
![画像 5](media/ahb05.png)

 
Windows Server 向け Azure ハイブリッド特典の詳細については、Azure ハイブリッド特典 の Web サイトを参照してください。

## <a name="how-to-maintain-compliance"></a>ライセンス要件への準拠を維持する方法

お客様が Windows Server の VM に Azure ハイブリッド特典を適用する場合、この特典をライセンス認証する前に、使用可能なライセンスの数と、SA/サブスクリプションのそれぞれの保証期間を確認したうえで、上記のガイドラインを適用して適切な数の VM に特典をデプロイする必要があります。 既に Azure ハイブリッド特典を使用して VM を実行している場合は、インベントリを実行して稼働ユニット数を確認し、保有するアクティブな SA ライセンスの数に照らしてチェックする必要があります。  ご使用中の SA ライセンス位置については、Microsoft Enterprise Agreement のライセンス専門家にお問い合わせください。
サブスクリプションで Windows Server 向け Azure ハイブリッド特典を使用してデプロイされたすべての仮想マシンを表示し、数を確認するには、次のいずれかの操作を行います。

1. Microsoft Azure Portal を構成して、Windows Server 向け Azure ハイブリッド特典の利用状況を表示します。Microsoft Azure Portal で仮想マシン セクションのリスト ビューに、“Azure Hybrid Benefit” 列を追加します。 

    ![画像 6](media/ahb06.png)

2.  PowerShell を使用して、Windows Server 向け Azure ハイブリッド特典の利用状況を一覧表示します。

    ```
    $vms = Get-AzureRMVM 
    foreach ($vm in $vms) {"VM Name: " + $vm.Name, "   Azure Hybrid Benefit for Windows Server: "+ $vm.LicenseType}
    ```

3.  Microsoft Azure の請求書で、Windows Server 向け Azure ハイブリッド特典を使用して実行している仮想マシンの数を確認します。 特典を使用したインスタンスの数に関する情報は、[追加情報] の下に表示されています。

    ```
    "{"ImageType":"WindowsServerBYOL","ServiceType":"Standard_A1","VMName":"","UsageType":"ComputeHR"}" 
    ```

情報は請求書にリアルタイムで反映されるわけではなく、ハイブリッド特典を使用して VM をアクティブ化してから請求書に表示されるまでに数時間の遅れがあります。
次に、下の **Azure Hybrid Benefit for Windows Server SA Count Tool** に結果を入力して、必要な SA またはサブスクリプションが適用される WS ライセンスの数を算出します。

所有する各サブスクリプションでインベントリを実行して、すべてのライセンス位置を包括的に把握してください。

[Azure Hybrid Benefit WS SA Count Tool](http://download.microsoft.com/download/7/1/2/712FEFF0-155C-4ABF-96C0-CE4EC4DB0516/Azure_Hybrid_Benefit_Windows_Server_SA_Count_Tool.xlsx)

上の操作を行った結果、実行中の Azure ハイブリッド特典インスタンス数に対応する十分なライセンスがあることが確認された場合、それ以上の作業は必要ありません。 特典を適用できる VM の数に余裕があることがわかった場合、現在、全額が課金されている実行中のインスタンスを特典利用に切り替えることで、料金をさらに最適化できます。

既にデプロイ済みの VM に対する十分な Windows Server ライセンスがない場合、下に示すいずれかのチャネルを介して、ソフトウェア アシュアランスが適用される追加の Windows Server オンプレミス ライセンスを購入するか、通常の時間単位の料金で Windows Server VM を購入するか、一部の VM でハイブリッド特典機能をオフにする必要があります。 コア ライセンスは、8 コア単位で購入して、Azure ハイブリッド特典の対象 VM を追加することができます。 

Windows Server のソフトウェア アシュアランスやサブスクリプションは、以下のマイクロソフトのライセンス チャネルを組み合わせて購入できます。

| Channel                      | Open     | OVS      | Select/ Select Plus  | MPSA       | EA/EAS   |
|------------------------------|----------|----------|-----------------------|-----------|----------|
| 一般的なサイズ (デバイス数)  | 5 ～ 250    | 5 ～ 250    | >250                  | >250      | >500     |
| SA/サブスクリプション            | 省略可能 | 含まれる | 省略可能              | 省略可能  | 含まれる |

マイクロソフトは、Azure ハイブリッド特典の使用の適格性を確認するために、随時、エンド カスタマーを監査する権利を留保します。 

## <a name="deployment-guidance"></a>デプロイの手引き 

マイクロソフトでは、対象のライセンスを持つすべてのお客様に対し、ライセンスの購入場所に関係なく、構築済みのギャラリー イメージを提供しています。またパートナー様は、お客様に代わってデプロイを実行できます。 

利用可能なすべてのデプロイ オプションについては、[ここ](https://azure.microsoft.com/pricing/hybrid-use-benefit/)をクリックして、次の資料を参照してください。 
-   構築済みのギャラリー イメージを利用した新しいデプロイ エクスペリエンスの詳細についてのビデオ
-   カスタム ビルドされた VM のアップロード方法についての詳細な説明 
-   Azure Site Recovery で PowerShell を使用して、既存の仮想マシンを移行する方法についての詳細な説明 
