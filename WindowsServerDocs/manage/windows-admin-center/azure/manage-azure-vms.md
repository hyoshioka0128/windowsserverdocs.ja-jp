---
title: Azure IaaS 仮想マシンを管理します。
description: Windows Admin center (Project Honolulu) の Azure IaaS 仮想マシンを管理します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6f162294076d7e12df09f31b0bbd7d9244abe679
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297016"
---
# Windows Admin Center での Azure IaaS 仮想マシンの管理します。

Windows Admin Center を使用して、Azure Vm と同様、オンプレミスのコンピューターを管理することができます。 複数の異なる構成が考えられます - 環境に適した構成を選択します。
- [オンプレミスの Windows Admin Center ゲートウェイから Azure Vm の管理します。](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM にインストールされている Windows Admin Center ゲートウェイから Azure Vm の管理します。](#use-a-windows-admin-center-gateway-deployed-in-azure)

## オンプレミスの Windows Admin Center ゲートウェイを管理します。

既にオンプレミス ゲートウェイ (いずれかの Windows 10 または Windows Server 2016) で Windows Admin Center をインストールしたら場合、は、この同じゲートウェイを使用して Windows 10 または Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を管理できます。Azure で Vm します。 

### パブリック IP を Vm に接続します。

パブリック ip アドレスは、ターゲット Vm (Windows Admin Center で管理する Vm) である場合、IP アドレスまたは FQDN によって、Windows Admin Center ゲートウェイに追加します。 これには、いくつかの考慮事項を考慮するがあります。

- ターゲット VM に PowerShell またはコマンド プロンプトで次を実行して、ターゲット VM に WinRM へのアクセスを有効にする必要があります。 `winrm quickconfig`
- していないドメインに参加している Azure VM では、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)対処するかどうかを確認する必要がありますので、VM がワークグループに属している、サーバーのように動作します。
- HTTP 経由で WinRM のポート 5985 への着信接続を有効にも Windows Admin Center をターゲットの VM を管理するためにする必要があります。
   1. ターゲット VM をゲスト OS のポート 5985 への着信接続を有効にするには、次の PowerShell スクリプトを実行します。   
`Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

   2. Azure ネットワーク ポートを開く必要があります。

    - **ネットワーク**、**受信ポート規則を追加**し、選択、Azure VM を選択します。 
    - **セキュリティの受信の規則の追加**のウィンドウの上部にある**基本的な**が選択したことを確認します。
    - **ポートの範囲**フィールドに、 **5985**を入力します。
    
    Windows Admin Center ゲートウェイに静的 IP がある場合は、アクセスを許可するのみ受信 WinRM、Windows Admin Center ゲートウェイから追加のセキュリティについて選択できます。
    これを行うには、**セキュリティの受信の規則の追加**のウィンドウの上部にある**詳細設定**を選択します。

    **ソース**の**IP アドレス**を選択し、Windows Admin Center ゲートウェイに対応するソース IP アドレスを入力します。

    - **プロトコル**の**TCP**を選択します。
    - 残りの部分は、既定値としてままことができます。

> [!NOTE]
> カスタムのポートの規則を作成する必要があります。 Azure ネットワークによって提供される WinRM ポートの規則では、(HTTP) 経由で 5985 ではなくポート 5986 (https) を使用します。 

### パブリック IP せず Vm に接続します。

ターゲットの Azure Vm は、パブリック ip アドレスがないし、オンプレミス ネットワークでの展開、Windows Admin Center ゲートウェイからこれらの Vm を管理する場合、は、ターゲット Vm は VNet に接続する、オンプレミス ネットワークを構成する必要があります。接続されています。 これを行う 3 つの方法がある: ExpressRoute、サイト間 VPN、またはポイントとサイト VPN します。 [環境内で意味の接続オプションについて説明します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>ポイントとサイト VPN を使用して、その VNet に Azure Vm を管理する、Azure VNet に、Windows Admin Center ゲートウェイに接続する場合は、Windows Admin Center で[Azure ネットワーク アダプター](https://aka.ms/WACNetworkAdapter)の機能を使用することができます。 これには、Windows Admin Center がインストールされているサーバーに接続する、ネットワーク ツールに移動し、"Azure ネットワーク アダプターの追加] を選択します。 必要な詳細を提供し、クリックして「設定」、Windows Admin Center は指定すると、その後に接続でき、オンプレミスの Windows Admin Center ゲートウェイから Azure Vm を管理する Azure VNet にポイントとサイト VPN を構成します。

WinRM はターゲット VM に PowerShell またはコマンド プロンプトで次を実行して、ターゲット Vm で実行されていることを確認します。 `winrm quickconfig`

していないドメインに参加している Azure VM では、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)対処するかどうかを確認する必要がありますので、VM がワークグループに属している、サーバーのように動作します。

問題が生じた場合は、 [Windows Admin Center のトラブルシューティング](../support/troubleshooting.md)に (たとえば、またはする場合、ローカル管理者アカウントを使用して接続しているドメインに参加していない) 追加の手順が必要な構成を参照してください。

## Azure に展開された Windows Admin Center ゲートウェイを使用します。

ターゲット Vm が接続されている VNet で Windows Admin Center を展開することによって、オンプレミスの依存関係なく Azure Vm を管理できます。 

Windows Admin Center ゲートウェイの展開先の VNet 外の Vm を管理するには、Windows Admin Center ゲートウェイの VNet と対象サーバーの VNet 間 VNet-VNet に接続を確立する必要があります。 VNet ピアリング、VNet-VNet に接続、またはサイトの接続でこの接続を確立することができます。 [どの VNet-VNet に接続に関するオプションは、環境内によりについて説明します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

Windows Admin Center は、環境内の既存のまたは新しく展開される VM にインストールすることができます。 Windows Admin Center のインストールを選択した VM には、パブリック IP および DNS 名が必要です。

[Azure で Windows Admin Center ゲートウェイの展開について詳しく知る](deploy-wac-in-azure.md)