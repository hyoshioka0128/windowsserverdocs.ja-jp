---
title: Azure Virtual network の統合
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 92c8241d861e72d5f9f409a334e6edbeed5eae4c
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310573"
---
# <a name="azure-virtual-network-integration"></a>Azure Virtual network の統合

>適用対象: Windows Server 2016 Essentials

組織がクラウドコンピューティングを行う方法を採用するのは、ほとんどの場合、すべてのリソースを一度に100% 移動するだけでなく、一部のリソースがクラウド内にあり、一部がオンプレミスにある場合もあります。 このハイブリッドアプローチにより、組織はコンピューティングリソースをクラウドに簡単に移行できるだけでなく、新しいハードウェアを購入しなくても IT インフラストラクチャを拡張することができます。

このハイブリッドアプローチをコンピューティングに実装する場合は、両方の場所にあるリソースが相互に通信するためのシームレスな方法が必要です。 Azure 仮想ネットワークは、azure で実行されているリソース (仮想マシンやストレージなど) が、次のように表示されるポイントツーポイント (P2P) またはサイト間 (S2S) 仮想プライベートネットワークを作成できるようにする Azure サービスです。アプリケーションとリソースへのシームレスなアクセスを可能にするローカルネットワーク。

Azure 仮想ネットワークの構成は複雑になる可能性があります。 Windows Server Essentials 2016 では、簡単なウィザードを使用して Azure 仮想ネットワークを簡単に構成できます。このウィザードを使用すると、ネットワーク環境に最適な既定値を選択できます。 次のスクリーンショットに示すように、Azure virtual network を導入し、統合を開始するためのクイックリンクを提供するために、Windows Essentials ダッシュボードの [Microsoft Cloud Services] セクションに新しい Azure 仮想ネットワーク統合タスクが追加されました.

![Windows Server Essentials ダッシュボードのホームページにある [作業の開始] タブを示すスクリーンショット。 [作業の開始] タブの [サービス] セクションが選択されています。ダッシュボードは、Azure 仮想ネットワークが現在無効になっている Microsoft Cloud Services 統合の下に表示されます。](media/azure-virtual-network-1.PNG)

上のスクリーンショットの Azure 仮想ネットワークの **[今すぐ統合]** リンクをクリックすると、Microsoft Azure アカウントにログインするよう求めるダイアログボックスが表示されます。 Microsoft Azure アカウントを持っていない場合は、この画面でサインアップするオプションが表示されます。これにより、Azure アカウントのサインアップポータルにリダイレクトされます。

![Azure 仮想ネットワークとの統合ウィザードの [Microsoft Azure へのサインイン] ページを示すスクリーンショット。](media/azure-virtual-network-2.PNG)

Azure にサインインすると、Azure Virtual network サービスに関連付けるサブスクリプションを選択するためのオプションが表示されます。

![Azure 仮想ネットワークとの統合ウィザードの [My Microsoft Azure サブスクリプション] ページを示すスクリーンショット。](media/azure-virtual-network-3.PNG)

Azure 仮想ネットワークに使用する Azure サブスクリプションを選択すると、新しい Azure 仮想ネットワークを作成するためのオプションが表示されます。また、このサブスクリプションに既に設定されている場合は、ドロップダウンボックスに表示されます。 また、Azure 仮想ネットワークがローカルネットワーク内のリソースを識別するために使用するローカルネットワークの名前も選択します。 最後に、Azure 仮想ネットワークをホストする Azure リージョンを選択します。 ローカルネットワークに物理的に近い場所を選択するのは、通常、Azure サービスでホストする可能性のあるリソースと通信するための帯域幅を最適化する場合に最適です。

![Azure 仮想ネットワークとの統合ウィザードの [Azure 仮想ネットワークの設定] ページを示すスクリーンショット。](media/azure-virtual-network-4.PNG)

統合プロセスの最後の手順では、S2S VPN 接続に使用される VPN デバイスを設定します。 ほとんどの小規模企業は環境内に少数のサーバーしかなく、Microsoft Azure に接続するように VPN ルーターを適切に構成する IT スタッフがいないため、既定の選択では、Windows Server Essentials サーバーを、リソースとして使用される VPN サーバーとしてセットアップします。では、Azure 仮想ネットワーク内のリソースにアクセスするために、ローカルネットワークのに接続されます。 ただし、環境内の別のサーバーを VPN サーバーとして使用する場合、または VPN ルーターを使用する場合は、これらのオプションを選択できます。

ルーターの種類とモデルのバリエーションにより、Windows Server Essentials は VPN ルーターの自動構成を試行しません。 この統合ウィザードで VPN ルーターを選択すると、デバイスの種類の Azure 仮想ネットワークに対してのみ、Azure で接続のために必要な適切なルーティング構成が通知されます。

統合ウィザードを完了すると、Azure 仮想ネットワーク用の Windows Server Essentials ダッシュボードに新しいタブが表示されます。

![Windows Server Essentials ダッシュボードの [Azure VNet] ページを示すスクリーンショット。 [Azure Virtual network] タブが選択され、[構成中] という状態が表示されます。](media/azure-virtual-network-5.PNG)

>!注クラウド内の Azure 仮想ネットワークの構成を完了するには、30分を超える時間がかかることがあります。 この間、ダッシュボードの [Azure 仮想ネットワークの状態] ページに、構成の状態が表示されます。

Azure 仮想ネットワークの構成が完了すると、状態が [接続済み] に変わり、Azure 仮想ネットワークの詳細 (入力/出力、ゲートウェイ IP アドレス、ローカル IP アドレス、アカウントの詳細など) が表示されます。

![Windows Server Essentials ダッシュボードの [Azure VNet] ページを示すスクリーンショット。 [Azure Virtual network] タブが選択され、状態が [接続済み] と表示されます。この状態情報には、仮想ネットワークの詳細が表示されます。](media/azure-virtual-network-6.PNG)

ダッシュボードの右側の [タスク] ウィンドウには、Azure 仮想ネットワークで実行できるさまざまなタスクがあります。

-   **AZURE VNET からの切断**Azure 仮想ネットワークのセットアップは無料ですが、オンプレミスと Azure のその他の Vnet に接続する VPN gateway には料金が発生します。 Azure VNET から切断すると、すべての課金が停止します。

-   **VPN デバイスを切り替える**VPN サーバーから VPN ルーターに変更する場合は、このタスクを使用してスイッチを作成し、Azure VNET に通知することができます。

-   **AZURE VNET の構成**このタスクでは、azure vnet の [Azure portal の構成] ページにリダイレクトして、Azure VNET の詳細な構成オプションを変更できます。

-   **更新状態**[状態] ページを更新し、データを含む Azure VNET の接続状態を更新します。

-   **Azure VNET 統合を無効にする**Azure VNET を切断し、Windows Server Essentials ダッシュボードから統合を削除します。 Azure VNET は削除されませんが、後で Azure VNET をダッシュボードに再度統合する場合は、azure に設定が保持されます。

-   **AZURE VNET** [https://azure.microsoft.com/services/virtual-network/](https://azure.microsoft.com/services/virtual-network/)の詳細については、こちらをご覧ください。

<a name="see-also"></a>参照
--------
[Windows Server Essentials の概要](get-started.md)
