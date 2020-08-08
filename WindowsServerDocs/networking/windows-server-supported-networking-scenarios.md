---
title: Windows Server でサポートされるネットワーク シナリオ
description: このトピックでは、Windows Server 2016 以降でサポートされる新しいネットワークシナリオについて説明します。
manager: brianlic
ms.topic: article
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
author: dcuomo
ms.author: dacuo
ms.openlocfilehash: 0059e04b79754a3fb183a51cbd75bc03e9a89ae5
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997549"
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server でサポートされるネットワーク シナリオ

>適用対象: Windows Server \( 半期チャネル \) 、windows server 2016

このトピックでは、または Windows Server 2016 のこのリリースで実行できないできるサポート対象およびサポートされていないシナリオに関する情報を提供します。
>[!IMPORTANT]
>すべての運用シナリオ、デバイスの製造元から最新ハードウェア ドライバーを使用して \(OEM\) または独立系ハードウェア ベンダー \(IHV\)します。

## <a name="supported-networking-scenarios"></a><a name="bkmk_supp"></a>サポートされているネットワークのシナリオ

ここでは、Windows Server 2016 のネットワークでサポートされるシナリオについて説明し、次のシナリオのカテゴリが含まれています。

-   [ソフトウェアによるネットワーク制御 (SDN) のシナリオ](#bkmk_sdn)

-   [プラットフォームのネットワークのシナリオ](#bkmk_netp)

-   [DNS サーバーのシナリオ](#bkmk_dns)

-   [IPAM DHCP および DNS を使用するシナリオ](#bkmk_ipam)

-   [NIC チーミングのシナリオ](#bkmk_nicteam)

- [埋め込みチーミング \( セットのシナリオを切り替える \)](#bkmk_set)

### <a name="software-defined-networking-sdn-scenarios"></a><a name="bkmk_sdn"></a>ソフトウェアによるネットワーク制御 (SDN) のシナリオ

次のドキュメントを使用すると、Windows Server 2016 SDN シナリオを展開します。


-   [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

詳細については、次を参照してください。 [ソフトウェアがネットワーク定義と #40 です。SDN (& a) #41;](sdn/software-defined-networking.md)します。

#### <a name="network-controller-scenarios"></a><a name="bkmk_netc"></a>ネットワーク コント ローラーのシナリオ

ネットワーク コント ローラーのシナリオを使用します。

-   展開し、ネットワーク コント ローラーの複数ノード インスタンスを管理します。 詳細については、次を参照してください。 [展開ネットワーク コント ローラーが Windows PowerShell を使用して](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)します。

-   ネットワーク コント ローラーを使用して、プログラムを使用して REST Northbound API を使用してネットワーク ポリシーを定義します。

-   作成し、HYPER-V ネットワーク仮想化 - NVGRE または VXLAN カプセル化を使用して仮想ネットワークを管理するには、ネットワーク コント ローラーを使用します。

詳細については、「[Network Controller (ネットワーク コントローラー)](sdn/technologies/network-controller/Network-Controller.md)」を参照してください。

#### <a name="network-function-virtualization-nfv-scenarios"></a><a name="bkmk_netf"></a>関数の仮想化 (NFV) のネットワークのシナリオ
NFV シナリオを使用します。

-   展開し、northbound と southbound の両方のトラフィックを分散するソフトウェア ロード バランサーを使用します。

-   展開し、HYPER-V ネットワーク仮想化で作成された仮想ネットワークの東、西のトラフィックを分散するソフトウェア ロード バランサーを使用します。

-   展開し、HYPER-V ネットワーク仮想化で作成された仮想ネットワークに NAT ソフトウェア ロード バランサーを使用します。

-   展開し、レイヤー 3 の転送ゲートウェイを使用します。

-   展開し、IPsec (IKEv2) トンネルでサイト間仮想プライベート ネットワーク (VPN) ゲートウェイを使用します。

-   展開し、Generic Routing Encapsulation (GRE) ゲートウェイを使用します。

-   展開し、動的ルーティングおよび転送中は、ボーダー ゲートウェイ プロトコル (BGP) を使用してサイト間でルーティングを構成します。

-   レイヤー 3 とサイト間ゲートウェイ、および BGP のルーティングは、M と N の冗長性を構成します。

-   ネットワーク コント ローラーを使用すると、仮想ネットワークとのネットワーク インターフェイス上の Acl を指定します。

詳細については、次を参照してください。 [ネットワーク機能の仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)します。

### <a name="network-platform-scenarios"></a><a name="bkmk_netp"></a>プラットフォームのネットワークのシナリオ

このセクションでは Windows Server ネットワークのシナリオでは、チームは、ドライバーの認定、Windows Server 2016 の使用をサポートします。 ネットワーク インターフェイス カードを確認してください \(NIC\) の製造元に、最新のドライバーの更新プログラムがあることを確認します。

ネットワーク プラットフォームのシナリオを使用します。

-   収束の NIC を使用して、単一のネットワーク アダプターを使用してトラフィックを RDMA とイーサネットの両方を組み合わせます。

-   低待機時間のデータ パスを作成するには、パケット ダイレクトでは、HYPER-V 仮想スイッチ、および単一のネットワーク アダプターで有効に使用します。

-   最大 2 つのネットワーク アダプター間で SMB ダイレクトと RDMA のトラフィック フローを分散するセットを構成します。

詳細については、「[リモートダイレクトメモリアクセス &#40;RDMA&#41;」と「スイッチ埋め込みチーミング &#40;設定&#41;](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」を参照してください。

#### <a name="hyper-v-virtual-switch-scenarios"></a><a name="bkmk_switch"></a>HYPER-V 仮想スイッチのシナリオ

HYPER-V 仮想スイッチのシナリオを使用します。

-   リモート ダイレクト メモリ アクセス (RDMA) vNIC を HYPER-V 仮想スイッチを作成します。

-   スイッチ埋め込みチーミング (SET)、および RDMA Vnic での HYPER-V 仮想スイッチの作成します。

-   HYPER-V 仮想スイッチのセット チームを作成します。

-   Windows PowerShell コマンドを使用してセット チームを管理します。

詳細については、次を参照してください。 [リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチには、チーム化 (&) #40; が含まれているとセットと #41 です。](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)

### <a name="dns-server-scenarios"></a><a name="bkmk_dns"></a>DNS サーバーのシナリオ

DNS サーバーのシナリオを使用します。

-   地理的な場所ベースの DNS のポリシーを使用したトラフィック管理を指定します。

-   DNS のポリシーを使用して、スプリット ブレイン DNS を構成します。

-   DNS のポリシーを使用して DNS クエリにフィルターを適用します。

-   DNS のポリシーを使用してアプリケーションの負荷分散を構成します。

-   インテリジェント DNS 応答が時間帯に基づく指定します。

-   DNS ゾーン転送のポリシーを構成します。

-   DNS サーバーの Active Directory ドメイン サービス (AD DS) のポリシーに統合されたゾーンを構成します。

-   構成回答率を制限します。

-   名前付きエンティティ (DANE) の DNS ベースの認証を指定します。

-   DNS で不明なレコードのサポートを構成します。

詳細については、トピックを参照してください。 [Windows Server 2016 での DNS クライアントの新](dns/What-s-New-in-DNS-Client.md) と [Windows Server 2016 の DNS サーバーの新](dns/What-s-New-in-DNS-Server.md)します。

### <a name="ipam-scenarios-with-dhcp-and-dns"></a><a name="bkmk_ipam"></a>IPAM DHCP および DNS を使用するシナリオ

IPAM のシナリオを使用します。

-   検出し、DNS と DHCP サーバーとフェデレーションの複数の Active Directory フォレスト間で IP アドレスの割り当ての管理

-   ゾーンとリソース レコードを含む、DNS プロパティの一元管理するためには、IPAM を使用します。

-   細分化された役割に基づいたアクセス制御ポリシーを定義し、指定した DNS プロパティのセットを管理するには、IPAM ユーザーまたはユーザー グループに委任します。

-   IPAM 用 Windows PowerShell コマンドを使用すると、DHCP と DNS のアクセス制御の構成を自動化できます。

    詳細については、次を参照してください。 [IPAM の管理](technologies/ipam/Manage-IPAM.md)します。

### <a name="nic-teaming-scenarios"></a><a name="bkmk_nicteam"></a>NIC チーミングのシナリオ

NIC チーミングのシナリオを使用します。

-   構成ではサポートされている NIC チームを作成します。

-   NIC チームを削除します。

-   サポートされている構成内の NIC チームにネットワーク アダプターを追加します。

-   NIC チームからのネットワーク アダプターを削除します。

> [!NOTE]
> Windows Server 2016 ではして NIC チーミング、HYPER-V が、場合によっては Virtual Machine Queues (VMQ) ない自動的に有効に基になるネットワーク アダプターで NIC チームを作成するときにします。 この問題が発生した場合は、次の Windows PowerShell コマンドを使用して、NIC チームメンバーアダプターで VMQ が有効になっていることを確認できます。`Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`

詳細については、次を参照してください。 [NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)します。

### <a name="switch-embedded-teaming-set-scenarios"></a><a name="bkmk_set"></a>埋め込みチーミング \( セットのシナリオを切り替える \)

セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。

詳細については、次を参照してください [リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)。](../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md)



## <a name="unsupported-networking-scenarios"></a><a name="bkmk_unsupp"></a>サポートされていないネットワークシナリオ
次のネットワークのシナリオは、Windows Server 2016 ではサポートされません。

-   VLAN ベースのテナントの仮想ネットワークです。

-   アンダーレイまたはオーバーレイには、IPv6 はサポートされていません。