---
title: 記憶域スペース ダイレクトの展開
ms.prod: windows-server-threshold
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 06/07/2019
description: ハイパー コンバージド インフラストラクチャまたは収束 (細分類とも呼ばれます) のインフラストラクチャのいずれかとして Storage Spaces Direct in Windows Server でのソフトウェア定義記憶域を展開する詳細な手順。
ms.localizationpriority: medium
ms.openlocfilehash: a4159c85be23025ef57084b47dcc77d4f749888f
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812358"
---
# <a name="deploy-storage-spaces-direct"></a>記憶域スペース ダイレクトの展開

> 適用対象:Windows Server 2019、Windows Server 2016

このトピックでデプロイする手順について説明します[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)します。

> [!Tip]
> Hyper-Converged インフラストラクチャを取得しようとしていますか。 検証済みハードウェア/ソフトウェア ソリューションをデプロイ ツールと手順を含むパートナーから購入することをお勧めします。 これらのソリューションの設計、アセンブル、および互換性と取得するための信頼性と簡単に実行されているように、参照アーキテクチャの検証にしていること。 Windows Server 2019 ソリューションでは、次を参照してください。、 [solutions の web サイトを Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci)します。 Windows Server 2016 のソリューションの詳細については、について説明します。 [Windows Server ソフトウェア定義](https://microsoft.com/wssd)します。

> [!Tip]
> Microsoft Azure におけるなど、HYPER-V 仮想マシンを使用する[ハードウェアなし記憶域スペース ダイレクトを評価](storage-spaces-direct-in-vm.md)します。 便利なを確認することも[Windows Server ラボの迅速な配置スクリプト](https://aka.ms/wslab)トレーニングのために使用します。

## <a name="before-you-start"></a>開始前の作業

レビュー、[記憶域スペース ダイレクトのハードウェア要件](Storage-Spaces-Direct-Hardware-Requirements.md)全体的なアプローチといくつかの手順に関連付けられている重要な注意事項を理解するには、このドキュメントを読み飛ばしてとします。

次の情報を収集します。

- **展開オプションです。** 記憶域スペース ダイレクトをサポートしています[2 つの展開オプション: ハイパーコンバージドし、コンバージド](storage-spaces-direct-overview.md#deployment-options)、細分類とも呼ばれます。 これは自分に適したを決定するそれぞれの利点を理解します。 1 ~ 3 以下の手順は、両方の展開オプションに適用されます。 手順 4 は、コンバージド展開にのみ必要です。

- **サーバー名。** コンピューター、ファイル、パス、およびその他のリソース、組織の名前付けポリシーを理解します。 各一意の名前を持つ複数のサーバーをプロビジョニングする必要があります。

- **ドメイン名です。** ドメイン名前付けとドメインに参加する組織のポリシーの理解します。  ドメインに、サーバーの参加とドメイン名を指定する必要があります。 

- **RDMA ネットワーク。** RDMA プロトコルの 2 種類があります: iWarp、RoCE します。 どちらか、ネットワーク アダプターを使用して、注場合 RoCE、メモ (v1 または v2) のバージョンもします。 、RoCE 用も - top-of-rack スイッチのモデルを注意してください。

- **VLAN ID。** 存在する場合は、管理 OS のネットワーク アダプターのサーバーで使用する VLAN ID に注意してください。 この情報はネットワーク管理者から入手できるはずです。

## <a name="step-1-deploy-windows-server"></a>手順 1:Windows Server を展開します。

### <a name="step-11-install-the-operating-system"></a>手順 1.1:オペレーティング システムをインストールする

最初の手順では、クラスターに追加するすべてのサーバーで Windows Server をインストールします。 記憶域スペース ダイレクトでは、Windows Server 2016 Datacenter Edition が必要です。 デスクトップ エクスペリエンス搭載、Server Core インストール オプション、またはサーバーを使用することができます。

セットアップ ウィザードを使用して Windows Server をインストールするときのことができます*Windows Server* (Server Core を参照する) と*Windows Server (デスクトップ エクスペリエンス搭載サーバー)* 、これは、相当です*完全*インストール オプションの Windows Server 2012 R2 で使用できます。 ない場合は、Server Core インストール オプションが表示されます。 詳細については、次を参照してください。 [Windows Server 2016 のインストール オプション](../../get-started/Windows-Server-2016.md)します。

### <a name="step-12-connect-to-the-servers"></a>手順 1.2:サーバーに接続します。

このガイドでは、Server Core インストール オプションと個別の管理システムである必要がありますからリモートで展開する/管理重点を置いています。

- Windows Server 2016 は、管理サーバーと同じ更新プログラム
- 管理サーバーへのネットワーク接続
- 同じドメインまたは完全に信頼されたドメインに参加しています。
- Hyper-V およびフェールオーバー クラスタリング用のリモート サーバー管理ツール (RSAT) と PowerShell モジュール。 RSAT ツールと PowerShell モジュールは Windows Server で使用でき、その他の機能をインストールしなくてもインストールできます。 インストールすることも、[リモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)Windows 10 PC の管理にします。

管理システムで、フェールオーバー クラスターと Hyper-V 管理ツールをインストールします。 この操作は、サーバー マネージャーで**役割と機能の追加**ウィザードを使用して行うことができます。 **[機能]** ページで、 **[リモート サーバー管理ツール]** を選択し、インストールするツールを選択します。

PS セッションを開始し、接続するノードのサーバー名または IP アドレスを使用します。 きっとこのコマンドを実行した後、パスワードの入力を求め、Windows セットアップ時に指定した管理者パスワードを入力してください。

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   これを 2 回以上実行する必要がある場合に、スクリプトでより便利な方法で同じことを実現する例を次に示します。

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 管理システムからリモートで展開している場合のようなエラーが発生する可能性があります*WinRM は、要求を処理できません。* この問題を解決するのにには、各サーバーを管理コンピューターに信頼されたホスト一覧に追加するのに Windows PowerShell を使用します。  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 注: 信頼されたホストの一覧をサポートしています、ワイルドカードなど`Server*`します。
>
> 信頼されたホスト一覧を表示するには、次のように入力します。`Get-Item WSMAN:\Localhost\Client\TrustedHosts`します。  
>   
> 一覧を空にするには、入力`Clear-Item WSMAN:\Localhost\Client\TrustedHost`します。  

### <a name="step-13-join-the-domain-and-add-domain-accounts"></a>手順 1.3:ドメインに参加し、ドメイン アカウントを追加

これまでに、ローカル管理者アカウントで個々 のサーバーを構成した`<ComputerName>\Administrator`します。

記憶域スペース ダイレクトを管理するには、サーバーがドメインに参加して内のすべてのサーバーの Administrators グループにある Active Directory Domain Services ドメイン アカウントを使用する必要があります。

管理システムからは、管理者特権で PowerShell コンソールを開きます。 使用`Enter-PSSession`を各サーバーに接続し、独自のコンピューター名、ドメイン名、およびドメインの資格情報に置き換えて、次のコマンドレットを実行します。

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

ストレージ管理者アカウントが Domain Admins グループのメンバーでない場合、各ノードでローカルの Administrators グループに、記憶域の管理者アカウントを追加またはさらに、記憶域管理者に使用するグループを追加します。 次のコマンドを使用することができます (そのため、確認する Windows PowerShell 関数を作成または[ローカル グループにドメイン ユーザーを追加するには、PowerShell の使用](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx)の詳細)。

```
Net localgroup Administrators <Domain\Account> /add
```

### <a name="step-14-install-roles-and-features"></a>手順 1.4:役割と機能をインストールします。

次の手順では、すべてのサーバーでサーバーの役割をインストールします。 使用してこれを行う[Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md)、[サーバー マネージャー](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md))、または PowerShell。 インストールする役割を次に示します。

- フェールオーバー クラスタリング
- Hyper-V
- (コンバージド展開など、ファイル共有をホストする) 場合、ファイル サーバー
- データ センター ブリッジング (iWARP ネットワーク アダプターではなく、RoCEv2 を使用している場合)
- RSAT クラスタ リング PowerShell
- Hyper-V の PowerShell

PowerShell を使用してをインストールするには、使用、 [Install-windowsfeature](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature)コマンドレット。 このような単一のサーバーで使用できます。

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

同時に、クラスター内のすべてのサーバー上でコマンドを実行するには、少しばかりの環境に合わせてスクリプトの先頭での変数の一覧を変更するスクリプトを使用します。

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## <a name="step-2-configure-the-network"></a>手順 2:ネットワークの構成

仮想マシン内で記憶域スペース ダイレクトを展開して、このセクションをスキップします。

記憶域スペース ダイレクトでは、高帯域幅、待ち時間の少ないクラスター内のサーバーの間のネットワークが必要です。 少なくとも 10 GbE のネットワークが必要ですし、リモート ダイレクト メモリ アクセス (RDMA) をお勧めします。 Windows Server 2016 ロゴがあるが、iWARP が通常は簡単にセットアップする限り、iWARP または RoCE のいずれかを使用することができます。

> [!Important]
> によって、ネットワーク機器、および、RoCE v2 では特に - top-of-rack スイッチのいくつかの構成が必要な場合があります。 適切なスイッチの構成は記憶域スペース ダイレクトの信頼性とパフォーマンスを確認します。

Windows Server 2016 では、スイッチ埋め込みチーミング (SET) 内での HYPER-V 仮想スイッチについて説明します。 これにより、必要な物理 NIC ポートの数を減らすと、RDMA の使用中にすべてのネットワーク トラフィックに使用する同じ物理 NIC ポートです。 記憶域スペース ダイレクト、スイッチ埋め込みチーミングすることをお勧めします。

ネットワーク接続記憶域スペース ダイレクトをセットアップする手順については、次を参照してください。 [Windows Server 2016 コンバージド NIC とゲスト RDMA の展開ガイド](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)します。

## <a name="step-3-configure-storage-spaces-direct"></a>手順 3:記憶域スペース ダイレクトの構成

次の手順は、構成されるサーバーと同じバージョンの管理システムで実行します。 次の手順をリモート PowerShell セッションを使用して実行できませんが代わりに管理者権限で、管理システムでローカルの PowerShell セッションで実行する必要があります。

### <a name="step-31-clean-drives"></a>手順 3.1:ドライブのクリーンアップ

記憶域スペース ダイレクトを有効する前に、ドライブが空ことを確認します。 古いパーティションのない、またはその他のデータ。 すべての古いパーティションまたはその他のデータを削除する、コンピューター名を置き換えて、次のスクリプトを実行します。

> [!Warning]
> このスクリプトでは、オペレーティング システムのブート ドライブ以外のすべてのドライブ上のデータを完全に削除されます。

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

出力は、次のようになります、**カウント**は各サーバーの各モデルのドライブの数です。

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

### <a name="step-32-validate-the-cluster"></a>手順 3.2:クラスターを検証します。

この手順では、記憶域スペース ダイレクトを使用してクラスターを作成するサーバーのノードが正しく構成されていることを確認して、クラスター検証ツールを実行します。 クラスターの検証 (`Test-Cluster`) は、構成がフェールオーバー クラスターとして正常に機能するに適した表示されることを確認するテストを実行するクラスターを作成する前に実行します。 直接使用して次の例、`-Include`パラメーターとし、テストの特定のカテゴリを指定します。 これにより、記憶域スペース ダイレクトの特定のテストが確実に検証に含まれるようになります。

記憶域スペース ダイレクト クラスターとして使用する一連のサーバーを検証するには、以下の PowerShell コマンドを使用します。

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### <a name="step-33-create-the-cluster"></a>手順 3.3:クラスターを作成する。

この手順では、次の PowerShell コマンドレットを使用して、前の手順でクラスターを作成するために検証したノードとクラスターを作成します。

クラスターを作成するときを示す警告が表示されます -"問題があるクラスター化された役割を作成することができない開始中にします。 詳細については、以下のレポート ファイルを参照してください" という警告が表示されます。 この警告は無視してかまいません。 クラスター クォーラムで使用可能なディスクがないことが原因です。 クラスターの作成後にファイル共有監視またはクラウド監視を構成することをお勧めします。

> [!Note]
> サーバーで静的 IP アドレスを使用している場合は、以下のコマンドを変更して静的 IP アドレスを反映させます。その場合、以下のパラメーターを追加し、IP アドレスとして –StaticAddress &lt;X.X.X.X&gt; を指定します。
> 次のコマンドでは、ClusterName プレースホルダーを、15 文字以内の固有の netbios 名に置き換える必要があります。
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

クラスターが作成された後、クラスター名の DNS エントリがレプリケートされるまで時間がかかる場合があります。 この時間は、環境と DNS レプリケーションの構成に依存します。 クラスターの解決に成功しなかった場合、クラスター名の代わりに、クラスターのアクティブ メンバーであるノードのコンピューター名を使用すれば、たいていは成功します。

### <a name="step-34-configure-a-cluster-witness"></a>手順 3.4:クラスターの監視を構成します。

次の 3 つまたは複数のサーバーを持つクラスターが失敗するかオフラインになった 2 つのサーバーに耐えられるように、クラスターでは、ミラーリング監視サーバーを構成することをお勧めします。 それ以外の場合も使用不可になるその他によりいずれかのサーバーがオフラインにして、2 台のサーバー配置にクラスターの監視が必要です。 これらのシステムでは、監視としてファイル共有を使用することも、クラウド監視を使用することもできます。 

詳細については、以下のトピックを参照してください。

- [クォーラムを構成および管理する](../../failover-clustering/manage-cluster-quorum.md)
- [フェールオーバー クラスターのクラウド監視をデプロイします。](../../failover-clustering/deploy-cloud-witness.md)

### <a name="step-35-enable-storage-spaces-direct"></a>手順 3.5:記憶域スペース ダイレクトを有効にする

クラスターを作成した後、 `Enable-ClusterStorageSpacesDirect` PowerShell コマンドレットに渡して、記憶域システムを記憶域スペース ダイレクト モードに設定され、自動的に、次の操作を行います。

-   **プールを作成します。** "S2D on Cluster1"などの名前を持つ単一の大きなプールを作成します。

-   **記憶域スペース ダイレクトのキャッシュを構成します。** できます (読み取りし、書き込みでは、ほとんどの場合) のキャッシュ デバイスとして最も高速な 1 つ以上のメディア (ドライブ) の種類が記憶域スペース ダイレクトの使用可能な場合

-   **階層:** 既定の階層として 2 つの層を作成します。 1 つを "Capacity" と呼び、もう 1 つを "Performance" と呼びます。 コマンドレットではデバイスを分析し、デバイスの種類と回復性を組み合わせて各階層を構成します。

管理システムから、管理者特権で開いた PowerShell コマンド ウィンドウで、次のコマンドを開始します。 クラスター名は、前の手順で作成したクラスターの名前です。 このコマンドをいずれかのノードのローカルで実行する場合、-CimSession パラメーターは必要ありません。

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

上のコマンドを使用して記憶域スペース ダイレクトを有効にする場合、クラスター名の代わりにノード名を使用することもできます。 新しく作成したクラスター名では DNS レプリケーションの遅延が発生する可能性があるため、ノード名を使用するほうが信頼性が高くなる場合があります。

このコマンドが完了すると (完了するまで数分かかる場合があります)、システムはボリュームを作成できる状態になります。

### <a name="step-36-create-volumes"></a>手順 3.6:ボリュームの作成

使用をお勧め、`New-Volume`ほどコマンドレットは、最も高速かつ最も簡単なエクスペリエンスを提供します。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

詳しくは、「[記憶域スペース ダイレクトのボリュームの作成](create-volumes.md)」をご覧ください。

### <a name="step-37-optionally-enable-the-csv-cache"></a>手順 3.7:必要に応じて、CSV キャッシュを有効にします。

必要に応じて、Windows のキャッシュ マネージャーによって既にキャッシュは読み取り操作のライト スルー ブロック レベル キャッシュとしてのシステム メモリ (RAM) を使用するクラスターの共有ボリューム (CSV) キャッシュを有効にできます。 これにより、HYPER-V などのアプリケーションのパフォーマンスが向上することができます。 CSV キャッシュは読み取り要求のパフォーマンスを向上させることができ、スケール アウト ファイル サーバーのシナリオにも役立ちます。

CSV キャッシュを有効にするには、Vhd を使用可能なメモリと記憶域のパフォーマンスのバランスを取る必要があるありますので、ハイパーコンバージド クラスターに Vm を実行する使用可能なメモリの量が軽減されます。

CSV キャッシュのサイズを設定する、記憶域クラスターの管理者権限を持つアカウントを使用して管理システムでの PowerShell セッションを開くし、変更、このスクリプトを使用して、`$ClusterName`と`$CSVCacheSize`(これを適切な変数例の設定 1 サーバーあたり 2 GB の CSV キャッシュ)。

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

詳細については、次を参照してください。[インメモリ CSV を使用してキャッシュを読み取る](csv-cache.md)します。

### <a name="step-38-deploy-virtual-machines-for-hyper-converged-deployments"></a>手順 3-8:ハイパーコンバージド展開用の仮想マシンをデプロイします。

ハイパーコンバージド クラスターをデプロイする場合、最後の手順では、記憶域スペース ダイレクト クラスターで仮想マシンをプロビジョニングします。

仮想マシンのファイルは、システム CSV 名前空間に保存する必要があります (例: c:\\ClusterStorage\\Volume1) フェールオーバー クラスターでクラスター化された Vm と同様です。

付属のツールや他のツールを使用して、記憶域と仮想マシン、System Center Virtual Machine Manager などを管理することができます。

## <a name="step-4-deploy-scale-out-file-server-for-converged-solutions"></a>手順 4:集約型のソリューションのスケール アウト ファイル サーバーをデプロイします。

収束のソリューションをデプロイする場合、次の手順は、スケール アウト ファイル サーバー インスタンスを作成して、いくつかのファイル共有をセットアップするは。 完了して、これは必要ありません、ハイパーコンバージド クラスターにデプロイする場合のセクション。

### <a name="step-41-create-the-scale-out-file-server-role"></a>手順 4.1:スケール アウト ファイル サーバー ロールを作成します。

次に、ファイル サーバー クラスター サービスを設定するには、継続的に使用可能なファイル共有がホストされているスケール アウト ファイル サーバー インスタンスを作成するときに、クラスター化されたファイルのサーバーの役割を作成しています。

#### <a name="to-create-a-scale-out-file-server-role-by-using-server-manager"></a>サーバー マネージャーを使用してスケール アウト ファイル サーバーの役割を作成するには

1. フェールオーバー クラスター マネージャーでは、クラスターを選択しに移動して、**ロール**、順にクリックします**役割の構成.** .<br>高可用性ウィザードが表示されます。
2. **役割の選択**] ページで [**ファイル サーバー**します。
3. **ファイル サーバーの種類**] ページで [**アプリケーション データ用のスケール アウト ファイル サーバー**します。
4. **クライアント アクセス ポイント** ページで、スケール アウト ファイル サーバーの名前を入力します。
5. ロールが正常に設定されているに移動して確認**ロール**いることを確認し、**状態**列には**を実行している**、作成したクラスター化されたファイル サーバーの役割の横にあります。図 1 に示す。

   ![スケール アウト ファイル サーバー フェールオーバー クラスター マネージャーのスクリーン ショット](media/Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016/SOFS_in_FCM.png "スケール アウト ファイル サーバー フェールオーバー クラスター マネージャー")

    **図 1**フェールオーバー クラスター マネージャーの実行中の状態でスケール アウト ファイル サーバーの表示

> [!NOTE]
>  クラスター化された役割を作成するには、後にある可能性がありますいくつかのネットワークから数分後に、または長い可能性があることでファイル共有の作成を妨げる可能性のある伝達の遅延。  
  
#### <a name="to-create-a-scale-out-file-server-role-by-using-windows-powershell"></a>Windows PowerShell を使用してスケール アウト ファイル サーバー ロールを作成するには

 ファイル サーバー クラスターに接続されている Windows PowerShell セッションで、変更、スケール アウト ファイル サーバー ロールを作成するには、次のコマンドを入力します*FSCLUSTER* 、クラスターの名前と一致すると*SOFS。* をスケール アウト ファイル サーバーの役割を与えたい名と一致します。

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  クラスター化された役割を作成するには、後にある可能性がありますいくつかのネットワークから数分後に、または長い可能性があることでファイル共有の作成を妨げる可能性のある伝達の遅延。 SOFS ロールがすぐに失敗が起動しない場合は、クラスターのコンピューター オブジェクトの SOFS ロールのコンピューター アカウントを作成するアクセス許可のない可能性があります。 このブログの投稿をその参照に役立ちます。[スケール アウト ファイル サーバーのロールが失敗イベント Id 1205、1069、および 1194 で開始する](http://www.aidanfinn.com/?p=14142)します。

### <a name="step-42-create-file-shares"></a>手順 4.2:ファイル共有を作成します。

仮想ディスクを作成し、Csv に追加したが後、は、CSV あたり 1 つの仮想ディスクの 1 つのファイル共有には、ファイル共有を作成する時間を勧めします。 System Center Virtual Machine Manager (VMM) は、おそらく便利方法は、処理、アクセス許可が、環境内でがない場合は、部分的に展開を自動化する Windows PowerShell を使用できます。

含まれるスクリプトを使用して、 [HYPER-V ワークロード用の SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)部分的にグループと共有を作成するプロセスを自動化するスクリプト。 HYPER-V のワークロードでは、書き込まれるため、他のワークロードをデプロイする場合は、設定を変更または共有を作成した後、追加の手順を実行する必要があります。 たとえば、Microsoft SQL Server を使用している場合、SQL Server サービス アカウント与える必要があります、共有とファイル システムへのフル コントロール。

> [!NOTE]
>  System Center Virtual Machine Manager を使用して、共有を作成しない限り、クラスター ノードを追加すると、グループ メンバーシップを更新する必要があります。

PowerShell スクリプトを使用してファイル共有を作成するには、次の操作を行います。

1. 含まれるスクリプトをダウンロード[HYPER-V ワークロード用の SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)ファイル サーバー クラスターのノードの 1 つ。
2. ドメイン管理者の資格情報管理システムで Windows PowerShell セッションを開くし、HYPER-V コンピュータ オブジェクト用の適切な変数の値を変更する Active Directory グループを作成する次のスクリプトを使用して環境:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. 記憶域ノードのいずれかの管理者の資格情報で Windows PowerShell セッションを開くし、各 CSV 用の共有を作成し、Domain Admins グループと、コンピューティング クラスターに、共有に対する管理権限を付与する次のスクリプトを使用します。

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

### <a name="step-43-enable-kerberos-constrained-delegation"></a>手順 4.3 を有効にする Kerberos の制約付き委任

リモートのシナリオの管理と、記憶域クラスターのノードのいずれかからのライブ マイグレーション セキュリティを強化に含まれる KCDSetup.ps1 スクリプトを使用する Kerberos の制約付き委任をセットアップする[HYPER-V ワークロードのSMB共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a). スクリプトのほとんどのラッパーを次に示しません。

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## <a name="next-steps"></a>次のステップ

クラスター化されたファイル サーバーをデプロイした後、実際のワークロードを構成する前に、合成ワークロードを使用して、ソリューションのパフォーマンス テストをお勧めします。 これにより、ソリューションが正しく実行していることを確認し、ワークロードの複雑さを追加する前に残留問題に対処できます。 詳細については、次を参照してください。[テスト記憶域スペースのパフォーマンスを使用して合成ワークロード](https://technet.microsoft.com/library/dn894707.aspx)します。

## <a name="see-also"></a>関連項目

-   [Windows Server 2016 での記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
-   [記憶域スペース ダイレクトでは、キャッシュを理解します。](understand-the-cache.md)
-   [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
-   [記憶域スペースのフォールト トレランス](storage-spaces-fault-tolerance.md)
-   [記憶域スペース ダイレクトのハードウェア要件](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question (RDMA すべきか、RDMA せざるべきか、それが問題だ)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (TechNet ブログ)
