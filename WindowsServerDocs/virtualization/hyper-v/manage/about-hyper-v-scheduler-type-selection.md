---
title: HYPER-V ハイパーバイザー スケジューラの種類の選択について
description: モードの HYPER-V のスケジューラの使用、HYPER-V ホスト管理者向けの情報を提供します
author: allenma
ms.author: allenma
ms.date: 08/14/2018
ms.topic: article
ms.prod: windows-server-hyper-v
ms.technology: virtualization
ms.localizationpriority: low
ms.assetid: 5fe163d4-2595-43b0-ba2f-7fad6e4ae069
ms.openlocfilehash: c5360d8e2fdc23f8b05c6be0f665407eebedeba2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823883"
---
# <a name="about-hyper-v-hypervisor-scheduler-type-selection"></a>HYPER-V ハイパーバイザー スケジューラの種類の選択について

適用先:

* Windows Server 2016
* Windows Server バージョン 1709
* Windows Server Version 1803
* Windows Server 2019

このドキュメントでは、HYPER-V の既定の重要な変更について説明し、スケジューラの種類のハイパーバイザーの使用をお勧めします。 これらの変更には、両方のシステムのセキュリティと仮想化のパフォーマンスが影響します。 確認および変更と、このドキュメントで説明されているへの影響を理解して影響、推奨される展開のガイダンスおよび展開および管理する方法をよく理解するために関連するリスク要因を慎重に評価する必要があります仮想化ホストの管理者急速に変化するセキュリティの状況が発生した場合、HYPER-V ホスト。

>[!IMPORTANT]
>現在既知の同時使用するホストで実行すると、レガシ ハイパーバイザー クラシック スケジューラのスケジュール動作では、悪意のあるゲスト仮想マシンで複数のプロセッサ アーキテクチャで見えるの脆弱性が悪用される可能性サイド チャネルのセキュリティ有効になっているをマルチ スレッド (SMT)。  悪用、悪意のあるワークロードはそのパーティションの境界外のデータを観察でした。 ハイパーバイザーの中核となるスケジューラ型とゲスト Vm の再構成を利用する、HYPER-V ハイパーバイザーを構成することで、この種の攻撃を軽減できます。 Core scheduler では、ハイパーバイザーは、そのため、VM のデータにアクセスできることを実行する物理コアの境界を厳密に分離する、同じ物理プロセッサ コアで実行するゲスト VM の Vp を制限します。  これは、他のパーティションからすべてのアイテムを観察するかどうかを VM を実行できなくなります、これらのサイド チャネル攻撃に対する非常に効果的な軽減策、ルートまたは別のゲスト パーティション。  そのため、Microsoft では、既定値を変更して、仮想化ホストとゲスト Vm の構成設定をお勧めします。

## <a name="background"></a>背景

Windows Server 2016 以降、HYPER-V のスケジューリングと管理仮想プロセッサ、ハイパーバイザーのスケジューラの型と呼ばれるいくつかのメソッドをサポートします。  すべてのハイパーバイザー スケジューラの種類の詳細な説明が記載されて[の概要と、HYPER-V ハイパーバイザーのスケジューラの型を使用して](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)します。

>[!NOTE]
>新しいハイパーバイザー スケジューラの型では、Windows Server 2016 では、最初に導入し、以前のリリースでは使用できません。 Windows Server 2016 より前に、HYPER-V のすべてのバージョンでは、クラシック スケジューラのみをサポートします。 Core スケジューラのサポートが最近発行されました。

## <a name="about-hypervisor-scheduler-types"></a>ハイパーバイザーのスケジューラの種類について

この記事では、従来の「クラシック」スケジューラと新しいハイパーバイザー core スケジューラ型を使用して、これらのスケジューラ型が Symmetric マルチ スレッド、または SMT の使用と交差する方法を具体的には重点を置いています。  コアとクラシックのスケジューラと基になるシステムのプロセッサでゲスト Vm から作業を配置の各方法の違いを理解しておく必要があります。

### <a name="the-classic-scheduler"></a>クラシックのスケジューラ

