---
title: Windows Server でサポートされるネットワークのシナリオ
description: このトピックの「新しいサポートされているネットワークのシナリオでは、Windows Server 2016 以降に関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 6de4232d-b0b3-4e43-8735-ebae35ae4f9f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 70198f97c4ec39de4b78de28ab196dc3e86a684c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="windows-server-supported-networking-scenarios"></a>Windows Server でサポートされるネットワークのシナリオ

>適用対象: Windows Server \(Semi-Annual Channel\)、Windows Server 2016

このトピックでは、今回のリリースの Windows Server 2016 で実行できないでしたりできるサポートされる/サポートされないシナリオに関する情報を提供します。  
>[!IMPORTANT]
>すべての運用シナリオでは、デバイスの製造元から最新ハードウェア ドライバーを使用して \(OEM\) または独立系ハードウェア ベンダー \(IHV\) します。
  
## <a name="bkmk_supp"></a>サポートされているネットワークのシナリオ

このセクションでは、Windows Server 2016 のネットワークでサポートされるシナリオに関する情報が含まれていて、次のシナリオのカテゴリが含まれています。  
  
-   [ソフトウェアによるネットワーク制御 (SDN) のシナリオ](#bkmk_sdn)  
  
-   [ネットワーク プラットフォームのシナリオ](#bkmk_netp)  
  
-   [DNS サーバーのシナリオ](#bkmk_dns)  
  
-   [DHCP および DNS を使用する IPAM シナリオ](#bkmk_ipam)  
  
-   [NIC チーミングのシナリオ](#bkmk_nicteam)

- [スイッチ埋め込みチーミング \(SET\) のシナリオ](#bkmk_set)
  
### <a name="bkmk_sdn"></a>ソフトウェアによるネットワーク制御 (SDN) のシナリオ
 
Windows Server 2016 SDN シナリオを展開するのに、次のドキュメントを使用できます。  
  
  
-   [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開します。](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
詳細については、次を参照してください。[ソフトウェア定義ネットワーク (&) #40 です。SDN & #41 です。](sdn/software-defined-networking.md).  
  
#### <a name="bkmk_netc"></a>ネットワーク コントローラーのシナリオ

ネットワーク コントローラーのシナリオを使用します。  
  
-   展開し、ネットワーク コントローラーの複数ノード インスタンスを管理します。 詳細については、次を参照してください。[展開ネットワーク コントローラーが Windows PowerShell を使用して](sdn/deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)します。  
  
-   プログラムを使用して REST Northbound API を使用してネットワーク ポリシーを定義するのにには、ネットワーク コントローラーを使用します。  
  
-   ネットワーク コントローラーを使用して作成し、Hyper-V ネットワーク仮想化 - NVGRE または VXLAN カプセル化を使用すると、仮想ネットワークを管理します。  
  
詳細については、次を参照してください。[ネットワーク コントローラー](sdn/technologies/network-controller/Network-Controller.md)します。  
  
#### <a name="bkmk_netf"></a>ネットワーク関数仮想化 (NFV) のシナリオ  
NFV シナリオを使用します。  
  
-   展開し、northbound と southbound の両方のトラフィックを分散するソフトウェア ロード バランサーを使用します。  
  
-   展開し、Hyper-V ネットワーク仮想化で作成された仮想ネットワークの東、西のトラフィックを分散するソフトウェア ロード バランサーを使用します。  
  
-   展開し、Hyper-V ネットワーク仮想化で作成された仮想ネットワークに NAT ソフトウェア ロード バランサーを使用します。  
  
-   展開し、レイヤー 3 の転送ゲートウェイを使用します。  
  
-   展開し、IPsec (IKEv2) トンネルでサイト間仮想プライベート ネットワーク (VPN) ゲートウェイを使用します。  
  
-   展開し、汎用ルーティング カプセル化 (GRE) ゲートウェイを使用します。  
  
-   展開し、動的ルーティングおよびボーダー ゲートウェイ プロトコル (BGP) を使用してサイト間のトランジット ルーティングを構成します。  
  
-   レイヤー 3 とサイト間ゲートウェイ、および BGP のルーティングは、M と N の冗長性を構成します。  
  
-   ネットワーク コントローラーを使用して、仮想ネットワークとのネットワーク インターフェイスを Acl を指定します。  
  
詳細については、次を参照してください。[ネットワーク関数仮想化](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)します。  
  
### <a name="bkmk_netp"></a>ネットワーク プラットフォームのシナリオ

このセクションでは Windows Server ネットワークのシナリオでは、チームは、ドライバーの認定、Windows Server 2016 の使用をサポートします。 ネットワーク インターフェイス カード \(NIC\) 製造元に問い合わせて、最新のドライバーの更新プログラムがあることを確認するを確認してください。
  
ネットワーク プラットフォームのシナリオを使用します。  
  
-   収束の NIC を使用して、単一のネットワーク アダプターを使用して RDMA とイーサネットの両方のトラフィックを結合します。  
  
-   低待機時間のデータ パスを作成するには、パケット ダイレクトでは、Hyper-V 仮想スイッチ、および単一のネットワーク アダプターで有効に使用します。  
  
-   最大 2 つのネットワーク アダプター間で SMB ダイレクトと RDMA のトラフィック フローを分散するセットを構成します。  
  
詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチ埋め込みチーミング (&) #40;セットと #41 です。](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md).  
  
#### <a name="bkmk_switch"></a>Hyper-V 仮想スイッチのシナリオ

Hyper-V 仮想スイッチのシナリオを使用します。  
  
-   リモート ダイレクト メモリ アクセス (RDMA) vNIC で Hyper-V 仮想スイッチを作成します。  
  
-   スイッチ埋め込みチーミング (SET) と RDMA Vnic で Hyper-V 仮想スイッチを作成します。  
  
-   Hyper-V 仮想スイッチのセット チームを作成します。  
  
-   Windows PowerShell コマンドを使用してセット チームを管理します。  
  
詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (&) #40 です。RDMA と #41 です。スイッチ埋め込みチーミング (&) #40;セットと #41 です。](../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)  
  
### <a name="bkmk_dns"></a>DNS サーバーのシナリオ

DNS サーバーのシナリオを使用します。  
  
-   地理的な場所ベースの DNS のポリシーを使用したトラフィック管理を指定します。  
  
-   DNS ポリシーを使用して、スプリット ブレイン DNS を構成します。  
  
-   DNS ポリシーを使用して DNS クエリにフィルターを適用します。  
  
-   DNS ポリシーを使用してアプリケーションの負荷分散を構成します。  
  
-   1 日の時間に基づき、インテリジェント DNS 応答を指定します。  
  
-   DNS ゾーン転送のポリシーを構成します。  
  
-   DNS サーバーのポリシー Active Directory ドメイン サービス (AD DS) 統合ゾーンを構成します。  
  
-   構成回答率を制限します。  
  
-   名前付きエンティティ (DANE) の DNS ベースの認証を指定します。  
  
-   DNS で不明なレコードのサポートを構成します。  
  
詳細については、トピックを参照してください。 [Windows Server 2016 での DNS クライアントの新](dns/What-s-New-in-DNS-Client.md)と[Windows Server 2016 での DNS サーバーの新](dns/What-s-New-in-DNS-Server.md)します。  
  
### <a name="bkmk_ipam"></a>DHCP および DNS を使用する IPAM シナリオ

IPAM のシナリオを使用します。  
  
-   検出し、DNS および DHCP サーバーとフェデレーションの複数の Active Directory フォレスト間で IP アドレスの割り当ての管理  
  
-   ゾーンとリソース レコードを含む、DNS プロパティの一元管理するためには、IPAM を使用します。  
  
-   細分化された役割に基づいたアクセス制御ポリシーを定義し、指定した DNS プロパティのセットを管理するには、IPAM ユーザーまたはユーザー グループに委任します。  
  
-   IPAM 用 Windows PowerShell コマンドを使用すると、DHCP と DNS のアクセス制御の構成を自動化できます。  
  
    詳細については、次を参照してください。 [IPAM の管理](technologies/ipam/Manage-IPAM.md)します。  
  
### <a name="bkmk_nicteam"></a>NIC チーミングのシナリオ

NIC チーミングのシナリオを使用します。  
  
-   構成ではサポートされている NIC チームを作成します。  
  
-   NIC チームを削除します。  
  
-   サポートされている構成内の NIC チームにネットワーク アダプターを追加します。  
  
-   NIC チームからのネットワーク アダプターを削除します。  
  
> [!NOTE]  
> Windows Server 2016 で使う NIC チーミング、インストールされた Hyper-v のただし、場合によっては Virtual Machine Queues (VMQ) 可能性がありますに自動的に有効にしない基礎となるネットワーク アダプターで NIC チームを作成するときにします。 このような場合は、次の Windows PowerShell コマンドを使用して NIC チームのメンバーのアダプターで VMQ が有効になっていることを確認することができます。 `Set-NetAdapterVmq -Name <NetworkAdapterName> -Enable`  

詳細については、次を参照してください。 [NIC チーミング](technologies/nic-teaming/NIC-Teaming.md)します。 

### <a name="bkmk_set"></a>スイッチ埋め込みチーミング \(SET\) のシナリオ

セットは、Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる代替 NIC チーミング ソリューションです。 セットは、Hyper-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 

詳細については、次を参照してください[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)。](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)
  
 
  
## <a name="bkmk_unsupp"></a>サポートされていないネットワークのシナリオ  
次のネットワークのシナリオは、Windows Server 2016 ではサポートされません。  
  
-   VLAN ベースのテナント仮想ネットワークです。  
  
-   アンダーレイまたはオーバーレイには、IPv6 はサポートされていません。  
  


