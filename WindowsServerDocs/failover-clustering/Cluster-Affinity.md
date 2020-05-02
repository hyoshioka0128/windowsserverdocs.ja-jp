---
title: クラスターのアフィニティ
ms.prod: windows-server
manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 03/07/2019
description: この記事では、フェールオーバークラスターのアフィニティレベルと反対のアフィニティレベルについて説明します。
ms.openlocfilehash: b0c2209680f3c34ac8376d5662620595aff92c0b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720614"
---
# <a name="cluster-affinity"></a>クラスターのアフィニティ

> 適用先:Windows Server 2019、Windows Server 2016

フェールオーバークラスターは、ノード間を移動して実行できる多数のロールを保持できます。 特定のロール (仮想マシン、リソースグループなど) が同じノードで実行されない場合もあります。  リソース消費、メモリ使用量などが原因である可能性があります。 たとえば、メモリと CPU を集中的に使用する2つの仮想マシンがあり、2つの仮想マシンが同じノードで実行されている場合、一方または両方の仮想マシンがパフォーマンスに影響を与える可能性があります。  この記事では、クラスターのアンチアフィニティレベルとその使用方法について説明します。

## <a name="what-is-affinity-and-antiaffinity"></a>アフィニティとその関係はどのようなものですか?

アフィニティは、2つ以上のロール (i、e、仮想マシン、リソースグループなど) の間にリレーションシップを確立するように設定するルールです。  "アンチアフィニティ" は同じですが、指定されたロールを相互に分離するために使用されます。 フェールオーバークラスターは、その役割に対して、"関係のない" アフィニティを使用します。  具体的には、ロールに定義されている[AntiAffinityClassNames](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/groups-antiaffinityclassnames)パラメーターが、同じノードで実行されないようにします。  

## <a name="antiaffinityclassnames"></a>AntiAffinityClassnames

グループのプロパティを見ると、AntiAffinityClassNames パラメーターが存在し、既定値として空白になります。  次の例では、Group1 と Group2 は、同じノードで実行されていると分離する必要があります。  プロパティを表示するために、PowerShell コマンドと結果は次のようになります。

    PS> Get-ClusterGroup Group1 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

    PS> Get-ClusterGroup Group2 | fl AntiAffinityClassNames
    AntiAffinityClassNames : {}

AntiAffinityClassNames は既定値として定義されていないため、これらのロールは一緒に実行することも、分離することもできます。  目標は、分離された状態を維持することです。  AntiAffinityClassNames の値は、任意のものにすることができます。同じである必要があります。  たとえば、Group1 と Group2 は仮想マシンで実行されているドメインコントローラーであり、それぞれ異なるノードで実行するのが最適です。  これらはドメインコントローラーであるため、クラス名には DC を使用します。  値を設定するために、PowerShell コマンドと結果は次のようになります。

    PS> $AntiAffinity = New-Object System.Collections.Specialized.StringCollection
    PS> $AntiAffinity.Add("DC")
    PS> (Get-ClusterGroup -Name "Group1").AntiAffinityClassNames = $AntiAffinity
    PS> (Get-ClusterGroup -Name "Group2").AntiAffinityClassNames = $AntiAffinity

    PS> Get-ClusterGroup "Group1" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

    PS> Get-ClusterGroup "Group2" | fl AntiAffinityClassNames
    AntiAffinityClassNames : {DC}

これらの設定が完了すると、フェールオーバークラスタリングによってそれらが分離されます。  

アンチ Affinityclassname パラメーターは "soft" ブロックです。  つまり、別のノードを維持しようとしますが、できない場合でも、同じノードでの実行が許可されます。  たとえば、グループが2ノードのフェールオーバークラスターで実行されているとします。  メンテナンスのために1つのノードをダウンさせる必要がある場合、両方のグループが同じノードで稼働していることを意味します。  この場合、これを行うことはできます。  これは最適ではない可能性がありますが、どちらの virtial マシンも許容可能なパフォーマンス範囲内で実行されます。

## <a name="i-need-more"></a>さらに必要です

前述のように、AntiAffinityClassNames はソフトブロックです。  しかし、ハードブロックが必要な場合はどうでしょうか。  同じノードで仮想マシンを実行することはできません。そうしないと、パフォーマンスに影響が生じ、一部のサービスがダウンする可能性があります。

そのような場合は、ClusterEnforcedAntiAffinity の追加のクラスタープロパティがあります。  このアンチアフィニティレベルにより、同じ AntiAffinityClassNames 値を持つすべてのコストが同じノードで実行されるのを防ぐことができます。

プロパティと値を表示するために、PowerShell コマンド (および結果) は次のようになります。

    PS> Get-Cluster | fl ClusterEnforcedAntiAffinity
    ClusterEnforcedAntiAffinity : 0

値 "0" は、無効になっていて、適用されないことを意味します。  値 "1" を指定すると、これが有効になり、ハードブロックになります。  このハードブロックを有効にするために、コマンド (および結果) は次のようになります。

    PS> (Get-Cluster).ClusterEnforcedAntiAffinity = 1
    ClusterEnforcedAntiAffinity : 1

これらの両方が設定されていると、グループは同時にオンラインになりません。  同じノード上にある場合は、フェールオーバークラスターマネージャーに表示されます。

![クラスターアフィニティ](media/Cluster-Affinity/Cluster-Affinity-1.png)

グループの PowerShell リストでは、次の内容が表示されます。

    PS> Get-ClusterGroup

    Name       State
    ----       -----
    Group1     Offline(Anti-Affinity Conflict)
    Group2     Online

## <a name="additional-comments"></a>その他のコメント

- ニーズに応じて、適切な [関係下] 設定を使用していることを確認します。
- 2ノードのシナリオと ClusterEnforcedAntiAffinity では、1つのノードがダウンしても、両方のグループが実行されないことに注意してください。  

- グループで優先所有者を使用することは、3つ以上のノードクラスターで、アンチアフィニティと組み合わせることができます。
- AntiAffinityClassNames と ClusterEnforcedAntiAffinity の設定は、リソースのリサイクル後にのみ行われます。 つまり、 設定することもできますが、両方のグループが設定時に同じノード上でオンラインになっている場合は、両方ともオンラインのままになります。
