---
title: PowerShell を使用してシールドされた VM を作成する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 888177c1288216c28f7d4c0a667fd81e93bdce8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402398"
---
# <a name="create-a-shielded-vm-using-powershell"></a>PowerShell を使用してシールドされた VM を作成する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

運用環境では、通常、ファブリックマネージャー (VMM など) を使用してシールドされた Vm をデプロイします。 ただし、次の手順を実行すると、ファブリックマネージャーを使用せずにシナリオ全体を展開および検証することができます。

簡単に言うと、テンプレートディスク、シールドデータファイル、無人インストール応答ファイル、およびその他のセキュリティアーティファクトを任意のコンピューターに作成し、これらのファイルを保護されたホストにコピーして、シールドされた VM をプロビジョニングします。

## <a name="create-a-signed-template-disk"></a>署名済みテンプレートディスクを作成する

新しいシールドされた VM を作成するには、まず、その OS ボリューム (または Linux 上のブートとルートパーティション) に署名されたシールドされた VM テンプレートディスクが必要です。
テンプレートディスクを作成する方法の詳細については、次のリンク先を参照してください。

- [Windows テンプレートディスクを準備する](guarded-fabric-create-a-shielded-vm-template.md)
- [Linux テンプレートディスクを準備する](guarded-fabric-create-a-linux-shielded-vm-template.md)

また、シールドデータファイルを作成するには、ディスクのボリューム署名カタログのコピーが必要です。
このファイルを保存するには、テンプレートディスクを作成したコンピューターで次のコマンドを実行します。

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>ガーディアンメタデータのダウンロード

シールドされた VM を実行する仮想化ファブリックごとに、ファブリックの HGS クラスターのガーディアンメタデータを取得する必要があります。
ホスティングプロバイダーは、この情報を提供できる必要があります。

エンタープライズ環境で、HGS サーバーと通信できる場合、ガーディアンメタデータは*http://\<HGSCLUSTERNAME @ no__t/KeyProtection/service/metadata/2014-07/metadata .xml*で入手できます。

## <a name="create-shielding-data-pdk-file"></a>シールドデータ (PDK) ファイルの作成

シールドデータは、テナント VM の所有者によって作成および所有され、シールドされた VM の管理者パスワードなど、ファブリック管理者から保護する必要があるシールドされた Vm を作成するために必要なシークレットを含みます。
シールドデータは、HGS サーバーとテナントのみが暗号化を解除できるように暗号化されます。
テナントまたは VM の所有者によって作成された後、結果として得られる PDK ファイルを保護されたファブリックにコピーする必要があります。
詳細については、「[シールドデータとは」および「必要な理由](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)」を参照してください。

また、無人インストール応答ファイルが必要になります (Windows の場合は unattend.xml、Linux では異なる)。 応答ファイルに含める内容のガイダンスについては[、「応答ファイルの作成](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)」を参照してください。

シールドされた Vm のリモートサーバー管理ツールがインストールされているコンピューターで、次のコマンドレットを実行します。
Linux VM 用の PDK を作成する場合は、Windows Server バージョン1709以降を実行しているサーバーでこれを行う必要があります。

 
```powershell
# Create owner certificate, don't lose this!
# The certificate is stored at Cert:\LocalMachine\Shielded VM Local Certificates
$Owner = New-HgsGuardian –Name 'Owner' –GenerateCertificates
 
# Import the HGS guardian for each fabric you want to run your shielded VM
$Guardian = Import-HgsGuardian -Path C:\HGSGuardian.xml -Name 'TestFabric'
 
# Create the PDK file
# The "Policy" parameter describes whether the admin can see the VM's console or not
# Use "EncryptionSupported" if you are testing out shielded VMs and want to debug any issues during the specialization process
New-ShieldingDataFile -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Owner $Owner –Guardian $guardian –VolumeIDQualifier (New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\MyTemplateDiskCatalog.vsc' -VersionRule Equals) -WindowsUnattendFile 'C:\unattend.xml' -Policy Shielded
```
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>保護されたホストでのシールドされた VM のプロビジョニング
テンプレートディスクファイル (ServerOS .vhdx) と PDK ファイル (contoso. pdk) を保護されたホストにコピーして、展開の準備をします。

保護されたホストで、保護されたファブリックツールの PowerShell モジュールをインストールします。このモジュールには、プロビジョニングプロセスを簡略化する ShieldedVM コマンドレットが含まれています。 保護されたホストがインターネットにアクセスできる場合は、次のコマンドを実行します。

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

また、インターネットにアクセスできる別のコンピューターにモジュールをダウンロードし、そのモジュールを保護されたホスト上の `C:\Program Files\WindowsPowerShell\Modules` にコピーすることもできます。

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

モジュールをインストールすると、シールドされた VM をプロビジョニングする準備が整います。

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

テンプレートディスクに Linux ベースの OS が含まれている場合は、コマンドの実行時に `-Linux` フラグを指定します。

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

コマンドレットに渡すことができる他のオプションの詳細については、`Get-Help New-ShieldedVM -Full` を使用してヘルプコンテンツを確認してください。

VM のプロビジョニングが完了すると、OS 固有の特殊化フェーズが開始され、その後で使用できるようになります。
VM を実行した後に接続できるように、VM を有効なネットワークに接続してください (RDP、PowerShell、SSH、または任意の管理ツールを使用します)。

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>Hyper-v クラスターでのシールドされた Vm の実行

(Windows フェールオーバークラスターを使用して) クラスター化された保護されたホストにシールドされた Vm を展開する場合は、次のコマンドレットを使用して、シールドされた VM を高可用性として構成できます。

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

シールドされた VM をクラスター内でライブ移行できるようになりました。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [VMM を使用してシールドを展開する](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)