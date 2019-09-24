---
title: Intel パフォーマンス監視ハードウェアを Hyper-v 仮想マシンに公開する
description: Hyper-v コンピューターに Intel のパフォーマンスモニターのハードウェアを公開する方法について説明します。 また、有効化によるライブマイグレーションの効果についても触れます。
ms.prod: windows-server-threshold
ms.reviewer: ifufondu
author: ifeomaufondu-ms
ms.author: ifufondu
manager: chhuybre
ms.topic: article
ms.date: 09/20/2019
ms.openlocfilehash: 1bc821cc46a3a402778e1c76f4a2d8feb862fd75
ms.sourcegitcommit: 45415ba58907d650cfda45f4c57f6ddf1255dcbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71213618"
---
# <a name="exposing-intel-performance-monitoring-hardware-to-a-hyper-v-virtual-machine"></a>Intel パフォーマンス監視ハードウェアを Hyper-v 仮想マシンに公開する
 
## <a name="background"></a>背景情報
Intel プロセッサには、パフォーマンス監視ハードウェア (PMU、PEBS、LBR など) と呼ばれる機能が含まれています。 これらの機能は、Intel VTune アンプのようなパフォーマンスチューニングソフトウェアによって、ソフトウェアのパフォーマンスを分析するために使用されます。  Windows Server 2019 および Windows 10 バージョン1809より前では、Hyper-v が有効になっている場合、ホストオペレーティングシステムと Hyper-v ゲスト仮想マシンのどちらもパフォーマンス監視ハードウェアを使用できませんでした。  Windows Server 2019 と Windows 10 バージョン1809以降では、ホストオペレーティングシステムは既定でパフォーマンス監視ハードウェアにアクセスできます。  Hyper-v ゲスト仮想マシンには、既定ではアクセス権はありませんが、Hyper-v 管理者は1つまたは複数のゲスト仮想マシンへのアクセスを許可することを選択できます。  このドキュメントでは、パフォーマンス監視ハードウェアをゲスト仮想マシンに公開するために必要な手順について説明します。
 
## <a name="requirements"></a>要件 
パフォーマンス監視ハードウェアを仮想マシンに公開するには、次のものが必要です。
- パフォーマンス監視ハードウェアを搭載した Intel プロセッサ (例: PMU、PEBS、IPT)
- Windows Server 2019 または Windows 10 バージョン 1809 (2018 10 月の更新プログラム) 以降
- 停止状態にある、[入れ子になった仮想化](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization)を_使用しない_hyper-v 仮想マシン
 
## <a name="exposing-the-pmu-capabilities-pmu-lbr-pebs-to-virtual-machines-via-powershells-set-vmprocessor-cmdlet"></a>Powershell の Set VMProcessor コマンドレットを使用した仮想マシンへの PMU 機能 (PMU、LBR、PEBS) の公開
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
 
>メモ:Perfmon コンポーネントを有効にする場合`"pebs"` 、が指定`"pmu"`されている場合は、を指定する必要があります。  また、ホストの物理プロセッサでサポートされていない perfmon コンポーネントを有効にすると、バーチャルマシンの起動エラーが発生します。
 
## <a name="effect-of-pmu-enabelement-on-saverestore-export-and-live-migration"></a>保存/復元、エクスポート、ライブマイグレーションに対する PMU enabelement の影響
 
Microsoft では、異なる Intel ハードウェアを搭載したシステム間で、パフォーマンスを監視するハードウェアを使用した仮想マシンのライブマイグレーションまたは保存/復元を推奨していません。 パフォーマンス監視ハードウェアの特定の動作は、多くの場合、Intel ハードウェアシステム間で非アーキテクチャと変更が行われます。  実行中の仮想マシンを異なるシステム間で移動すると、アーキテクチャ以外のカウンターが予期しない動作になる可能性があります。