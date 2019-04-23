---
title: 仮想マシン リソースの管理
description: VM の CPU グループの使用
keywords: Windows 10, Hyper-V
author: allenma
ms.date: 06/18/2018
ms.topic: article
ms.prod: windows-10-hyperv
ms.service: windows-10-hyperv
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: 7c4ddf3e5d2ff58eef844c50960327c27a3e0a3d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854763"
---
>適用先:Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

# <a name="virtual-machine-resource-controls"></a>仮想マシン リソースの管理

この記事では、仮想マシンの HYPER-V リソースと分離のコントロールについて説明します。  これらの機能では、仮想マシンの CPU グループ、またはだけ「CPU グループ」と呼びますは、Windows Server 2016 で導入されました。  CPU のグループを使用するより優れたに HYPER-V 管理者を管理およびゲスト仮想マシン間で、ホストの CPU リソースを割り当てます。  CPU のグループを使用して、HYPER-V 管理者は次のことができます。

* 異なる割り当てグループ全体で共有仮想化ホストの合計 CPU リソースの各グループで、仮想マシンのグループを作成します。 これにより、さまざまな種類の Vm 用のサービスのクラスを実装するホストの管理者ができます。

* 特定のグループには、CPU リソースの制限を設定します。 この「グループの上限」は、ホストの上限の境界に、そのグループ用のサービスの目的のクラスを効果的に強制するグループ全体が消費する CPU リソースを設定します。

* 特定のホスト システムのプロセッサ セットでのみ実行する CPU のグループを制限します。 これは、互いに別の CPU グループに属している Vm の分離を使用できます。

## <a name="managing-cpu-groups"></a>CPU のグループを管理します。

CPU のグループは、HYPER-V ホストのコンピューティング サービス、または HCS によって管理されます。 HCS、その起源の優れた説明 HCS api などへのリンクは、Microsoft Virtualization チームのブログ投稿でご確認いただけます[ホスト コンピューティング サービス (HCS) を導入](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/)します。

>[!NOTE] 
>CPU のグループです。 作成および管理に HCS だけことができます。HYPER-V Manager アプレット、WMI と PowerShell の管理インターフェイスが CPU グループをサポートしません。

Microsoft は、コマンド ライン ユーティリティ、cpugroups.exe、上、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=865968) HCS インターフェイスを使用する CPU のグループを管理します。  このユーティリティは、ホストの CPU のトポロジを表示できます。

## <a name="how-cpu-groups-work"></a>CPU グループの動作

ホストのコンピューティング リソースの CPU グループの割り当ては、計算の CPU グループ cap を使用して、HYPER-V ハイパーバイザーによって強制されます。 CPU のグループの上限は、CPU のグループの合計 CPU 容量の一部です。 グループのキャップの値は、グループのクラス、またはレベルが割り当てられた優先度によって異なります。 計算されたグループの上限は、「CPU 時間の分 LP's 数」として考えることができます。 このグループの予算を共有すると、それ自身のグループ全体の CPU 割り当てを使用できるように、単一の VM がアクティブであった、だけの場合。

CPU のグループの上限は G として計算されます = *n* x *C*、場所。

    *G* is the amount of host LP we'd like to assign to the group
    *n* is the total number of logical processors (LPs) in the group
    *C* is the maximum CPU allocation — that is, the class of service desired for the group, expressed as a percentage of the system’s total compute capacity

たとえば、4 つの論理プロセッサ (LPs) と上限の 50% に構成されている CPU グループがあるとします。

    G = n * C
    G = 4 * 50%
    G = 2 LP's worth of CPU time for the entire group

この例では、G の CPU グループには CPU 時間の分の 2 LP's が割り当てられます。  

