---
title: Windows Server 2016 にインストールされた Hyper-v の新機能します。
description: Hyper-v の新機能の概要を示します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 1a65a98e-54b6-4c41-9732-1e3d32fe3a5f
author: kbdazure
ms.author: kathydav
ms.date: 09/21/2017
ms.openlocfilehash: 5fc82d8eea78ad5605dceb6a21e8d543f9d9c88e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857965"
---
# <a name="whats-new-in-hyper-v-on-windows-server"></a>Windows Server での Hyper-v の新機能

>適用対象: Windows Server 2019、Microsoft Hyper-V Server 2016、Windows Server 2016
  
この記事では、Windows Server 2019、Windows Server 2016、および Microsoft Hyper-V Server 2016 での Hyper-v の新機能と変更された機能について説明します。 Windows Server 2012 R2 で作成され、Windows Server 2019 または Windows Server 2016 で Hyper-v を実行するサーバーに移動またはインポートされた仮想マシンで新機能を使用するには、仮想マシンの構成バージョンを手動でアップグレードする必要があります。 手順については、「[仮想マシンのバージョンのアップグレード](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)」を参照してください。  
  
この記事に記載されていることと、機能が新機能か更新されたものかを示します。  

## <a name="windows-server-version-1903"></a>Windows Server バージョン 1903

### <a name="add-hyper-v-manager-to-server-core-installations-updated"></a>Hyper-v マネージャーの Server Core インストールへの追加 (更新)

ご存じのとおり、運用環境で Windows Server の半期チャンネルを使用する場合、コア インストール オプションの使用をお勧めしています。 ただし、Server Core では多数の便利な管理ツールが既定で省かれています。 アプリ互換性機能をインストールすると、最もよく使用されているツールが多数追加されますが、それでもそこにはないツールがいくつかあります。

そのため、お客様からのフィードバックに基づいて、このバージョンのアプリの互換性機能にもう1つツールを追加しました。 Hyper-v マネージャー (virtmgmt)。

詳細については、[Server Core アプリ互換性機能](../../get-started-19/install-fod-19.md)に関するページを参照してください。

## <a name="windows-server-2019"></a>Windows Server 2019

### <a name="security-shielded-virtual-machines-improvements-new"></a>セキュリティ: シールドされた Virtual Machines の機能強化 (新機能)

- **ブランチ オフィスの機能強化**

    新しい[フォールバック HGS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration) 機能と[オフライン モード](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode) 機能を利用することにより、ホスト ガーディアン サービスへの接続が断続的なコンピューターで、シールドされた仮想マシンを実行できるようになりました。 フォールバック HGS を使用すると、プライマリ HGS サーバーにアクセスできない場合に試すことができるように、Hyper-V の URL のセカンダリ セットを構成できます。

    オフライン モードでは、VM が一度正常に開始されたことがあり、ホストのセキュリティ構成が変更されていない限り、HGS にアクセスできない場合でも、シールドされた VM を継続的に起動できます。

- **トラブルシューティングの機能強化**

    VMConnect 拡張セッション モードと PowerShell ダイレクトのサポートが有効になり、[シールドされた仮想マシンのトラブルシューティング](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms)も容易になりました。 これらのツールは、VM へのネットワーク接続が失われたため構成を更新してアクセスを復元する必要がある場合に特に役立ちます。

    これらの機能は構成する必要がなく、Windows Server Version 1803 以降を実行している Hyper-V ホストにシールドされた VM が配置されると、自動的に利用可能になります。

- **Linux のサポート**

    OS が混在する環境を使用している場合、Windows Server 2019 では、シールドされた仮想マシンでの Ubuntu、Red Hat Enterprise Linux、および SUSE Linux Enterprise Server の実行がサポートされるようになりました。

## <a name="windows-server-2016"></a>Windows Server 2016

### <a name="compatible-with-connected-standby-new"></a>コネクトスタンバイ \(新しい\) との互換性

