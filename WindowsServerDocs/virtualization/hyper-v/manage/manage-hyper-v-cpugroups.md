---
title: 仮想マシンのリソースコントロール
description: VM の CPU グループの使用
author: allenma
ms.date: 06/18/2018
ms.topic: article
ms.service: windows-10-hyperv
ms.assetid: cc7bb88e-ae75-4a54-9fb4-fc7c14964d67
ms.openlocfilehash: 1f902a37dd4df28b2591380e78fe86c271f4ed3e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963598"
---
# <a name="virtual-machine-resource-controls"></a>仮想マシンのリソースコントロール

> 適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

この記事では、仮想マシンの Hyper-v リソースと分離の制御について説明します。  これらの機能は、仮想マシンの CPU グループとして、または "CPU グループ" と呼ばれますが、Windows Server 2016 で導入されました。  CPU グループを使用すると、Hyper-v 管理者は、ゲスト仮想マシン間でホストの CPU リソースの管理と割り当てをより適切に行うことができます。  Hyper-v 管理者は、CPU グループを使用して次のことができます。

* 仮想マシンのグループを作成します。各グループは、仮想化ホストの合計 CPU リソースの割り当てが異なるため、グループ全体で共有されます。 これにより、ホスト管理者は、さまざまな種類の Vm に対してサービスのクラスを実装できます。

* CPU リソースの制限を特定のグループに設定します。 この "グループ上限" は、グループ全体が使用する可能性があるホスト CPU リソースの上限を設定し、そのグループに必要なサービスのクラスを効果的に適用します。

* CPU グループがホストシステムのプロセッサの特定のセットでのみ実行されるように制約を設定します。 これは、異なる CPU グループに属する Vm を相互に分離するために使用できます。

## <a name="managing-cpu-groups"></a>CPU グループの管理

