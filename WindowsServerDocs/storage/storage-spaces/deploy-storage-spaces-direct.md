---
title: 記憶域スペース ダイレクトの展開
ms.prod: windows-server
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 06/07/2019
description: 記憶域スペースダイレクトを使用して、Windows Server のソフトウェア定義記憶域を、ハイパー集約型インフラストラクチャまたは収束 (disaggregated とも呼ばれる) インフラストラクチャとして展開する手順を説明します。
ms.localizationpriority: medium
ms.openlocfilehash: 0ab96f737f7700e202c9d0382c06859c4ea84118
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402813"
---
# <a name="deploy-storage-spaces-direct"></a>記憶域スペース ダイレクトの展開

> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、[記憶域スペースダイレクト](storage-spaces-direct-overview.md)を展開する手順について説明します。

> [!Tip]
> ハイパー集約型インフラストラクチャの取得を検討していますか? Microsoft では、展開ツールと手順を含む、検証済みのハードウェア/ソフトウェアソリューションをパートナーから購入することをお勧めします。 これらのソリューションは、互換性と信頼性を確保するために、参照アーキテクチャに対して設計、組み立て、検証を行い、迅速に稼働させることができます。 Windows Server 2019 ソリューションについては、 [AZURE STACK HCI solutions の web サイト](https://azure.microsoft.com/overview/azure-stack/hci)を参照してください。 Windows Server 2016 ソリューションの詳細については、「 [Windows Server Software Defined](https://microsoft.com/wssd)」を参照してください。

> [!Tip]
> Microsoft Azure に含まれる Hyper-v 仮想マシンを使用して、[ハードウェアなしで記憶域スペースダイレクトを評価](storage-spaces-direct-in-vm.md)することができます。 また、トレーニング目的で使用する[Windows Server の迅速なラボデプロイスクリプト](https://aka.ms/wslab)を確認することもできます。

## <a name="before-you-start"></a>開始前の作業

記憶域スペースダイレクトの[ハードウェア要件](Storage-Spaces-Direct-Hardware-Requirements.md)を確認し、このドキュメントを読み、いくつかの手順に関連する全体的なアプローチと重要な注意事項について理解してください。

次の情報を収集します。

- **配置オプション。** 記憶域スペースダイレクトで[は、ハイパー収束と収束の2つのデプロイオプション](storage-spaces-direct-overview.md#deployment-options)がサポートされています。 それぞれの利点を理解して、どちらが適切かを判断してください。 次の手順1-3 は、両方の展開オプションに適用されます。 手順4は、収束デプロイの場合にのみ必要です。

- **サーバー名。** コンピューター、ファイル、パス、およびその他のリソースに関する組織の名前付けポリシーについて理解を深めます。 複数のサーバーをプロビジョニングする必要があり、それぞれに一意の名前を付けます。

- **ドメイン名。** ドメイン名とドメイン参加に関する組織のポリシーについて理解を深めます。  サーバーをドメインに参加させるため、ドメイン名を指定する必要があります。 

- **RDMA ネットワーク。** RDMA プロトコルには、iWarp と RoCE の2種類があります。 ネットワークアダプターで使用されているものを確認し、RoCE の場合はバージョン (v1 または v2) にも注意してください。 RoCE の場合は、ラックの最上位スイッチのモデルにも注意してください。

- **VLAN ID。** サーバー上の管理 OS ネットワークアダプターに使用される VLAN ID をメモしておきます (存在する場合)。 この情報はネットワーク管理者から入手できるはずです。

## <a name="step-1-deploy-windows-server"></a>手順 1: Windows Server を展開する

### <a name="step-11-install-the-operating-system"></a>手順 1.1: オペレーティングシステムをインストールする

最初の手順では、クラスター内のすべてのサーバーに Windows Server をインストールします。 記憶域スペースダイレクトには、Windows Server 2016 Datacenter Edition が必要です。 Server Core インストールオプションまたはデスクトップエクスペリエンス搭載サーバーを使用できます。

セットアップウィザードを使用して Windows Server をインストールする場合 *、windows server (Server* Core を参照) と*Windows Server (デスクトップエクスペリエンス搭載サーバー)* のどちらかを選択できます。これは、windows server 2012 R2 で使用できる*フル*インストールオプションに相当します。 選択しない場合は、Server Core インストールオプションが表示されます。 詳細については、「 [Windows Server 2016 のインストールオプション](../../get-started/Windows-Server-2016.md)」を参照してください。

### <a name="step-12-connect-to-the-servers"></a>手順 1.2: サーバーに接続する

このガイドでは、Server Core インストールオプションに焦点を当て、別の管理システムからリモートでを展開/管理します。これには次のものが必要です。

- 管理しているサーバーと同じ更新プログラムを含む Windows Server 2016
- 管理しているサーバーへのネットワーク接続
- 同じドメインまたは完全に信頼されたドメインに参加している
- Hyper-V およびフェールオーバー クラスタリング用のリモート サーバー管理ツール (RSAT) と PowerShell モジュール。 RSAT ツールと PowerShell モジュールは Windows Server で使用でき、その他の機能をインストールしなくてもインストールできます。 Windows 10 管理 PC に[リモートサーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)をインストールすることもできます。

管理システムで、フェールオーバー クラスターと Hyper-V 管理ツールをインストールします。 この操作は、サーバー マネージャーで**役割と機能の追加**ウィザードを使用して行うことができます。 **[機能]** ページで、 **[リモート サーバー管理ツール]** を選択し、インストールするツールを選択します。

PS セッションを開始し、接続するノードのサーバー名または IP アドレスを使用します。 このコマンドを実行した後でパスワードの入力を求められます。 Windows のセットアップ時に指定した管理者パスワードを入力してください。

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   次に示すのは、スクリプトの方が便利な方法で同じことを行う例です。これを複数回実行する必要がある場合は、次のようになります。

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 管理システムからリモートで展開している場合、 *WinRM で要求を処理できない*ようなエラーが発生することがあります。 この問題を解決するには、Windows PowerShell を使用して、管理コンピューターの信頼されたホストの一覧に各サーバーを追加します。  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 注: 信頼されたホストの一覧では、`Server*`のようにワイルドカードがサポートされています。
>
> 信頼されたホストの一覧を表示するには、「`Get-Item WSMAN:\Localhost\Client\TrustedHosts`」と入力します。  
>   
> 一覧を空にするには、「`Clear-Item WSMAN:\Localhost\Client\TrustedHost`」と入力します。  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>手順 1.3: ドメインに参加してドメインアカウントを追加する

ここまでで、ローカル管理者アカウントを使用して個々のサーバーを構成しました。 `<ComputerName>\Administrator`ます。

記憶域スペースダイレクトを管理するには、サーバーをドメインに参加させ、すべてのサーバーの Administrators グループにある Active Directory Domain Services ドメインアカウントを使用する必要があります。

管理システムから、管理者特権で PowerShell コンソールを開きます。 `Enter-PSSession` を使用して各サーバーに接続し、次のコマンドレットを実際のコンピューター名、ドメイン名、ドメイン資格情報に置き換えて実行します。

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

ストレージ管理者アカウントが Domain Admins グループのメンバーでない場合は、各ノードのローカルの Administrators グループにストレージ管理者アカウントを追加します。または、さらに詳細には、記憶域管理者に使用するグループを追加します。 次のコマンドを使用できます (または Windows PowerShell 関数を記述して、詳細については、「 [powershell を使用してドメインユーザーをローカルグループに追加](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx)する」を参照してください)。

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>手順 1.4: 役割と機能をインストールする

次の手順では、すべてのサーバーにサーバーの役割をインストールします。 これを行うには、 [Windows 管理センター](../../manage/windows-admin-center/use/manage-servers.md)、[サーバーマネージャー](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md))、または PowerShell を使用します。 インストールするロールを次に示します。

- フェールオーバー クラスタリング
- Hyper-V
- ファイルサーバー (収束展開の場合など、任意のファイル共有をホストする場合)
- データ センター ブリッジング (iWARP ネットワーク アダプターではなく、RoCEv2 を使用している場合)
- RSAT クラスタ リング PowerShell
- Hyper-V の PowerShell

PowerShell を使用してインストールするには、 [install-add-windowsfeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature)コマンドレットを使用します。 これは、次のように1つのサーバーで使用できます。

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

クラスター内のすべてのサーバーでこのコマンドを同時に実行するには、このスクリプトを使用して、スクリプトの先頭にある変数の一覧を環境に合わせて変更します。

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## <a name="step-2-configure-the-network"></a>手順 2: ネットワークを構成する

仮想マシン内に記憶域スペースダイレクトを展開している場合は、このセクションをスキップします。

記憶域スペースダイレクトには、クラスター内のサーバー間に高帯域幅の低待機時間のネットワークが必要です。 少なくとも 10 GbE ネットワークが必要で、リモートダイレクトメモリアクセス (RDMA) が推奨されます。 IWARP または RoCE は、Windows Server 2016 ロゴがある限り使用できますが、iWARP は通常、セットアップが簡単です。

> [!Important]
> ネットワーク機器や、特に RoCE v2 によっては、ラックの最上位スイッチの構成が必要になる場合があります。 記憶域スペースダイレクトの信頼性とパフォーマンスを確保するには、正しいスイッチ構成が重要です。

Windows Server 2016 では、Hyper-v 仮想スイッチ内にスイッチ埋め込みのチーミング (SET) が導入されています。 これにより、RDMA を使用しているときに、すべてのネットワークトラフィックに同じ物理 NIC ポートを使用して、必要な物理 NIC ポートの数を減らすことができます。 記憶域スペースダイレクトには、スイッチ埋め込みチーミングを使用することをお勧めします。

スイッチまたは switchless ノードの相互接続
- スイッチ: ネットワークスイッチが帯域幅とネットワークの種類を処理するように適切に構成されている必要があります。 RoCE プロトコルを実装する RDMA を使用している場合は、ネットワークデバイスとスイッチの構成がさらに重要になります。
- Switchless: ノードは、直接接続を使用して相互接続できます。スイッチの使用は避けてください。 すべてのノードがクラスターの他のすべてのノードと直接接続している必要があります。

記憶域スペースダイレクトのネットワークをセットアップする手順については、「 [Windows Server 2016 の収束 NIC およびゲスト RDMA 展開ガイド](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)」を参照してください。

## <a name="step-3-configure-storage-spaces-direct"></a>手順 3: 記憶域スペース ダイレクトを構成する

次の手順は、構成されるサーバーと同じバージョンの管理システムで実行します。 次の手順は、PowerShell セッションを使用してリモートで実行するのではなく、管理システムのローカル PowerShell セッションで実行し、管理者権限で実行する必要があります。

### <a name="step-31-clean-drives"></a>手順 3.1: ドライブをクリーニングする

記憶域スペースダイレクトを有効にする前に、ドライブが空であることを確認してください。古いパーティションやその他のデータは含まれません。 コンピューター名を置き換えて、次のスクリプトを実行して、古いパーティションやその他のデータをすべて削除します。

> [!Warning]
> このスクリプトは、オペレーティングシステムのブートドライブ以外のすべてのドライブのデータを完全に削除します。

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"

Invoke-Command ($ServerList) {
    Update-StorageProviderCache
    Get-StoragePool | ? IsPrimordial -eq $false | Set-StoragePool -IsReadOnly:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$false -ErrorAction SilentlyContinue
    Get-StoragePool | ? IsPrimordial -eq $false | Remove-StoragePool -Confirm:$false -ErrorAction SilentlyContinue
    Get-PhysicalDisk | Reset-PhysicalDisk -ErrorAction SilentlyContinue
    Get-Disk | ? Number -ne $null | ? IsBoot -ne $true | ? IsSystem -ne $true | ? PartitionStyle -ne RAW | % {
        $_ | Set-Disk -isoffline:$false
        $_ | Set-Disk -isreadonly:$false
        $_ | Clear-Disk -RemoveData -RemoveOEM -Confirm:$false
        $_ | Set-Disk -isreadonly:$true
        $_ | Set-Disk -isoffline:$true
    }
    Get-Disk | Where Number -Ne $Null | Where IsBoot -Ne $True | Where IsSystem -Ne $True | Where PartitionStyle -Eq RAW | Group -NoElement -Property FriendlyName
} | Sort -Property PsComputerName, Count
```

出力は次のようになります。ここで、 **Count**は各サーバーの各モデルのドライブ数です。

```
Count Name                          PSComputerName
----- ----                          --------------
4     ATA SSDSC2BA800G4n            Server01
10    ATA ST4000NM0033              Server01
4     ATA SSDSC2BA800G4n            Server02
10    ATA ST4000NM0033              Server02
4     ATA SSDSC2BA800G4n            Server03
10    ATA ST4000NM0033              Server03
4     ATA SSDSC2BA800G4n            Server04
10    ATA ST4000NM0033              Server04
```

### <a name="step-32-validate-the-cluster"></a>手順 3.2: クラスターを検証する

この手順では、クラスター検証ツールを実行して、記憶域スペースダイレクトを使用してクラスターを作成するようにサーバーノードが正しく構成されていることを確認します。 クラスターが作成される前にクラスター検証 (`Test-Cluster`) が実行されると、フェールオーバークラスターとして正常に機能するために適切に構成されているかどうかを確認するテストが実行されます。 次の例では、`-Include` パラメーターを使用して、特定のカテゴリのテストを指定しています。 これにより、記憶域スペース ダイレクトの特定のテストが確実に検証に含まれるようになります。

記憶域スペース ダイレクト クラスターとして使用する一連のサーバーを検証するには、以下の PowerShell コマンドを使用します。

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>手順 3.3: クラスターを作成する

この手順では、次の PowerShell コマンドレットを使用して、前の手順でクラスター作成のために検証したノードを含むクラスターを作成します。

クラスターを作成すると、"クラスター化された役割の作成中に問題が発生したため、起動できない可能性があります" という警告が表示されます。 詳細については、以下のレポート ファイルを参照してください" という警告が表示されます。 この警告は無視しても問題ありません。 クラスター クォーラムで使用可能なディスクがないことが原因です。 クラスターの作成後にファイル共有監視またはクラウド監視を構成することをお勧めします。

> [!Note]
> サーバーで静的 IP アドレスを使用している場合は、以下のコマンドを変更して静的 IP アドレスを反映させます。その場合、以下のパラメーターを追加し、IP アドレスとして –StaticAddress &lt;X.X.X.X&gt; を指定します。
> 次のコマンドでは、ClusterName プレースホルダーを、15 文字以内の固有の netbios 名に置き換える必要があります。
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

クラスターが作成された後、クラスター名の DNS エントリがレプリケートされるまで時間がかかる場合があります。 この時間は、環境と DNS レプリケーションの構成に依存します。 クラスターの解決に成功しなかった場合、クラスター名の代わりに、クラスターのアクティブ メンバーであるノードのコンピューター名を使用すれば、たいていは成功します。

### <a name="step-34-configure-a-cluster-witness"></a>手順 3.4: クラスター監視を構成する

クラスターのミラーリング監視サーバーを構成することをお勧めします。これにより、3台以上のサーバーを持つクラスターは、2台のサーバーで障害が発生したり、オフラインになったりする可能性があります。 2サーバー配置にはクラスター監視が必要です。それ以外の場合は、オフラインになっているサーバーによって、もう一方も使用できなくなります。 これらのシステムでは、監視としてファイル共有を使用することも、クラウド監視を使用することもできます。 

詳細については、以下のトピックを参照してください。

- [クォーラムを構成および管理する](../../failover-clustering/manage-cluster-quorum.md)
- [フェールオーバークラスターのクラウド監視をデプロイする](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>手順 3.5: 記憶域スペース ダイレクトを有効にする

クラスターを作成したら、`Enable-ClusterStorageSpacesDirect` PowerShell コマンドレットを使用します。これにより、ストレージシステムが記憶域スペースダイレクトモードになり、次の操作が自動的に実行されます。

-   **プールを作成する:** "S2D on Cluster1" などの名前を持つ単一の大きなプールを作成します。

-   **記憶域スペース ダイレクトのキャッシュを構成する:** 記憶域スペース ダイレクトで使用可能なメディア (ドライブ) の種類が複数ある場合は、最も高速なものがキャッシュ デバイスとして構成されます (ほとんどの場合、読み書き可能なもの)。

-   **レベル:** 既定のレベルとして2つの層を作成します。 1 つを "Capacity" と呼び、もう 1 つを "Performance" と呼びます。 コマンドレットではデバイスを分析し、デバイスの種類と回復性を組み合わせて各階層を構成します。

管理システムから、管理者特権で開いた PowerShell コマンド ウィンドウで、次のコマンドを開始します。 クラスター名は、前の手順で作成したクラスターの名前です。 このコマンドをいずれかのノードのローカルで実行する場合、-CimSession パラメーターは必要ありません。

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

上のコマンドを使用して記憶域スペース ダイレクトを有効にする場合、クラスター名の代わりにノード名を使用することもできます。 新しく作成したクラスター名では DNS レプリケーションの遅延が発生する可能性があるため、ノード名を使用するほうが信頼性が高くなる場合があります。

このコマンドが完了すると (完了するまで数分かかる場合があります)、システムはボリュームを作成できる状態になります。

### <a name="step-36-create-volumes"></a>手順 3.6: ボリュームを作成する

`New-Volume` コマンドレットを使用することをお勧めします。これは、最も高速で簡単なエクスペリエンスを提供するためです。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

詳しくは、「[記憶域スペース ダイレクトのボリュームの作成](create-volumes.md)」をご覧ください。

### <a name="step-37-optionally-enable-the-csv-cache"></a>手順 3.7: オプションで CSV キャッシュを有効にする

必要に応じて、クラスターの共有ボリューム (CSV) キャッシュを有効にして、Windows キャッシュマネージャーによってまだキャッシュされていない読み取り操作のライトスルーブロックレベルキャッシュとして、システムメモリ (RAM) を使用することもできます。 これにより、Hyper-v などのアプリケーションのパフォーマンスが向上します。 CSV キャッシュを使用すると、読み取り要求のパフォーマンスを向上させることができ、スケールアウトファイルサーバーシナリオにも役立ちます。

CSV キャッシュを有効にすると、ハイパー収束クラスターで Vm を実行するために使用できるメモリの量が減ります。そのため、記憶域のパフォーマンスと Vhd で使用可能なメモリのバランスを取る必要があります。

CSV キャッシュのサイズを設定するには、記憶域クラスターに対する管理者のアクセス許可を持つアカウントを使用して、管理システムで PowerShell セッションを開き、次のスクリプトを使用して、`$ClusterName` と `$CSVCacheSize` の変数を必要に応じて変更します (この例では、サーバーごとに 2 GB の CSV キャッシュを設定します)。

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

詳細については、「 [CSV インメモリ読み取りキャッシュの使用](csv-cache.md)」を参照してください。

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>手順 3.8: ハイパー集約型展開用の仮想マシンを展開する

ハイパー収束クラスターをデプロイする場合は、最後の手順として、記憶域スペースダイレクトクラスターに仮想マシンをプロビジョニングします。

仮想マシンのファイルは、フェールオーバークラスター上のクラスター化された Vm と同様に、systems CSV 名前空間 (例: c:\\ClusterStorage\\Volume1) に格納されている必要があります。

インボックスツールまたはその他のツールを使用して、System Center Virtual Machine Manager などのストレージと仮想マシンを管理できます。

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>手順 4: 収束型ソリューションのスケールアウトファイルサーバーをデプロイする

収束ソリューションをデプロイする場合は、次の手順として、スケールアウトファイルサーバーインスタンスを作成し、いくつかのファイル共有を設定します。 ハイパー収束クラスターをデプロイしている場合は、このセクションは必要ありません。

### <a name="step-41-create-the-scale-out-file-server-role"></a>手順 4.1: スケールアウトファイルサーバーの役割を作成する

ファイルサーバーのクラスターサービスを設定する次の手順では、クラスター化されたファイルサーバーの役割を作成します。これは、継続的に使用できるファイル共有がホストされているスケールアウトファイルサーバーインスタンスを作成するときに使用します。

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>サーバーマネージャーを使用してスケールアウトファイルサーバーロールを作成するには

1. フェールオーバークラスターマネージャーで、クラスターを選択し、 **[役割]** にアクセスして、 **[役割の構成...]** をクリックします。<br>高可用性ウィザードが表示されます。
2. **[役割の選択]** ページで、 **[ファイルサーバー]** をクリックします。
3. **[ファイルサーバーの種類]** ページで、[**アプリケーションデータ] の [スケールアウトファイルサーバー**] をクリックします。
4. **[クライアントアクセスポイント]** ページで、スケールアウトファイルサーバーの名前を入力します。
5. 図1に示す**ように、ロールに移動**し、作成したクラスター化されたファイルサーバーロールの横に **[状態]** 列に **[実行中]** と表示されていることを確認して、役割が正常に設定されていることを確認します。

   スケールアウトファイルサーバーフェールオーバークラスターマネージャー表示されて(media/Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016/SOFS_in_FCM.png "スケールアウトファイルサーバーいる")![フェールオーバークラスターマネージャーのスクリーンショット]

    **図 1**実行中の状態のスケールアウトファイルサーバーを示すフェールオーバークラスターマネージャー

> [!NOTE]
>  クラスター化された役割を作成した後、数分間でファイル共有を作成できない可能性があるネットワークの伝達の遅延が発生する可能性があります。  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>Windows PowerShell を使用してスケールアウトファイルサーバーの役割を作成するには

 ファイルサーバークラスターに接続されている Windows PowerShell セッションで、次のコマンドを入力してスケールアウトファイルサーバーの役割を作成し、クラスターの名前に合わせて*Fscluster*を変更し、スケールアウトファイルサーバーの役割を付与する名前と一致するように*SOFS*します。

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  クラスター化された役割を作成した後、数分間でファイル共有を作成できない可能性があるネットワークの伝達の遅延が発生する可能性があります。 SOFS ロールが直ちに失敗して開始されない場合は、クラスターのコンピューターオブジェクトに SOFS ロールのコンピューターアカウントを作成するアクセス許可がないことが原因である可能性があります。 詳細については、このブログの投稿「[スケールアウトファイルサーバーロールがイベント id 1205、1069、および1194で開始](http://www.aidanfinn.com/?p=14142)できない」を参照してください。

### <a name="step-42-create-file-shares"></a>手順 4.2: ファイル共有を作成する

仮想ディスクを作成して Csv に追加した後、仮想ディスクごとに1つの CSV につき1つのファイル共有を作成します。 Handiest (VMM) は、アクセス許可を処理するので、これを行う方法としては想定されていますが、環境内に存在しない場合は、Windows PowerShell を使用して展開を部分的に自動化できます。 System Center Virtual Machine Manager

[Hyper-v ワークロードの SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)スクリプトに含まれるスクリプトを使用して、グループと共有の作成プロセスを部分的に自動化します。 Hyper-v ワークロード用に記述されているため、他のワークロードを展開する場合は、共有を作成した後で設定を変更したり、追加の手順を実行したりすることが必要になる場合があります。 たとえば、Microsoft SQL Server を使用している場合、SQL Server サービスアカウントには、共有およびファイルシステムに対するフルコントロール権限が付与されている必要があります。

> [!NOTE]
>  System Center Virtual Machine Manager を使用して共有を作成しない限り、クラスターノードを追加するときにグループメンバーシップを更新する必要があります。

PowerShell スクリプトを使用してファイル共有を作成するには、次の手順を実行します。

1. [Hyper-v ワークロードの SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)に含まれるスクリプトを、ファイルサーバークラスターのいずれかのノードにダウンロードします。
2. 管理システムでドメイン管理者の資格情報を使用して Windows PowerShell セッションを開き、次のスクリプトを使用して、Hyper-v コンピューターオブジェクトの Active Directory グループを作成し、変数の値を適切なものに変更します。environment

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. いずれかのストレージノードで管理者の資格情報を使用して Windows PowerShell セッションを開き、次のスクリプトを使用して各 CSV の共有を作成し、その共有に対する管理アクセス許可を Domain Admins グループとコンピューティングクラスターに付与します。

    ```PowerShell
    # Replace the values of these variables
    $StorageClusterName = "StorageSpacesDirect1"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $SOFSName = "SOFS"
    $SharePrefix = "Share"
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of the script itself
    CD $ScriptFolder
    Get-ClusterSharedVolume -Cluster $StorageClusterName | ForEach-Object
    {
        $ShareName = $SharePrefix + $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume")
        Write-host "Creating share $ShareName on "$_.name "on Volume: " $_.SharedVolumeInfo.friendlyvolumename
        .\FileShareSetup.ps1 -HyperVClusterName $StorageClusterName -CSVVolumeNumber $_.SharedVolumeInfo.friendlyvolumename.trimstart("C:\ClusterStorage\Volume") -ScaleOutFSName $SOFSName -ShareName $ShareName -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName
    }
    ```

### <a name="step-43-enable-kerberos-constrained-delegation"></a>手順 4.3 Kerberos の制約付き委任を有効にする

リモートのシナリオ管理に Kerberos の制約付き委任を設定し、ライブマイグレーションセキュリティを強化するには、いずれかの記憶域クラスターノードから、 [Hyper-v ワークロードの SMB 共有構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)に含まれる KCDSetup. ps1 スクリプトを使用します。 スクリプトのための小さなラッパーを次に示します。

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>次のステップ

クラスター化されたファイルサーバーをデプロイした後は、実際のワークロードを導入する前に、合成ワークロードを使用してソリューションのパフォーマンスをテストすることをお勧めします。 これにより、ソリューションが正常に実行されていることを確認し、残存している問題を解決してからワークロードの複雑さを増すことができます。 詳細については、「[合成ワークロードを使用した記憶域スペースのパフォーマンスのテスト](https://technet.microsoft.com/library/dn894707.aspx)」を参照してください。

## <a name="see-also"></a>関連項目

-   [Windows Server 2016 の記憶域スペースダイレクト](storage-spaces-direct-overview.md)
-   [記憶域スペースダイレクトのキャッシュについて](understand-the-cache.md)
-   [記憶域スペースダイレクトのボリュームの計画](plan-volumes.md)
-   [記憶域スペースのフォールトトレランス](storage-spaces-fault-tolerance.md)
-   [ハードウェア要件の記憶域スペースダイレクト](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question (RDMA すべきか、RDMA せざるべきか、それが問題だ)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (TechNet ブログ)