クラシックのスケジューラは、ルート Vp のゲスト Vm に属する Vp などのシステム全体で仮想プロセッサ (Vp) での作業をスケジューリングの公平、ラウンド ロビンの方法を参照します。 クラシックのスケジューラは、既定のスケジューラの種類 (Windows Server 2019、記載されている説明に従って) までのすべてのバージョンの HYPER-V で使用されました。  クラシックのスケジューラのパフォーマンス特性を十分に理解、およびクラシックのスケジューラがまさに合理的な余白によって、ホストの VP:LP 比率のオーバー サブスクリプションは、ワークロードのオーバー サブスクリプションをサポートするために示されています (に応じて、種類のワークロードを仮想化、全体的なリソース使用率など。)。

SMT を有効になっていると、仮想化ホストで実行と、クラシックのスケジューラはしないにコアを個別に属する各 SMT スレッド上にある VM からゲスト Vp をスケジュールします。 そのため、同時に (1 つの VM が別の VM の他のスレッドで実行中には、コアの 1 つのスレッドで実行されている場合)、同じコア上の異なる Vm を実行できます。

### <a name="the-core-scheduler"></a>スケジューラ コア

Core スケジューラは、両方のセキュリティとシステムのパフォーマンスに影響がゲストのワークロードの分離を提供する SMT のプロパティを活用します。 Core スケジューラにより Vp VM からは兄弟 SMT のスレッドでスケジュールされているようになります。 これは、対称的 LPs がいる場合、2 つの Vp のグループをスケジュールする、2 つのグループにしてシステムの CPU コアは Vm 間で共有しないようにします。

ゲスト Vp SMT ペアを基になるをスケジュールすることによっては、コア スケジューラは、ワークロードの分離のための強力なセキュリティ境界を提供し、待機時間の機密性の高いワークロードのパフォーマンス変動の影響を軽減するも使用できます。

なお SMT を有効にせず、担当副社長が仮想マシンのスケジュールされている場合、それが実行すると、コアの兄弟 SMT スレッドはアイドル状態のままになる場合に、担当副社長が全体のコアを使用します。  これにより、適切なワークロードの分離を提供する必要がありますが、特にシステム LPs になるとオーバーサブスク - つまり、合計 VP:LP 比率が 1:1 を超えると、システム全体のパフォーマンスに影響を与えます。 そのため、ゲスト Vm のコアあたり複数のスレッドを使わずに構成を実行しているは、最適化の構成です。

### <a name="benefits-of-the-using-the-core-scheduler"></a>コアのスケジューラを使用する利点

Core スケジューラには次の利点があります。

* ゲスト ワークロードの分離 - ゲスト Vp の強力なセキュリティ境界は、基になる物理コアのペア、サイド チャネル スヌーピング攻撃に対する脆弱性を減らすことで実行に制限されます。

* 大きいワークロードの整合性を提供する、ワークロードの削減の可変性 - ゲスト ワークロード スループットの可変性が大幅に減少します。

* ゲスト Vm の OS とゲストの仮想マシンで実行されているアプリケーションでの SMT の使用は、SMT の動作を利用でき、プログラミング インターフェイス (Api) を制御し、SMT のスレッド間で作業を分散させるときに実行される場合と同様に非仮想化します。

Core スケジューラは、強力なセキュリティ境界と負荷が低い variabilty を活用するには、具体的には現在、Azure の仮想化ホストで使用されます。 Microsoft では、主要なスケジューラのタイプがする必要がありは引き続き既定ハイパーバイザー仮想化シナリオの大半の種類のスケジュール設定と考えています。  そのため、お客様は既定でセキュリティで保護されたさせるには、Microsoft はこの変更を行う Windows Server 2019 のようになりました。

### <a name="core-scheduler-performance-impacts-on-guest-workloads"></a>ゲストのワークロードに core スケジューラ パフォーマンスの影響

脆弱性の特定のクラスを効果的に軽減するために必要なコア スケジューラ可能性がありますパフォーマンスが低下する可能性があります。 お客様には、その仮想化ホストの全体的なワークロードの容量をその仮想マシンへの影響とパフォーマンス特性の違いを表示可能性があります。 Core スケジューラが SMT VP を実行する必要がありますの場合、他の必要がありますがアイドル状態になったときに基になる論理コアで命令ストリームの 1 つだけ実行します。 これにより、ゲストのワークロードのホストの合計容量が制限されます。

このドキュメントで、デプロイ ガイダンスに従って、これらのパフォーマンスに及ぼす影響を最小化できます。 ホスト管理者は、特定の仮想化展開シナリオを検討してくださいし、最大ワークロード密度、過剰な統合仮想化ホストなどの必要性とセキュリティのリスク許容度のバランスを取る慎重にする必要があります。

