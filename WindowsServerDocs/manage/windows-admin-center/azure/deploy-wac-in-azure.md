---
title: Azure で Windows Admin Center ゲートウェイをデプロイします。
description: Azure で Windows Admin Center ゲートウェイをデプロイする方法
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a3fa1838096d910505faf9a2c5bd819b3a256fe2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280421"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Azure で Windows Admin Center を展開します。

## <a name="deploy-using-script"></a>スクリプトを使用してデプロイします。

ダウンロードできる[デプロイ WACAzVM.ps1](https://aka.ms/deploy-wacazvm)から実行する[Azure Cloud Shell](https://shell.azure.com) Azure で Windows Admin Center ゲートウェイを設定します。 このスクリプトでは、リソース グループを含む環境全体を作成できます。

[手動展開の手順にジャンプします。](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>前提条件

* アカウントを設定する[Azure Cloud Shell](https://shell.azure.com)します。 Cloud Shell を使用して、初めての場合は、求められますの関連付けまたは Cloud Shell で Azure storage アカウントを作成します。
* **PowerShell** Cloud Shell では、ホーム ディレクトリに移動します。 ```PS Azure:\> cd ~```
* アップロードする、```Deploy-WACAzVM.ps1```ファイル、ドラッグし、任意の場所に、ローカル コンピューターからドロップ Cloud Shell ウィンドウにします。

独自の証明書を指定する場合

* 証明書をアップロード[Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)します。 最初に、Azure ポータルでは、key vault を作成し、key vault に証明書をアップロードします。 または、証明書を生成するため、Azure Portal を使用できます。

### <a name="script-parameters"></a>スクリプト パラメーター

* **ResourceGroupName** -[String] は、VM を作成するリソース グループの名前を指定します。

* **名前**-[String] は、VM の名前を指定します。

* **資格情報**-[PSCredential] は、VM の資格情報を指定します。

* **MsiPath** -既存の VM で Windows Admin Center を展開するときに [String] に、Windows Admin Center MSI のローカル パスを指定します。 既定値からバージョン http://aka.ms/WACDownload を省略するとします。

* **VaultName** -[String] は、証明書を含む key vault の名前を指定します。

* **証明書名**-[String] は、MSI のインストールに使用する証明書の名前を指定します。

* **GenerateSslCert** -[スイッチ] True の場合は、MSI は、自己署名 ssl 証明書を生成する必要があります。

* **PortNumber** -[int] を Windows Admin Center サービスの ssl ポート番号を指定します。 省略した場合は 443 に既定値です。

* **OpenPorts** -[int]、VM の開いているポートを指定します。

* **場所**-[String] は、VM の場所を指定します。

* **サイズ**-[String] は、VM のサイズを指定します。 既定値は"Standard_DS1_v2"を省略した場合です。

* **イメージ**-[String] は、VM のイメージを指定します。 既定値は"Win2016Datacenter"を省略した場合です。

* **VirtualNetworkName** -[String] は、VM の仮想ネットワークの名前を指定します。

* **SubnetName** -[String] は、VM のサブネットの名前を指定します。

* **SecurityGroupName** -[String] は、VM のセキュリティ グループの名前を指定します。

* **PublicIpAddressName** -[String] は、VM のパブリック IP アドレスの名前を指定します。

* **InstallWACOnly** -WAC の既存の Azure VM にインストールする場合に、[Switch] が True に設定します。

展開する MSI および MSI のインストールに使用する証明書の 2 つの異なるオプションがあります。 MSI を aka.ms/WACDownload からダウンロードできますか。 またはを既存の VM にデプロイする場合、VM でローカル MSI の filepath を与えることができます。 いずれかの Azure Key Vault に証明書が見つかりませんまたは MSI によって自己署名証明書が生成されます。

### <a name="script-examples"></a>スクリプトの例

まず、スクリプトのパラメーターに必要な共通の変数を定義します。

```PowerShell
$ResourceGroupName = "wac-rg1" 
$VirtualNetworkName = "wac-vnet"
$SecurityGroupName = "wac-nsg"
$SubnetName = "wac-subnet"
$VaultName = "wac-key-vault"
$CertName = "wac-cert"
$Location = "westus"
$PublicIpAddressName = "wac-public-ip"
$Size = "Standard_D4s_v3"
$Image = "Win2016Datacenter"
$Credential = Get-Credential
```

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>例 1:スクリプトを使用すると、新しい仮想ネットワークとリソース グループに新しい VM で WAC ゲートウェイを展開できます。 Aka.ms/WACDownload から MSI と MSI から自己署名証明書を使用します。

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm1"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>例 2:1 が、Azure Key Vault から証明書を使用したのと同じです。

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm2"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    VaultName = $VaultName
    CertName = $CertName
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>例 3: 既存の VM でローカルの MSI を使用して、WAC を展開します。

```PowerShell
$MsiPath = "C:\Users\<username>\Downloads\WindowsAdminCenter<version>.msi"
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm3"
    Credential = $Credential
    MsiPath = $MsiPath
    InstallWACOnly = $true
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Windows Admin Center ゲートウェイを実行している VM の要件

ポート 443 (HTTPS) を開く必要があります。
スクリプトに対して定義されているものと同じ変数を使用して、することができますを使用して、次のコード Azure Cloud Shell で、ネットワーク セキュリティ グループを更新します。

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>管理対象の Azure VM のための要件

ポート 5985 (HTTP 経由の WinRM) は、開くし、アクティブなリスナーがある必要があります。
Azure Cloud Shell で次のコードを使用して、管理対象ノードを更新することができます。 ```$ResourceGroupName``` ```$Name``` 、デプロイ スクリプトと同じ変数を使用しますを使用する必要があります、```$Credential```管理する VM を特定します。

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>既存の Azure 仮想マシンを手動で展開します。

必要なゲートウェイ VM で Windows Admin Center をインストールする前に、HTTPS 通信に使用する SSL 証明書をインストールまたは Windows Admin Center によって生成された自己署名証明書を使用することもできます。 ただし、後者のオプションを選択した場合、ブラウザーから接続しようとするとき、警告が表示されます。 Edge では、この警告をバイパスするにはクリックして**詳細 >」web ページに進みます**または Chrome を選択して **[詳細設定] > [web ページ] に進みます**します。 テスト環境のみに自己署名証明書を使用することをお勧めします。

> [!NOTE]
> これらの手順では、Server Core インストールではなくデスクトップ エクスペリエンス搭載の Windows Server をインストールするためです。 

1. [ダウンロードの Windows Admin Center](https://aka.ms/windowsadmincenter)をローカル コンピューターにします。

2. VM にリモート デスクトップ接続を確立、ローカル コンピューターから msi ファイルをコピーし、VM に貼り付けます。

3. インストールを開始して、MSI をダブルクリックし、ウィザードの指示に従います。 次の注意。

   - 既定では、インストーラーは、推奨されるポート 443 (HTTPS) を使用します。 別のポートを選択する場合は、ことも、ファイアウォールでそのポートを開く必要がありますに注意してください。 

   - VM に既に SSL 証明書をインストールする場合は、そのオプションを選択して、拇印を入力してを確認します。

4. (C:/プログラムのファイル/Windows 管理者 Center/sme.exe を実行する) Windows Admin Center サービスを開始します。

[Windows Admin Center をデプロイの詳細について説明します。](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>ゲートウェイの HTTPS ポートへのアクセスを有効にする VM を構成します。 

1. クリックし、ポータル、azure VM に移動します**ネットワーク**します。 

2. 選択**受信ポート ルールの追加**選択と**HTTPS** **サービス**します。 

> [!NOTE]
> 既定の 443 以外のポートを選択した場合は、選択**カスタム**サービスの下で 手順 3 で選択したポートを入力し、**ポート範囲を**。 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Azure VM にインストールされている Windows Admin Center ゲートウェイへのアクセス

この時点では、ゲートウェイ VM の DNS 名に移動して、ローカル コンピューターで最新のブラウザー (Edge または Chrome) から Windows Admin Center にアクセスできる必要があります。 

> [!NOTE]
> 443 以外のポートを選択した場合は、 https:// に移動して Windows Admin Center をアクセスできる\<、VM の DNS 名\>:\<カスタム ポート\>

Windows Admin Center にアクセスしようとしたときに、ブラウザーは Windows Admin Center がインストールされている仮想マシンへのアクセスに資格情報の入力を求められます。 ここでは、ローカル ユーザーまたはローカルの administrators グループ、仮想マシンの資格情報を入力する必要があります。 

VNet 内の他の Vm を追加するには、WinRM がターゲット VM で PowerShell またはコマンド プロンプトで、次を実行して、ターゲット Vm で実行されていることを確認します。 `winrm quickconfig`

VM のために考慮するかどうかを確認する必要がありますのワークグループにサーバーのように動作をしていないドメインに参加している Azure VM 場合、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)します。