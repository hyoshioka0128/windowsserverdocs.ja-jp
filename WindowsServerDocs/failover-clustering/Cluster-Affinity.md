---
title: クラスターのアフィニティ
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 03/07/2019
description: この記事では、フェールオーバー クラスターのアフィニティと antiAffinity レベルを説明します。
ms.openlocfilehash: a38d53f6aed1ca634d41822f4486779f6d279ec0
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476046"
---
# <a name="cluster-affinity"></a>クラスターのアフィニティ

> 適用対象:Windows Server 2019、Windows Server 2016

フェールオーバー クラスター ノード間を移動して実行できる多くの役割を保持できます。  同じノードで、特定の役割 (仮想マシン、リソース グループなど) を実行してしないでください場合もあります。  リソースの消費量、メモリ使用量などが考えられます。たとえば、メモリと CPU を集中的には 2 つの仮想マシンがあるし、2 つの仮想マシンを同じノードで実行している場合、仮想マシンのいずれかでしたへの影響のパフォーマンスの問題が。  この記事で説明がクラスターの antiaffinity レベルとその使用方法。

## <a name="what-is-affinity-and-antiaffinity"></a>アフィニティおよび AntiAffinity は何か

アフィニティでは、(i、e、仮想マシン、リソース グループなど) にまとめておくためには、2 つ以上のロール間の関係を確立するルールを設定する場合です。  AntiAffinity は同じですが、相互の指定されたロールをようにするために使用します。  フェールオーバー クラスターでは、そのロールの AntiAffinity を使用します。  具体的には、 [AntiAffinityClassNames](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames)同じノードで実行されないように、ロールで定義されたパラメーター。  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

AntiAffinityClassNames パラメーターがあるグループのプロパティを調べるときに、既定値として空白。  次の例では Group1 と Group2 区切る必要があります、同じノードで実行されているからです。  プロパティを表示するには、PowerShell コマンドと結果になります。

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

以降、AntiAffinityClassNames は一緒に実行したり、離れているこれらの役割は、既定値として定義されていません。  目標は、分割を保持することです。  AntiAffinityClassNames の値は、好きにするには、接続同じであるがします。  たとえば Group1 と Group2 は仮想マシンで実行されているドメイン コント ローラーとそれらが最も適して別々 のノードで実行されています。  これらはドメイン コント ローラーであるため、クラス名の DC を使用します。  値を設定するには、PowerShell コマンドと結果になります。

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

これで設定されているフェールオーバー クラスタ リングは離れているようにしようとします。  

AntiAffinityClassName パラメーターは、「ソフト」ブロックです。  つまり、離れている場合は、引き続き試行されますが、できない場合は、これも、同じノードで実行するようにします。  たとえば、グループは、2 ノード フェールオーバー クラスターで実行されます。  を 1 つのノードがメンテナンスのためダウンする必要がある場合、両方のグループになります。 稼働している同じノードがどういうは。  この場合、これを指定してもかまいませんがあります。  最も理想的なできない可能性がありますが、両方の virtial マシンはパフォーマンスが許容できる範囲内でまだ実行されています。

## <a name="i-need-more"></a>詳細は必要があります。

前述のように、AntiAffinityClassNames、ソフト ブロックです。  しかし、ハード ブロックが必要な場合でしょうか。  彼の仮想マシンを実行することはできませんと同じノードであります。それ以外の場合、パフォーマンスに与える影響は発生し、いくつかのサービスがダウンする可能性がありますがあります。

ような場合、ClusterEnforcedAntiAffinity の追加のクラスターのプロパティがあります。  この antiaffinity レベルできなくなります是が非でも同じ AntiAffinityClassNames 値のいずれか、同じノードで実行されています。

プロパティと値を表示するには、PowerShell コマンド (および結果) ようになります。

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

値「0」は、無効になっていることを意味し、適用するのにはありません。  「1」の値では、有効で、ハード ブロック。  このハード ブロックを有効にするには、コマンド (および結果) はします。

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

これらの両方が設定されている場合、グループをまとめてオンラインをできません。  同じノードにある場合、これは、フェールオーバー クラスター マネージャーで表示します。

![クラスターのアフィニティ](media\Cluster-Affinity\Cluster-Affinity-1.png)

グループの PowerShell の一覧では、これが表示されます。

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>その他のコメント

- ニーズに応じて、適切な AntiAffinity 設定を使用していることを確認します。
- 注意 ClusterEnforcedAntiAffinity、2 つのノード シナリオで 1 つのノードがダウンして両方のグループが実行されない場合。  

- グループでの優先所有者の使用は、次の 3 つまたは複数のノード クラスターで AntiAffinity と組み合わせることができます。
- AntiAffinityClassNames と ClusterEnforcedAntiAffinity 設定、リソースの再利用後の場所になります。 つまり 両方のグループでオンラインに同じノードに設定すると、どちらも、引き続きオンラインのままですが、それらを設定できます。