## <a name="changes-to-the-default-and-recommended-configurations-for-windows-server-2016-and-windows-server-2019"></a>既定の Windows Server 2016 および Windows Server 2019 で推奨される構成の変更

最大限のセキュリティ体制での HYPER-V ホストを展開するには、ハイパーバイザーの中核となるスケジューラ型の使用が必要です。 お客様は既定でセキュリティで保護されたさせるには、Microsoft は次の既定値を変更して、設定をお勧めします。

>[!NOTE]
>スケジューラの種類のハイパーバイザーの内部のサポートは、Windows Server 2016、Windows Server 1709 では、および Windows Server 1803 の最初のリリースに含まれていた、更新プログラムは、構成コントロールで選択できますこれにアクセスするために必要な、。ハイパーバイザーのスケジューラの型。  参照してください[の概要と、HYPER-V ハイパーバイザーのスケジューラの型を使用して](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types)これらの更新プログラムの詳細について。

### <a name="virtualization-host-changes"></a>仮想化ホストの変更

* ハイパーバイザーは Windows Server 2019 以降、既定で core スケジューラを使用します。

* Microsoft reccommends が Windows Server 2016 core スケジューラを構成します。 ハイパーバイザーの中核となるスケジューラ型は、既定値は、クラシックのスケジューラでは、Windows Server 2016 でサポートされます。 Core スケジューラは省略可能で、HYPER-V ホストの管理者によって明示的に有効にする必要があります。

### <a name="virtual-machine-configuration-changes"></a>仮想マシンの構成の変更

* Windows Server の 2019 の既定の VM バージョン 9.0 を使用して作成された新しい仮想マシンは自動的に継承 SMT プロパティ (有効または無効になっています) の仮想化ホスト。 SMT が有効な場合、新しく作成された Vm、物理ホスト SMT を有効にする必要があり、既定では、基になるシステムと同じコアごとのハードウェア スレッド数を持つ VM のホストの SMT トポロジが継承されます。 これは、HwThreadCountPerCore で VM の構成に反映 = 0、0 が、VM は、ホストの SMT の設定を継承する必要がありますを示します。

* 8.2 またはそれ以前はの VM バージョンで既存の仮想マシンの HwThreadCountPerCore、元の VM のプロセッサ設定を保持して、8.2 VM バージョンのゲストの既定値は HwThreadCountPerCore = 1。 を Windows Server 2019 ホストでこれらのゲストを実行するときに、次のように扱われます。

    1. VM は、LP コアの数を小さい担当副社長の数がある場合、VM がコア スケジューラによって SMT 以外の VM として扱われます。 ゲスト担当副社長は、1 つの SMT スレッドで実行しているときに、core の兄弟 SMT スレッドがアイドル状態が。 これは最適なであり、全体的なパフォーマンスが低下なります。

    2. LP のコア数よりも多くの Vp と、VM がある、その VM は、core スケジューラによって、SMT VM として扱われます。 ただし、VM は、SMT の VM があるその他の問題を確認しません。 たとえば、OS やアプリケーションで CPU のトポロジを照会する CPUID 命令または Windows Api の使用では、SMT が有効になっているは示しません。

* 既存の VM が明示的に更新されるとオフの VM バージョンから更新 VM 操作では、バージョン 9.0、VM は HwThreadCountPerCore の現在の値を保持します。  VM には、SMT の強制対応はありません。

* 、Windows Server 2016 では、ゲスト Vm に SMT を有効にするをお勧めします。  明示的に変更しない限り、既定では SMT を無効、Windows Server 2016 で作成された Vm を 1 に設定されている HwThreadCountPerCore です。

>[!NOTE]
>Windows Server 2016 では、0 に設定 HwThreadCountPerCore はサポートしません。

#### <a name="managing-virtual-machine-smt-configuration"></a>仮想マシンの SMT 構成を管理します。

ゲスト仮想マシンの SMT 構成は、VM ごとに設定されます。 ホストの管理者は、検査し、次のオプションから選択するには、VM の SMT の構成します。

    1. その SMT-有効になっている、必要に応じてホストの SMT トポロジを自動的に継承を実行する Vm を構成します。

    2. SMT 以外として実行する Vm を構成します。

VM の SMT 構成は、HYPER-V Manager コンソールの概要ペインに表示されます。  VM の SMT 設定の構成は、VM の設定または PowerShell を使用して行うことができます。

