---
title: Azure IaaS 仮想マシンを管理します。
description: Windows Admin Center (プロジェクト ホノルル) を使用した Azure IaaS Vm の管理
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ac98f42c4ad5606cc8d2b142f209f9bdb2b9611c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445901"
---
# <a name="manage-azure-iaas-virtual-machines-with-windows-admin-center"></a>Windows Admin Center での Azure IaaS 仮想マシンの管理します。

Windows Admin Center を使用して、Azure Vm だけでなく、オンプレミス マシンを管理することができます。 考えられる複数の異なる構成 - お客様の環境に適した構成を選択します。
- [オンプレミスの Windows Admin Center ゲートウェイから Azure Vm の管理します。](#manage-with-an-on-premises-windows-admin-center-gateway)
- [Azure VM にインストールされている Windows Admin Center ゲートウェイから Azure Vm の管理します。](#use-a-windows-admin-center-gateway-deployed-in-azure)

## <a name="manage-with-an-on-premises-windows-admin-center-gateway"></a>オンプレミスの Windows Admin Center ゲートウェイで管理します。

オンプレミス ゲートウェイ (、Windows 10 または Windows Server 2016 上) で Windows Admin Center を既にインストールした場合は、Windows 10 または Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を管理するこの同じゲートウェイを使用できます。Azure 内の Vm。 

### <a name="connecting-to-vms-with-a-public-ip"></a>パブリック IP を持つ Vm に接続します。

ターゲットの Vm (Windows Admin Center で管理する Vm) には、パブリック ip アドレスがある、IP アドレスまたは FQDN、Windows Admin Center ゲートウェイに追加します。 これには考慮に入れて、いくつかの考慮事項があります。

- ターゲット VM で PowerShell またはコマンド プロンプトで、次を実行して、ターゲット VM に WinRM アクセスを有効にする必要があります。 `winrm quickconfig`
- VM のために考慮するかどうかを確認する必要がありますのワークグループにサーバーのように動作をしていないドメインに参加している Azure VM 場合、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)します。
- ターゲット VM を管理する Windows Admin Center での HTTP 経由で winrm ポート 5985 への着信接続も有効にする必要があります。
  1. ターゲット VM のゲスト OS ではポート 5985 への着信接続を有効にするのには、次の PowerShell スクリプトを実行します。   
     `Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any`

  2. Azure ネットワークでポートを開く必要があります。

     - Azure VM を選択して、**ネットワーク**、し**受信ポート ルールの追加**します。 
     - 確認**基本的な**の上部にあるが選択されている、**受信セキュリティ規則の追加**ウィンドウ。
     - **ポート範囲を**フィールドに、入力**5985**します。
    
     場合は、Windows Admin Center ゲートウェイは、静的 IP を持つ、アクセスを許可するのみ受信 WinRM Windows Admin Center ゲートウェイから追加のセキュリティを選択できます。
     これを行うには、次のように選択します。**詳細**の上部にある、**受信セキュリティ規則の追加**ウィンドウ。

     **ソース**を選択します**IP アドレス**、Windows Admin Center ゲートウェイに対応する送信元 IP アドレスを入力します。

     - **プロトコル**選択**TCP**します。
     - 残りの部分は、既定のまま残してかまいません。

> [!NOTE]
> カスタム ポートの規則を作成する必要があります。 Azure ネットワー キングによって提供される、WinRM ポート規則は、5985 ではなく、(HTTP) 経由でポート 5986 (HTTPS) 経由でを使用します。 

### <a name="connecting-to-vms-without-a-public-ip"></a>パブリック ip アドレスなしの Vm に接続します。

ターゲットの Azure Vm は、パブリック ip アドレスがないし、オンプレミス ネットワークにデプロイされている Windows Admin Center ゲートウェイからこれらの Vm を管理する場合、は、によって、どのターゲット Vm が VNet に接続するオンプレミス ネットワークを構成する必要があります。接続されています。 これを行う 3 つの方法があります。ExpressRoute、サイト対サイト VPN、またはポイント対サイト VPN。 [環境内でどの接続オプションの意味について説明します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) 

>[!TIP]
>ポイント対サイト VPN を使用して Windows Admin Center を使用する VNet で Azure Vm を管理するための Azure VNet にゲートウェイを接続するかどうか、 [Azure のネットワーク アダプター](https://aka.ms/WACNetworkAdapter) Windows Admin Center で機能します。 これを行うには、Windows Admin Center がインストールされているサーバーに接続するネットワーク ツールに移動して「Azure ネットワーク アダプターの追加」を選択します。 必要な詳細を提供しをクリックしたときの設定、Windows Admin Center では、指定すると、その後に接続して、オンプレミスの Windows Admin Center ゲートウェイから Azure Vm を管理する Azure VNet にポイント対サイト VPN を構成します。

WinRM は PowerShell またはコマンド プロンプトで次のターゲット VM で実行して、ターゲット Vm で実行されていることを確認します。 `winrm quickconfig`

VM のために考慮するかどうかを確認する必要がありますのワークグループにサーバーのように動作をしていないドメインに参加している Azure VM 場合、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)します。

問題が発生した場合を参照してください[トラブルシューティング Windows Admin Center](../support/troubleshooting.md)に (たとえば、ローカル管理者アカウントを使用して接続する場合がドメインに参加していない)、追加の手順が構成に必要なかどうかを参照してください。

## <a name="use-a-windows-admin-center-gateway-deployed-in-azure"></a>Azure にデプロイされた Windows Admin Center ゲートウェイを使用します。

ターゲット Vm が接続されている VNet での Windows Admin Center を展開することで、オンプレミスに依存することがなく Azure Vm を管理できます。 

Windows Admin Center ゲートウェイが展開されている VNet の外部で Vm を管理するには、Windows Admin Center ゲートウェイの VNet と対象サーバーの VNet 間の VNet 対 VNet 接続を確立する必要があります。 VNet ピアリング、VNet 対 VNet 接続、またはサイト対サイト接続では、この接続を確立することができます。 [VNet 対 VNet 接続のオプションは、環境内によりについて説明します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal)

環境内の既存のまたは新たにデプロイされた VM には、Windows Admin Center をインストールすることができます。 Windows Admin Center のインストール用に選択した VM のパブリック IP と DNS 名が必要です。

[Azure で Windows Admin Center ゲートウェイのデプロイの詳細について説明します](deploy-wac-in-azure.md)