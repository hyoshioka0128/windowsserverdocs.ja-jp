---
title: Windows Server 2016 にインストールされた Hyper-v の新機能します。
description: HYPER-V の新機能の概要します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a65a98e-54b6-4c41-9732-1e3d32fe3a5f
author: KBDAzure
ms.author: kathydav
ms.date: 09/21/2017
ms.openlocfilehash: 1384a15d3b8ecee32d36c6265d478edace0bdb09
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848103"
---
# <a name="whats-new-in-hyper-v-on-windows-server-2016"></a>Windows Server 2016 にインストールされた Hyper-v の新機能します。

>適用先:Microsoft HYPER-V Server 2016、Windows Server 2016
  
この記事では、Windows Server 2016 と Microsoft HYPER-V Server 2016 で HYPER-V の機能と変更された機能について説明します。 仮想マシンと Windows Server 2012 R2 で作成、移動、または Windows Server 2016 で HYPER-V を実行しているサーバーにインポートでの新機能を使用するには、仮想マシンの構成バージョンを手動でアップグレードする必要があります。 手順については、次を参照してください。[アップグレードの仮想マシン バージョン](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)します。  
  
この記事の内容し、機能は、新しいまたは更新されたかどうかを次に示します。  

## <a name="BKMK_standby"></a>コネクト スタンバイと互換性のある\(新規\)
Always On/Always Connected (AOAC) 電源モデルを使用するコンピューターに HYPER-V ロールがインストールされているときに、**コネクト スタンバイ**電源の状態が使用できるようになりました。  
  
## <a name="BKMK_device"></a>個別のデバイス割り当て\(新規\) 
この機能では、一部の PCIe ハードウェア デバイスに仮想マシンのダイレクトと排他アクセスできるようにすることができます。 この方法でデバイスを使用して、結果より高速アクセスが、HYPER-V 仮想化スタックをバイパスします。 サポートされているハードウェアについて詳しくは、「個別のデバイスの割り当て」を参照してください[Windows Server 2016 で HYPER-V のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)します。 この機能および考慮事項は、使用する方法などの詳細は、投稿を参照してください"[個別のデバイスの割り当て-説明およびバック グラウンド](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)"仮想化のブログ。

## <a name="encryption-support-for-the-operating-system-disk-in-generation-1-virtual-machines-new"></a>第 1 世代仮想マシンでオペレーティング システム ディスクの暗号化のサポート\(新規)

第 1 世代仮想マシンでの BitLocker ドライブ暗号化を使用して、オペレーティング システム ディスクを保護することができますようになりました。 キーの記憶域の新機能では、システム ドライブの BitLocker キーを格納する小さな、専用のドライブを作成します。 これは、これは第 2 世代仮想マシンでのみ使用可能な仮想トラステッド プラットフォーム モジュール (TPM) を使用する代わりに実行されます。 ディスクの暗号化を解除し、仮想マシンを開始するには、HYPER-V ホストする必要があります承認済みの保護されたファブリックの一部にするか、秘密キー、仮想マシンのガーディアンのいずれかからします。 キー記憶域には、バージョン 8 の仮想マシンが必要です。 仮想マシンのバージョンについては、次を参照してください。 [Windows 10 または Windows Server 2016 での Hyper-v で仮想マシンのアップグレード バージョン](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)します。  
  
## <a name="BKMK_host"></a>ホスト リソース保護\(新規\)
この機能は、仮想マシンがアクティビティの過剰なレベルを探すことによって複数のシステム リソースの共有を使用することを防ぐのに役立ちます。 これにより、仮想マシンの過剰なアクティビティが、ホストまたは他の仮想マシンのパフォーマンスが低下するを防ぐことができます。 監視すると、過剰な活動に仮想マシンが検出されたら、仮想マシンより少ないリソースが与えられます。 この監視と適用は既定で無効です。 Windows PowerShell を使用して、これをオンまたはオフにします。 オンにするには、このコマンドを実行します。  
  
```  
Set-VMProcessor TestVM -EnableHostResourceProtection $true 
```       