仮想マシンまたはグループにバインドされている仮想プロセッサの数に関係なく、状態に関係なく、グループの上限が適用されます (シャット ダウンなどの開始または) の CPU グループに割り当てられている仮想マシン。 したがって、同じの CPU グループにバインドされている各 VM の CPU 割り当ての合計をグループの一部が表示されます、これが CPU グループにバインドされている Vm の数に変更されます。 そのため、Vm がバインドされているか、または CPU のグループから Vm をバインド解除、全体的な CPU グループ上限あり必要があります再調整されます必要な結果として得られる VM あたりの上限を維持するために設定します。 VM ホストの管理者または仮想化管理ソフトウェア レイヤーは、VM あたりの必要な CPU リソースの割り当てを実現するために必要に応じてグループの上限を管理する責任を負います。

## <a name="example-classes-of-service"></a>サービスの例のクラス

簡単な例を見てみましょう。 最初に、HYPER-V ホストの管理者がゲスト Vm 用のサービスの 2 つの階層をサポートしたいとします。

1. ローエンドの"C"層。 この層に全体のホストのコンピューティング リソースの 10% お任せします。

1. ミッドレンジ"B"層。 この層には、ホスト全体のコンピューティング リソースの 50% が割り当てられます。

この時点でこの例では、その他の CPU リソースの管理は、重みを個々 の VM cap など、使用し、予約をアサートします。
ただし、少し後で表示されるように、個々 の VM の上限は重要ですと。

わかりやすくするために、仮定が各 VM に 1 VP、およびホストに 8 LPs します。 まず、空のホスト。

"B"層を作成するには、ホスト adminstartor は、グループの上限を 50% に設定します。

    G = n * C
    G = 8 * 50%
    G = 4 LP's worth of CPU time for the entire group

ホストの管理者は、1 つの"B"層 VM を追加します。
この時点で、"B"レベルの VM で使用できます多くて、ホストの CPU、または 4 LPs のそれと同等の価値が 50%、システムの例。

ここで、管理者は、2 番目"層 B"VM を追加します。 CPU のグループの割り当て-すべての Vm 間で均等に分割されます。 各 VM を今すぐ取得 50%、25%、それぞれまたはコンピューティング時間の分の 2 LPs の同等のグループ B の総数の半数グループ b の 2 つの Vm の合計ものがいます。

## <a name="setting-cpu-caps-on-individual-vms"></a>個々 の Vm 上の CPU 上限の設定

グループの上限だけでなく、各 VM は、各「VM の上限」ことができます。 CPU の上限、重量、予約など、VM あたりの CPU リソースの制御以来、HYPER-V の一部であった。
グループの上限と組み合わせると、グループが使用可能な CPU リソースを持つ場合でも、VM の上限は各担当副社長が取得できる、CPU の最大量を指定します。

たとえば、ホストの管理者は"C"の Vm 上で、cap を 10 %vm を配置する可能性があります。
そうすること"C"Vp のほとんどがアイドル状態になった場合でも各担当副社長でした達しません 10% を超える。
VM の上限では、なし"C"Vm はさせる以外の階層によって許可されるレベルのパフォーマンスを得ることができます。

## <a name="isolating-vm-groups-to-specific-host-processors"></a>特定のホストのプロセッサに VM のグループを分離します。

HYPER-V ホストの管理者には、VM にコンピューティング リソースを専用に使用できる必要もあります。
たとえば、管理者は、premium を提供しようとしています"A"を 100% のクラスのキャップを持つ VM。
スケジュールの最小の待機時間を必要とし、ジッター可能であればこれらの premium Vm可能性がありますいない解除によってスケジュールされる他の VM。
この分離を実現するために CPU グループを特定の LP アフィニティ マッピングを構成こともできます。

やなどの"A"の VM は、この例では、ホスト上に合わせて、管理者が新しい CPU グループを作成、ホストの LPs のサブセットにグループのプロセッサのアフィニティを設定します。
グループ B と C は、残りの LPs に関連付け。
管理者でしたはおそらく下位のレベル グループ B の中に、グループ a すべて LPs への排他アクセスを持ち、グループ A の 1 つの VM を作成し、残りの LPs 共有 C の場合します。

