---
title: Azure で Windows Admin Center ゲートウェイを展開します。
description: Azure で Windows Admin Center ゲートウェイを展開する方法
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: af766c2e0502d9fe633cae42d999db5cbffc32c8
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296997"
---
# Azure で Windows Admin Center を展開します。

## スクリプトを使用して展開します。

Azure で Windows Admin Center ゲートウェイを設定する[Azure クラウド シェル](https://shell.azure.com)から実行することは[展開 WACAzVM.ps1](https://aka.ms/deploy-wacazvm)をダウンロードすることができます。 このスクリプトは、リソース グループを含める環境全体を作成できます。

[手動展開手順にジャンプします。](#deploy-manually-on-an-existing-azure-virtual-machine)

### 前提条件

* [Azure クラウド シェル](https://shell.azure.com)でアカウントを設定します。 初めてクラウド シェルを使用する場合が求められることに関連付ける、またはクラウド シェルで Azure ストレージ アカウントを作成します。
* **PowerShell**のクラウドのシェルのホーム ディレクトリに移動します。 ```PS Azure:\> cd ~```
* アップロードする、```Deploy-WACAzVM.ps1```ファイル、ドラッグし、ローカル コンピューターから任意の場所にドロップ クラウド シェル ウィンドウにします。

独自の証明書を指定する場合

* [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)を証明書をアップロードします。 最初に、Azure Portal で、キーの資格情報コンテナーを作成し、キーの資格情報コンテナーに証明書をアップロードします。 また、Azure ポータルを使用するの証明書を生成します。

### スクリプトのパラメーター

* **ResourceGroupName** - [文字列] では、VM を作成するリソース グループの名前を指定します。

* **名**- [文字列] では、VM の名前を指定します。

* **資格情報**の [PSCredential] は、VM の資格情報を指定します。

* **MsiPath** - [文字列] は、既存の VM で Windows Admin Center を展開するときに、Windows Admin Center MSI のローカル パスを指定します。 既定値からバージョンhttp://aka.ms/WACDownloadを省略するとします。

* **VaultName** - [文字列] では、証明書を含むキーの資格情報コンテナーの名前を指定します。

* **証明書名**- [文字列] では、MSI のインストールに使用する証明書の名前を指定します。

* **GenerateSslCert** - [スイッチ] MSI は自己署名 ssl 証明書を生成する場合は True。

* **ポート番号**の [int] では、Windows Admin Center サービスの ssl ポート番号を指定します。 既定値は 443 を省略するとします。

* **OpenPorts** - [int [] VM に開いているポートを指定します。

* **位置情報**- [文字列] では、VM の場所を指定します。

* **サイズ**の [文字列] では、VM のサイズを指定します。 既定値は"Standard_DS1_v2"を省略するとします。

* **画像**- [文字列] では、VM の画像を指定します。 既定値は"Win2016Datacenter"を省略するとします。

* **VirtualNetworkName** - [文字列] は、VM の仮想ネットワークの名前を指定します。

* **SubnetName** - [文字列] は、VM のサブネットの名前を指定します。

* **SecurityGroupName** - [文字列] は、VM のセキュリティ グループの名前を指定します。

* **PublicIpAddressName** - [文字列] は、VM のパブリック IP アドレスの名前を指定します。

* **InstallWACOnly** - [スイッチ] が WAC は、既存の Azure VM にインストールする必要がある場合は True に設定します。

Msi ファイルを展開して MSI のインストールに使用される証明書の 2 つの異なるオプションがあります。 MSI を aka.ms/WACDownload からダウンロードできますか。 または、既存の VM に配置する場合、VM 上にローカルに MSI のファイルパスを与えることができます。 いずれかの Azure キーの資格情報コンテナーに証明書が見つからないまたは MSI で自己署名証明書が生成されます。

### スクリプトの例

まず、スクリプトのパラメーターに必要な一般的な変数を定義します。

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

#### 例 1: 新しい仮想ネットワークとリソース グループ内の新しい VM での WAC ゲートウェイを展開するのにスクリプトを使用します。 Aka.ms/WACDownload から MSI と MSI から自己署名証明書を使用します。

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

#### 例 2: と同じ 1、Azure Key Vault からの証明書を使用しています。

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

#### 例 3: では、既存の VM でローカル MSI を使用して、WAC を展開します。

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

### Windows Admin Center ゲートウェイを実行している VM の要件

ポート 443 (HTTPS) を開く必要があります。
スクリプトに定義されている同じ変数を使用して、以下のコード Azure クラウド シェルに使えるネットワーク セキュリティ グループを更新します。

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### 管理対象の Azure VM のための要件

ポート 5985 (HTTP over WinRM) は、開いているし、アクティブなリスナーがある必要があります。
Azure クラウド シェルで以下のコードを使用すると、管理対象のノードを更新します。 ```$ResourceGroupName``` ```$Name``` 、展開スクリプトと同じ変数を使用しますが、使用する必要があります、```$Credential```管理する VM を特定します。

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## 既存の Azure 仮想マシンに手動で展開します。

目的のゲートウェイ VM で Windows Admin Center をインストールする前に、HTTPS 通信に使用する SSL 証明書をインストールまたは Windows Admin Center によって生成された自己署名証明書を使用することもできます。 ただし、後者のオプションを選択した場合、ブラウザーから接続しようとしたとき、警告が表示されます。 **高度な _gt [web ページ] に続行**を選択することによって **、web ページに進みます詳細 _gt** ] をクリックしてまたは Chrome、Edge では、この警告をバイパスできます。 テスト環境用の自己署名証明書のみを使用することをお勧めします。

> [!NOTE]
> これらの手順では、Server Core インストールではなくデスクトップ エクスペリエンス搭載 Windows Server にインストールする場合です。 

1. ローカル コンピューターに[Windows Admin Center のダウンロード](https://aka.ms/windowsadmincenter)します。

2. VM へのリモート デスクトップ接続を確立し、ローカル コンピューターから msi ファイルをコピーし、VM に貼り付けます。

3. MSI インストールを開始をダブルクリックし、ウィザードの指示に従ってください。 次の注意が必要。

   - 既定では、インストーラーは、推奨されるポート 443 (HTTPS) を使用します。 別のポートを選択する場合も、ファイアウォールでそのポートを開く必要があることに注意してください。 

   - VM 上、SSL 証明書が既にインストールされている場合は、そのオプションをオンにし、拇印を入力を確認します。

4. Windows Admin Center サービス (c:/プログラム ファイルや Windows Admin Center/sme.exe の実行) を開始します。

[Windows Admin Center の展開について説明します。](../deploy/install.md)

### ゲートウェイを HTTPS ポートへのアクセスを有効にする VM を構成します。 

1. Azure portal で、VM に移動し、**ネットワーク**を選択します。 

2. **受信ポート規則の追加**を選択し、[**サービス**の**HTTPS** ] を選択します。 

> [!NOTE]
> 443 既定以外のポートを選択した場合は、**カスタム**[サービス] を選択し、**ポートの範囲**] の下の手順 3 で選択したポートを入力します。 

### Azure VM にインストールされている Windows Admin Center ゲートウェイへのアクセス

この時点では、ゲートウェイ VM の DNS 名に移動して、ローカル コンピューター上エッジ (クロム) 最新のブラウザーから Windows Admin Center にアクセスできる必要があります。 

> [!NOTE]
> ポート 443 以外を選択した場合、VM\>:\<custom port\> の https://\<DNS 名前に移動して Windows Admin Center にアクセスすることができます。

Windows Admin Center にアクセスしようとすると、ブラウザーは Windows Admin Center がインストールされている仮想マシンにアクセスする資格情報の入力を求められます。 ここでは、ローカル ユーザーまたは仮想マシンのローカル administrators グループの資格情報を入力する必要があります。 

VNet に他の Vm を追加するために WinRM がターゲット VM に PowerShell またはコマンド プロンプトで次を実行して、ターゲット Vm で実行されていることを確認します。 `winrm quickconfig`

していないドメインに参加している Azure VM では、[ワークグループで Windows Admin Center を使用して](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)対処するかどうかを確認する必要がありますので、VM がワークグループに属している、サーバーのように動作します。