詳細については、このコマンドレットは、次を参照してください。 [Set-vmprocessor](https://docs.microsoft.com/powershell/module/hyper-v/set-vmprocessor)します。

## <a name="BKMK_hot"></a>ホット アドし、ホット ネットワーク アダプターとメモリの削除\(新規\) 
追加または、ダウンタイムを発生させることがなく、仮想マシンの実行中にネットワーク アダプタを削除できます。 これは、Windows または Linux のいずれかのオペレーティング システムを実行する第 2 世代仮想マシンに対して機能します。  
  
動的メモリを有効にしていない場合でも、実行中、仮想マシンに割り当てるメモリの量を調整することもできます。 これは、第 1 世代と第 2 世代仮想マシン、Windows Server 2016 または Windows 10 搭載の両方に対して機能します。  
  
## <a name="BKMK_Mgmt"></a>HYPER-V マネージャーの機能強化\(更新\) 
  
-   **代替の資格情報のサポート**-別の Windows Server 2016 または Windows 10 のリモート ホストに接続するときに、HYPER-V マネージャーで異なる資格情報セットに使用することようになりましたことができます。 もう一度ログオンするが簡単にこれらの資格情報を保存することもできます。  
  
-   **以前のバージョン管理**-HYPER-V マネージャーで Windows Server 2016 および Windows 10、Windows Server 2012、Windows 8、Windows Server 2012 R2 および Windows 8.1 で HYPER-V を実行しているコンピューターを管理することができます。  
  
-   **管理プロトコルの更新**-HYPER-V マネージャーが、CredSSP、Kerberos または NTLM 認証を許可する WS-MAN プロトコルを使用してリモートの HYPER-V ホストと通信するようになりました。 CredSSP を使用してリモート HYPER-V ホストに接続するときに、Active Directory で制約付き委任を有効にせず、ライブ マイグレーションを行うことができます。 WS MAN ベースのインフラストラクチャでは、簡単なリモート管理のためのホストを使用します。 WS-MAN はポート 80 で接続します。このポートは既定で開かれています。  
  
## <a name="BKMK_IS"></a>統合サービスが Windows Update を通じて配信\(更新\) 
Windows ゲストの integration services の更新プログラムは、Windows Update を通じて配布されます。 サービス プロバイダーとプライベート クラウドのホスト側は、これは、仮想マシンを所有しているテナントの手に更新プログラムを適用するコントロールを配置します。 テナントを更新できます、Windows 仮想マシンの統合サービスを含むすべての更新プログラムを 1 つのメソッドを使用しています。 Linux ゲスト統合サービスに関する詳細については、次を参照してください。 [Linux と FreeBSD 仮想マシン、Hyper-v](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)します。  
  
> [!IMPORTANT]  
> Vmguest.iso イメージ ファイルは必要なくなりましたので、HYPER-V で Windows Server 2016 に含まれています。  
  
## <a name="BKMK_linux"></a>Linux セキュア ブート\(新規\) 
第 2 世代仮想マシンで実行されている Linux オペレーティング システムは、セキュア ブート オプションを有効にして起動できるようになりました。 Ubuntu 14.04 およびそれ以降、SUSE Linux Enterprise Server 12 と以降では、Red Hat Enterprise Linux 7.0 および以降、および CentOS 7.0 以降は、セキュア ブートの Windows Server 2016 を実行するホストで有効にされます。 最初に仮想マシンを起動する前に、Microsoft UEFI 証明機関を使用する仮想マシンを構成する必要があります。 HYPER-V マネージャー、Virtual Machine Manager、または管理者特権の Windows Powershell セッションから、これを行うことができます。 Windows powershell では、このコマンドを実行します。  
  
```  
Set-VMFirmware TestVM -SecureBootTemplate MicrosoftUEFICertificateAuthority  
```  
  
HYPER-V で Linux 仮想マシンに関する詳細については、次を参照してください。 [Linux と FreeBSD 仮想マシン、Hyper-v](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)します。 コマンドレットの詳細については、次を参照してください。 [Set-vmfirmware](https://docs.microsoft.com/powershell/module/hyper-v/set-vmfirmware)します。

## <a name="more-memory-and-processors-for-generation-2-virtual-machines-and-hyper-v-hosts-updated"></a>追加のメモリと第 2 世代仮想マシンと HYPER-V ホストのプロセッサ\(更新\)
バージョン 8 以降、はるかに多くのメモリと仮想プロセッサ、第 2 世代仮想マシンは使用できます。 ホストは以前サポートされていたよりもに、はるかに多くのメモリと仮想プロセッサで構成できます。 これらの変更は、電子商取引のオンライン トランザクション処理 (OLTP) とデータ ウェアハウス (DW) の大規模なメモリ内データベースを実行しているなどの新しいシナリオをサポートします。 Windows Server のブログと 5.5 数テラバイト メモリと 4 TB のメモリ内のデータベースを実行している 128 の仮想プロセッサの仮想マシンのパフォーマンスの結果が最近発行されました。 パフォーマンスが、物理サーバーのパフォーマンスの 95% を超えています。 詳細については、「 [メモリ内のトランザクション処理が大規模な VM パフォーマンスを Windows Server 2016 HYPER-V](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/)します。 詳細については、仮想マシンのバージョンは、次を参照してください。 [Windows 10 または Windows Server 2016 での Hyper-v で仮想マシンのアップグレード バージョン](./deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)します。 サポートされている最大構成の完全な一覧で、次を参照してください。[の Windows Server 2016 で Hyper-v のスケーラビリティの計画](./plan/plan-hyper-v-scalability-in-windows-server.md)します。 

## <a name="BKMK_nested"></a>入れ子になった仮想化\(新規\) 
この機能では、仮想マシンを HYPER-V ホストとして使用し、その仮想化されたホスト内の仮想マシンを作成することができます。 これは、開発およびテスト環境に特に便利だことができます。 入れ子になった仮想化を使用するには、必要があります。  
  
-   以上で実行する Windows Server 2016 または物理的な HYPER-V ホストと仮想化されたホストの両方で Windows 10。  
  
-   Intel VT x (入れ子になった仮想化は Intel プロセッサでのみ使用できますこの時点で) のプロセッサ。  
  
詳細と手順については、次を参照してください。[実行、Hyper-v 仮想マシンで入れ子になった仮想化で](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)します。  
  
## <a name="BKMK_networking"></a>ネットワーク機能\(新規\) 
新しいネットワーク機能は次のとおりです。  
  
-   **リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)** します。 セットも使用されるかどうかに関係なく、HYPER-V 仮想スイッチにバインドされているネットワーク アダプターで RDMA を設定することができます。 セットは、NIC チーミングと同じ機能の一部の仮想スイッチを提供します。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming)します。  
  
