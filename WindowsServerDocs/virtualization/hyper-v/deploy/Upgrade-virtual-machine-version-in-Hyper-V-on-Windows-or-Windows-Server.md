---
title: Windows 10 または Windows Server、HYPER-V で仮想マシンのバージョンをアップグレードします。
description: 手順については、仮想マシンのバージョンのアップグレードに関する考慮事項は、します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 897f2454-5aee-445c-a63e-f386f514a0f6
author: KBDAzure
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 8b277796492ca7d72b1a8713484c691cb9a8dca3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819443"
---
# <a name="upgrade-virtual-machine-version-in-hyper-v-on-windows-10-or-windows-server"></a>Windows 10 または Windows Server、HYPER-V で仮想マシンのバージョンをアップグレードします。

>適用先:Windows 10、Windows Server 2016、Windows Server 2019

HYPER-V の最新の機能で利用できるように、仮想マシン構成バージョンをアップグレードします。 これを行わないまで。

- HYPER-V ホストを最新バージョンの Windows または Windows Server をアップグレードするとします。
- クラスターの機能レベルをアップグレードするとします。
- 仮想マシンを以前のバージョンの Windows または Windows Server を実行する HYPER-V ホストに移動する必要はありませんを確認します。

詳細については、次を参照してください。[クラスター オペレーティング システムのローリング アップグレード](../../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)と[VMM で Hyper-v ホスト クラスターのローリング アップグレード実行](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade)します。

## <a name="step-1-check-the-virtual-machine-configuration-versions"></a>手順 1:仮想マシンの構成バージョンを確認してください。

1. Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。
2. Windows PowerShell を右クリックして **管理者として実行**します。
3. 使用して、 [GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレット。 仮想マシンのバージョンを取得するのには、次のコマンドを実行します。

```PowerShell
Get-VM * | Format-Table Name, Version
```

仮想マシンを選択して見て、、HYPER-V マネージャーで構成のバージョンもわかります、**概要**タブ。

## <a name="step-2-upgrade-the-virtual-machine-configuration-version"></a>手順 2:仮想マシンの構成バージョンをアップグレードします。

1. HYPER-V マネージャーで仮想マシンをシャット ダウンします。
2. アクションを選択 > 構成バージョンをアップグレードします。 このオプションは、仮想マシンの使用できない場合、既に最新の構成バージョンのでサポートされて、HYPER-V ホスト。

Windows PowerShell を使用して仮想マシンの構成バージョンをアップグレードするには、使用、[更新 VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)コマンドレット。 Vmname は仮想マシンの名前に、次のコマンドを実行します。

```PowerShell
Update-VMVersion <vmname>
```

## <a name="BKMK_SupportedConfigVersions"></a>サポートされている仮想マシンの構成のバージョン

PowerShell コマンドレットを実行[Get VMHostSupportedVersion](https://docs.microsoft.com/powershell/module/hyper-v/get-vmhostsupportedversion)を HYPER-V ホストがサポートしている仮想マシン構成バージョンを参照してください。 仮想マシンを作成するときに、既定の構成のバージョンで作成されます。 既定値とは何を表示するには、次のコマンドを実行します。

```PowerShell
Get-VMHostSupportedVersion -Default
```

以前のバージョンの Windows を使用してを実行している HYPER-V ホストに移動できる仮想マシンを作成する必要がある場合、 [NEW-VM](https://docs.microsoft.com/powershell/module/hyper-v/new-vm)コマンドレットのバージョン パラメーターを使用します。 たとえば、Windows Server 2012 R2 を実行する HYPER-V ホストに移動できる仮想マシンを作成するには、次のコマンドを実行します。 このコマンドは、構成バージョン 5.0"WindowsCV5"をという名前の仮想マシンに作成されます。

```PowerShell
New-VM -Name "WindowsCV5" -Version 5.0
```

>[!NOTE]
>Windows の以前のバージョンを実行する HYPER-V ホスト用に作成された仮想マシンをインポートしたり、バックアップから復元できます。 次の表に、HYPER-V ホスト OS のサポートされている VM の構成のバージョンが表示されない場合は、VM を開始する前に、VM 構成のバージョンを更新する必要があります。

### <a name="supported-vm-configuration-versions-for-long-term-servicing-hosts"></a>長期的なサービス ホストでサポートされる VM 構成バージョン

次の表は、Windows の長期的なサービスのバージョンを実行しているホストでサポートされている VM の構成バージョンを一覧表示します。

|Windows のバージョンの HYPER-V ホスト| 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
|---|---|---|---|---|---|---|---|---|---|
|Windows Server 2019|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise LTSC 2019|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2016 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2015 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|
|Windows Server 2012 R2|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|
|Windows 8.1|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|

### <a name="supported-vm-configuration-versions-for-semi-annual-channel-hosts"></a>半年チャネルのホストでサポートされる VM 構成バージョン

次の表では、現在サポートされている半年チャネル バージョンの Windows を実行しているホスト VM 構成のバージョンを一覧表示します。 Windows の半年チャネルのバージョンで詳細を取得するには、次のページを参照してください[Windows Server](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview)と[Windows 10。](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels)

|Windows のバージョンの HYPER-V ホスト| 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
|---|---|---|---|---|---|---|---|---|---|
|Windows Server、バージョン 1809|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 年 2018年 10 月 Update (バージョンは 1809)|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server Version 1803|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 April 2018 Update (バージョン 1803)|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Fall Creators Update (バージョン 1709)|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server バージョン 1709|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Creators Update (バージョン 1703)|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Anniversary Update (バージョン 1607)|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="why-should-i-upgrade-the-virtual-machine-configuration-version"></a>仮想マシンの構成バージョンをアップグレードする理由は必要がありますか。

移動または Windows Server 2019、Windows Server 2016 または Windows 10 では、仮想マシンで HYPER-V を実行するコンピューターに仮想マシンをインポートするときに"の構成は自動的に更新します。 つまり、戻すことができます、仮想マシンを以前のバージョンの Windows または Windows Server を実行する HYPER-V ホスト。 ただし、使用できないこと、新しい仮想マシンの機能のいくつかの構成バージョンを手動で更新されるまでこれも意味します。 アップグレードした後は、仮想マシンの構成バージョンをダウン グレードすることはできません。

仮想マシンの構成のバージョンでは、仮想マシンの構成、状態、およびスナップショット ファイルを保存、HYPER-V のバージョンとの互換性を表します。 構成バージョンを更新する際に、仮想マシンの構成とチェックポイント ファイルを格納するために使用するファイルの構造を変更します。 また、構成バージョンを更新するには、その HYPER-V ホストでサポートされている最新バージョンにします。 アップグレードされた仮想マシンは、新しい構成ファイル形式を使用します。新しいバージョンは、仮想マシン構成データを読み書きするときの効率を上げるように設計されています。 アップグレードすると、記憶域で障害が発生した場合のデータ破損の確率も低くなります。

次の表は、説明、ファイル名拡張子、および新しいまたはアップグレードされた仮想マシンに使用されるファイルの種類ごとの既定の場所を示します。

 |仮想マシン ファイルの種類 | 説明|
 |---|---|
|構成 |バイナリ ファイル形式で格納されている仮想マシン構成情報。 <br /> ファイル名拡張子: .vmcx <br /> 既定の場所:C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
 |ランタイムの状態|バイナリ ファイル形式で格納されている仮想マシンのランタイム状態情報。 <br />ファイル名拡張子: .vmrs と .vmgs <br />既定の場所:C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
|バーチャル ハード_ディスク|仮想マシンの仮想ハード_ディスクを格納します。 <br /> ファイル名拡張子: .vhd または .vhdx <br />既定の場所:C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Hard Disks|
 |自動仮想ハード ディスク |仮想マシンのチェックポイントに使用されるディスク ファイルの差分を表示します。 <br /> ファイル名拡張子: .avhdx <br /> 既定の場所:C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Hard Disks|
 |Checkpoint|チェックポイントは、複数のチェックポイント ファイルに格納されます。 各チェックポイントで、構成ファイルとランタイム状態ファイルが作成されます。 <br /> ファイル名拡張子: .vmrs と .vmcx <br />既定の場所:C:\ProgramData\Microsoft\Windows\Snapshots|

## <a name="what-happens-if-i-dont-upgrade-the-virtual-machine-configuration-version"></a>仮想マシンの構成バージョンをアップグレードしないとどうなりますか。

場合は、HYPER-V の以前のバージョンで作成した仮想マシンがある場合は、一部の機能はそれらの仮想マシンでは、構成のバージョンを更新するまで OS が動作しない新しいホストで使用できます。

一般的なガイダンスでは、としては Windows の新しいバージョンに仮想化ホストが正常にアップグレードすると構成のバージョンの更新をお勧めし、ロールバックする必要がないことを確信します。 使用する場合は、[クラスター OS のローリング アップグレード](https://docs.microsoft.com/windows-server/failover-clustering/Cluster-Operating-System-Rolling-Upgrade)機能、これは通常にクラスターの機能レベルを更新した後。 新機能と内部の変更と同様の最適化によるメリットは、これにより、します。

>[!NOTE]
>VM 構成のバージョンを更新すると、VM 構成の更新バージョンをサポートしていないホストを開始することはできません。

次の表では、いくつかの HYPER-V 機能を使用するために必要な最小の仮想マシン構成バージョンを示します。

|機能|VM 構成の最小バージョン|
|---|---|
|ホット アド/リムーブ メモリ|6.2|
|Linux VM のセキュア ブート|6.2|
|運用チェックポイント|6.2|
|PowerShell ダイレクト |6.2|
|仮想マシンのグループ化|6.2|
|仮想トラステッド プラットフォーム モジュール (vTPM)|7.0|
|複数の仮想マシン キュー (VMMQ)|7.1|
|XSAVE のサポート|8.0|
|キー記憶域ドライブ|8.0|
|ゲストの仮想化ベースのセキュリティのサポート (VBS)|8.0|
|入れ子になった仮想化|8.0|
|仮想プロセッサ数|8.0|
|大規模なメモリの Vm|8.0|
|仮想デバイスをデバイス (例: ネットワークと割り当てられたデバイス) ごとに 64 個の既定の最大数を増やす|8.3|
|パフォーマンス モニターの追加のプロセッサ機能を許可します。|9.0|
|自動的に公開[同時マルチ スレッド](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#background)を使用してホストで実行されている Vm の構成、 [Core スケジューラ](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler)|9.0|
|休止状態のサポート|9.0|

これらの機能に関する詳細については、次を参照してください。[新機能については、Hyper-v で Windows Server](../What-s-new-in-Hyper-V-on-Windows.md)します。