#### <a name="configuring-vm-smt-settings-using-powershell"></a>PowerShell を使用して VM に SMT 設定を構成します。

ゲスト仮想マシンの SMT 設定を構成するには、十分なアクセス許可、および種類と PowerShell ウィンドウを開きます。

``` powershell
Set-VMProcessor -VMName <VMName> -HwThreadCountPerCore <0, 1, 2>
```

各項目の意味は次のとおりです。

    0 = Inherit SMT topology from the host (this setting of HwThreadCountPerCore=0 is not supported on Windows Server 2016)

    1 = Non-SMT

    Values > 1 = the desired number of SMT threads per core. May not exceed the number of physical SMT threads per core.

ゲスト仮想マシンの SMT を読み取り、十分なアクセス許可、および種類と、PowerShell ウィンドウを開きます。

``` powershell
(Get-VMProcessor -VMName <VMName>).HwThreadCountPerCore
```

そのゲスト HwThreadCountPerCore で構成された Vm に注意してください = 0 の SMT は、ゲストに対して有効にして、通常 2 基になる仮想化ホスト上にある同じ、ゲストに SMT スレッド数が公開されます。

### <a name="guest-vms-may-observe-changes-to-cpu-topology-across-vm-mobility-scenarios"></a>ゲスト Vm モビリティのシナリオで VM の CPU のトポロジへの変更が生じる

OS と VM でのアプリケーションは、VM のライフ サイクル イベントなどのライブ マイグレーションまたは保存操作と復元操作後に変更をホストしたりする前に、VM 設定の両方を表示するがあります。 状態の保存および復元する VM での操作中に、VM の HwThreadCountPerCore 設定と実際の値 (つまり、VM の設定とソース ホストの構成の計算組み合わせ) の両方が移行します。 VM がこれらの設定で、転送先ホストの実行を続けます。 VM がシャット ダウンを時点と、再開始、ことを実現した値を監視する VM でが変更されます。 問題のないこのアカウントは、OS およびアプリケーションと、レイヤー ソフトウェアが、通常の起動と初期化コード フローの一部として CPU トポロジの情報を検索する必要があります。 ただし、シーケンスがライブ移行または保存/復元操作、状態遷移を受ける Vm 中にスキップされたブート時の初期化にこれらを確認できるため最初の計算がシャット ダウンされるまでの値を実現し、再開します。  

### <a name="alerts-regarding-non-optimal-vm-configurations"></a>最適ではない VM の構成に関するアラート

構成詳細 Vp、最適ではない構成で物理コアのホストの結果がより多くの仮想マシン。 ハイパーバイザーのスケジューラは、SMT を認識している場合、これらの Vm を扱います。 ただし、OS とアプリケーション ソフトウェアで VM に SMT が無効になっているかを示す CPU トポロジが表示されます。 この条件が検出されると、HYPER-V のワーカー プロセスがイベント ログに記録、VM の構成が最適なあり、SMT の推奨であること、ホストの管理者を警告する仮想化ホスト上の VM を有効にします。

#### <a name="how-to-identify-non-optimally-configured-vms"></a>非最適に識別する方法には、Vm が構成されています。

非 SMT Vm、HYPER-V のワーカー プロセスのイベント ID 3498、イベント ビューアーのシステム ログを調べることで Vp VM の数が、物理コア数より大きい場合に、VM の起動されるを識別できます。 イベント ビューアー、または PowerShell を使用して、ワーカー プロセスのイベントを取得できます。

#### <a name="querying-the-hyper-v-worker-process-vm-event-using-powershell"></a>PowerShell を使用して、HYPER-V ワーカー プロセスの VM イベントのクエリを実行します。

クエリに HYPER-V ワーカー プロセスのイベント ID 3498 の PowerShell を使用して、次のコマンド プロンプトから入力 PowerShell。

``` powershell
Get-WinEvent -FilterHashTable @{ProviderName="Microsoft-Windows-Hyper-V-Worker"; ID=3498}
```

### <a name="impacts-of-guest-smt-configuaration-on-the-use-of-hypervisor-enlightenments-for-guest-operating-systems"></a>ゲスト オペレーティング システム用のハイパーバイザー啓発の使用にゲスト SMT 構成の影響

