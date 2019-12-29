---
title: Azure IaaS 仮想マシンの管理
description: Windows 管理センター (Project ホノルル) を使用した Azure IaaS Vm の管理
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7b85f64d108283d4865b718b565ad3ba40f14f02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357341"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Windows 管理センターを使用して Azure IaaS 仮想マシンを管理する

Windows Admin Center を使用すると、Azure VM だけでなくオンプレミス コンピューターを管理することができます。 可能な構成はいくつかあります。環境に適した構成を選択してください。
- [オンプレミスの Windows 管理センターゲートウェイから Azure Vm を管理する](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM にインストールされている Windows 管理センターゲートウェイから Azure Vm を管理する](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>オンプレミスの Windows 管理センターゲートウェイを使用して管理する

オンプレミスのゲートウェイ (Windows 10 または Windows Server 2016) に既に Windows 管理センターがインストールされている場合は、この同じゲートウェイを使用して、Windows 10 または windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を管理できます。Azure の Vm。 

### <a name="connecting-to-vms-with-a-public-ip"></a>パブリック IP を使用した Vm への接続

ターゲット Vm (Windows 管理センターで管理する Vm) にパブリック Ip がある場合は、IP アドレスまたは FQDN によって Windows 管理センターゲートウェイに追加します。 考慮する必要がある考慮事項がいくつかあります。

- ターゲット vm への WinRM アクセスを有効にするには、PowerShell で次のコマンドを実行するか、ターゲット VM でコマンドプロンプトを実行します。 `winrm quickconfig`
- Azure VM にドメイン参加していない場合、VM はワークグループ内のサーバーのように動作するため、[ワークグループで Windows 管理センターを使用](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)することを確認する必要があります。
- Windows 管理センターでターゲット VM を管理するには、HTTP 経由で WinRM のポート5985への着信接続を有効にする必要もあります。
  1. 次の PowerShell スクリプトをターゲット VM で実行して、ゲスト OS 上のポート5985への着信接続を有効にします。   
     `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. また、Azure ネットワークでポートを開く必要があります。

     - Azure VM を選択し、 **[ネットワーク]** 、 **[受信ポートの規則の追加]** の順に選択します。 
     - **[受信セキュリティ規則の追加]** ウィンドウの上部で **[基本]** が選択されていることを確認します。
     - **[ポートの範囲]** フィールドに「 **5985**」と入力します。
    
     Windows 管理センターゲートウェイに静的 IP がある場合は、セキュリティを強化するために、Windows 管理センターゲートウェイからの受信 WinRM アクセスのみを許可するように選択できます。
     これを行うには、 **[受信セキュリティ規則の追加]** ウィンドウの上部にある **[詳細設定]** を選択します。

     **[ソース]** で **[IP アドレス]** を選択し、Windows 管理センターゲートウェイに対応する発信元 ip アドレスを入力します。

     - **[プロトコル]** で **[TCP]** を選択します。
     - 残りは既定値のままにすることができます。

> [!NOTE]
> カスタムポート規則を作成する必要があります。 Azure ネットワークによって提供される WinRM ポートルールでは、5985 (HTTP 経由) ではなく、ポート 5986 (HTTPS 経由) が使用されます。 

### <a name="connecting-to-vms-without-a-public-ip"></a>パブリック IP を使用しない Vm への接続

ターゲットの Azure Vm にパブリック Ip がなく、オンプレミスネットワークにデプロイされた Windows 管理センターゲートウェイからこれらの Vm を管理する必要がある場合は、ターゲット Vm が存在する VNet に接続できるようにオンプレミスネットワークを構成する必要があります。中. これを行うには、次の3つの方法があります。ExpressRoute、サイト間 VPN、またはポイント対サイト VPN。 [環境に適した接続オプションについて説明します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>ポイント対サイト VPN を使用して Windows 管理センターゲートウェイを Azure VNet に接続し、その VNet 内の Azure Vm を管理する場合は、Windows 管理センターの[Azure ネットワークアダプター](https://aka.ms/WACNetworkAdapter)機能を使用できます。 これを行うには、Windows 管理センターがインストールされているサーバーに接続し、ネットワークツールに移動して、[Azure ネットワークアダプターの追加] を選択します。 必要な情報を入力し、[セットアップ] をクリックすると、指定した Azure VNet に対してポイント対サイト VPN が構成されます。その後、オンプレミスの Windows 管理センターゲートウェイから Azure Vm に接続して管理できるようになります。

PowerShell またはターゲット VM でコマンドプロンプトで次のコマンドを実行して、ターゲット Vm で WinRM が実行されていることを確認します。 `winrm quickconfig`

Azure VM にドメイン参加していない場合、VM はワークグループ内のサーバーのように動作するため、[ワークグループで Windows 管理センターを使用](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)することを確認する必要があります。

何らかの問題が発生した場合は、「 [Windows 管理センターのトラブルシューティング](../support/troubleshooting.md)」を参照して、構成に追加の手順が必要かどうかを確認してください (たとえば、ローカルの管理者アカウントを使用して接続している場合や、ドメインに参加していない場合など)。

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Azure にデプロイされた Windows 管理センターゲートウェイを使用する

ターゲット Vm が接続されている VNet に Windows 管理センターをデプロイすることで、オンプレミスの依存関係なしで Azure Vm を管理できます。 

Windows 管理センターゲートウェイがデプロイされている VNet の外部にある Vm を管理するには、Windows 管理センターゲートウェイの VNet と対象サーバーの vnet 間の VNet 間接続を確立する必要があります。 この接続を確立するには、VNet ピアリング、vnet 間接続、またはサイト対サイト接続を使用します。 [お使いの環境での VNet 間接続オプションの詳細については、こちらをご覧ください。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows 管理センターは、環境内の既存または新規にデプロイされた VM にインストールできます。 Windows 管理センターのインストール用に選択する VM には、パブリック IP と DNS 名が必要です。

[Azure での Windows 管理センターゲートウェイのデプロイに関する詳細情報](deploy-wac-in-azure.md)