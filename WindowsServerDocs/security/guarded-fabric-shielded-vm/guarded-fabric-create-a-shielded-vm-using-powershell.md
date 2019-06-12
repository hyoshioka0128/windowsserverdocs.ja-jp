---
title: PowerShell を使用して、シールドされた VM を作成します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 0086edb7781a604cc90b9e76d34e5a3dc2725547
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447525"
---
# <a name="create-a-shielded-vm-using-powershell"></a>PowerShell を使用して、シールドされた VM を作成します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

運用環境では、シールドされた Vm をデプロイする通常 fabric manager (VMM など) を使用します。 ただし、次の図の手順を使用すると、デプロイし、ファブリック マネージャーがないシナリオ全体を検証できます。

簡単に言うと、すべてのコンピューターでテンプレート ディスク、シールド データ ファイルを無人インストール応答ファイル、およびその他のセキュリティ アーティファクトを作成は保護されたホストにこれらのファイルをコピーし、シールドされた VM のプロビジョニングとします。

## <a name="create-a-signed-template-disk"></a>署名付きテンプレート ディスクを作成します。

新しいシールドされた VM を作成するには、最初は、OS ボリューム (または Linux 上のブートとルート パーティション) で署名済み暗号化は、シールドされた VM テンプレート ディスクを必要します。
テンプレート ディスクを作成する方法の詳細については、以下のリンクに従います。

- [Windows のテンプレート ディスクを準備します。](guarded-fabric-create-a-shielded-vm-template.md)
- [Linux のテンプレート ディスクを準備します。](guarded-fabric-create-a-linux-shielded-vm-template.md)

シールド データ ファイルを作成するディスクのボリューム署名カタログのコピーも必要になります。
このファイルを保存するには、テンプレート ディスクを作成したコンピューターの次のコマンドを実行します。

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath "C:\temp\MyTemplateDisk.vhdx" -VolumeSignatureCatalogPath "C:\temp\MyTemplateDiskCatalog.vsc"
```

## <a name="download-guardian-metadata"></a>ガーディアン メタデータをダウンロードします。

シールドされた VM を実行する仮想化ファブリックのそれぞれについては HGS クラスターのファブリックのガーディアン メタデータを取得する必要があります。
ホスティング プロバイダーは、この情報を提供できる必要があります。

ガーディアン メタデータは、エンタープライズ環境では、HGS サーバーと通信できる場合は、 *http://\<HGSCLUSTERNAME\>/KeyProtection/service/metadata/2014-07/metadata.xml*

## <a name="create-shielding-data-pdk-file"></a>シールド データ (PDK) ファイルを作成します。

シールド データが作成されるとテナント VM の所有者によって所有されているし、シールドされた VM の管理者パスワードなど、ファブリック管理者から保護する必要がシールドされた Vm を作成するために必要な機密情報が含まれています。
HGS サーバーとテナントのみ暗号化を解除できるように、シールド データが暗号化されます。
テナント VM/所有者によって作成されると、結果として得られる PDK ファイルが保護されたファブリックをコピーする必要があります。
詳細については、次を参照してください。[シールド データを使用するものが、なぜ必要ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)します。

さらに、必要があります、無人インストール応答ファイル (、Windows の unattend.xml for Linux は異なります)。 参照してください[応答ファイルを作成](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file)ガイダンスについては、応答ファイルに含める内容にします。

シールドされた Vm がインストールされているため、コンピューター、リモート サーバー管理ツールで、次のコマンドレットを実行します。
PDK を Linux VM を作成する場合は、Windows Server バージョン 1709 以降を実行するサーバーでこれを行う必要があります。

 
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
    
## <a name="provision-shielded-vm-on-a-guarded-host"></a>保護されたホストでシールドされた VM のプロビジョニング
保護されたホストの展開を準備するには、テンプレート ディスク ファイル (ServerOS.vhdx) と PDK ファイル (contoso.pdk) をコピーします。

保護されたホストでは、プロビジョニング プロセスを簡略化する新しい shieldedvm の各コマンドレットを含む保護されたファブリックのツールの PowerShell モジュールをインストールします。 保護されたホストにインターネットへのアクセスがある場合は、次のコマンドを実行します。

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

インターネットにアクセスし、結果として得られるモジュールのコピーを持つ別のコンピューター上のモジュールをダウンロードすることもできます。`C:\Program Files\WindowsPowerShell\Modules`で保護されたホストです。

```powershell
Save-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0 -Path C:\temp\
```

モジュールをインストールするには、シールドされた VM をプロビジョニングする準備ができました。

```powershell
New-ShieldedVM -Name 'MyShieldedVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait
```

テンプレート ディスクに Linux ベースの OS が含まれている場合は、`-Linux`コマンドの実行時フラグを設定します。

```powershell
New-ShieldedVM -Name 'MyLinuxVM' -TemplateDiskPath 'C:\temp\MyTemplateDisk.vhdx' -ShieldingDataFilePath 'C:\temp\Contoso.pdk' -Wait -Linux
```

ヘルプ コンテンツを使用して、確認`Get-Help New-ShieldedVM -Full`詳細については、その他のオプションをコマンドレットに渡すことができます。

VM では、プロビジョニングが完了すると、過ぎた後ことが使用できるように、OS 固有の特殊化フェーズを入力します。
(RDP、PowerShell、SSH、または任意の管理ツールを使用して) 実行後に接続するために、有効なネットワークに VM を接続することを確認します。

## <a name="running-shielded-vms-on-a-hyper-v-cluster"></a>シールドされた Vm を HYPER-V クラスターで実行されています。

(Windows フェールオーバー クラスターを使用して) クラスターの保護されたホストでシールドされた Vm をデプロイしようとする場合に高い可用性を次のコマンドレットを使用して、シールドされた VM を構成できます。

```powershell
Add-ClusterVirtualMachineRole -VMName 'MyShieldedVM' -Cluster <Hyper-V cluster name>
```

シールドされた VM できるようになりましたライブ クラスター内で移行します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [デプロイをシールドされた VMM を使用して](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)