## <a name="segregating-root-vps-from-guest-vps"></a>ゲストの Vp から分離したルート Vp

既定では、HYPER-V は、基になる各物理 LP で、担当副社長、ルートを作成します。
これらルート Vp 厳密にマップされた 1 対 1 LPs、システムでは、移行しない-は、各ルート担当副社長は、同じ物理 LP で実行が常にします。
ゲスト Vp は、使用可能な LP で実行することがあり、実行はルート Vp、共有します。

ただし、かもしれません望ましいまったく別のルート アクティビティの担当副社長にゲストの Vp から。
Premium"A"レベルの VM を実装して上記の例を検討してください。
"A"VM の Vp は最短の待機時間と「ジッター」、またはスケジュールのバリエーションがあることを確認するには、LPs の専用セット上で実行し、ルートがこれら LPs で稼働していないことを確認することをおいただきます。

これは、システム全体の論理プロセッサと 1 つのサブセットで実行されているホスト OS のパーティションを制限する"minroot"構成の組み合わせを使用して実現できます。 または複数の CPU グループが関連付けられます。

残り LPs に関連付けられた 1 つまたは複数の CPU グループで特定の LPs をホストのパーティションを制限するのには、仮想化ホストを構成できます。
この方法で、ルートおよびゲスト パーティションは、専用の CPU リソースを実行し、CPU を共有せず、完全に分離します。

"Minroot"構成の詳細については、次を参照してください。[で Hyper-v ホストの CPU リソースの管理](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016)します。

## <a name="using-the-cpugroups-tool"></a>CpuGroups ツールを使用します。

CpuGroups ツールを使用する方法の例をいくつか見てみましょう。

>[!NOTE] 
>区切り記号としてスペースのみを使用して、CpuGroups ツールのコマンド ライン パラメーターが渡されます。 いいえ '/' または '-' 文字は、必要なコマンド ライン スイッチを続行する必要があります。

### <a name="discovering-the-cpu-topology"></a>CPU のトポロジを検出します。

CpuGroups、GetCpuTopology でを実行すると、次に示す、LP インデックス、LP が所属する、パッケージ、およびコアの Id とルート担当副社長インデックス NUMA ノードを含む現在のシステムに関する情報が返されます。

次の例は、2 つの CPU ソケットを使用してシステムを示しています。 NUMA ノード、32 の LPs とマルチ スレッドの合計を有効になっており、8 ルート Vp、各 NUMA ノードから 4 Minroot を有効にするように構成します。
持つルート Vp LPs がある、RootVpIndex > = 0 になります。-1 の RootVpIndex で LPs は、ルート パーティションを使用できません、ハイパーバイザーでまだ管理されていて、他の構成設定で許可されているゲスト Vp を実行します。

```console
C:\vm\tools>CpuGroups.exe GetCpuTopology

LpIndex NodeNumber PackageId CoreId RootVpIndex
------- ---------- --------- ------ -----------
      0          0         0      0           0
      1          0         0      0           1
      2          0         0      1           2
      3          0         0      1           3
      4          0         0      2          -1
      5          0         0      2          -1
      6          0         0      3          -1
      7          0         0      3          -1
      8          0         0      4          -1
      9          0         0      4          -1
     10          0         0      5          -1
     11          0         0      5          -1
     12          0         0      6          -1
     13          0         0      6          -1
     14          0         0      7          -1
     15          0         0      7          -1
     16          1         1     16           4
     17          1         1     16           5
     18          1         1     17           6
     19          1         1     17           7
     20          1         1     18          -1
     21          1         1     18          -1
     22          1         1     19          -1
     23          1         1     19          -1
     24          1         1     20          -1
     25          1         1     20          -1
     26          1         1     21          -1
     27          1         1     21          -1
     28          1         1     22          -1
     29          1         1     22          -1
     30          1         1     23          -1
     31          1         1     23          -1
```

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>例 2: ホスト上のすべての CPU グループを印刷します。