Always On/Always Connected (ビデオ) 電源モデルを使用しているコンピューターに Hyper-v の役割がインストールされている場合、**コネクトスタンバイ**電源の状態が使用できるようになりました。  
  
### <a name="discrete-device-assignment-new"></a>個別のデバイスの割り当て \(新しい\)

この機能を使用すると、仮想マシンにいくつかの PCIe ハードウェアデバイスへの直接の排他的アクセスを与えることができます。 この方法でデバイスを使用すると、Hyper-v 仮想化スタックがバイパスされるため、アクセスが高速になります。 サポートされているハードウェアの詳細については、「 [Windows Server 2016 の hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)」の「個別のデバイスの割り当て」を参照してください。 この機能の使用方法や考慮事項などの詳細については、仮想化のブログの「[個別のデバイスの割り当て-説明と背景](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)」を参照してください。

### <a name="encryption-support-for-the-operating-system-disk-in-generation-1-virtual-machines-new"></a>第1世代仮想マシンでのオペレーティングシステムディスクの暗号化サポート \(新規)

第1世代の仮想マシンで BitLocker ドライブ暗号化を使用して、オペレーティングシステムディスクを保護できるようになりました。 新しい機能であるキー記憶域によって、システムドライブの BitLocker キーを格納するための小型の専用ドライブが作成されます。 これは、第2世代仮想マシンでのみ使用できる仮想トラステッドプラットフォームモジュール (TPM) を使用する代わりに実行されます。 ディスクの暗号化を解除し、バーチャルマシンを起動するには、Hyper-v ホストが承認された保護されたファブリックの一部であるか、またはいずれかの仮想マシンのガーディアンの秘密キーを持っている必要があります。 キーストレージには、バージョン8の仮想マシンが必要です。 仮想マシンのバージョンの詳細については、「 [windows 10 または Windows Server 2016 で hyper-v の仮想マシンのバージョンをアップグレード](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)する」を参照してください。  
  
### <a name="host-resource-protection-new"></a>新しい\) \(ホストリソース保護

この機能は、過剰なレベルのアクティビティを探すことで、仮想マシンがシステムリソースの共有を使用しないようにするために役立ちます。 これにより、仮想マシンの過剰なアクティビティによってホストまたは他の仮想マシンのパフォーマンスが低下するのを防ぐことができます。 アクティビティが過剰になっている仮想マシンが監視によって検出されると、仮想マシンのリソースが減少します。 この監視と強制は、既定ではオフになっています。 Windows PowerShell を使用して、オンまたはオフにします。 有効にするには、次のコマンドを実行します。  
  
```
Set-VMProcessor TestVM -EnableHostResourceProtection $true
```

