---
title: Hyper-V 仮想スイッチ
description: このトピックでは、Windows Server 2016 の Hyper-v 仮想スイッチの概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fb2ebf485b5004e457558fc16d8535662c0c5ff2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307982"
---
# <a name="hyper-v-virtual-switch"></a>Hyper-V 仮想スイッチ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、hyper-v 仮想スイッチの概要について説明します。これにより、仮想マシン \(Vm\) を、組織のイントラネットやインターネットなど、\-Hyper-v ホストの外部にあるネットワークに接続できるようになります。 

ソフトウェア定義のネットワーク \(SDN\)を展開するときに、\-Hyper-v を実行しているサーバー上の仮想ネットワークに接続することもできます。

> [!NOTE]  
> このトピックに加え、次の Hyper-v 仮想スイッチのドキュメントも参照してください。  
>   
> - [Hyper-V 仮想スイッチを管理する](Manage-Hyper-V-Virtual-Switch.md) 
> - [リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Windows PowerShell のネットワークスイッチチームのコマンドレット](https://technet.microsoft.com/library/jj553812.aspx)
> - [VMM 2016 の新機能](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [VMM ネットワークファブリックのセットアップ](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [VMM 2012 を使用してネットワークを作成する](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-v: Vlan と VLAN タグの構成](https://social.technet.microsoft.com/wiki/contents/articles/1306.hyper-v-configure-vlans-and-vlan-tagging.aspx)  
> - [Hyper-v: サードパーティ製の拡張機能に必要な場合は、WFP 仮想スイッチ拡張機能を有効にする必要があります。](https://social.technet.microsoft.com/wiki/contents/articles/13071.hyper-v-the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions.aspx)
>
> その他のネットワークテクノロジの詳細については、「 [Windows Server 2016 のネットワーク](https://docs.microsoft.com/windows-server/networking/networking)」を参照してください。
  
Hyper-v 仮想スイッチは、hyper-v サーバーの役割を\-インストールするときに Hyper-v マネージャーで使用できる、ソフトウェアベースのレイヤー2イーサネットネットワークスイッチです。このスイッチは、ハイパー\-V Manager で使用できます。\-

Hyper-v 仮想スイッチには、仮想ネットワークと物理ネットワークの両方に Vm を接続する、プログラムによって管理される拡張可能な機能が含まれています。 また、Hyper-V 仮想スイッチでは、セキュリティ、分離、およびサービスのレベルでポリシーを適用できます。  
  
> [!NOTE]  
> Hyper-V 仮想スイッチは、イーサネットのみをサポートしており、その他のワイヤード (有線) ローカル エリア ネットワーク (LAN) テクノロジ (Infiniband やファイバー チャネルなど) はサポートしていません。  
  
Hyper-v 仮想スイッチには、テナント分離機能、トラフィックのシェイプ、悪意のある仮想マシンに対する保護、簡単なトラブルシューティングなどが含まれます。 

ネットワークデバイスインターフェイス仕様のサポートが組み込まれている \(、NDIS\) フィルタードライバーおよび Windows フィルタリングプラットフォーム \(WFP\) コールアウトドライバーを使用することで、Hyper-v 仮想スイッチを使用して、Isv \(は、拡張可能なプラグイン (仮想スイッチ拡張機能と呼ばれる) を作成し、ネットワークとセキュリティの機能を強化することができます。\) Hyper-V 仮想スイッチに追加した仮想スイッチ拡張機能は、Hyper-V マネージャーの仮想スイッチ マネージャー機能で表示されます。
  
次の図では、VM の仮想 NIC はスイッチポートを介して Hyper-v 仮想スイッチに接続されています。  
  
![仮想スイッチ接続](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Hyper-v 仮想スイッチの機能を使用すると、テナントの分離の強制、ネットワークトラフィックの整形と制御、および悪意のある Vm に対する保護対策の使用を行うための、より多くのオプションが提供されます。

>[!NOTE]
> Windows Server 2016 では、仮想 NIC を持つ VM は、仮想 NIC の最大スループットを正確に表示します。 **ネットワーク接続**の仮想 nic 速度を表示するには、目的の仮想 nic アイコンを右クリックし、 **[状態]** をクリックします。 [仮想 NIC の**状態**] ダイアログボックスが開きます。 **[接続]** の **[速度]** の値は、サーバーにインストールされている物理 NIC の速度と一致します。
  
## <a name="uses-for-hyper-v-virtual-switch"></a><a name="bkmk_apps"></a>Hyper-v 仮想スイッチの使用

Hyper-v 仮想スイッチのいくつかのユースケースシナリオを次に示します。

**統計情報の表示**: ホスト型クラウドのベンダーの開発者は、hyper-v 仮想スイッチの現在の状態を表示する管理パッケージを実装します。 この管理パッケージでは、WMI を使って、スイッチ全体の現在の機能、構成設定、および個々のポートのネットワーク統計情報を照会できます。 それにより、スイッチのステータスが表示され、管理者はスイッチの状態をすばやく把握できます。  
  
**リソース追跡**: メンバーシップのレベルに従って、ホスティングサービスを販売しています。 各種のメンバーシップ レベルでは、ネットワーク パフォーマンスのレベルがさまざまに異なります。 管理者は、ネットワークの可用性のバランスを取りながら SLA を満足できるように、リソースを割り当てます。 管理者は、割り当てられた帯域幅の現在の使用状況や、仮想マシン (VM) に割り当てられた仮想マシンキュー (VMQ) または SR-IOV チャネルの数などの情報をプログラムで追跡します。 また、同じプログラムで、割り当てられた VM ごとのリソースに加えて、使用中のリソースを定期的に記録することで、二重エントリによるリソース追跡を行います。  
  
**スイッチ拡張機能の順序の管理**: 企業では、トラフィックの監視と侵入検出の報告の両方を行うために、hyper-v ホストに拡張機能をインストールしています。 メンテナンス中に、いくつかの拡張機能が更新されることで、拡張機能の順序が変更される場合があります。 単純なスクリプト プログラムの実行により、更新後に拡張機能の順序を再設定します。  
  
**転送拡張機能は、VLAN ID を管理**します。主要なスイッチ会社は、ネットワークのすべてのポリシーを適用する転送拡張機能を構築しています。 管理される要素の 1 つに、仮想ローカル エリア ネットワーク (VLAN) ID があります。 仮想スイッチは、VLAN の制御を転送拡張機能に渡します。 会社のインストールをプログラムによって呼び出す Windows Management Instrumentation (WMI) アプリケーションプログラミングインターフェイス (API) を呼び出して、透過性をオンにし、Hyper-v 仮想スイッチに対して、VLAN タグに対する操作を実行しないように指示します。  
  
## <a name="hyper-v-virtual-switch-functionality"></a><a name="bkmk_func"></a>Hyper-v 仮想スイッチの機能
 
Hyper-V 仮想スイッチに備えられているいくつかの主要な機能について説明します。  
  
-   **Arp/ND ポイズニング (スプーフィング) 保護**: アドレス解決プロトコル (ARP) スプーフィングを使用して、他の VM から IP アドレスを盗み出そうとする悪意のある VM からの保護を提供します。 近隣探索 (ND) スプーフィングを使って IPv6 で行われる可能性のある攻撃に対しても保護を提供します。  
  
-   **Dhcp ガードによる保護**: 動的ホスト構成プロトコル (dhcp) サーバーとしてそれ自体を表す悪意のある VM から、man-in-the-middle 攻撃に対して保護されます。  
  
-   **ポート acl**: メディア ACCESS CONTROL (MAC) またはインターネットプロトコル (IP) のアドレス/範囲に基づくトラフィックのフィルター処理を提供します。これにより、仮想ネットワークの分離を設定できます。  
  
-   **Vm へのトランクモード**: 管理者が特定の vm を仮想アプライアンスとして設定し、さまざまな vlan からのトラフィックをその vm に転送できます。  
  
-   **ネットワークトラフィックの監視**: ネットワークスイッチを通過するトラフィックを管理者が確認できるようにします。  
  
-   分離された **(プライベート) VLAN**: 管理者が複数の vlan 上のトラフィックを分離し、分離されたテナントコミュニティをより簡単に確立できるようにします。  
  
Hyper-V 仮想スイッチの操作性を向上させる機能の一覧を次に示します。  
  
-   **帯域幅の制限とバーストのサポート**: 帯域幅の最小値は、予約されている帯域幅の量を保証します。 最大帯域幅によって、VM が使用できる帯域幅の大きさが制限されます。  
  
-   **明示的な輻輳通知 (ecn) マーキングのサポート**: ecn マーキング (データセンター TCP (dctcp) とも呼ばれます) を使用すると、物理スイッチとオペレーティングシステムは、スイッチのバッファーリソースがあふれないようにトラフィックフローを制御できます。これにより、トラフィックのスループットが向上します。  
  
-   **診断**: 診断を使用すると、仮想スイッチを介したイベントとパケットのトレースと監視を簡単に行うことができます。