ここでは、現在のホスト、GroupId、グループの CPU の上限、およびそのグループに割り当てられている LPs のインデックス上のすべての CPU グループをリストします。

有効な CPU の上限値は範囲 [0, 65536] で、これらの値は % で、グループの上限を express (たとえば、32768 = 50%)。

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>例 3-1 つの CPU グループを印刷します。

この例で、フィルターとして、GroupId を使用して 1 つの CPU グループをクエリします。

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>例 4-新しい CPU グループの作成

ここでは、グループに割り当てるには、グループ ID と LPs のセットを指定する、新しい CPU グループを作成します。

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

これで、新しく追加されたグループを表示します。

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>例 5: 50% に、CPU のグループの上限を設定します。

ここでは、50 %cpu グループの上限を設定します。

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

今すぐ更新しましたグループを表示することの設定を確認しましょう。

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>例 6 – ホスト上のすべての Vm の印刷の CPU グループ id

```console
C:\vm\tools>CpuGroups.exe GetVmGroup

VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36ab08cb-3a76-4b38-992e-000000000002
```

### <a name="example-7--unbind-a-vm-from-the-cpu-group"></a>例 7-CPU のグループから VM をバインド解除

CPU グループから VM を削除するには、NULL の GUID に VM の CpuGroupId に設定します。 これは、CPU のグループから VM をバインド解除します。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000

C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>例 8: VM を既存の CPU グループにバインドします。

ここでは、既存の CPU グループに VM を追加します。
既存の CPU グループに VM をバインドしない必要がありますまたは CPU グループ id の設定が失敗することに注意してください。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

ここで、VM G1 が CPU グループに必要なことを確認します。

```console
C:\vm\tools>CpuGroups.exe GetVmGroup
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G2 4ABCFC2F-6C22-498C-BB38-7151CE678758 36ab08cb-3a76-4b38-992e-000000000002
    P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC 36ab08cb-3a76-4b38-992e-000000000003
    P2 A593D93A-3A5F-48AB-8862-A4350E3459E8 36ab08cb-3a76-4b38-992e-000000000004
    G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200 36ab08cb-3a76-4b38-992e-000000000002
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 36AB08CB-3A76-4B38-992E-000000000001
```

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>例 9 – CPU グループ id でグループ化されたすべての Vm を印刷します。

```console
C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId                           VmName                                 VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36ab08cb-3a76-4b38-992e-000000000003     P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004     P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>例 10-1 つの CPU グループのすべての Vm を印刷します。

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>例 11-空ではない CPU グループを削除しようとしています。

空の CPU グループにのみ-なしでの CPU グループに Vm がバインドされている、-削除することができます。
空ではない CPU グループを削除することは失敗します。

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>例 – 12 が CPU グループからの唯一の VM のバインドを解除し、グループを削除します

この例では、いくつかのコマンドを使用して、CPU のグループを調べて、そのグループに属する 1 つの VM を削除するをし、グループを削除します。

最初に、グループ内の Vm を列挙してみましょう。

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

G1、という名前の単一 VM のみがこのグループに属していることがわかります。
VM のグループ ID を NULL に設定して、グループから G1 VM の削除しましょう。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

移動を確認してください.

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

これで、グループが空、安全に削除ができます。

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

グループがなくなったことを確認します。

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>13-の例は、元の CPU グループに VM をバインドします。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000002

C:\vm\tools>CpuGroups.exe GetGroupVms
CpuGroupId VmName VmId
------------------------------------ -------------------------------- ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002 G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002 G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
36AB08CB-3A76-4B38-992E-000000000002 G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
36ab08cb-3a76-4b38-992e-000000000003 P1 973B9426-0711-4742-AD3B-D8C39D6A0DEC
36ab08cb-3a76-4b38-992e-000000000004 P2 A593D93A-3A5F-48AB-8862-A4350E3459E8
```
