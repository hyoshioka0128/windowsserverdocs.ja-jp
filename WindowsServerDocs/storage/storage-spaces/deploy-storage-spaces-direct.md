---
title: 記憶域スペース ダイレクトの展開
ms.prod: windows-server-threshold
manager: eldenc
ms.author: stevenek
ms.technology: storage-spaces
ms.topic: get-started-article
ms.assetid: 20fee213-8ba5-4cd3-87a6-e77359e82bc0
author: stevenek
ms.date: 8/16/2018
description: ハイパーコンバージド インフラストラクチャまたはコンバージド (集約型とも呼ばれます) のインフラストラクチャのいずれかとして記憶域スペース ダイレクトでは、Windows Server ソフトウェア定義記憶域を展開する手順を示します。
ms.localizationpriority: medium
ms.openlocfilehash: 55cfa0e066506d7174f9e5b1e61cc0aa290706d7
ms.sourcegitcommit: 65e4f760be73104e67847f77e834e7b5e065211b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "5429044"
---
# 記憶域スペース ダイレクトの展開

> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)を展開するための詳しい手順を説明します。

> [!Tip]
> ハイパーコンバージド インフラストラクチャを取得しようとしているかどうか。 Microsoft では、パートナーからこれらの[Windows Server ソフトウェア定義](https://microsoft.com/wssd)ソリューションをお勧めします。 設計、アセンブル、および互換性と取得するための信頼性とすばやく実行していることを確認するには、当社の参照をアーキテクチャに対して検証します。

> [!Tip]
> Microsoft azure では、[記憶域スペース ダイレクトのハードウェアを評価](storage-spaces-direct-in-vm.md)するなど、HYPER-V 仮想マシンを使用することができます。 便利な[Windows Server の迅速なラボの展開スクリプト](https://aka.ms/wslab)トレーニングの目的の使用を確認することもできます。

## 開始前の作業

[記憶域スペース ダイレクトのハードウェア要件](Storage-Spaces-Direct-Hardware-Requirements.md)を確認し、重要な注意事項がいくつかの手順に関連付けられている、全体的なアプローチを理解するには、このドキュメントを読み取るようにします。

次の情報を収集します。

- **展開オプションです。** 記憶域スペース ダイレクトのサポート[2 つの展開オプション: ハイパーコンバージドおよび集約型の](storage-spaces-direct-overview.md#deployment-options)、集約型とも呼ばれます。 これが適切かを決定するそれぞれの利点を理解します。 手順 1 ~ 3 以下では、両方の展開オプションに適用されます。 手順 4 はコンバージド展開に必要なだけです。

- **サーバー名。** コンピューター、ファイル、パス、およびその他のリソースの名前付けポリシーを組織の知識を取得します。 それぞれ一意の名前を持つ複数のサーバーをプロビジョニングする必要があります。

- **ドメイン名。** ドメインの名前付けと、ドメインに参加するための組織のポリシーを使い慣れてを取得します。  サーバーをドメインに参加して、ドメイン名を指定する必要があります。 

- **RDMA ネットワーク。** RDMA プロトコルの 2 種類があります: iWarp や RoCE します。 注: いずれが、ネットワーク アダプターを使用して、し、RoCE、また注意してください (v1 または v2) のバージョン。 RoCE のも、上部のラックのスイッチのモデルに注意してください。

- **VLAN ID。** 存在する場合は、サーバー上のネットワーク アダプターの OS の管理に使用される VLAN ID に注意してください。 この情報はネットワーク管理者から入手できるはずです。

## 手順 1: Windows Server を展開する

### 手順 1.1: オペレーティング システムをインストールします。

最初の手順では、クラスターを構成するすべてのサーバーを Windows Server をインストールします。 記憶域スペース ダイレクトでは、Windows Server 2016 Datacenter Edition が必要です。 デスクトップ エクスペリエンス搭載サーバー、Server Core インストール オプションを使用できます。

セットアップ ウィザードを使用して Windows Server をインストールするときのできます (Server Core を参照) *Windows Server*および*Windows Server (デスクトップ エクスペリエンス搭載サーバー)* と同等の*完全な*インストール オプションであります。Windows Server 2012 R2 で利用できます。 しない場合は、Server Core インストール オプションが表示されます。 詳細については、 [Windows Server 2016 のインストール オプション](../../get-started/Windows-Server-2016.md)を参照してください。

### 手順 1.2: サーバーに接続します。

このガイドでは、Server Core インストール オプションと、別の管理システムが必要ですからリモートでの展開/管理焦点を当てています。

- Windows Server 2016 は、管理対象のサーバーと同じ更新プログラム
- 管理対象のサーバーへのネットワーク接続
- 同じドメインまたは完全に信頼されたドメインに参加しています。
- Hyper-V およびフェールオーバー クラスタリング用のリモート サーバー管理ツール (RSAT) と PowerShell モジュール。 RSAT ツールと PowerShell モジュールは Windows Server で使用でき、その他の機能をインストールせずにインストールできます。 Windows 10 の管理 PC で[リモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)をインストールすることもできます。

管理システムで、フェールオーバー クラスターと Hyper-V 管理ツールをインストールします。 この操作は、サーバー マネージャーで**役割と機能の追加**ウィザードを使用して行うことができます。 **[機能]** ページで、**[リモート サーバー管理ツール]** を選択し、インストールするツールを選択します。

PS セッションを開始し、接続するノードのサーバー名または IP アドレスを使用します。 次のコマンドを実行した後、パスワードの入力を求め、Windows のセットアップ時に指定した管理者パスワードを入力します。

   ```PowerShell
   Enter-PSSession -ComputerName <myComputerName> -Credential LocalHost\Administrator
   ```

   これを複数回実行する必要がある場合、スクリプトでより便利な方法で同じことを行う例を次に示します。

   ```PowerShell
   $myServer1 = "myServer-1"
   $user = "$myServer1\Administrator"

   Enter-PSSession -ComputerName $myServer1 -Credential $user
   ```

> [!TIP]
> 管理システムからリモートで展開する場合のようなエラーを取得する可能性があります*WinRM が要求を処理できません*。 この問題を解決するのにには、各サーバーを管理コンピューターの信頼されたホストの一覧に追加するのに Windows PowerShell を使用します。  
>   
> `Set-Item WSMAN:\Localhost\Client\TrustedHosts -Value Server01 -Force`
>  
> 注: 信頼されたホストの一覧をサポート ワイルドカードはこのような`Server*`します。
>
> 信頼されたホストの一覧を表示するには、入力`Get-Item WSMAN:\Localhost\Client\TrustedHosts`します。  
>   
> 一覧を空にするには、入力`Clear-Item WSMAN:\Localhost\Client\TrustedHost`します。  

### 手順 1.3: ドメインに参加し、ドメイン アカウントを追加します。

ここまで、ローカル管理者アカウントで個々 のサーバーを構成した`<ComputerName>\Administrator`します。

記憶域スペース ダイレクトを管理するには、サーバーをドメインに参加させるし、すべてのサーバー上の管理者グループに含まれる Active Directory Domain Services ドメイン アカウントを使用する必要があります。

管理システムから、管理者特権で PowerShell コンソールを開きます。 使用`Enter-PSSession`各サーバーに接続し、独自のコンピューター名、ドメイン名、およびドメイン資格情報に置き換えて、次のコマンドレットを実行します。

```PowerShell  
Add-Computer -NewName "Server01" -DomainName "contoso.com" -Credential "CONTOSO\User" -Restart -Force  
```

記憶域管理者アカウントには、Domain Admins グループのメンバーがない場合は場合、は、各ノードのローカル Administrators グループに、記憶域管理者アカウントを追加するか、さらに、管理者は記憶域を使用するグループを追加します。 次のコマンドを使用して (またはできますように - について詳しくは[ローカル グループにドメイン ユーザーを追加する PowerShell を使用](http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/19/use-powershell-to-add-domain-users-to-a-local-group.aspx)する Windows PowerShell 関数を作成)。

```
Net localgroup Administrators <Domain\Account> /add
```

### 手順 1.4: 役割と機能をインストールします。

次の手順では、すべてのサーバーのサーバーの役割をインストールします。 これを行う[Windows Admin Center](../../manage/windows-admin-center/use/manage-servers.md)、[サーバー マネージャー](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)を使用して)、または PowerShell します。 インストールする役割を以下に示します。

- フェールオーバー クラスタリング
- Hyper-V
- (コンバージド展開など、ファイル共有をホストするには) 場合、ファイル サーバー
- データ センター ブリッジング (iWARP ネットワーク アダプターではなく、RoCEv2 を使用している場合)
- RSAT クラスタ リング PowerShell
- Hyper-V の PowerShell

PowerShell を使ってインストールするには、[インストール](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature)したらを使用します。 このような単一サーバーに使用できます。

```PowerShell
Install-WindowsFeature -Name "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"
```

同時に、クラスター内のすべてのサーバーでコマンドを実行するには、この少し環境に適したスクリプトの開始時の変数の一覧を変更するスクリプトを使用します。

```PowerShell
# Fill in these variables with your values
$ServerList = "Server01", "Server02", "Server03", "Server04"
$FeatureList = "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "RSAT-Clustering-PowerShell", "Hyper-V-PowerShell", "FS-FileServer"

# This part runs the Install-WindowsFeature cmdlet on all servers in $ServerList, passing the list of features into the scriptblock with the "Using" scope modifier so you don't have to hard-code them here.
Invoke-Command ($ServerList) {
    Install-WindowsFeature -Name $Using:Featurelist
}
```

## 手順 2: ネットワークを構成する

仮想マシン内で記憶域スペース ダイレクトを展開していて、このセクションを省略します。

記憶域スペース ダイレクトでは、高帯域幅、クラスター内のサーバー間ネットワーク低待機時間が必要です。 少なくとも 10 GbE ネットワークが必要であり、リモート ダイレクト メモリ アクセス (RDMA) をお勧めします。 Windows Server 2016 のロゴがあるが、iWARP は通常は簡単にセットアップする限り、iWARP または RoCE のいずれかを使用できます。

> [!Important]
> ネットワーク機器、に応じて、特に RoCE v2、上部のラックのスイッチの一部の構成が必要な場合があります。 スイッチの適切な構成は、記憶域スペース ダイレクトの信頼性とパフォーマンスを確保する必要があります。

Windows Server 2016 には、スイッチ埋め込みチーミング (SET) 内での HYPER-V 仮想スイッチが導入されています。 これにより、必要な物理 NIC ポートの数を減らし、RDMA の使用中のすべてのネットワーク トラフィックに使用する同じ物理 NIC ポートができます。 スイッチ埋め込みチーミングは、記憶域スペース ダイレクトを使用することをお勧めします。

記憶域スペース ダイレクトのネットワークをセットアップする手順については、 [Windows Server 2016 コンバージド NIC とゲスト RDMA 展開ガイド](https://github.com/Microsoft/SDN/blob/master/Diagnostics/S2D%20WS2016_ConvergedNIC_Configuration.docx)を参照してください。

## 手順 3: 記憶域スペース ダイレクトを構成する

次の手順は、構成されるサーバーと同じバージョンの管理システムで実行します。 次の手順を PowerShell セッションを使用してリモートで実行いないが代わりに、ローカルの PowerShell セッションを管理者のアクセス許可の管理システムで実行する必要があります。

### 手順 3.1: ドライブのクリーンアップ

記憶域スペース ダイレクトを有効にする、前に、ドライブが空ことを確認します。 古いパーティションのない、またはその他のデータ。 すべての古いパーティションまたはその他のデータを削除する、コンピューター名に置き換えて、次のスクリプトを実行します。

> [!Warning]
> このスクリプトは、オペレーティング システムのブート ドライブ以外のすべてのドライブ上のデータを完全に削除されます。

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

出力は、**カウント**が各サーバーの各モデルのドライブの数は、このように表示されます。

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

### 手順 3.2: クラスターを検証します。

この手順では、記憶域スペース ダイレクトを使用してクラスターを作成するサーバー ノードが正しく構成されていることを確認するクラスター検証ツールが実行されます。 クラスター検証のとき (`Test-Cluster`) が構成表示フェールオーバー クラスターとして正常に機能するに適していることを確認したテストを実行するクラスターが作成される前に、実行します。 使用のすぐ下の例、`-Include`パラメーター、し、テストの特定のカテゴリが指定されています。 これにより、記憶域スペース ダイレクトの特定のテストが確実に検証に含まれるようになります。

記憶域スペース ダイレクト クラスターとして使用する一連のサーバーを検証するには、以下の PowerShell コマンドを使用します。

```PowerShell
Test-Cluster –Node <MachineName1, MachineName2, MachineName3, MachineName4> –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
```

### 手順 3.3: クラスターを作成します。

この手順では、次の PowerShell コマンドレットを使用して前の手順でクラスター作成用に検証したノードを持つクラスターを作成します。

クラスターを作成するときを示す警告が表示されます、"問題中あったクラスター化された役割を作成することができないを開始します。 詳細については、以下のレポート ファイルを参照してください" という警告が表示されます。 この警告は無視しても問題ありません。 クラスター クォーラムで使用可能なディスクがないことが原因です。 クラスターの作成後にファイル共有監視またはクラウド監視を構成することをお勧めします。

> [!Note]
> サーバーで静的 IP アドレスを使用している場合は、以下のコマンドを変更して静的 IP アドレスを反映させます。その場合、以下のパラメーターを追加し、IP アドレスとして –StaticAddress &lt;X.X.X.X&gt; を指定します。
> 次のコマンドでは、ClusterName プレースホルダーを、15 文字以内の固有の netbios 名に置き換える必要があります。
> ```PowerShell
> New-Cluster –Name <ClusterName> –Node <MachineName1,MachineName2,MachineName3,MachineName4> –NoStorage
> ```

クラスターが作成された後、クラスター名の DNS エントリがレプリケートされるまで時間がかかる場合があります。 この時間は、環境と DNS レプリケーションの構成に依存します。 クラスターの解決に成功しなかった場合、クラスター名の代わりに、クラスターのアクティブ メンバーであるノードのコンピューター名を使用すれば、たいていは成功します。

### 手順 3.4: クラスターの監視を構成します。

次の 3 つまたは複数のサーバーを持つクラスターが失敗またはオフラインの 2 つのサーバーに耐えられるように、クラスターの監視を構成することをお勧めします。 それ以外の場合、他にも使用不可になるとサーバーがオフラインか、2 台のサーバーの展開には、クラスターの監視が必要です。 これらのシステムでは、監視としてファイル共有を使用することも、クラウド監視を使用することもできます。 

詳細については、以下のトピックを参照してください。

- [クォーラムを構成および管理する](../../failover-clustering/manage-cluster-quorum.md)
- [フェールオーバー クラスターのクラウド監視を展開する](../../failover-clustering/deploy-cloud-witness.md)

### 手順 3.5: 記憶域スペース ダイレクトを有効にする

使用してクラスターを作成した後、 `Enable-ClusterStorageSpacesDirect` 、記憶域システムを記憶域スペース ダイレクト モードに設定され、自動的には、次の PowerShell コマンドレット。

-   **プールを作成する:** "S2D on Cluster1" などの名前を持つ単一の大きなプールを作成します。

-   **記憶域スペース ダイレクトのキャッシュを構成する:** 記憶域スペース ダイレクトで使用可能なメディア (ドライブ) の種類が複数ある場合は、最も高速なものがキャッシュ デバイスとして構成されます (ほとんどの場合、読み書き可能なもの)。

-   **階層:** 既定の階層として 2 つの階層を作成します。 1 つを "Capacity" と呼び、もう 1 つを "Performance" と呼びます。 コマンドレットではデバイスを分析し、デバイスの種類と回復性を組み合わせて各階層を構成します。

管理システムから、管理者特権で開いた PowerShell コマンド ウィンドウで、次のコマンドを開始します。 クラスター名は、前の手順で作成したクラスターの名前です。 このコマンドをいずれかのノードのローカルで実行する場合、-CimSession パラメーターは必要ありません。

```PowerShell
Enable-ClusterStorageSpacesDirect –CimSession <ClusterName>
```

上のコマンドを使用して記憶域スペース ダイレクトを有効にする場合、クラスター名の代わりにノード名を使用することもできます。 新しく作成したクラスター名では DNS レプリケーションの遅延が発生する可能性があるため、ノード名を使用するほうが信頼性が高くなる場合があります。

このコマンドが完了すると (完了するまで数分かかる場合があります)、システムはボリュームを作成できる状態になります。

### 手順 3.6: ボリュームを作成する

使用することをお勧め、`New-Volume`ので、コマンドレットは最も素早く直感的なエクスペリエンスを提供します。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

詳しくは、「[記憶域スペース ダイレクトのボリュームの作成](create-volumes.md)」をご覧ください。

### 手順 3.7: 必要に応じて、CSV キャッシュを有効にします。

必要に応じて、Windows のキャッシュ マネージャーによって既にキャッシュされていない読み取り操作の書き込みによってブロック レベル キャッシュとしてシステム メモリ (RAM) を使用するクラスター共有ボリューム (CSV) のキャッシュを有効にできます。 これにより、HYPER-V などのアプリケーションのパフォーマンスが向上することができます。 CSV のキャッシュは、読み取り要求のパフォーマンスを向上させることができはスケール アウト ファイル サーバーのシナリオにも役立ちます。

CSV のキャッシュを有効にすると、メモリを Vhd に利用可能な記憶域のパフォーマンスのバランスを取る必要がありますので、ハイパーコンバージド クラスターで Vm を実行できるメモリの量が減少します。

CSV キャッシュのサイズを設定するの [を記憶域クラスター上で管理者のアクセス許可を持つアカウントを使用して管理システムで PowerShell セッションを開き、このスクリプトは、変更を使用して、`$ClusterName`と`$CSVCacheSize`に応じて変数 (この例の設定、2 GB CSV キャッシュ サーバーごと):

```PowerShell
$ClusterName = "StorageSpacesDirect1"
$CSVCacheSize = 2048 #Size in MB

Write-Output "Setting the CSV cache..."
(Get-Cluster $ClusterName).BlockCacheSize = $CSVCacheSize

$CSVCurrentCacheSize = (Get-Cluster $ClusterName).BlockCacheSize
Write-Output "$ClusterName CSV cache size: $CSVCurrentCacheSize MB"
```

詳しくは、「 [、CSV メモリ内読み取りキャッシュ](csv-cache.md)」を参照してください。

### 手順 3-8: ハイパーコンバージド展開では仮想マシンを展開します。

ハイパーコンバージド クラスターを展開している場合は、最後に、記憶域スペース ダイレクト クラスター上で仮想マシンのプロビジョニングします。

仮想マシンのファイルは、フェールオーバー クラスターにクラスター化された VM のようにシステム CSV 名前空間 (c:\\ClusterStorage\\Volume1 など) に格納する必要があります。

インボックス ツールやその他のツールを使用して、記憶域と System Center の仮想マシン Manager などの仮想マシンを管理することができます。

## 手順 4: コンバージド ソリューションのスケール アウト ファイル サーバーを展開します。

コンバージド ソリューションを展開している場合、次の手順は、スケール アウト ファイル サーバーのインスタンスを作成して、いくつかのファイル共有をセットアップするには 完了して、これは不要のハイパーコンバージド クラスターを展開する場合のセクションです。

### 手順 4.1: スケール アウト ファイル サーバーの役割を作成します。

ファイル サーバー クラスター サービスを設定するのには、次の手順は、継続的に利用可能なファイル共有がホストされている、スケール アウト ファイル サーバーのインスタンスを作成するときは、クラスター化されたファイルのサーバーの役割を作成しています。

#### サーバー マネージャーを使用して、スケール アウト ファイル サーバーの役割を作成するには

1.  フェールオーバー クラスター マネージャーでは、クラスターの選択、**役割**に移動し、**役割の構成]** をクリックします。<br>高可用性ウィザードが表示されます。
2.  **役割の選択**] ページで、**ファイル サーバー**をクリックします。
3.  **ファイル サーバーの種類**] ページで、**アプリケーション データのスケール アウト ファイル サーバー**をクリックします。
4.  **クライアント アクセス ポイント**] ページで、スケール アウト ファイル サーバーの名前を入力します。
5.  図 1 に示すように、ロールが正常に**ロール**に移動して、設定し、[**状態**] 列表示される**を実行している**クラスター化されたファイル サーバーの役割の横にあることを確認する、作成したことを確認します。

    ![表示スケール アウト ファイル サーバー フェールオーバー クラスター マネージャーのスクリーン ショット](media\Hyper-converged-solution-using-Storage-Spaces-Direct-in-Windows-Server-2016\SOFS_in_FCM.png "Failover Cluster Manager showing the Scale-Out File Server")

     **図 1**フェールオーバー クラスター マネージャーの実行状態でスケール アウト ファイル サーバーの表示

