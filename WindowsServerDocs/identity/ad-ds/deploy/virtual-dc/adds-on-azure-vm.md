---
title: Azure の仮想マシンに Active Directory Domain Services をインストールする
description: Azure 仮想マシン上の仮想マシン (VM) に新しい Active Directory フォレストを作成する方法について説明します。
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 04/11/2019
ms.technology: identity-adds
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: e0a10e27e044fd1df7cbdb943964440983ce494c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390648"
---
# <a name="install-a-new-active-directory-forest-using-azure-cli"></a>Azure CLI を使用して新しい Active Directory フォレストをインストールする

AD DS は、多くのオンプレミスのインスタンスで実行されるのと同じ方法で、Azure 仮想マシン (VM) で実行できます。 この記事では、Azure portal と Azure CLI を使用して、Azure 可用性セットに新しい AD DS フォレストを2つの新しいドメインコントローラーにデプロイする手順について説明します。 多くのお客様は、ラボを作成するとき、または Azure でドメインコントローラーをデプロイする準備をする際に役立つこのガイダンスを見つけています。

## <a name="components"></a>コンポーネント

* すべてを配置するリソースグループ。
* Vm への RDP アクセスを許可する[Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview.md)、サブネット、ネットワークセキュリティグループ、およびルール。
* に2つの Active Directory Domain Services (AD DS) ドメインコントローラーを配置するように設定された Azure 仮想マシンの[可用性セット](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability#availability-sets)。
* AD DS と DNS を実行する2つの Azure 仮想マシン。

### <a name="items-that-are-not-covered"></a>カバーされていない項目

* オンプレミスの場所からの[サイト間 VPN 接続の作成](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Azure でのネットワークトラフィックのセキュリティ保護](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices.md)
* [サイトトポロジの設計](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/designing-the-site-topology)
* [操作マスターの役割の配置の計画](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/planning-operations-master-role-placement)
* [Id を Azure AD に同期するための Azure AD Connect のデプロイ](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express)

## <a name="build-the-test-environment"></a>テスト環境を構築する

環境の作成には、 [Azure portal](https://portal.azure.com)と[Azure CLI](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest)を使用します。

この Azure CLI は、コマンドラインまたはスクリプトで Azure リソースを作成および管理するために使用されます。 このチュートリアルでは、Azure CLI を使用して、Windows Server 2019 を実行する仮想マシンを展開する方法について詳しく説明します。 デプロイが完了したら、サーバーに接続して AD DS をインストールします。

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free)してください。

### <a name="using-azure-cli"></a>Azure CLI の使用

次のスクリプトは、Azure で新しい Active Directory フォレストのドメインコントローラーを構築するために、2つの Windows Server 2019 Vm の構築プロセスを自動化します。 管理者は、必要に応じて以下の変数を変更し、1つの操作として完了することができます。 このスクリプトは、必要なリソースグループ、ネットワークセキュリティグループ、リモートデスクトップ、仮想ネットワークとサブネット、および可用性グループを作成します。 各 Vm は、20 GB のデータディスクを使用して構築され、AD DS をインストールするためにキャッシュが無効になります。

次のスクリプトは、Azure portal から直接実行できます。 CLI をローカルにインストールして使用することを選択した場合、このクイックスタートでは Azure CLI バージョン2.0.4 以降を実行している必要があります。 を`az --version`実行してバージョンを確認します。 をインストールまたはアップグレードする必要がある場合は、「 [install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)」を参照してください。

| 変数名 | 目的 |
| :---: | :--- |
| AdminUsername | ローカル管理者として各 VM で構成されるユーザー名。 |
| AdminPassword | 各 VM でローカル管理者のパスワードとして構成されるクリアテキストのパスワード。 |
| ResourceGroupName | リソースグループに使用する名前。 既存の名前を複製することはできません。 |
| Location | デプロイ先となる Azure の場所の名前。 @No__t-0 を使用して、現在のサブスクリプションでサポートされているリージョンを一覧表示します。 |
| VNetName | Azure 仮想ネットワークに割り当てる名前は、既存の名前と重複させることはできません。 |
| VNetAddress | Azure ネットワークに使用する IP スコープ。 既存の範囲を複製することはできません。 |
| SubnetName | IP サブネットを割り当てる名前。 既存の名前を複製することはできません。 |
| サブネットアドレス | ドメインコントローラーのサブネットアドレス。 は、VNet 内のサブネットである必要があります。 |
| AvailabilitySet | ドメインコントローラー Vm が参加する可用性セットの名前。 |
| VMSize | デプロイの場所で使用できる標準の Azure VM サイズ。 |
| DataDiskSize | AD DS によってインストールされるデータディスクのサイズ (GB)。 |
| DomainController1 | 最初のドメインコントローラーの名前。 |
| DC1IP | 最初のドメインコントローラーの IP アドレス。 |
| DomainController2 | 2番目のドメインコントローラーの名前。 |
| DC2IP | 2番目のドメインコントローラーの IP アドレス。 |

```azurecli
#Update based on your organizational requirements
Location=westus2
ResourceGroupName=ADonAzureVMs
NetworkSecurityGroup=NSG-DomainControllers
VNetName=VNet-AzureVMsWestUS2
VNetAddress=10.10.0.0/16
SubnetName=Subnet-AzureDCsWestUS2
SubnetAddress=10.10.10.0/24
AvailabilitySet=DomainControllers
VMSize=Standard_DS1_v2
DataDiskSize=20
AdminUsername=azureuser
AdminPassword=ChangeMe123456
DomainController1=AZDC01
DC1IP=10.10.10.11
DomainController2=AZDC02
DC2IP=10.10.10.12

# Create a resource group.
az group create --name $ResourceGroupName \
                --location $Location

# Create a network security group
az network nsg create --name $NetworkSecurityGroup \
                      --resource-group $ResourceGroupName \
                      --location $Location

# Create a network security group rule for port 3389.
az network nsg rule create --name PermitRDP \
                           --nsg-name $NetworkSecurityGroup \
                           --priority 1000 \
                           --resource-group $ResourceGroupName \
                           --access Allow \
                           --source-address-prefixes "*" \
                           --source-port-ranges "*" \
                           --direction Inbound \
                           --destination-port-ranges 3389

# Create a virtual network.
az network vnet create --name $VNetName \
                       --resource-group $ResourceGroupName \
                       --address-prefixes $VNetAddress \
                       --location $Location \

# Create a subnet
az network vnet subnet create --address-prefix $SubnetAddress \
                              --name $SubnetName \
                              --resource-group $ResourceGroupName \
                              --vnet-name $VNetName \
                              --network-security-group $NetworkSecurityGroup

# Create an availability set.
az vm availability-set create --name $AvailabilitySet \
                              --resource-group $ResourceGroupName \
                              --location $Location

# Create two virtual machines.
az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController1 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC1IP \
    --no-wait

az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController2 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC2IP

```

## <a name="dns-and-active-directory"></a>DNS と Active Directory

このプロセスの一部として作成された Azure 仮想マシンが、既存のオンプレミス Active Directory インフラストラクチャの拡張機能である場合は、仮想ネットワークの DNS 設定を、デプロイ前にオンプレミスの DNS サーバーを含めるように変更する必要があります。 この手順は、Azure で新しく作成されたドメインコントローラーがオンプレミスのリソースを解決し、レプリケーションを実行できるようにするために重要です。 DNS、Azure、および設定の構成方法の詳細については、「[独自の dns サーバーを使用する名前解決](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server)」セクションを参照してください。

Azure で新しいドメインコントローラーを昇格した後、仮想ネットワークのプライマリおよびセカンダリ DNS サーバーに設定する必要があります。オンプレミスの DNS サーバーは、3番目以降に降格されます。 DNS サーバーの変更の詳細については、「[仮想ネットワークの作成、変更、削除](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers)」を参照してください。

オンプレミスネットワークを Azure に拡張する方法の詳細については、@no__t 「サイト間 VPN 接続を作成する no__t-1」を参照してください。

## <a name="configure-the-vms-and-install-active-directory-domain-services"></a>Vm を構成してインストール Active Directory Domain Services

スクリプトが完了したら、 [Azure portal](https://portal.azure.com)を参照し、 **[仮想マシン]** をクリックします。

### <a name="configure-the-first-domain-controller"></a>最初のドメインコントローラーを構成する

スクリプトで指定した資格情報を使用して AZDC01 に接続します。

* データディスクの初期化とフォーマットを F:
   * スタート メニューを開き、**コンピューターの管理** を参照します。
   * **記憶域**@no__t の参照-1**ディスク管理**
   * MBR としてディスクを初期化する
   * 新しいシンプルボリュームを作成してドライブ文字を割り当てる F: 必要に応じてボリュームラベルを指定できます。
* サーバーマネージャーを使用して Active Directory Domain Services をインストールする
* 新しいフォレストの最初のドメインコントローラーを昇格させる
   * [ドメインコントローラーオプション] ページで、[ドメインネームシステム (DNS) サーバーおよびグローバルカタログ (GC)] チェックボックスをオンのままにします。
   * 組織の要件に基づいてディレクトリサービス復元モードのパスワードを指定する
   * C: のパスを、場所の入力を求められたときに作成した F: ドライブを指すように変更します。
   * ウィザードで選択した内容を確認し、 **[次へ]** をクリックします。

> [!NOTE]
> 前提条件の確認では、物理ネットワークアダプターに静的 IP アドレスが割り当てられていないことが警告されます。これは、Azure 仮想ネットワークで静的 IP が割り当てられているため、無視してかまいません。

* **インストール**の選択

ウィザードがインストールプロセスを完了すると、VM が再起動されます。

VM が再起動すると、使用された資格情報ではなく、この時点で作成したドメインのメンバーとして再度ログインします。

   > [!NOTE]
   > ドメインコントローラーへの昇格後の最初のログオンは、通常よりも時間がかかる場合があります。 紅茶、コーヒー、水、その他の飲み物を選ぶことができます。

[Azure 仮想ネットワークでは ipv6 がサポートされ](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6)ないため、ipv6 経由の IPv4 を優先するように vm を設定する必要があります。 このタスクを実行する方法の詳細については、サポート技術情報の記事「 [Windows で IPv6 を構成](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users)する」を参照してください。

### <a name="configure-the-second-domain-controller"></a>2番目のドメインコントローラーを構成する

スクリプトで指定した資格情報を使用して AZDC02 に接続します。

* データディスクの初期化とフォーマットを F:
   * スタート メニューを開き、**コンピューターの管理** を参照します。
   * **記憶域**@no__t の参照-1**ディスク管理**
   * MBR としてディスクを初期化する
   * 新しいシンプルボリュームを作成してドライブ文字を割り当てる F: 必要に応じてボリュームラベルを指定できます。
* サーバーマネージャーを使用して Active Directory Domain Services をインストールする
* ドメインコントローラーの昇格
   * 既存のドメインにドメインコントローラーを追加する-CONTOSO.com
   * 操作を実行するための資格情報を指定します
   * C: のパスを、場所の入力を求められたときに作成した F: ドライブを指すように変更します。
   * [ドメインコントローラーオプション] ページで、[ドメインネームシステム (DNS) サーバーおよびグローバルカタログ (GC)] チェックボックスがオンになっていることを確認します。
   * 組織の要件に基づいてディレクトリサービス復元モードのパスワードを指定する
   * ウィザードで選択した内容を確認し、 **[次へ]** をクリックします。

> [!NOTE]
> 前提条件の確認では、物理ネットワークアダプターに静的 IP アドレスが割り当てられていないことが警告されます。これは、Azure 仮想ネットワークで静的 IP が割り当てられているため、無視してかまいません。

* **インストール**の選択

ウィザードがインストールプロセスを完了すると、VM が再起動されます。

VM が再起動すると、使用された資格情報ではなく、CONTOSO.com ドメインのメンバーとして再度ログインします。

[Azure 仮想ネットワークでは ipv6 がサポートされ](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6)ないため、ipv6 経由の IPv4 を優先するように vm を設定する必要があります。 このタスクを実行する方法の詳細については、サポート技術情報の記事「 [Windows で IPv6 を構成](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users)する」を参照してください。

### <a name="configure-dns"></a>DNS を構成する

Azure で新しいドメインコントローラーを昇格した後、仮想ネットワークのプライマリおよびセカンダリ DNS サーバーに設定する必要があります。オンプレミスの DNS サーバーは、3番目以降に降格されます。 DNS サーバーの変更の詳細については、「[仮想ネットワークの作成、変更、削除](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers)」を参照してください。

### <a name="wrap-up"></a>折り返し

この時点で、環境にはドメインコントローラーのペアがあり、追加のサーバーが環境に追加されるように Azure 仮想ネットワークが構成されています。 サイトとサービスの構成、監査、バックアップ、組み込みの管理者アカウントのセキュリティ保護などの Active Directory Domain Services のインストール後のタスクは、この時点で完了する必要があります。

## <a name="removing-the-environment"></a>環境を削除しています

上記で作成したリソースグループのテストが完了したときに環境を削除するには、この手順によって、そのリソースグループの一部であるすべてのコンポーネントが削除されます。

### <a name="remove-using-the-azure-portal"></a>Azure portal を使用して削除する

Azure portal から、 **[リソースグループ]** に移動し、この例の ADonAzureVMs で作成したリソースグループを選択し、 **[リソースグループの削除]** を選択します。 このプロセスでは、リソースグループ内に含まれるすべてのリソースを削除する前に確認メッセージが表示されます。

### <a name="remove-using-the-azure-cli"></a>Azure CLI を使用して削除する

Azure CLI 次のコマンドを実行します。

```azurecli
az group delete --name ADonAzureVMs
```

## <a name="next-steps"></a>次の手順

* [Active Directory Domain Services (AD DS) の安全な仮想化](../../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)
* [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-express)
* [バックアップと回復](https://docs.microsoft.com/azure/virtual-machines/windows/backup-recovery)
* [サイト間 VPN 接続](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [監査](https://docs.microsoft.com/azure/virtual-machines/windows/monitor)
* [セキュリティとポリシー](https://docs.microsoft.com/azure/virtual-machines/windows/security-policy)
* [メンテナンスと更新](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates)