このコマンドレットの詳細については、「 [Set-VMProcessor](https://docs.microsoft.com/powershell/module/hyper-v/set-vmprocessor)」を参照してください。

### <a name="hot-add-and-remove-for-network-adapters-and-memory-new"></a>ネットワークアダプターとメモリ \(新しい\) のホットアドと削除

ダウンタイムを発生させることなく、仮想マシンの実行中にネットワークアダプターを追加または削除できるようになりました。 これは、Windows または Linux オペレーティングシステムを実行する第2世代仮想マシンに対して機能します。  
  
動的メモリを有効にしていない場合でも、実行中にバーチャルマシンに割り当てられたメモリの量を調整することもできます。 これは、Windows Server 2016 または Windows 10 を実行している第1世代と第2世代仮想マシンの両方に対して機能します。  

### <a name="hyper-v-manager-improvements-updated"></a>Hyper-v マネージャーの機能強化 \(更新されました\) 
  
-   **代替の資格情報のサポート**-別の windows Server 2016 または windows 10 リモートホストに接続するときに、hyper-v マネージャーで別の資格情報のセットを使用できるようになりました。 また、これらの資格情報を保存しておくと、もう一度ログオンしやすくなります。  
  
-   **以前のバージョンを管理**する-windows server 2019、windows server 2016、および windows 10 の Hyper-v マネージャーを使用して、windows server 2012、windows 8、windows Server 2012 R2、および Windows 8.1 で hyper-v を実行しているコンピューターを管理できます。  
  
-   **更新された管理プロトコル**-hyper-v マネージャーが、CredSSP、Kerberos、または NTLM 認証を許可する ws-i プロトコルを使用して、リモートの hyper-v ホストと通信できるようになりました。 CredSSP を使用してリモート Hyper-v ホストに接続する場合は、Active Directory で制約付き委任を有効にせずにライブマイグレーションを実行できます。 また、WS MAN ベースのインフラストラクチャを使用すると、ホストをリモート管理用に簡単に有効にすることもできます。 WS-MAN はポート 80 で接続します。このポートは既定で開かれています。  
  
### <a name="integration-services-delivered-through-windows-update-updated"></a>Windows Update \(によって配信された統合サービス\) 

Windows ゲストの統合サービスの更新プログラムは、Windows Update を通じて配布されます。 サービスプロバイダーとプライベートクラウドのホスト側については、仮想マシンを所有するテナントに更新プログラムを適用する制御があります。 テナントは、1つの方法を使用して、統合サービスを含むすべての更新を使用して Windows 仮想マシンを更新できるようになりました。 Linux ゲストの integration services の詳細については、「 [hyper-v での linux および FreeBSD Virtual Machines](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)」を参照してください。  
  
> [!IMPORTANT]  
> Vmguest .iso イメージファイルは不要になったため、Windows Server 2016 の Hyper-v には含まれていません。  
  
### <a name="linux-secure-boot-new"></a>Linux セキュアブート \(新しい\) 

第2世代仮想マシンで実行されている Linux オペレーティングシステムは、セキュアブートオプションを有効にして起動できるようになりました。 Ubuntu 14.04 以降、SUSE Linux Enterprise Server 12 以降、Red Hat Enterprise Linux 7.0 以降、および CentOS 7.0 以降では、Windows Server 2016 を実行するホストでセキュアブートが有効になっています。 仮想マシンを初めて起動する前に、Microsoft UEFI 証明機関を使用するように仮想マシンを構成する必要があります。 これは、Hyper-v マネージャー、Virtual Machine Manager、または管理者特権の Windows Powershell セッションから行うことができます。 Windows PowerShell の場合は、次のコマンドを実行します。  
  
```  
Set-VMFirmware TestVM -SecureBootTemplate MicrosoftUEFICertificateAuthority  
```  
  
Hyper-v 上の Linux 仮想マシンの詳細については、「 [hyper-v 上の linux および FreeBSD Virtual Machines](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)」を参照してください。 コマンドレットの詳細については、「 [set-vmfirmware](https://docs.microsoft.com/powershell/module/hyper-v/set-vmfirmware)」を参照してください。

### <a name="more-memory-and-processors-for-generation-2-virtual-machines-and-hyper-v-hosts-updated"></a>第2世代のバーチャルマシンと Hyper-v ホストのメモリとプロセッサが増えると \(が更新され\)

バージョン8以降では、第2世代仮想マシンで、より多くのメモリと仮想プロセッサを使用できます。 ホストは、以前にサポートされていたものよりもはるかに多くのメモリおよび仮想プロセッサを使用して構成できます。 これらの変更は、オンライントランザクション処理 (OLTP) およびデータウェアハウス (DW) 用の e コマース大容量メモリ内データベースの実行など、新しいシナリオに対応しています。 Windows Server のブログと 5.5 数テラバイト メモリと 4 TB のメモリ内のデータベースを実行している 128 の仮想プロセッサの仮想マシンのパフォーマンスの結果が最近発行されました。 物理サーバーのパフォーマンスが95% を超えています。 詳細については、「 [メモリ内のトランザクション処理が大規模な VM パフォーマンスを Windows Server 2016 HYPER-V](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/)します。 仮想マシンのバージョンの詳細については、「 [windows 10 または Windows Server 2016 で hyper-v の仮想マシンのバージョンをアップグレード](./deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)する」を参照してください。 サポートされる最大構成の完全な一覧については、「 [Windows Server 2016 での hyper-v のスケーラビリティの計画](./plan/plan-hyper-v-scalability-in-windows-server.md)」を参照してください。 

### <a name="nested-virtualization-new"></a>入れ子になった仮想化 \(新しい\)

この機能を使用すると、仮想マシンを Hyper-v ホストとして使用し、仮想化されたホスト内に仮想マシンを作成することができます。 これは、開発およびテスト環境で特に便利です。 入れ子になった仮想化を使用するには、次のものが必要です。  
  
-   物理 Hyper-v ホストと仮想化ホストの両方で少なくとも Windows Server 2019、Windows Server 2016、または Windows 10 を実行する場合は。  
  
-   Intel VT-x のプロセッサ (入れ子になった仮想化は、現時点では Intel プロセッサでのみ使用できます)。  
  
詳細と手順については、「[入れ子になった仮想化を使用した仮想マシンでの hyper-v の実行](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)」を参照してください。  
  
### <a name="networking-features-new"></a>ネットワーク機能 \(新しい\)

新しいネットワーク機能は次のとおりです。  
  
-   **リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)** 。 SET が使用されているかどうかに関係なく、Hyper-v 仮想スイッチにバインドされているネットワークアダプターで RDMA を設定できます。 SET には、NIC チーミングと同じ機能の一部を備えた仮想スイッチが用意されています。 詳細については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)」を参照してください。  
  