-   **複数の仮想マシン キュー (VMMQ)** します。 仮想マシンごとに複数のハードウェア キューを割り当てることによって、VMQ スループットが向上します。  既定のキューが仮想マシンは、キューのセットとなり、キュー間のトラフィックの負荷が分散されます。  
  
-   **サービスの品質 (QoS ソフトウェア定義ネットワークの)** します。 既定のクラスの帯域幅内で仮想スイッチを通過するトラフィックの既定のクラスを管理します。  
  
詳細については、新しいネットワーク機能は、次を参照してください。[ネットワークにおける新](../../networking/What-s-New-in-Networking.md)します。  
  
## <a name="BKMK_check"></a>運用チェックポイント\(新規\)
運用チェックポイントは、仮想マシンのイメージを「ポイント イン タイム」です。 仮想マシンは、実稼働ワークロードを実行すると、サポート ポリシーに準拠しているチェックポイントを適用する方法を提供します。 運用チェックポイントは、保存された状態ではなく、ゲスト内バックアップのテクノロジに基づいています。 Windows 仮想マシンの場合は、ボリューム スナップショット サービス (VSS) が使用されます。 Linux 仮想マシンの場合は、ファイル システムのバッファーは、ファイル システムで一貫性のあるチェックポイントを作成するフラッシュされます。 チェックポイントの保存された状態に基づいて、使用する場合は、標準のチェックポイントを選択します。 詳細については、次を参照してください。 [、Hyper-v で標準または実稼働のチェックポイント間選択](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)します。  
  