CPU グループは、Hyper-v ホストコンピューティングサービス (HCS) を介して管理されます。 HCS、その genesis、HCS Api へのリンクの詳細については、Microsoft 仮想化チームのブログで[ホストコンピューティングサービス (hcs) の導入](https://blogs.technet.microsoft.com/virtualization/2017/01/27/introducing-the-host-compute-service-hcs/)に関する投稿を参照してください。

>[!NOTE]
>CPU グループを作成および管理するために使用できるのは HCS だけです。Hyper-v マネージャーアプレット、WMI および PowerShell 管理インターフェイスは、CPU グループをサポートしていません。

Microsoft では、HCS インターフェイスを使用して CPU グループを管理する、 [Microsoft ダウンロードセンター](https://go.microsoft.com/fwlink/?linkid=865968)で cpugroups.exe コマンドラインユーティリティを提供しています。  このユーティリティでは、ホストの CPU トポロジを表示することもできます。

## <a name="how-cpu-groups-work"></a>CPU グループのしくみ

CPU グループ間でのホストコンピューティングリソースの割り当ては、計算された CPU グループの上限を使用して Hyper-v ハイパーバイザーによって実施されます。 Cpu グループの上限は、cpu グループの合計 CPU 容量の割合を示します。 グループキャップの値は、グループクラス、または割り当てられた優先度レベルによって異なります。 計算されたグループキャップは、"大量の LP の CPU 時間" と考えることができます。 このグループの予算は共有されているので、1つの VM だけがアクティブだった場合は、グループの CPU 割り当て全体を使用できます。

CPU グループの上限は、G = *n* x *C*として計算されます。

- *G*は、グループに割り当てるホスト LP の量です。
- *n*は、グループ内の論理プロセッサ (lps) の合計数です。
- *C*は、最大 CPU 割り当て (グループに必要なサービスのクラス) です。これは、システムの合計コンピューティング容量に対する割合で表されます。

たとえば、CPU グループが4つの論理プロセッサ (LPs) で構成され、キャップが50% であるとします。

- G = n * C
- G = 4 * 50%
- G = グループ全体に対して 2 LP の CPU 時間

この例では、CPU グループ G に2世代の CPU 時間が割り当てられています。

グループキャップは、グループにバインドされている仮想マシンまたは仮想プロセッサの数に関係なく、CPU グループに割り当てられている仮想マシンの状態 (シャットダウンや開始など) に関係なく適用されることに注意してください。 そのため、同じ CPU グループにバインドされている各 VM は、グループの合計 CPU 割り当ての割合を受け取り、CPU グループにバインドされている Vm の数によって変化します。 そのため、vm が CPU グループからバインドまたはバインド解除されている場合、CPU グループ全体の上限を readjusted に設定し、結果として得られる VM あたりの上限を維持するように設定する必要があります。 VM ホスト管理者または仮想化管理ソフトウェアレイヤーは、必要に応じてグループキャップを管理し、必要に応じて VM ごとの CPU リソース割り当てを実現します。

## <a name="example-classes-of-service"></a>サービスのクラスの例

いくつかの簡単な例を見てみましょう。 まず、Hyper-v ホスト管理者がゲスト Vm 用に2層のサービスをサポートするとします。

1. ローエンドの "C" 層。 このレベルには、ホストのコンピューティングリソース全体の10% を与えます。

1. 中間範囲 "B" 層。 この層には、ホストのコンピューティングリソース全体の50% が割り当てられます。

この例のこの時点では、個々の VM キャップ、重み、予約など、他の CPU リソース制御が使用されていないことをアサートします。
ただし、後で説明するように、個々の VM の上限は重要です。

わかりやすくするために、各 VM には VP が1つあり、ホストには8個の LPs があると仮定してみましょう。 空のホストから始めます。

"B" 層を作成するために、ホストの管理は、グループの上限を50% に設定します。

- G = n * C
- G = 8 * 50%
- G = グループ全体に対して 4 LP の CPU 時間

ホスト管理者は、1つの "B" 層の VM を追加します。
この時点で、"B" 層の VM は、ホストの CPU のうち最大50% を使用できます。また、この例のシステムでは、4つの LPs に相当します。

これで、管理者は2つ目の "Tier B" VM を追加します。 CPU グループの割り当ては、すべての Vm 間で均等に分割されます。 グループ B には合計2つの Vm があります。そのため、各 VM は、グループ B の合計である50%、25%、またはそれに相当する2つのコンピューティング時間の半分を獲得します。

## <a name="setting-cpu-caps-on-individual-vms"></a>個々の Vm での CPU キャップの設定

グループキャップに加えて、各 VM は個別の "VM cap" も持つことができます。 CPU の上限、重量、予約など、VM ごとの CPU リソース制御は、その概要以降、Hyper-v に含まれていました。
グループの上限と組み合わせると、VM の上限は、グループに使用可能な CPU リソースがある場合でも、各 VP が取得できる CPU の最大量を指定します。

たとえば、ホスト管理者は、"C" Vm に10% の VM キャップを配置することができます。
このようにして、ほとんどの "C" VPs がアイドル状態であっても、各 VP が10% を超えることはありません。
VM cap を使用しない場合、"C" Vm は、その層で許可されているレベルを超えてパフォーマンスをさせる可能性があります。

## <a name="isolating-vm-groups-to-specific-host-processors"></a>特定のホストプロセッサに VM グループを分離する

Hyper-v ホスト管理者は、コンピューティングリソースを VM に専用にすることもできます。
たとえば、管理者が、クラスキャップが100% の premium "A" VM を提供したいとします。
これらの premium Vm では、最小のスケジューリング待機時間とジッターも必要です。つまり、他の VM によってスケジュール解除されていない可能性があります。
この分離を実現するために、特定の LP アフィニティマッピングで CPU グループを構成することもできます。

たとえば、この例でホストの "A" VM に適合させるために、管理者は新しい CPU グループを作成し、グループのプロセッサアフィニティをホストの LPs のサブセットに設定します。
グループ B と C は、残りの LPs に関連付けられます。
管理者は、グループ A に1つの VM を作成できます。これにより、グループ A のすべての LPs に排他的にアクセスできます。一方、下位層グループ B と C は残りの LPs を共有します。

## <a name="segregating-root-vps-from-guest-vps"></a>ルート VPs とゲスト VPs の分離

既定では、Hyper-v は基礎となる各物理 LP にルート VP を作成します。
これらのルート VPs は、厳密には1:1 とシステム LPs にマップされており、移行されません。つまり、各ルート VP は常に同じ物理 LP で実行されます。
ゲスト VPs は、利用可能なすべての LP で実行でき、ルート VPs との実行を共有します。

ただし、ルート VP アクティビティをゲスト VPs から完全に分離することが望ましい場合があります。
上の例では、premium "A" 層の VM を実装しています。
"A" VM の VPs が可能な限り最短の待機時間と "ジッター"、またはスケジュールのバリエーションを持つようにするには、それらを専用の LPs で実行し、ルートがこれらの LPs で実行されないようにします。

これを行うには、"minroot" 構成を組み合わせて使用します。これにより、ホスト OS パーティションは、合計システム論理プロセッサのサブセット上で実行されるように制限され、1つまたは複数の関連付けられた CPU グループが適用されます。

仮想化ホストは、ホストパーティションを特定の LPs に制限するように構成できます。これは、残りの LPs に関連付けられた1つ以上の CPU グループで構成できます。
この方法では、ルートパーティションとゲストパーティションは専用の CPU リソースで実行でき、CPU を共有せずに完全に分離されます。

"Minroot" 構成の詳細については、「 [Hyper-v ホスト CPU リソース管理](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/manage-hyper-v-minroot-2016)」を参照してください。

## <a name="using-the-cpugroups-tool"></a>Cpu 使用グループツールの使用

Cpu 使用率ツールの使用方法の例をいくつか見てみましょう。

>[!NOTE]
>Cpu グループツールのコマンドラインパラメーターは、区切り記号としてスペースのみを使用して渡されます。 '/' または '-' 文字は、必要なコマンドラインスイッチを続行できません。

### <a name="discovering-the-cpu-topology"></a>CPU トポロジの検出

次に示すように、Getcpu トポロジで Cpu グループを実行すると、現在のシステムに関する情報が返されます。これには、LP インデックス、LP が属する NUMA ノード、パッケージとコア Id、およびルート VP インデックスが含まれます。

次の例は、2つの CPU ソケットと NUMA ノード、合計 32 LPs、およびマルチスレッド化が有効になっているシステムを示しています。また、各 NUMA ノードの8つのルート VPs である Minroot を有効にするように構成されています。
ルート VPs を持つ LPs は RootVpIndex >= 0 です。RootVpIndex が-1 の LPs は、ルートパーティションでは使用できませんが、ハイパーバイザーによって引き続き管理されており、他の構成設定で許可されているようにゲスト VPs を実行します。

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

### <a name="example-2--print-all-cpu-groups-on-the-host"></a>例2–ホスト上のすべての CPU グループを印刷する

ここでは、現在のホスト上のすべての CPU グループ、GroupId、グループの CPU 上限、およびそのグループに割り当てられた LPs の決まっの一覧を示します。

有効な CPU 上限値は [0, 65536] の範囲内であり、これらの値はグループの上限をパーセントで表します (例: 32768 = 50%)。

```console
C:\vm\tools>CpuGroups.exe GetGroups

CpuGroupId                          CpuCap  LpIndexes
------------------------------------ ------ --------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536  24,25,26,27,28,29,30,31
```

### <a name="example-3--print-a-single-cpu-group"></a>例3–単一の CPU グループを印刷する

この例では、GroupId をフィルターとして使用して、単一の CPU グループに対してクエリを実行します。

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000003
CpuGroupId                          CpuCap   LpIndexes
------------------------------------ ------ ----------
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
```

### <a name="example-4--create-a-new-cpu-group"></a>例4–新しい CPU グループを作成する

ここでは、グループ ID とグループに割り当てる LPs のセットを指定して、新しい CPU グループを作成します。

```console
C:\vm\tools>CpuGroups.exe CreateGroup /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /GroupAffinity:0,1,16,17
```

新しく追加したグループを表示します。

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 65536 0,1,16,17
36AB08CB-3A76-4B38-992E-000000000002 32768 4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536 12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-5--set-the-cpu-group-cap-to-50"></a>例 5-CPU グループの上限を50% に設定する

ここでは、CPU グループの上限を50% に設定します。

```console
C:\vm\tools>CpuGroups.exe SetGroupProperty /GroupId:36AB08CB-3A76-4B38-992E-000000000001 /CpuCap:32768
```

次に、更新したばかりのグループを表示して設定を確認してみましょう。

```console
C:\vm\tools>CpuGroups.exe GetGroups /GroupId:36AB08CB-3A76-4B38-992E-000000000001

CpuGroupId                          CpuCap LpIndexes
------------------------------------ ------ ---------
36AB08CB-3A76-4B38-992E-000000000001 32768 0,1,16,17
```

### <a name="example-6--print-cpu-group-ids-for-all-vms-on-the-host"></a>例6–ホスト上のすべての Vm の CPU グループ id を出力する

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

### <a name="example-7--unbind-a-vm-from-the-cpu-group"></a>例 7: CPU グループからの VM のバインドを解除する

CPU グループから VM を削除するには、VM の cpu の Groupid を NULL の GUID に設定します。 これにより、VM が CPU グループからバインド解除されます。

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

### <a name="example-8--bind-a-vm-to-an-existing-cpu-group"></a>例 8-既存の CPU グループに VM をバインドする

ここでは、既存の CPU グループに VM を追加します。
VM が既存の CPU グループにバインドされていないこと、または CPU グループ id の設定が失敗することに注意してください。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:36AB08CB-3A76-4B38-992E-000000000001
```

ここで、VM G1 が目的の CPU グループにあることを確認します。

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

### <a name="example-9--print-all-vms-grouped-by-cpu-group-id"></a>例 9: CPU グループ id でグループ化されたすべての Vm を印刷する

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

### <a name="example-10--print-all-vms-for-a-single-cpu-group"></a>例10–1つの CPU グループのすべての Vm を印刷する

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36ab08cb-3a76-4b38-992e-000000000002

CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36ab08cb-3a76-4b38-992e-000000000002     G2 4ABCFC2F-6C22-498C-BB38-7151CE678758
36ab08cb-3a76-4b38-992e-000000000002     G3 B0F3FCD5-FECF-4A21-A4A2-DE4102787200
```

### <a name="example-11--attempting-to-delete-a-non-empty-cpu-group"></a>例 11: 空でない CPU グループを削除しようとしています

空の CPU グループ (つまり、バインドされた Vm のない CPU グループ) のみを削除できます。
空でない CPU グループを削除しようとすると失敗します。

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
(null)
Failed with error 0xc0350070
```

### <a name="example-12--unbind-the-only-vm-from-a-cpu-group-and-delete-the-group"></a>例 12: CPU グループからのみ VM をバインド解除し、グループを削除する

この例では、複数のコマンドを使用して CPU グループを調べ、そのグループに属する単一の VM を削除してから、グループを削除します。

まず、グループ内の Vm を列挙してみましょう。

```console
C:\vm\tools>CpuGroups.exe GetGroupVms /GroupId:36AB08CB-3A76-4B38-992E-000000000001
CpuGroupId                           VmName                                VmId
------------------------------------ ------ ------------------------------------
36AB08CB-3A76-4B38-992E-000000000001     G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC
```

G1 という名前の単一の VM のみがこのグループに属していることがわかります。
グループから G1 VM を削除してみましょう。 VM のグループ ID を NULL に設定します。

```console
C:\vm\tools>CpuGroups.exe SetVmGroup /VmName:g1 /GroupId:00000000-0000-0000-0000-000000000000
```

変更を確認してください...

```console
C:\vm\tools>CpuGroups.exe GetVmGroup /VmName:g1
VmName                                 VmId                           CpuGroupId
------ ------------------------------------ ------------------------------------
    G1 F699B50F-86F2-4E48-8BA5-EB06883C1FDC 00000000-0000-0000-0000-000000000000
```

グループが空になったので、安全に削除できます。

```console
C:\vm\tools>CpuGroups.exe DeleteGroup /GroupId:36ab08cb-3a76-4b38-992e-000000000001
```

グループが消えていることを確認します。

```console
C:\vm\tools>CpuGroups.exe GetGroups
CpuGroupId                          CpuCap                     LpIndexes
------------------------------------ ------ -----------------------------
36AB08CB-3A76-4B38-992E-000000000002 32768  4,5,6,7,8,9,10,11,20,21,22,23
36AB08CB-3A76-4B38-992E-000000000003 65536  12,13,14,15
36AB08CB-3A76-4B38-992E-000000000004 65536 24,25,26,27,28,29,30,31
```

### <a name="example-13--bind-a-vm-back-to-its-original-cpu-group"></a>例13– VM を元の CPU グループにバインドする

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