-   **仮想マシンの複数のキュー (VMMQ)** 。 は、仮想マシンごとに複数のハードウェアキューを割り当てることによって、VMQ スループットを向上させます。  既定のキューは、仮想マシンのキューのセットになり、キュー間にトラフィックが分散されます。  
  
-   **ソフトウェアで定義されたネットワークのサービス品質 (QoS)** 。 既定のクラスの帯域幅内で仮想スイッチを経由するトラフィックの既定のクラスを管理します。  
  
新しいネットワーク機能の詳細については、「[ネットワークの新](../../networking/What-s-New-in-Networking.md)機能」を参照してください。  
  
### <a name="production-checkpoints-new"></a>新しい\) \(運用チェックポイント

運用チェックポイントは、仮想マシンの "特定の時点" イメージです。 これらの方法を使用すると、仮想マシンが運用ワークロードを実行するときに、サポートポリシーに準拠するチェックポイントを適用できます。 運用チェックポイントは、保存された状態ではなく、ゲスト内のバックアップテクノロジをベースにしています。 Windows 仮想マシンの場合、ボリュームスナップショットサービス (VSS) が使用されます。 Linux 仮想マシンの場合、ファイルシステムバッファーをフラッシュして、ファイルシステムと一貫性のあるチェックポイントを作成します。 保存された状態に基づいてチェックポイントを使用する場合は、代わりに標準チェックポイントを選択します。 詳細については、「 [hyper-v で標準または運用チェックポイントを選択](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)する」を参照してください。  
  
> [!IMPORTANT]  
> 新しい仮想マシンでは、既定として運用チェックポイントが使用されます。  
  
### <a name="rolling-hyper-v-cluster-upgrade-new"></a>Hyper-v クラスターアップグレードのローリング \(新しい\)

Windows server 2019 または Windows Server 2016 を実行しているノードを、Windows Server 2012 R2 を実行しているノードで Hyper-v クラスターに追加できるようになりました。 これにより、ダウンタイムなしでクラスターをアップグレードできます。 クラスターは、クラスター内のすべてのノードをアップグレードし、Windows PowerShell コマンドレット[ClusterFunctionalLevel](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel)を使用してクラスターの機能レベルを更新するまで、windows Server 2012 R2 の機能レベルで実行されます。  
  
