---
title: Windows 10 または Windows Server の Hyper-v で仮想マシンのバージョンをアップグレードする
description: バーチャルマシンのバージョンをアップグレードするための手順と考慮事項を示します。
manager: dongill
ms.topic: article
ms.assetid: 897f2454-5aee-445c-a63e-f386f514a0f6
author: jasongerend
ms.author: jgerend
ms.date: 05/22/2019
ms.openlocfilehash: e7c86cc15877c622cf3554a7ae69fe3d0aea1c50
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938926"
---
# <a name="upgrade-virtual-machine-version-in-hyper-v-on-windows-10-or-windows-server"></a>Windows 10 または Windows Server の Hyper-v で仮想マシンのバージョンをアップグレードする

>適用対象: Windows 10、Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

構成バージョンをアップグレードして、仮想マシンで最新の Hyper-v 機能を使用できるようにします。 これを行わないと、次のようになります。

- Hyper-v ホストを最新バージョンの Windows または Windows Server にアップグレードします。
- クラスターの機能レベルをアップグレードします。
- 以前のバージョンの Windows または Windows Server を実行している Hyper-v ホストに仮想マシンを戻す必要がないことを確認します。

詳細については、「[クラスターオペレーティングシステムのローリングアップグレード](../../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)」および「 [VMM で hyper-v ホストクラスターのローリングアップグレードを実行する](https://docs.microsoft.com/system-center/vmm/hyper-v-rolling-upgrade)」を参照してください。

## <a name="step-1-check-the-virtual-machine-configuration-versions"></a>手順 1: 仮想マシンの構成バージョンを確認する

1. Windows デスクトップで [スタート] ボタンをクリックし、名前の一部を入力 **Windows PowerShell**します。
2. [Windows PowerShell] を右クリックし、[**管理者として実行**] を選択します。
3. [GET VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレットを使用します。 次のコマンドを実行して、仮想マシンのバージョンを取得します。

```PowerShell
Get-VM * | Format-Table Name, Version
```

仮想マシンを選択して [**概要**] タブを表示することで、hyper-v マネージャーで構成バージョンを確認することもできます。

## <a name="step-2-upgrade-the-virtual-machine-configuration-version"></a>手順 2: 仮想マシンの構成バージョンをアップグレードする

1. Hyper-v マネージャーで仮想マシンをシャットダウンします。
2. [アクション > アップグレード構成バージョン] を選択します。 特定の仮想マシンについてこのオプションを選択できない場合、その仮想マシンは既に Hyper-V ホストでサポートされる最新の構成バージョンになっています。

Windows PowerShell を使用して仮想マシンの構成バージョンをアップグレードするには、[更新プログラム VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)コマンドレットを使用します。 次のコマンドを実行します。ここで、vmname は仮想マシンの名前です。

```PowerShell
Update-VMVersion <vmname>
```

## <a name="supported-virtual-machine-configuration-versions"></a>サポートされている仮想マシンの構成バージョン

PowerShell コマンドレット[VMHostSupportedVersion](https://docs.microsoft.com/powershell/module/hyper-v/get-vmhostsupportedversion)を実行して、hyper-v ホストでサポートされている仮想マシンの構成バージョンを確認します。 仮想マシンを作成すると、既定の構成バージョンで作成されます。 既定値を確認するには、次のコマンドを実行します。

```PowerShell
Get-VMHostSupportedVersion -Default
```

以前のバージョンの Windows を実行している Hyper-v ホストに移動できる仮想マシンを作成する必要がある場合は、-version パラメーターを指定して、[新しい VM](https://docs.microsoft.com/powershell/module/hyper-v/new-vm)コマンドレットを使用します。 たとえば、Windows Server 2012 R2 を実行している Hyper-v ホストに移動できる仮想マシンを作成するには、次のコマンドを実行します。 このコマンドは、"WindowsCV5" という名前の仮想マシンを、構成バージョン5.0 で作成します。

```PowerShell
New-VM -Name "WindowsCV5" -Version 5.0
```

>[!NOTE]
>以前のバージョンの Windows を実行している Hyper-v ホスト用に作成された仮想マシンをインポートしたり、バックアップから復元したりすることができます。 VM の構成バージョンが、次の表の Hyper-v ホストの OS でサポートされていると表示されていない場合は、vm を起動する前に VM 構成のバージョンを更新する必要があります。

### <a name="supported-vm-configuration-versions-for-long-term-servicing-hosts"></a>長期的なサービスホストでサポートされている VM 構成バージョン

次の表は、Windows の長期的なサービスバージョンを実行しているホストでサポートされている VM 構成のバージョンを示しています。

| Hyper-v ホストの Windows バージョン | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
|Windows Server 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise LTSC 2019|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2016 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Enterprise 2015 LTSB|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|
|Windows Server 2012 R2|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|
|Windows 8.1|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|

### <a name="supported-vm-configuration-versions-for-semi-annual-channel-hosts"></a>半期チャネルホストでサポートされている VM 構成バージョン

次の表は、現在サポートされている半期チャネルバージョンの Windows を実行しているホストの VM 構成バージョンを示しています。 Windows の半期チャネルバージョンの詳細については、 [Windows Server](../../../get-started-19/servicing-channels-19.md)と[windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview#servicing-channels)の次のページを参照してください。

| Hyper-v ホストの Windows バージョン | 9.1 | 9.0 | 8.3 | 8.2 | 8.1 | 8.0 | 7.1 | 7.0 | 6.2 | 5.0 |
| --- |---|---|---|---|---|---|---|---|---|---|
| Windows 10 5 月2019更新プログラム (バージョン 1903) |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
| Windows Server バージョン 1903 |&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;| &#10004;|
|Windows Server、バージョン 1809|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 October 2018 Update (バージョン 1809)|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server バージョン 1803|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 April 2018 Update (バージョン 1803)|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Fall Creators Update (バージョン 1709)|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Creators Update (バージョン 1703)|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows 10 Anniversary Update (バージョン 1607)|&#10006;|&#10006;|&#10006;|&#10006;|&#10006;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="why-should-i-upgrade-the-virtual-machine-configuration-version"></a>仮想マシンの構成バージョンをアップグレードする必要があるのはなぜですか。

Windows Server 2019、Windows Server 2016、または Windows 10 で Hyper-v を実行しているコンピューターに仮想マシンを移動またはインポートすると、仮想マシンの構成が自動的に更新されません。 これは、以前のバージョンの Windows または Windows Server を実行している Hyper-v ホストに仮想マシンを戻すことができることを意味します。 ただし、これは、構成バージョンを手動で更新するまで、新しい仮想マシンの機能の一部を使用できないことも意味します。 アップグレード後に仮想マシンの構成バージョンをダウングレードすることはできません。

仮想マシンの構成バージョンは、仮想マシンの構成、保存された状態、およびスナップショットファイルと Hyper-v のバージョンとの互換性を表します。 構成バージョンを更新するときに、仮想マシンの構成とチェックポイントファイルを格納するために使用するファイル構造を変更します。 また、構成バージョンを、その Hyper-v ホストでサポートされている最新バージョンに更新します。 アップグレードされた仮想マシンは、新しい構成ファイル形式を使用します。新しいバージョンは、仮想マシン構成データを読み書きするときの効率を上げるように設計されています。 アップグレードすると、記憶域で障害が発生した場合のデータ破損の確率も低くなります。

次の表に、新規またはアップグレードされた仮想マシンで使用されるファイルの種類ごとの説明、ファイル名拡張子、および既定の場所を示します。

 |仮想マシンのファイルの種類 | 説明|
 |---|---|
|構成 |バイナリファイル形式で格納されている仮想マシンの構成情報。 <br /> ファイル名拡張子:. vmcx <br /> 既定の場所: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
 |ランタイムの状態|バイナリファイル形式で格納されている仮想マシンのランタイム状態情報。 <br />ファイル名拡張子: vmrs と vmrs <br />既定の場所: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines|
|仮想ハード ディスク|バーチャルマシンのバーチャルハードディスクを保管します。 <br /> ファイル名拡張子: .vhd または .vhdx <br />既定の場所: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual ハードディスク|
 |自動仮想ハードディスク |バーチャルマシンのチェックポイントに使用される差分ディスクファイル。 <br /> ファイル名拡張子:. .avhdx <br /> 既定の場所: C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual ハードディスク|
 |Checkpoint|チェックポイントは、複数のチェックポイント ファイルに格納されます。 各チェックポイントで、構成ファイルとランタイム状態ファイルが作成されます。 <br /> ファイル名拡張子:. vmrs と. vmcx <br />既定の場所: C:\ProgramData\Microsoft\Windows\Snapshots|

## <a name="what-happens-if-i-dont-upgrade-the-virtual-machine-configuration-version"></a>仮想マシンの構成バージョンをアップグレードしないとどうなりますか。

以前のバージョンの Hyper-v で作成した仮想マシンがある場合は、構成バージョンを更新するまで、新しいホスト OS で使用できる一部の機能がこれらの仮想マシンで動作しない可能性があります。

一般的なガイダンスとして、仮想化ホストを新しいバージョンの Windows に正常にアップグレードした後で、ロールバックする必要がないことを確認した後で、構成バージョンを更新することをお勧めします。 [クラスター OS のローリングアップグレード](https://docs.microsoft.com/windows-server/failover-clustering/Cluster-Operating-System-Rolling-Upgrade)機能を使用している場合、通常はクラスターの機能レベルを更新した後になります。 このようにして、新機能や内部的な変更と最適化にもメリットがあります。

>[!NOTE]
>VM 構成のバージョンが更新されると、更新された構成バージョンをサポートしていないホストで VM を起動することはできません。

次の表は、一部の Hyper-v 機能を使用するために必要な仮想マシン構成の最小バージョンを示しています。

|機能|VM 構成の最小バージョン|
|---|---|
|ホット アド/リムーブ メモリ|6.2|
|Linux VM のセキュア ブート|6.2|
|運用チェックポイント|6.2|
|PowerShell ダイレクト |6.2|
|仮想マシンのグループ化|6.2|
|仮想トラステッド プラットフォーム モジュール (vTPM)|7.0|
|仮想マシンの複数のキュー (VMMQ)|7.1|
|XSAVE のサポート|8.0|
|キーストレージドライブ|8.0|
|ゲスト仮想化ベースのセキュリティサポート (VBS)|8.0|
|入れ子になった仮想化|8.0|
|仮想プロセッサ数|8.0|
|大容量メモリ Vm|8.0|
|仮想デバイスの既定の最大数をデバイスあたり64に増やします (ネットワークと割り当てられたデバイスなど)。|8.3|
|Perfmon の追加プロセッサ機能を許可する|9.0|
|[コアスケジューラ](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#windows-server-2019-hyper-v-defaults-to-using-the-core-scheduler)を使用してホスト上で実行されている vm の[同時マルチスレッド](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types#background)構成を自動的に公開する|9.0|
|休止状態のサポート|9.0|

これらの機能の詳細については、「 [Windows Server の hyper-v の新](../What-s-new-in-Hyper-V-on-Windows.md)機能」を参照してください。