> [!IMPORTANT]  
> 新しいバーチャル マシンは、既定値として、実稼働のチェックポイントを使用します。  
  
## <a name="BKMK_HyperVRollingUpgrades"></a>HYPER-V クラスターのアップグレードをロールバック\(新規\) 
Windows Server 2012 R2 を実行するノードで HYPER-V クラスターに Windows Server 2016 を実行するノードを追加できます。 これにより、ダウンタイムなしのクラスターをアップグレードすることができます。 Windows Server 2012 R2 の機能レベルで、クラスターで実行されるクラスター内のすべてのノードをアップグレードして、Windows PowerShell コマンドレットを使用したクラスターの機能レベルを更新するまで[Update-clusterfunctionallevel](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel)します。  
  
> [!IMPORTANT]  
> クラスターの機能レベルを更新した後は、Windows Server 2012 R2 を返すことはできません。  
  
Windows Server 2012 R2 および Windows Server 2016 を実行するノードで Windows Server 2012 R2 の機能レベルでの HYPER-V クラスターでは、次のことを確認してください。  
  
-   Windows Server 2016 または Windows 10 を実行するノードからクラスター、HYPER-V、および仮想マシンを管理します。  
  
-   すべての HYPER-V クラスター内のノード間で仮想マシンを移動できます。  
  
-   HYPER-V の新機能を使用するすべてのノードが Windows Server 2016 を実行する必要があり、クラスターの機能レベルを更新する必要があります。  
  
-   既存の仮想マシンの仮想マシン構成バージョンはアップグレードされません。 クラスターの機能レベルをアップグレードした後にのみ構成のバージョンをアップグレードすることができます。  
  
-   作成する仮想マシンは、Windows Server 2012 R2 の仮想マシンの構成レベル 5 に対応。  
  
後は、クラスターの機能レベルを更新します。  
  
-   HYPER-V の新機能を有効にすることができます。  
  
-   新しい仮想マシンの機能を使用できるようにするのにには、仮想マシンの構成レベルを手動で更新するのに Update VmConfigurationVersion コマンドレットを使用します。 手順については、次を参照してください。[アップグレードの仮想マシン バージョン](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)します。    
-   Windows Server 2012 R2 を実行する HYPER-V クラスターにノードを追加することはできません。  
  
> [!NOTE]  
> Windows 10 での HYPER-V では、フェールオーバー クラスタ リングをサポートしていません。  
  
