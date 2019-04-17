---
title: "Azure の仮想ネットワークの統合"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 21057359967c73d8d9fc434694b8f203ad5c1f6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
#<a name="azure-virtual-network-integration"></a>Azure の仮想ネットワークの統合

>Windows Server 2016 Essentials の適用対象:

組織にクラウド コンピューティングの方法と、ほとんどありませんが、すべてのリソースの 100% 一度に移動しますが、ではなく、クラウド内のいくつかのリソースが内部設置型上に残っているいくつか方法。 このハイブリッド手法は簡単にするだけでなく、組織がクラウドにいくつかのコンピューティング リソースを移動が、新しいハードウェアを入手することがなく、IT インフラストラクチャを拡張することもできます。

コンピューティングするには、このハイブリッド アプローチを実装するには、相互に通信するために両方の場所のリソースにシームレスな方法が必要です。 Azure の仮想ネットワークは、組織 point-to-point (P2P) を作成できる Azure サービスまたはサイト間 (S2S) 仮想プライベート ネットワークをシームレスなアプリケーションとリソースのアクセスをローカル ネットワーク上にあるものとして Azure (バーチャル マシンと記憶域) などの場所で実行されているリソースです。

Azure の仮想ネットワークの構成は複雑になることができます。 Windows Server Essentials 2016 でネットワークに接続された環境に最も適切な既定値を選択するのに役立つ簡単なウィザードを通じて、Azure の仮想ネットワークを簡単に構成できます。 次のスクリーン ショットのように、新しい Azure の仮想ネットワークの統合タスクが Azure の仮想ネットワークを導入するだけでなく統合を開始するクイック リンクを提供する Windows Essentials ダッシュ ボードの Microsoft クラウド サービス] セクションに追加されました。

![Windows Server Essentials ダッシュ ボードのホーム ページで、[概要] タブを示すスクリーン ショット。 [概要] タブの [サービス] が選択されているし、Azure の仮想ネットワークが現在無効になっている Microsoft クラウド サービスの統合サービスで、ダッシュ ボードを示します。](media/azure-virtual-network-1.PNG)

クリックすると、**統合できるようになりました**Azure の仮想ネットワーク、上記のスクリーン ショットのためのリンク、Microsoft Azure アカウントにログインするように要求する] ダイアログ ボックスが表示されます。 Microsoft Azure アカウントを持っていない場合は、この画面では、Azure アカウントのサインアップ ポータルにリダイレクトする 1 つにサインアップするオプションがあります。

![ログ内に Microsoft Azure ウィザードのページを統合すると Azure 仮想ネットワークを示すスクリーン ショット。](media/azure-virtual-network-2.PNG)

後にサインイン Azure、表示され、Azure 仮想に関連付けるサブスクリプションを選択するオプションを使用してネットワーク サービス。

![Azure の仮想ネットワーク ウィザードを使用して統合の自分の Microsoft Azure サブスクリプション] ページを示すスクリーン ショット。](media/azure-virtual-network-3.PNG)

1 回、どの Azure サブスクリプションを Azure の仮想ネットワークでは、使用する場合、新しい Azure の仮想ネットワークを作成するオプションが表示されますまたは場合いずれかの既にセットアップされているこのサブスクリプションの下で、ドロップダウン ボックスが表示される利用可能なを選択しました。 また、ローカル ネットワーク上のリソースを識別する、Azure の仮想ネットワークが使用するローカル ネットワークの名前を選択します。 最後は、Azure の仮想ネットワークをホストする場合、どの Azure 地域を選択します。 ローカル ネットワークの最も近い物理的な場所の選択がリソースの Azure サービスではホストと通信するための帯域速度を最適化するため通常最適です。

![統合することで Azure 仮想ネットワークのウィザードの設定を Azure 仮想ネットワーク] ページを示すスクリーン ショット。](media/azure-virtual-network-4.PNG)

統合のプロセスの最後の手順では、S2S VPN 接続に使用される VPN デバイスを設定します。 ほとんどの小規模企業、環境内でいくつかのサーバーのみがある、Microsoft Azure に接続する VPN ルーターを正しく構成する IT スタッフが不足しているため、既定の選択は、Azure の仮想ネットワークのリソースにアクセスするために、ローカル ネットワーク内のリソースに接続する VPN サーバーとして Windows Server Essentials サーバーをセットアップするされます。 ただし場合は、VPN サーバーとして、環境内で別のサーバーを使用することではなく、または VPN ルーターを使用ではなく、これらのオプションを選択できます。

により、バリエーション ルーターの種類とモデルでは、Windows Server Essentials しようとしません VPN ルーターを自動的に構成します。 この統合ウィザードで、VPN ルーターを選択すると、Azure での接続に必要なルーティング構成の適切なデバイスの種類の Azure の仮想ネットワークのみに通知します。

統合ウィザードを完了すると、新しいタブが Azure の仮想ネットワークの Windows Server Essentials ダッシュ ボードに表示されます。

![Windows Server Essentials ダッシュ ボードの Azure VNet] ページを示すスクリーン ショット。 Azure の仮想ネットワーク] タブが選択されているし、構成と状態が表示します。](media/azure-virtual-network-5.PNG)

>!クラウドでの Azure の仮想ネットワークの構成を完了するメモには、30 分の上に長い時間がかかります。 この間、構成の状態は、Azure 仮想ネットワークの状態] ページで、ダッシュ ボードの表示になります。

Azure の仮想ネットワークの構成を完了すると、ステータスが接続済みに変更し、データ入力/出力、ゲートウェイの IP アドレス、ローカル IP アドレスとアカウントの詳細など、Azure の仮想ネットワークの詳細を表示します。

![Windows Server Essentials ダッシュ ボードの Azure VNet] ページを示すスクリーン ショット。 Azure の仮想ネットワーク] タブが選択されていて、接続状態が表示され、このステータス情報の下にある仮想ネットワークの詳細が表示されます。](media/azure-virtual-network-6.PNG)

ダッシュ ボードの右側にある [タスク] ウィンドウで、さまざまなタスクのために、Azure の仮想ネットワークにです。

-   **切断から Azure VNET**、Azure の仮想ネットワークの設定はするが、空きが、オンプレミスと Azure での他の VNETs に接続する VPN ゲートウェイの充電します。 Azure VNET から切断するすべての課金を停止します。

-   **VPN 経由でデバイスを切り替える**イベントで、VPN サーバーから VPN ルーターに変更するには、このタスクを有効にするスイッチを作成および Azure VNET に通知することです。

-   **Azure VNET を構成する**このタスクでは、Azure VNET の Azure ポータルの構成] ページにリダイレクトする Azure VNET の高度な構成オプションを変更することができます。

-   **ステータスを更新する**/縮小、データを含む Azure VNET の接続状態の更新の状態] ページを更新します。

-   **Azure VNET 統合を無効にする**Azure VNET が切断され、Windows Server Essentials ダッシュ ボードからの統合を削除します。 この Azure VNET は削除されません、Azure では、後で、ダッシュ ボードで Azure VNET を再統合する場合の設定が維持も注意してください。

-   **Azure VNET に関する詳細をご覧ください**[https://azure.microsoft.com/en-us/services/virtual-network/](https://azure.microsoft.com/en-us/services/virtual-network/)します。

<a name="see-also"></a>参照してください。
--------
[Windows Server Essentials を使ってみる](get-started.md)
