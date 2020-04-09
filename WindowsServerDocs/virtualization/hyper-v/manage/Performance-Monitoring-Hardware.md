---
title: Hyper-v 仮想マシンで Intel パフォーマンス監視ハードウェアを有効にする
description: Hyper-v マシンで Intel のパフォーマンス監視ハードウェアを有効にする方法について説明します。 また、パフォーマンス監視ハードウェアがライブマイグレーションを有効にする方法についても触れます。
ms.prod: windows-server
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 1165ce58cf781d6ef5f905cb8b01c00fa4552edb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860265"
---
# <a name="enable-intel-performance-monitoring-hardware-in-a-hyper-v-virtual-machine"></a>Hyper-v 仮想マシンで Intel パフォーマンス監視ハードウェアを有効にする

Intel プロセッサには、パフォーマンス監視ハードウェア (PMU、PEBS、LBR など) と呼ばれる機能が含まれています。 これらの機能は、Intel VTune アンプのようなパフォーマンスチューニングソフトウェアによって、ソフトウェアのパフォーマンスを分析するために使用されます。  Windows Server 2019 および Windows 10 バージョン1809より前では、Hyper-v が有効になっている場合、ホストオペレーティングシステムと Hyper-v ゲスト仮想マシンのどちらもパフォーマンス監視ハードウェアを使用できませんでした。  Windows Server 2019 と Windows 10 バージョン1809以降では、ホストオペレーティングシステムは既定でパフォーマンス監視ハードウェアにアクセスできます。  Hyper-v ゲスト仮想マシンには、既定ではアクセス権はありませんが、Hyper-v 管理者は1つまたは複数のゲスト仮想マシンへのアクセスを許可することを選択できます。  このドキュメントでは、パフォーマンス監視ハードウェアをゲスト仮想マシンに公開するために必要な手順について説明します。

## <a name="requirements"></a>要件

仮想マシンでパフォーマンスの監視ハードウェアを有効にするには、次のものが必要です。

- パフォーマンス監視ハードウェアを搭載した Intel プロセッサ (PMU、PEBS、LBR など)。  システムでサポートされているパフォーマンス監視ハードウェアを判断するには、Intel の[このドキュメント]( https://software.intel.com/en-us/vtune-amplifier-cookbook-configuring-a-hyper-v-virtual-machine-for-hardware-based-hotspots-analysis)を参照してください。
- Windows Server 2019 または Windows 10 バージョン 1809 (2018 10 月の更新プログラム) 以降
- [入れ子になった仮想化](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)を_使用しない_hyper-v 仮想マシン (停止状態でもあります)

仮想マシンで今後の Intel Processor Trace (IPT) パフォーマンス監視ハードウェアを有効にするには、次のものが必要です。

- IPT と PT2GPA 機能をサポートする Intel プロセッサ。  システムでサポートされているパフォーマンス監視ハードウェアを判断するには、Intel の[このドキュメント]( https://software.intel.com/en-us/vtune-amplifier-cookbook-configuring-a-hyper-v-virtual-machine-for-hardware-based-hotspots-analysis)を参照してください。
- Windows Server バージョン 1903 (SAC) または Windows 10 バージョン 1903 (2019 更新プログラム) 以降
- [入れ子になった仮想化](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)を_使用しない_hyper-v 仮想マシン (停止状態でもあります)

## <a name="enabling-performance-monitoring-components-in-a-virtual-machine"></a>バーチャルマシンのパフォーマンス監視コンポーネントの有効化

特定のゲスト仮想マシンに対して異なるパフォーマンス監視コンポーネントを有効にするには、管理者として実行しているときに `Set-VMProcessor` PowerShell コマンドレットを使用します。

``` Powershell
# Enable all components except IPT
Set-VMProcessor MyVMName -Perfmon @("pmu", "lbr", "pebs")
```

``` Powershell
# Enable a specific component
Set-VMProcessor MyVMName -Perfmon @("pmu")
```

``` Powershell
# Enable IPT 
Set-VMProcessor MyVMName -Perfmon @("ipt")
```

``` Powershell
# Disable all components
Set-VMProcessor MyVMName -Perfmon @()
```
> [!NOTE]
> パフォーマンス監視コンポーネントを有効にする場合、`"pebs"` が指定されている場合は、`"pmu"` も指定する必要があります。 PEBS は、PMU バージョン > = 4 のハードウェアでのみサポートされます。 ホストの物理プロセッサでサポートされていないコンポーネントを有効にすると、バーチャルマシンの起動エラーが発生します。

## <a name="effects-of-enabling-performance-monitoring-hardware-on-saverestore-export-and-live-migration"></a>保存/復元、エクスポート、ライブマイグレーションのパフォーマンス監視ハードウェアを有効にした場合の影響

Microsoft では、異なる Intel ハードウェアを搭載したシステム間で、パフォーマンスを監視するハードウェアを使用した仮想マシンのライブマイグレーションまたは保存/復元を推奨していません。 パフォーマンス監視ハードウェアの特定の動作は、多くの場合、Intel ハードウェアシステム間で非アーキテクチャと変更が行われます。  実行中の仮想マシンを異なるシステム間で移動すると、アーキテクチャ以外のカウンターが予期しない動作になる可能性があります。