詳細と手順については、次を参照してください。、[クラスター オペレーティング システムのローリング アップグレード](https://technet.microsoft.com/library/dn850430.aspx)します。  

## <a name="BKMK_shared"></a>共有仮想ハード_ディスク\(更新\)
共有仮想ハード_ディスク (.vhdx ファイル) のゲスト クラスタ リング、ダウンタイムなしの使用のサイズを変更することができますようになりました。 共有仮想ハード_ディスクを拡大または仮想マシンがオンラインの間に圧縮できます。 ゲスト クラスターが、ディザスター リカバリーのため、HYPER-V レプリカを使用して共有仮想ハード_ディスクも保護してようになりましたことができます。

コレクションでのレプリケーションを有効にします。 コレクションでのレプリケーションの有効化は**WMI インターフェイスを介してのみ公開**します。 ドキュメントを参照して[Msvm_CollectionReplicationService クラス](https://msdn.microsoft.com/library/mt167787%28v=vs.85%29.aspx)の詳細。 **PowerShell コマンドレット、または UI でコレクションのレプリケーションを管理することはできません。** Vm は、コレクションに固有の機能にアクセスする HYPER-V クラスターの一部であるホストにする必要があります。 これにより、共有 VHD が含まれます。-スタンドアロン ホスト上の共有の Vhd は HYPER-V レプリカでサポートされていません。

共有 Vhd でのガイドラインに従う[Virtual Hard Disk Sharing Overview](https://technet.microsoft.com/library/dn281956.aspx)、共有 Vhd、ゲスト クラスターの一部であることを確認してください。 

共有 VHD ですが関連付けられているゲスト クラスターを持つコレクションには、(かどうか、共有 VHD は、参照ポイントの作成に含まれるか) に関係なく、コレクションの参照ポイントを作成できません。 

## <a name="virtual-machine-backupnew"></a>仮想マシンのバックアップ\(新規\)

(かどうかどうかホストがクラスター化) に関係なく、単一の仮想マシンをバックアップする場合は、VM グループを使用する必要があります。  スナップショット コレクションを使用する必要がありますもできません。 VM のグループとスナップショット コレクションは、共有 vhdx を使用しているゲスト クラスターのバックアップのみに使用するものです。 使用してスナップショットを実行する必要があります、代わりに、 [HYPER-V WMI v2 プロバイダー](https://msdn.microsoft.com/library/windows/desktop/hh850319(v=vs.85).aspx)します。 同様に、使用しないでください、[フェイル オーバー クラスタ WMI プロバイダ](https://msdn.microsoft.com/library/windows/desktop/mt167750(v=vs.85).aspx)します。

## <a name="BKMK_shielded"></a>シールドされた仮想マシン\(新規\)
HYPER-V 管理者やホスト上でマルウェア検査、改ざん、またはシールドされた仮想マシンの状態からのデータを盗むを防ぐためにいくつかの機能の仮想マシンの使用の影響を受けません。 データと状態が暗号化されて、ビデオ出力とディスクは、HYPER-V administrators が表示されないし、仮想マシンは、ホスト ガーディアン サーバーによって決定される、正常である、既知のホストでのみ実行に制限することができます。 詳細については、次を参照してください。[保護されたファブリックとシールドされた Vm](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)します。
  
>[!NOTE]  
> シールドされた仮想マシンは、HYPER-V レプリカとの互換性です。 シールドされた仮想マシンをレプリケートするには、シールドされた仮想マシンを実行するにレプリケートするホストを承認する必要があります。  

## <a name="BKMK_StartOrder"></a>クラスター化された仮想マシンの順序の優先順位をスタート\(新規\)
この機能では、クラスター化された仮想マシンを起動または再起動最初を詳細に制御できます。 これにより、それらのサービスを使用する仮想マシンの前にサービスを提供する仮想マシンを起動しやすくします。 セットを定義、セットでは、仮想マシンを配置し、依存関係を指定します。 Windows PowerShell コマンドレットを使用して、セットなどの管理[新規 ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/new-clustergroupset)、 [Get ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustergroupset)、および[追加 ClusterGroupSetDependency](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergroupsetdependency)します。
.  
## <a name="BKMK_QoS"></a>記憶域の品質 (qos)\(更新\)
スケールアウト ファイル サーバーで記憶域の QoS ポリシーを作成し、Hyper-V 仮想マシンの 1 つ以上の仮想ディスクにそのポリシーを割り当てることができるようになりました。 記憶域のパフォーマンスは、記憶域の負荷の変動に従って、ポリシーに合わせて自動的に再調整されます。 詳細については、次を参照してください。[記憶域サービスの品質](../../storage/storage-qos/storage-qos-overview.md)します。  
  
## <a name="BKMK_Config"></a>仮想マシン構成ファイルの形式\(更新\)
仮想マシンの構成ファイルでは、読み取りと書き込みの構成データをより効率的な新しい形式を使用します。 形式も、データの破損可能性を低減記憶域の障害が発生した場合。 .Vmcx ファイル名拡張子を使用して、仮想マシンの構成データ ファイルと .vmrs ファイル名拡張子を使用して、ランタイム状態のデータ ファイル。  
  
> [!IMPORTANT]  
> .Vmcx ファイル名拡張子では、バイナリ ファイルを示します。 .Vmcx と .vmrs ファイルの編集はサポートされていません。  
  
## <a name="BKMK_ConfgVersion"></a>仮想マシン構成バージョン\(更新\)
バージョンは、仮想マシンの構成、状態、およびスナップショット ファイルを保存、HYPER-V のバージョンとの互換性を表します。 バージョン 5 を使用する仮想マシンは、Windows Server 2012 R2 と互換性があるし、Windows Server 2012 R2 と Windows Server 2016 の両方で実行できます。 Windows Server 2016 で導入されたバージョンを持つ仮想マシンは、Windows Server 2012 R2 の HYPER-V で実行できません。   
  
移動または Windows Server 2012 R2 から Windows Server 2016 で HYPER-V を実行しているサーバーに仮想マシンをインポートする場合、仮想マシンの構成は自動的に更新します。 つまり、Windows Server 2012 R2 を実行するサーバーに戻る仮想マシンを移動することができます。 しかし、つまり、仮想マシンの構成のバージョンを手動で更新するまで、新しい仮想マシンの機能を使用することはできません。  
  
チェック、およびバージョンのアップグレードについては、次を参照してください。[アップグレードの仮想マシン バージョン](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)します。 この記事では、一部の機能が導入されたバージョンも示します。   
  
> [!IMPORTANT]  
> -   バージョンを更新した後は、Windows Server 2012 R2 を実行しているサーバーに仮想マシンを移動できません。  
> -   以前のバージョンに、構成をダウン グレードすることはできません。  
> -   [更新 VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)クラスターの機能レベルが Windows Server 2012 R2 HYPER-V クラスターでコマンドレットがブロックされます。  

## <a name="virtualization-based-security-for-generation-2-virtual-machines-new"></a>第 2 世代仮想マシンの Virtualization-based security\(新規)
仮想化ベースのセキュリティは、Device Guard と Credential Guard、マルウェアから悪用からオペレーティング システムの保護の強化を提供するなどの機能を強化します。 仮想化ベースのセキュリティは、世代 2 のゲストの仮想マシン バージョン 8 以降で使用できます。 仮想マシンのバージョンについては、次を参照してください。 [Windows 10 または Windows Server 2016 での Hyper-v で仮想マシンのアップグレード バージョン](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)します。


## <a name="BKMK_Containers"></a>Windows コンテナー\(新規\) 
Windows コンテナーは、1 つのコンピューター システムで実行する多くの分離されたアプリケーションを許可します。 構築するには、高速、高度にスケーラブルで移植可能なは。 2 つの種類のコンテナー ランタイムは、使用可能な各アプリケーションの分離の度合いが異なります。 Windows Server コンテナーでは、名前空間とプロセスの分離を使用します。 HYPER-V コンテナーは、コンテナーごとに、軽量の仮想マシンを使用します。  
  
主な機能は次のとおりです。  
  
-   Web サイトおよび HTTPS を使用してアプリケーションのサポート  
  
-   Nano server は、Windows Server と HYPER-V コンテナーの両方をホストできます。  
  
-   コンテナー共有フォルダーを使用してデータを管理する機能  
  
-   コンテナー リソースを制限する機能  
  
クイック スタート ガイドなどの詳細を参照してください、 [Windows コンテナー ドキュメント](https://docs.microsoft.com/virtualization/windowscontainers/index)します。  
  
## <a name="BKMK_PowerShellDirect"></a>Windows PowerShell ダイレクト\(新規\)  
これにより、ホストから仮想マシンで Windows PowerShell コマンドを実行する方法。 Windows PowerShell ダイレクトは、ホストと仮想マシン間で実行されます。 つまり、ネットワークまたはファイアウォールの要件は必要ありませんし、リモート管理の構成に関係なく動作します。  
  
Windows PowerShell ダイレクトは、HYPER-V 管理者、HYPER-V ホスト上のバーチャル マシンへの接続を使用して既存のツールの代替です。  
  
-   PowerShell またはリモート デスクトップなどのリモート管理ツール  
  
-   HYPER-V 仮想マシン接続 (VMConnect)  
  
これらのツールは適切に機能が上のトレードオフです。VMConnect は信頼性が高くが、自動化することが困難。 リモート PowerShell は強力ですが、設定および管理することが困難。 これらのトレードオフを HYPER-V の展開の拡大に合わせてより重要になる可能性があります。 VMConnect を使用するだけでは、強力なスクリプト作成と自動化エクスペリエンスを提供することで Windows PowerShell ダイレクトこの対処します。   
  
要件と手順については、次を参照してください。 [PowerShell ダイレクトでの管理の Windows 仮想マシン](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)します。  
