---
title: Azure の仮想ネットワーク統合
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7d38505-cff5-4f15-9fd5-ae6dba15ce88
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 673cb5a2292bab113aefb1de37f80bf4d880b467
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433907"
---
# <a name="azure-virtual-network-integration"></a>Azure の仮想ネットワーク統合

>適用先:Windows Server 2016 Essentials

組織にクラウド コンピューティングの方法と、ことはほとんどありませんが、移動すべてのリソース 100% 一度に 1 つがではなく、一部のリソースは、クラウドとオンプレミスでもいくつかのアプローチを実行します。 このハイブリッド アプローチにより、組織だけでなく、クラウドにいくつかのコンピューティング リソースを移動するが、新しいハードウェアを取得することがなく、IT インフラストラクチャを拡張することができます。

コンピューティングには、このハイブリッド アプローチを実装すると、シームレスな方法は、両方の場所のリソースで互いと通信する必要があります。 Azure の仮想ネットワークは、組織は、ポイント ツー ポイント (P2P) を作成できるようにする Azure のサービスまたはサイト間 (S2S) 仮想プライベート ネットワークのように参照してください (仮想マシン記憶域など) は Azure で実行されているリソースをシームレスなアプリケーションとリソースのアクセスをローカル ネットワーク。

Azure Virtual network の構成は複雑になることができます。 Windows Server Essentials 2016 では、ネットワーク環境に最も適切な既定値を選択するのに役立つ簡単なウィザードを介して Azure 仮想ネットワークに簡単に構成できます。 Azure 仮想ネットワークの導入し、の統合を開始するためのクイック リンクを提供する Windows Essentials ダッシュ ボードの Microsoft クラウド サービスのセクションに新しい Azure の仮想ネットワーク統合タスクが追加されて次のスクリーン ショットに示すように、.

![Windows Server Essentials ダッシュ ボードのホーム ページで、[概要] タブを示すスクリーン ショット。 [概要] タブの [サービス] を選択すると Azure Virtual network が現在無効になっている Microsoft クラウド サービスの統合サービスでダッシュ ボードを示します。](media/azure-virtual-network-1.PNG)

クリックすると、**今すぐ統合**、上記のスクリーン ショットでの Azure 仮想ネットワークのリンクと、Microsoft Azure アカウントにログインするように求めるダイアログ ボックスが表示されます。 Microsoft Azure アカウントがない、この画面は、Azure アカウントのサインアップ ポータルにリダイレクトする、1 つのオプションをサインアップする必要があります。

![統合と Azure の仮想ネットワークのウィザードの Microsoft Azure にサインイン ページを示すスクリーン ショット。](media/azure-virtual-network-2.PNG)

いったんサインインすると azure が表示されます関連付ける Azure の仮想にサブスクリプションを選択するオプションを使用してサービスのネットワークします。

![Azure の仮想ネットワークのウィザードとの統合の個人用の Microsoft Azure サブスクリプション ページを示すスクリーン ショット。](media/azure-virtual-network-3.PNG)

1 回の Azure 仮想ネットワークで使用する Azure サブスクリプションは、新しい Azure の仮想ネットワークを作成するオプションが表示されますまたはいずれかが既にこのサブスクリプションのセットアップ、入手可能になったドロップダウン ボックスが表示するを選択しました。 ローカル ネットワーク内のリソースを識別するために Azure Virtual network を使用するローカル ネットワークの名前を選択することもされます。 最後は、Azure の仮想ネットワークをホストする必要がある Azure リージョンを選択します。 物理的に、ローカル ネットワークに最も近い場所を選択するが、Azure サービスではホストのリソースと通信するための帯域速度を最適化するために通常最適です。

![統合と Azure の仮想ネットワークのウィザードの設定を Azure 仮想ネットワーク ページを示すスクリーン ショット。](media/azure-virtual-network-4.PNG)

統合プロセスの最後の手順、S2S VPN 接続のために使用する VPN デバイスをセットアップすることです。 ほとんどの小規模企業が、環境内でいくつかのサーバーのみがある、Microsoft Azure に接続する VPN ルーターを適切に構成する IT スタッフがないので、既定の選択はリソースする VPN サーバーとして Windows Server Essentials サーバーをセットアップします。ローカル ネットワークでは、Azure の仮想ネットワーク内のリソースにアクセスするために接続します。 ただし、VPN サーバーとして、環境内で別のサーバーを使用するものではなく、または VPN ルーターを使用するようではなく、これらのオプションを選択できます。

ルーターの種類とモデルのバリエーションにより、Windows Server Essentials が VPN ルーターを自動的に構成する試みません。 この統合ウィザードで、VPN ルーターを選択すると、接続に必要な Azure での適切なルーティング構成のデバイスの種類の Azure 仮想ネットワークのみに通知します。

統合ウィザードを完了すると、新しいタブが Azure 仮想ネットワークの Windows Server Essentials ダッシュ ボードに表示されます。

![Windows Server Essentials ダッシュ ボードの Azure VNet のページを示すスクリーン ショット。 Azure の仮想ネットワーク タブが選択され、構成と状態が表示されます。](media/azure-virtual-network-5.PNG)

>!クラウドでの Azure 仮想ネットワークの構成を完了するメモには、30 分の上に長い時間がかかります。 この期間中、構成の状態は、ダッシュ ボードの Azure 仮想ネットワークの状態 ページで表示にされます。

Azure Virtual network の構成が完了すると、状態は Connected に変更され、入力/出力データ、ゲートウェイの IP アドレス、ローカルの IP アドレスとアカウントの詳細など、Azure Virtual network の詳細が表示されます。

![Windows Server Essentials ダッシュ ボードの Azure VNet のページを示すスクリーン ショット。 Azure の仮想ネットワーク] タブが選択されているし、接続状態が表示され、この状態情報 [仮想ネットワークの詳細が表示されます。](media/azure-virtual-network-6.PNG)

ダッシュ ボードの右側にある [タスク] ウィンドウで、さまざまなタスクのために実行できる Azure 仮想ネットワークでです。

-   **Azure VNET から切断**Azure Virtual network をセットアップは無料、ですが、オンプレミスと Azure での他の Vnet に接続する VPN gateway の料金が発生します。 Azure VNET から切断するには、すべての課金が停止します。

-   **VPN デバイスを切り替える**VPN サーバーから VPN ルーターに変更することこのタスクは有効にするスイッチを作成および Azure VNET に通知することです。

-   **Azure VNET を構成する**このタスクでは、Azure VNET の Azure portal の構成 ページにリダイレクトして、Azure VNET の高度な構成オプションを変更することができます。

-   **ステータスの更新**入力/出力データを含む Azure VNET の接続状態を更新する [状態] ページを更新します。

-   **Azure VNET の統合を無効にする**Azure VNET の接続を切断し、Windows Server Essentials ダッシュ ボードからの統合を削除します。 この Azure VNET は削除されません、Azure では、後で、ダッシュ ボードと Azure VNET を再統合する場合は、設定が保持も注意してください。

-   **詳細については、Azure VNET は** [ https://azure.microsoft.com/services/virtual-network/](https://azure.microsoft.com/services/virtual-network/)します。

<a name="see-also"></a>関連項目
--------
[Windows Server Essentials の概要](get-started.md)
