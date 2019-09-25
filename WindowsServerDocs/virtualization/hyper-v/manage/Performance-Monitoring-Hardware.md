---
title: Hyper-v 仮想マシンで Intel パフォーマンス監視ハードウェアを有効にする
description: Hyper-v マシンで Intel のパフォーマンス監視ハードウェアを有効にする方法について説明します。 また、パフォーマンス監視ハードウェアがライブマイグレーションを有効にする方法についても触れます。
ms.prod: windows-server-threshold
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 67f32a6e2ceeaf07701d558f473e2f997fbd8219
ms.sourcegitcommit: d12d9e6afd71d23e8a24682ad80d2cf3bc486588
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71226025"
---
# <a name="enable-intel-performance-monitoring-hardware-in-a-hyper-v-virtual-machine"></a>Hyper-v 仮想マシンで Intel パフォーマンス監視ハードウェアを有効にする

Intel プロセッサには、パフォーマンス監視ハードウェア (PMU、PEBS、LBR など) と呼ばれる機能が含まれています。 これらの機能は、Intel VTune アンプのようなパフォーマンスチューニングソフトウェアによって、ソフトウェアのパフォーマンスを分析するために使用されます。  Windows Server 2019 および Windows 10 バージョン1809より前では、Hyper-v が有効になっている場合、ホストオペレーティングシステムと Hyper-v ゲスト仮想マシンのどちらもパフォーマンス監視ハードウェアを使用できませんでした。  Windows Server 2019 と Windows 10 バージョン1809以降では、ホストオペレーティングシステムは既定でパフォーマンス監視ハードウェアにアクセスできます。  Hyper-v ゲスト仮想マシンには、既定ではアクセス権はありませんが、Hyper-v 管理者は1つまたは複数のゲスト仮想マシンへのアクセスを許可することを選択できます。  このドキュメントでは、パフォーマンス監視ハードウェアをゲスト仮想マシンに公開するために必要な手順について説明します。

## <a name="requirements"></a>要件

仮想マシンでパフォーマンスの監視ハードウェアを有効にするには、次のものが必要です。

- パフォーマンス監視ハードウェアを搭載した Intel プロセッサ (例: PMU、PEBS、IPT)
- Windows Server 2019 または Windows 10 バージョン 1809 (2018 10 月の更新プログラム) 以降
- [入れ子になった仮想化](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)を_使用しない_hyper-v 仮想マシン (停止状態でもあります)
 
## <a name="enabling-performance-monitoring-components-in-a-virtual-machine"></a>バーチャルマシンのパフォーマンス監視コンポーネントの有効化

特定のゲスト仮想マシンに対してさまざまなパフォーマンス監視コンポーネントを有効`Set-VMProcessor`にするには、PowerShell コマンドレットを使用します。
 
``` Powershell
# Enable all components
Set-VMProcessor MyVMName -Perfmon @("pmu", "lbr", "pebs")
```
 
``` Powershell
# Enable a specific component
Set-VMProcessor MyVMName -Perfmon @("pmu")
```
 
``` Powershell
# Disable all components
Set-VMProcessor MyVMName -Perfmon @()
```
> [!NOTE]
> パフォーマンス監視コンポーネントを有効にする場合`"pebs"` 、が指定`"pmu"`されている場合は、を指定する必要があります。  また、ホストの物理プロセッサでサポートされていないコンポーネントを有効にすると、バーチャルマシンの起動エラーが発生します。
 
## <a name="effects-of-enabling-performance-monitoring-hardware-on-saverestore-export-and-live-migration"></a>保存/復元、エクスポート、ライブマイグレーションのパフォーマンス監視ハードウェアを有効にした場合の影響
 
Microsoft では、異なる Intel ハードウェアを搭載したシステム間で、パフォーマンスを監視するハードウェアを使用した仮想マシンのライブマイグレーションまたは保存/復元を推奨していません。 パフォーマンス監視ハードウェアの特定の動作は、多くの場合、Intel ハードウェアシステム間で非アーキテクチャと変更が行われます。  実行中の仮想マシンを異なるシステム間で移動すると、アーキテクチャ以外のカウンターが予期しない動作になる可能性があります。