> [!IMPORTANT]  
> クラスターの機能レベルを更新しても、Windows Server 2012 R2 には返されません。  
  
Windows server 2012 R2 の機能レベルが windows server 2012 R2、Windows Server 2019、および Windows Server 2016 を実行している Hyper-v クラスターの場合は、次の点に注意してください。  
  
-   Windows Server 2016 または Windows 10 が実行されているノードからクラスター、Hyper-v、および仮想マシンを管理します。  
  
-   Hyper-v クラスター内のすべてのノード間で仮想マシンを移動できます。  
  
-   新しい Hyper-v 機能を使用するには、すべてのノードが Windows Server 2016 を実行している必要があります。また、クラスターの機能レベルを更新する必要があります。  
  
-   既存のバーチャルマシンのバーチャルマシン構成のバージョンがアップグレードされていません。 構成バージョンは、クラスターの機能レベルをアップグレードした後にのみアップグレードできます。  
  
-   作成した仮想マシンは、Windows Server 2012 R2、仮想マシンの構成レベル5と互換性があります。  
  
クラスターの機能レベルを更新すると、次のようになります。  
  
-   新しい Hyper-v 機能を有効にすることができます。  
  
-   新しいバーチャルマシン機能を使用できるようにするには、更新プログラム VmConfigurationVersion コマンドレットを使用して、バーチャルマシンの構成レベルを手動で更新します。 手順については、「[仮想マシンのバージョンのアップグレード](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)」を参照してください。    
-   Windows Server 2012 R2 を実行している Hyper-v クラスターにノードを追加することはできません。  
  
> [!NOTE]  
> Windows 10 の hyper-v では、フェールオーバークラスタリングはサポートされていません。  
  