> [!NOTE]
>  クラスター化された役割を作成すると、可能性がありますネットワーク伝達遅延、数分以上可能性のあるにファイル共有の作成を妨げる可能性。  
  
#### Windows PowerShell を使用して、スケール アウト ファイル サーバーの役割を作成するには

 ファイル サーバー クラスターに接続されている Windows PowerShell セッションでを提供する*FSCLUSTER*クラスターの名前と一致して、名前と一致する*SOFS*の変更、スケール アウト ファイル サーバーの役割を作成する次のコマンドを入力しますスケール アウト ファイル サーバーの役割:

```PowerShell
Add-ClusterScaleOutFileServerRole -Name SOFS -Cluster FSCLUSTER
```

> [!NOTE]
>  クラスター化された役割を作成すると、可能性がありますネットワーク伝達遅延、数分以上可能性のあるにファイル共有の作成を妨げる可能性。 SOFS 役割は、すぐに失敗し、開始は場合、は、クラスターのコンピューター オブジェクトは SOFS ロールのコンピューター アカウントを作成するためのアクセス許可があるない可能性があります。 ヘルプ、その参照をこのブログの投稿:[スケール アウト ファイル サーバーの役割が失敗したにスタート画面のイベント Id 1205 1069、および 1194](http://www.aidanfinn.com/?p=14142)します。

### 手順 4.2: ファイル共有を作成します。

仮想ディスクを作成し、Csv に追加したら、CSV あたり 1 つの仮想ディスクの 1 つのファイル共有上のファイル共有を作成する時間を勧めします。 System Center の仮想マシン Manager (VMM) は、おそらく、これを行う権限を取得して、処理しますが、部分的に展開を自動化する Windows PowerShell を使用するには、環境内でをお持ちでない場合ため便利方法です。

一部のグループと共有の作成プロセスを自動化する[HYPER-V ワークロードの SMB 共有構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)スクリプトに含まれるスクリプトを使用します。 HYPER-V ワークロードの場合、書き込まれるため、他のワークロードを展開している場合は、設定を変更または共有を作成した後、追加の手順を実行する必要があります。 たとえば、Microsoft SQL Server を使用している場合、SQL Server のサービス アカウント与える必要があります、共有やファイル システムを完全に制御します。

> [!NOTE]
>  System Center の仮想マシン Manager を使用して、共有を作成しない限り、クラスター ノードを追加する場合は、グループ メンバーシップを更新する必要があります。

PowerShell スクリプトを使用してファイル共有を作成するには、次の操作を行います。

1. ファイル サーバー クラスターのノードのいずれかに[HYPER-V ワークロードの SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)に含まれるスクリプトをダウンロードします。
2. 管理システムで、ドメイン管理者の資格情報を使って、Windows PowerShell セッションを開き、に応じて変数の値を変更する HYPER-V コンピューター オブジェクトは、Active Directory グループを作成する次のスクリプトを使用して、環境:

    ```PowerShell
    # Replace the values of these variables
    $HyperVClusterName = "Compute01"
    $HyperVObjectADGroupSamName = "Hyper-VServerComputerAccounts" <#No spaces#>
    $ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

    # Start of script itself
    CD $ScriptFolder
    .\ADGroupSetup.ps1 -HyperVObjectADGroupSamName $HyperVObjectADGroupSamName -HyperVClusterName $HyperVClusterName
    ```
3. 記憶域のノードのいずれかで管理者の資格情報で Windows PowerShell セッションを開くし、各 CSV の共有を作成し、Domain Admins グループと計算クラスターを共有の管理アクセス許可を付与する次のスクリプトを使用します。

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

### 手順 4.3 を有効にする Kerberos の制約付き委任

リモート シナリオの管理と、記憶域クラスター ノードのいずれかからのライブ マイグレーション セキュリティ強化の Kerberos の制約付き委任をセットアップするには、 [HYPER-V ワークロードの SMB 共有の構成](http://gallery.technet.microsoft.com/SMB-Share-Configuration-4a36272a)に含まれている KCDSetup.ps1 スクリプトを使用します。 スクリプトのほとんどのラッパーを次に示しません。

```PowerShell
$HyperVClusterName = "Compute01"
$ScaleOutFSName = "SOFS"
$ScriptFolder = "C:\Scripts\SetupSMBSharesWithHyperV"

CD $ScriptFolder
.\KCDSetup.ps1 -HyperVClusterName $HyperVClusterName -ScaleOutFSName $ScaleOutFSName -EnableLM
```

## 次のステップ

クラスター化されたファイル サーバーを展開した後、実際のワークロードを移行する前に合成ワークロードを使用して、ソリューションのパフォーマンスのテストをお勧めします。 これによりソリューションが正常に動作していることを確認し、ワークロードの複雑さを追加する前に、残留の問題を操作できます。 詳しくは、[記憶域スペースのパフォーマンスを使用して合成ワークロードのテスト](https://technet.microsoft.com/library/dn894707.aspx)を参照してください。

## 関連項目

-   [Windows Server 2016 の記憶域スペース ダイレクト](storage-spaces-direct-overview.md)
-   [記憶域スペース ダイレクトのキャッシュについて](understand-the-cache.md)
-   [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
-   [記憶域スペースのフォールト トレランス](storage-spaces-fault-tolerance.md)
-   [記憶域スペース ダイレクトのハードウェア要件](Storage-Spaces-Direct-Hardware-Requirements.md)
-   [To RDMA, or not to RDMA – that is the question (RDMA すべきか、RDMA せざるべきか、それが問題だ)](https://blogs.technet.microsoft.com/filecab/2017/03/27/to-rdma-or-not-to-rdma-that-is-the-question/) (TechNet ブログ)
