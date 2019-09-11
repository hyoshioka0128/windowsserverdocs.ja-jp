---
title: Azure で Windows 管理センターゲートウェイをデプロイする
description: Azure で Windows 管理センターゲートウェイをデプロイする方法
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d0ebc957715f88898a9c14d2841d8b820f862a0d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869141"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Windows 管理センターを Azure にデプロイする

## <a name="deploy-using-script"></a>スクリプトを使用したデプロイ

[Azure Cloud Shell](https://shell.azure.com)から実行する[Deploy-WACAzVM](https://aka.ms/deploy-wacazvm)をダウンロードして、Azure で Windows 管理センターゲートウェイを設定できます。 このスクリプトは、リソースグループを含む環境全体を作成できます。

[手動配置の手順に移動する](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>前提条件

* [Azure Cloud Shell](https://shell.azure.com)でアカウントを設定します。 初めて Cloud Shell を使用する場合は、Cloud Shell を使用して Azure ストレージアカウントを関連付けるか、作成するかを確認するメッセージが表示されます。
* **PowerShell** Cloud Shell で、ホームディレクトリに移動します。```PS Azure:\> cd ~```
* ```Deploy-WACAzVM.ps1```ファイルをアップロードするには、ローカルコンピューターから [Cloud Shell] ウィンドウの任意の場所にファイルをドラッグアンドドロップします。

独自の証明書を指定する場合:

* 証明書を[Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)にアップロードします。 まず、Azure Portal でキーコンテナーを作成し、その証明書を key vault にアップロードします。 または、Azure ポータルを使用して証明書を生成することもできます。

### <a name="script-parameters"></a>スクリプトパラメーター

* **ResourceGroupName** -[STRING] VM が作成されるリソースグループの名前を指定します。

* **名前**-[文字列] VM の名前を指定します。

* **Credential** -[PSCREDENTIAL] VM の資格情報を指定します。

* **Msipath** -[文字列] 既存の VM に Windows 管理センターを展開するときに、Windows 管理センターの MSI のローカルパスを指定します。 省略した場合、 http://aka.ms/WACDownload 既定値はからのバージョンになります。

* **VaultName** -[String] 証明書を含むキーコンテナーの名前を指定します。

* **Certname** -[STRING] MSI のインストールに使用する証明書の名前を指定します。

* **GenerateSslCert** -[SWITCH] MSI が自己署名 ssl 証明書を生成する必要がある場合は True を指定します。

* **ポート**番号-[Int] Windows 管理センターサービスの ssl ポート番号を指定します。 省略した場合、既定値は443です。

* **Openports** -[int []] VM の開いているポートを指定します。

* **Location** -[STRING] VM の場所を指定します。

* **サイズ**-[文字列] VM のサイズを指定します。 省略した場合、既定値は "Standard_DS1_v2" です。

* **Image** -[STRING] VM のイメージを指定します。 省略した場合、既定値は "Win2016Datacenter" です。

* **VirtualNetworkName** -[STRING] VM の仮想ネットワークの名前を指定します。

* サブネット**名**-[文字列] VM のサブネットの名前を指定します。

* **SecurityGroupName** -[STRING] VM のセキュリティグループの名前を指定します。

* **PublicIpAddressName** -[STRING] VM のパブリック IP アドレスの名前を指定します。

* **Installwaconly** -[Switch] は、既存の Azure VM に WAC をインストールする必要がある場合は True に設定します。

MSI には2つの異なるオプションがあり、MSI のインストールには証明書が使用されます。 MSI は aka.ms/WACDownload からダウンロードすることも、既存の VM にデプロイする場合は、VM 上のローカルの MSI の filepath を指定することもできます。 証明書は Azure Key Vault いずれかで見つかるか、または MSI によって自己署名証明書が生成されます。

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

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>例 1 : 新しい仮想ネットワークとリソースグループの新しい VM に WAC gateway をデプロイするには、スクリプトを使用します。 Aka.ms/WACDownload から MSI を使用し、MSI から自己署名証明書を使用します。

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

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>例 2:#1 と同じですが、Azure Key Vault の証明書を使用しています。

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

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>例 3: 既存の VM でローカル MSI を使用して WAC をデプロイする。

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

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Windows 管理センターゲートウェイを実行している VM の要件

ポート 443 (HTTPS) が開いている必要があります。
スクリプトに対して定義されているものと同じ変数を使用して、Azure Cloud Shell の次のコードを使用して、ネットワークセキュリティグループを更新できます。

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>管理対象の Azure VM の要件

ポート 5985 (WinRM over HTTP) は開いている必要があり、アクティブなリスナーを持っている必要があります。
Azure Cloud Shell の次のコードを使用して、管理対象ノードを更新できます。 ```$ResourceGroupName```と```$Name```は配置スクリプトと同じ変数を使用しますが、管理対象の VM ```$Credential```に固有のを使用する必要があります。

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>既存の Azure 仮想マシンに手動でデプロイする

必要なゲートウェイ VM に Windows 管理センターをインストールする前に、HTTPS 通信に使用する SSL 証明書をインストールするか、Windows 管理センターによって生成された自己署名証明書を使用するかを選択できます。 ただし、後者のオプションを選択した場合は、ブラウザーから接続しようとすると警告が表示されます。 Edge でこの警告を回避するには、[> 詳細] をクリックして**web ページにアクセス**するか、Chrome で [詳細] を選択し **> [web ページ] に進み**ます。 テスト環境では自己署名証明書のみを使用することをお勧めします。

> [!NOTE]
> これらの手順は、Server Core インストールではなく、デスクトップエクスペリエンスで Windows Server にをインストールするためのものです。 

1. [Windows 管理センター](https://aka.ms/windowsadmincenter)をローカルコンピューターにダウンロードします。

2. VM へのリモートデスクトップ接続を確立し、ローカルコンピューターから MSI をコピーして、VM に貼り付けます。

3. MSI をダブルクリックしてインストールを開始し、ウィザードの指示に従います。 次の点に注意してください。

   - 既定では、インストーラーは推奨されるポート 443 (HTTPS) を使用します。 別のポートを選択する場合は、ファイアウォールでそのポートも開く必要があることに注意してください。 

   - VM に SSL 証明書が既にインストールされている場合は、そのオプションを選択し、拇印を入力してください。

4. Windows 管理センターサービスを開始する (C:/Program Files/Windows 管理センター/sme を実行する)

[Windows 管理センターの展開の詳細については、こちらを参照してください。](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>HTTPS ポートアクセスを有効にするゲートウェイ VM を構成します。 

1. Azure portal で VM に移動し、 **[ネットワーク]** を選択します。 

2. **[受信ポートの規則の追加]** を選択し、 **[サービス]** で **[HTTPS]** を選択します。 

> [!NOTE]
> 既定の443以外のポートを選択した場合は、サービス で **カスタム** を選択し、**ポートの範囲** の手順3で選択したポートを入力します。 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Azure VM にインストールされている Windows 管理センターゲートウェイへのアクセス

この時点で、ゲートウェイ VM の DNS 名に移動することで、ローカルコンピューター上の最新のブラウザー (Edge または Chrome) から Windows 管理センターにアクセスできるようになります。 

> [!NOTE]
> 443以外のポートを選択した場合は、VM\<\>の https://DNS 名: カスタムポートに移動すると、Windows\<管理センターにアクセスできます。\>

Windows 管理センターにアクセスしようとすると、Windows 管理センターがインストールされている仮想マシンにアクセスするための資格情報を要求するプロンプトが表示されます。 ここでは、仮想マシンのローカルユーザーまたはローカルの administrators グループにある資格情報を入力する必要があります。 

VNet 内の他の Vm を追加するには、PowerShell で次のコマンドを実行するか、ターゲット VM でコマンドプロンプトを実行して、ターゲット Vm で WinRM が実行されていることを確認します。`winrm quickconfig`

Azure VM にドメイン参加していない場合、VM はワークグループ内のサーバーのように動作するため、[ワークグループで Windows 管理センターを使用](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)することを確認する必要があります。