詳細と手順については、「[クラスターのオペレーティングシステムのローリングアップグレード](https://technet.microsoft.com/library/dn850430.aspx)」を参照してください。  

### <a name="shared-virtual-hard-disks-updated"></a>共有仮想ハードディスク \(更新されました\)
ゲストクラスタリングに使用される共有仮想ハードディスク (.vhdx ファイル) のサイズをダウンタイムなしで変更できるようになりました。 共有仮想ハードディスクは、仮想マシンがオンラインの間に拡張または圧縮できます。 ゲストクラスターでは、Hyper-v レプリカを使用して障害回復を行うことで、共有仮想ハードディスクを保護することもできます。

コレクションでレプリケーションを有効にします。 コレクションでのレプリケーションの有効化は **、WMI インターフェイスを介してのみ公開**されます。 詳細については、 [Msvm_CollectionReplicationService クラス](https://msdn.microsoft.com/library/mt167787%28v=vs.85%29.aspx)のドキュメントを参照してください。 **PowerShell コマンドレットまたは UI を使用して、コレクションのレプリケーションを管理することはできません。** コレクションに固有の機能にアクセスするには、Hyper-v クラスターの一部であるホスト上に Vm を配置する必要があります。 これには、Hyper-v レプリカでサポートされていないスタンドアロンホスト上の共有 VHD 共有 Vhd が含まれます。

[「仮想ハードディスクの共有の概要](https://technet.microsoft.com/library/dn281956.aspx)」の共有 vhd のガイドラインに従って、共有 vhd がゲストクラスターの一部であることを確認します。 

共有 VHD が関連付けられていないコレクションでは、共有 VHD が参照ポイントの作成に含まれるかどうかに関係なく、コレクションの参照ポイントを作成することはできません。 

### <a name="virtual-machine-backupnew"></a>仮想マシンのバックアップ\(新しい\)

(ホストがクラスター化されているかどうかに関係なく) 1 つの仮想マシンをバックアップする場合は、VM グループを使用しないでください。  また、スナップショットコレクションを使用する必要もありません。 VM グループとスナップショットコレクションは、共有 vhdx を使用しているゲストクラスターのバックアップ専用に使用することを目的としています。 代わりに、 [HYPER-V WMI v2 プロバイダー](https://msdn.microsoft.com/library/windows/desktop/hh850319(v=vs.85).aspx)を使用してスナップショットを作成する必要があります。 同様に、[フェールオーバークラスター WMI プロバイダー](https://msdn.microsoft.com/library/windows/desktop/mt167750(v=vs.85).aspx)は使用しないでください。

### <a name="shielded-virtual-machines-new"></a>シールドされた仮想マシン \(新しい\)

シールドされた仮想マシンはいくつかの機能を使用して、ホスト上の Hyper-v 管理者とマルウェアが、シールドされた仮想マシンの状態からデータを検査、改ざん、または盗むことを困難にします。 データと状態は暗号化されており、Hyper-v 管理者はビデオの出力とディスクを見ることができず、バーチャルマシンはホストガーディアンサーバーによって決定された既知の正常なホストでのみ実行されるように制限することができます。 詳細については、「保護された[ファブリックとシールド](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)された vm」をご覧ください。
  
> [!NOTE]  
> シールドされた仮想マシンは、Hyper-v レプリカと互換性があります。 シールドされたバーチャルマシンをレプリケートするには、そのシールドされたバーチャルマシンの実行を承認する必要があります。  

### <a name="start-order-priority-for-clustered-virtual-machines-new"></a>クラスター化された仮想マシンの開始順序の優先順位 \(新しい\)

この機能を使用すると、最初に起動または再起動するクラスター化された仮想マシンをより細かく制御できます。 これにより、これらのサービスを使用する仮想マシンの前にサービスを提供する仮想マシンを簡単に起動できます。 セットを定義し、仮想マシンをセットに配置して、依存関係を指定します。 Windows PowerShell コマンドレットを使用して、[新しい-ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/new-clustergroupset)、 [Get clustergroupset](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustergroupset)、および[Add clustergroupsetdependency](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergroupsetdependency)などのセットを管理します。
。  
### <a name="storage-quality-of-service-qos-updated"></a>記憶域のサービスの品質 (QoS) \(更新されました\)

スケールアウト ファイル サーバーで記憶域の QoS ポリシーを作成し、Hyper-V 仮想マシンの 1 つ以上の仮想ディスクにそのポリシーを割り当てることができるようになりました。 記憶域のパフォーマンスは、記憶域の負荷の変動に従って、ポリシーに合わせて自動的に再調整されます。 詳細については、「[記憶域のサービスの品質](../../storage/storage-qos/storage-qos-overview.md)」を参照してください。  
  
### <a name="virtual-machine-configuration-file-format-updated"></a>仮想マシンの構成ファイルの形式 \(更新されました\)

仮想マシンの構成ファイルでは、構成データの読み取りと書き込みをより効率的に行う新しい形式が使用されます。 また、この形式では、ストレージ障害が発生した場合にデータの破損が発生する可能性が低くなります。 仮想マシンの構成データファイルは、. vmcx ファイル名拡張子とランタイム状態データファイルを使用します。ファイル名拡張子は vmrs です。  
  
> [!IMPORTANT]  
> Vmcx ファイル名拡張子は、バイナリファイルを示します。 Vmcx または vmrs ファイルの編集はサポートされていません。  
  
### <a name="virtual-machine-configuration-version-updated"></a>仮想マシンの構成バージョン \(更新されました\)

バージョンは、仮想マシンの構成、保存された状態、およびスナップショットファイルと Hyper-v のバージョンとの互換性を表します。 バージョン5の仮想マシンは Windows Server 2012 R2 と互換性があり、Windows Server 2012 R2 と Windows Server 2016 の両方で実行できます。 Windows server 2016 および Windows Server 2019 で導入されたバージョンの仮想マシンは、Windows Server 2012 R2 の Hyper-v では実行されません。   
  
Windows server 2012 R2 の 2019 2016 Hyper-v を実行するサーバーに仮想マシンを移動またはインポートする場合、仮想マシンの構成は自動的に更新されません。 これは、Windows Server 2012 R2 を実行しているサーバーに仮想マシンを戻すことができることを意味します。 ただし、これは、仮想マシンの構成のバージョンを手動で更新するまで、新しい仮想マシンの機能を使用できないことも意味します。  
  
バージョンの確認とアップグレードの手順については、「[仮想マシンバージョンのアップグレード](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)」を参照してください。 この記事では、一部の機能が導入されたバージョンも示します。   
  
> [!IMPORTANT]  
> -   バージョンを更新した後は、Windows Server 2012 R2 を実行しているサーバーに仮想マシンを移動することはできません。  
> -   構成を以前のバージョンにダウングレードすることはできません。  
> -   クラスターの機能レベルが Windows Server 2012 R2 の場合、Hyper-v クラスターで[更新プログラム VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)コマンドレットがブロックされます。  

### <a name="virtualization-based-security-for-generation-2-virtual-machines-new"></a>第2世代仮想マシンの仮想化ベースのセキュリティ \(新しい)

仮想化ベースのセキュリティでは、Device Guard や Credential Guard などの機能により、マルウェアからの悪用に対するオペレーティングシステムの保護が強化されています。 仮想化ベースのセキュリティは、バージョン8以降の第2世代ゲスト仮想マシンで使用できます。 仮想マシンのバージョンの詳細については、「 [windows 10 または Windows Server 2016 で hyper-v の仮想マシンのバージョンをアップグレード](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)する」を参照してください。

### <a name="windows-containers-new"></a>Windows コンテナー \(新しい\)

Windows コンテナーを使用すると、多くの分離アプリケーションを1つのコンピューターシステムで実行できます。 これらは構築が高速で、高い拡張性と移植性を備えています。 2種類のコンテナーランタイムを使用できます。それぞれ、アプリケーションの分離の度合いが異なります。 Windows Server コンテナーは、名前空間とプロセスの分離を使用します。 Hyper-v コンテナーは、コンテナーごとに軽量の仮想マシンを使用します。  
  
主な機能は次のとおりです。  
  
-   HTTPS を使用した web サイトとアプリケーションのサポート  
  
-   Nano server は、Windows Server と Hyper-v の両方のコンテナーをホストできます。  
  
-   コンテナーの共有フォルダーを使用してデータを管理する機能  
  
-   コンテナーリソースを制限する機能  
  
クイックスタートガイドを含む詳細については、 [Windows コンテナーのドキュメント](https://docs.microsoft.com/virtualization/windowscontainers/index)を参照してください。  
  
### <a name="windows-powershell-direct-new"></a>Windows PowerShell Direct \(新しい\)

これにより、ホストから仮想マシンで Windows PowerShell コマンドを実行できるようになります。 Windows PowerShell は、ホストと仮想マシンの間で直接実行されます。 これは、ネットワークやファイアウォールの要件を必要としないことを意味し、リモート管理の構成に関係なく機能します。  
  
Windows PowerShell Direct は、hyper-v 管理者が Hyper-v ホスト上の仮想マシンに接続するために使用する既存のツールの代わりとなるものです。  
  
-   PowerShell またはリモート デスクトップなどのリモート管理ツール  
  
-   Hyper-v 仮想マシン接続 (VMConnect)  
  
これらのツールは適切に機能しますが、トレードオフがあります。 VMConnect は信頼できますが、自動化するのは困難です。 リモート PowerShell は強力ですが、設定と保守が困難な場合があります。 これらのトレードオフは、Hyper-v の展開の拡大に伴って重要になる可能性があります。 Windows PowerShell Direct では、VMConnect を使用するのと同じように、強力なスクリプトと自動化のエクスペリエンスを提供することによって、このことに対処しています。
  
要件と手順については、「 [PowerShell ダイレクトを使用した Windows 仮想マシンの管理](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)」を参照してください。  