Microsoft ハイパーバイザーには、複数の啓発やヒントは、照会可能パフォーマンスが向上する可能性があります、またはを実行しているときにそれ以外の場合、さまざまな条件の処理を向上するような最適化のトリガーを使用して、ゲスト仮想マシンで実行されている OS が提供しています仮想化します。 最近導入された啓蒙の 1 つは、仮想プロセッサのスケジュールの処理と SMT を悪用したサイド チャネル攻撃の緩和策の OS の使用に関するものです。

>[!NOTE]
>Microsoft では、ホスト管理者は、ワークロードのパフォーマンスを最適化するために、ゲスト Vm に SMT を有効にすることをお勧めします。

このゲスト啓蒙の詳細については、指定された、しかし仮想化ホストの管理者の重要な習得事項が仮想マシンでは、HwThreadCountPerCore ホストの物理 SMT 構成と一致するように構成される場合がありますには。 これにより、非アーキテクチャのコアがないことを報告するハイパーバイザーを共有します。 そのため、啓蒙を必要とゲスト OS サポート最適化を有効にすることがあります。 Windows Server の 2019 で新しい Vm を作成し、HwThreadCountPerCore (0) の既定値のままにします。 Windows Server 2016 から移行された古い Vm ホストは、Windows Server 2019 構成バージョンを更新することができます。 そう、Microsoft をお勧めします HwThreadCountPerCore を設定後に 0 を = です。  、Windows Server 2016 では、マイクロソフトは、ホストの構成 (通常は 2) と一致する HwThreadCountPerCore の設定を推奨します。

### <a name="nononarchitecturalcoresharing-enlightenment-details"></a>NoNonArchitecturalCoreSharing 啓蒙の詳細

Windows Server 2016 以降、ハイパーバイザーは VP のスケジュール設定とゲスト OS への配置の処理を記述する新しい啓蒙を定義します。 定義されているこの啓蒙、[ハイパーバイザー トップレベル機能仕様 v5.0c](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/tlfs)します。

ハイパーバイザーの代理 CPUID リーフ CPUID.0x40000004.EAX:18[NoNonArchitecturalCoreSharing = 1] 仮想プロセッサは SMT の兄弟として報告される仮想プロセッサを除く、他の仮想プロセッサと物理コアを共有しないことを示しますスレッド。 たとえば、ゲスト担当副社長はことはありませんスレッドで実行、SMT ルート VP と共に兄弟同じプロセッサ コアの SMT スレッドで同時に実行されています。 この状態は、仮想化を実行している場合にのみ可能なは、これも深刻なセキュリティへの影響を持っている非アーキテクチャ SMT 動作を表します。 ゲスト OS は NoNonArchitecturalCoreSharing を使用できることは安全 STIBP の設定のパフォーマンスのオーバーヘッドを避けるために役立つ場合がありますの最適化を有効にすることを示す値として 1 を =。

特定の構成において、ハイパーバイザーは示しませんその NoNonArchitecturalCoreSharing = 1。 たとえば、ホストが SMT を有効になっているが、ハイパーバイザーのクラシック scheduler を使用して構成されている場合 NoNonArchitecturalCoreSharing 0 になります。 特定の最適化を有効にするから対応のゲストができなくなります。 そのため、マイクロソフトは、SMT を使用してホスト管理者がハイパーバイザーの中核となるスケジューラに依存し、仮想マシンが最適なワークロードのパフォーマンスを確実にホストから、SMT の構成を継承するように構成されていることを確認をお勧めします。

## <a name="summary"></a>概要

セキュリティの脅威は進化し続けています。 お客様は既定でセキュリティで保護された、Microsoft が、ハイパーバイザーと Windows Server 2019 ハイパー-V を開始する仮想マシンの既定の構成を変更する、およびガイダンスと推奨事項の Windows を実行しているお客様に更新を提供することを確認するにはServer 2016 Hyper-v の概要。 仮想化ホストの管理者にする必要があります。

* 読み、このドキュメントに記載されたガイダンスを理解します。

* 慎重に評価し、セキュリティ、パフォーマンス、仮想化の密度、およびユーザー固有の要件のワークロードの応答性の目標を満たしていることを確認するには、その仮想化展開を調整します。

* ハイパーバイザーの中核となるスケジューラによって提供される強力なセキュリティ上の利点を活用する既存の Windows Server 2016 の HYPER-V ホストを再度構成を検討してください。

* 更新既存以外 SMT の Vm のハードウェア セキュリティの脆弱性に対処担当副社長の分離によって課される制約のスケジュール設定からパフォーマンスの影響を軽減するには
