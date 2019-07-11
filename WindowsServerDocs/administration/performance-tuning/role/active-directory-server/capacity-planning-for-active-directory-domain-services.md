---
title: Active Directory Domain Services のキャパシティ プランニング
description: AD DS のキャパシティ プランニング中に考慮すべき点の詳細について説明します。
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 5a9e2d39d4eedd1e8fdb4bfeaf267ad4cb4c596a
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67799834"
---
# <a name="capacity-planning-for-active-directory-domain-services"></a>Active Directory Domain Services のキャパシティ プランニング

このトピックが最初に Ken Brumfield、Microsoft、シニア プレミア フィールド エンジニアで記述し、Active Directory Domain Services (AD DS) の容量計画に関する推奨事項を提供します。

## <a name="goals-of-capacity-planning"></a>容量計画の目標

容量計画は、パフォーマンスの問題のトラブルシューティングと同じではありません。 密接に関連が大きく異なります。 容量計画の目標は次のとおりです。  

- 適切に実装し、環境を操作 
- パフォーマンス問題のトラブルシューティングに費やされた時間を最小限に抑えます。  
  
容量計画、組織は、クライアントのパフォーマンス要件を満たし、データ センターのハードウェアをアップグレードするために必要な時間に対応するために、ピーク期間中に 40% のプロセッサ使用率の基準のターゲットがあります。 一方、パフォーマンスの異常なインシデントの通知には、監視アラートのしきい値を 5 分間隔での 90% に設定することがあります。

容量管理のしきい値を超えると継続的に、違いは (1 回限りのイベントに問題がない)、ソリューションになります (つまりより高速なプロセッサの追加) の容量、またはある複数のサーバー、サービスのスケーリングを追加します。ソリューションです。 パフォーマンス警告のしきい値は、現在クライアント エクスペリエンスに影響が生じていないことと、即時の手順が、問題に対処する必要を示します。

類推: 容量管理が (防御的な driving、ブレーキは、適切に作業していることを確認) 自動車事故を回避する方法は、警察の消防署と緊急の医療専門家には何がパフォーマンスのトラブルシューティング事故します。 防御的な"driving"の詳細については、このディレクトリのアクティブなスタイル。

最後のいくつかの長年にわたってスケール アップ システムの容量計画のガイダンスが大幅に変更されました。 システム アーキテクチャでは、次の変更には、設計と、サービスのスケーリングに関する基本的な前提条件が求められています。

- 64 ビット サーバー プラットフォーム  
- 仮想化  
- 電力消費の増加の注意  
- SSD ストレージ  
- クラウドのシナリオ  

さらに、サーバー ベース キャパシティ プランニングのサービスに基づくキャパシティ プランニングの手順を演習からアプローチがシフトします。 Active Directory Domain Services (AD DS)、多くの Microsoft とサード パーティ製の製品が、バックエンドとして使用する完成度の高い分散サービスが 1 つ正しくを計画すると、その他のアプリケーションを実行するために必要な容量を確保する最も重要な製品です。

### <a name="baseline-requirements-for-capacity-planning-guidance"></a>キャパシティ プランニング ガイダンスのベースラインの要件

この記事では、全体で、次の基準要件が必要です。

- リーダーを読み、慣れて[パフォーマンス チューニング ガイドラインの Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85))します。
- Windows Server プラットフォームが x64 ベースのアーキテクチャ。 場合でも、Active Directory 環境は、(今すぐサポート ライフ サイクルの末尾) の次の Windows Server 2003 x86 にインストールされているがあり、ディレクトリ情報ツリー (DIT) が少ない 1.5 GB のサイズとすることができます簡単にメモリに保持して、このガイドラインが、記事では、引き続き適用されます。
- 容量計画は、継続的なプロセスと環境がどの程度期待を満たすを定期的に確認する必要があります。
- ハードウェア コストの変更として複数のハードウェア ライフ サイクルでの最適化が発生します。 たとえば、メモリが低コスト、コアあたりのコストが減少したら、または別のストレージの価格オプションを変更します。
- 1 日のピーク時のビジー期間を計画します。 30 分または時間間隔でこれを確認することをお勧めします。 実際、ピークと以下の環境は、「一時的なスパイクです」によって変形される程度が何を非表示にも長く可能性があります。
- 企業向けハードウェア ライフ サイクルの過程で成長を計画します。 これには、アップグレードするか、交互に 3 ~ 5 年おきに更新を完全なハードウェアを追加する方法があります。 各 Active Directory の負荷より大きく方法に「推測」が必要です。 履歴データを収集するには場合に、この評価に役立ちます。 
- フォールト トレランスを計画します。 推定値に 1 回*N*が派生するシナリオの計画*N* &ndash; 1、 *N* &ndash; 2、 *N* &ndash; *x*します。
  - 1 つまたは複数のサーバーの損失が最大のピーク時容量の見積もりを超過しないようにする組織のニーズに合わせて追加のサーバーに追加します。
  - また、成長プランとフォールト トレランスの計画を統合する必要を検討します。 など、負荷をサポートする 1 つの DC が必要ですが、推定される場合、負荷が次の年の 2 倍し、フォールト トレランスをサポートするために十分な容量されません、合計 2 つの Dc が必要です。 ソリューションは、次の 3 つの Dc で開始することです。 予算が厳しい場合、3、6 か月後に 3 番目のドメイン コント ローラーを追加する 1 つも計画します。

    >[!NOTE]
    >Active Directory に対応するアプリケーションを追加する場合は、負荷がアプリケーション サーバーまたはクライアントから送信されるかどうか、DC の負荷に顕著な影響があります。

### <a name="three-step-process-for-the-capacity-planning-cycle"></a>容量の計画サイクルの 3 つの手順

容量計画でまず必要なサービスの品質はどのようなを決定します。 たとえば、コア データ センターより高いレベルの同時実行をサポートし、ユーザーとコンシューマー冗長性に細心の注意を必要とするアプリケーション、およびシステムおよびインフラストラクチャのボトルネックを最小限に抑えることのより一貫性のあるエクスペリエンスを要求します。 これに対し、少数のユーザーとサテライトの場所には、同じレベルの同時実行またはフォールト トレランスの必要はありません。 そのため、サテライト オフィスには、基になるハードウェアとインフラストラクチャ コストの削減につながる可能性がありますを最適化するには、あまり気の必要はありません。 すべての推奨事項とガイダンスは記載されているはパフォーマンスを最適化し、必要条件が低いシナリオの選択的に緩和されたことができます。

次の質問が: 仮想または物理ですか? 容量計画の観点からは回答が正解や間違いはありません。あるのみ異なる一連の変数を使用します。 仮想化のシナリオでは、2 つのオプションのいずれかにはあります。

- 1 つのゲスト (仮想化が、サーバーから、物理ハードウェアを抽象化するためだけに存在) ホストごとに「直接マッピング」
- 「共有ホスト」

テストと実稼働のシナリオでは、「直接マッピング」シナリオを物理ホストに同じ扱うことことを示します。 「共有ホストでは、」ただし、いくつかの考慮事項について詳しくのスペル後でします。 「共有ホスト」のシナリオでは、AD DS は、リソースの競合もと、罰金やこれを行うためのチューニングに関する考慮事項があることを意味します。

これらの考慮事項を念頭には、容量の計画サイクルは、反復的な 3 段階のプロセスです。

1. 既存の環境を測定し、、特定、システムのボトルネック現在は、必要な容量を計画するために必要な環境の基礎を取得します。
1. 手順 1. で説明されている条件に従って必要なハードウェアを決定します。
1. 監視および実装されているインフラストラクチャが仕様内で動作していることを検証します。 このステップで収集されたデータでは、容量計画の次のサイクルのベースラインになります。

### <a name="applying-the-process"></a>プロセスを適用します。

パフォーマンスを最適化するには、これらの主要なコンポーネントが正しく選択されているし、アプリケーションの負荷を調整を確認します。

1. Memory
1. ネットワーク
1. ストレージ
1. プロセッサ
1. Net Logon

AD DS の基本的な記憶域の要件と適切に記述されたクライアント ソフトウェアの全般的な動作は、容量計画に関して、ほとんどの最新のサーバーとして、物理ハードウェアに多額の投資が行われずに 10,000 ~ 20,000 ユーザーの環境を使用します。クラスのシステムでは、負荷を処理します。 ただし、次の表は、適切なハードウェアを選択するには、既存の環境を評価する方法をまとめたものです。 各コンポーネントは、AD DS 管理者のベースラインの推奨事項と環境固有のプリンシパルを使用して、インフラストラクチャを評価するのに役立つ後続のセクションで詳細に分析されます。

原則として：

- 現在のデータに基づいて、サイズ変更は、現在の環境の正確なのみになります。
- 評価では、予想される需要、ハードウェアのライフ サイクルの経過に伴って大きくします。
- 今日過大するかどうかを判断し、大規模な環境に拡大またはライフ サイクルの容量を追加します。
- 仮想化、すべて同じ容量計画のプリンシパルと方法論、場合以外は適用、仮想化のオーバーヘッドは、関連するドメインに何も追加する必要があります。
- 容量計画には、予測しようとする部分と同様には、正確なサイエンスではありません。 完璧と 100% の精度を計算することを望んでいません。 このガイダンスは leanest の推奨事項です。追加の安全のための容量を追加し、継続的に、環境をターゲットに残ることを検証します。

### <a name="data-collection-summary-tables"></a>データ コレクションの概要テーブル

#### <a name="new-environment"></a>新しい環境

| コンポーネント | 見積もり |
|-|-|
|ストレージ/データベースのサイズ|60 KB ユーザーごとに 40 KB|
|RAM|Database Size<br />基本のオペレーティング システムの推奨事項<br />サード パーティ製のアプリケーション|
|ネットワーク|1 GB|
|CPU|同時実行ユーザーを各コアは 1000|

#### <a name="high-level-evaluation-criteria"></a>高度な評価基準

| コンポーネント | 評価基準 | 計画時の注意事項 |
|-|-|-|
|ストレージ/データベースのサイズ|最適化によって解放されるディスク領域のログ記録をアクティブ化"するには」というタイトルのセクション[ストレージの制限](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|記憶域]、[データベースのパフォーマンス|<ul><li>"論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg Disk Sec/read、""の論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg Disk Sec/write、""論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg Disk Sec/transfer"</li><li>"LogicalDisk( *\<NTDS Database Drive\>* )\Reads/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Writes/sec," "LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec"</li></ul>|<ul><li>記憶域がアドレスに 2 つの問題<ul><li>今日のスピンドルをベースと SSD サイズ ベースのストレージが、使用可能な領域は、ほとんどの AD 環境に関連はありません。</li> <li>– 多くの環境で使用できる入力/出力 (IO) 操作、これは、よく見過ごされます。 環境のみを評価することが重要に NTDS データベース全体をメモリに読み込むための十分な RAM がないです。</li></ul><li>ストレージは、複雑なトピックし、ハードウェア ベンダーの専門知識の適切なサイズ設定する必要があります。 特に、SAN、NAS、および iSCSI シナリオなどのより複雑なシナリオです。 ただし、一般に、ストレージのギガバイトあたりのコストは多くの場合、IO ごとのコストに直接の正対です。<ul><li>RAID 5 は、Raid 1 よりもギガバイトあたりのコストを削減するが、Raid 1 は IO あたりのコスト削減</li><li>ハード ドライブのスピンドルに基づく、ギガバイトあたりのコスト削減ですが SSDs のある IO あたりのコストを削減</li></ul><li>コンピューターまたは Active Directory Domain Services のサービスの再起動後に、Extensible Storage Engine (ESE) キャッシュが空、パフォーマンスは、キャッシュのウォーム中にバインドされているディスクになります。</li><li>ほとんどの環境では、AD が否定のキャッシュの利点は、多くのディスクへのランダムなパターンに処理を要する I/O の読み取りし、最適化戦略を読み取る。  さらに、AD は、ほとんどの記憶域システムのキャッシュよりも大きい方法キャッシュ メモリ内が。</li></ul>
|RAM|<ul><li>データベース サイズ</li><li>基本のオペレーティング システムの推奨事項</li><li>サード パーティ製のアプリケーション</li></ul>|<ul><li>ストレージは、コンピューターで最も低速なコンポーネントです。 ディスクに移動する必要が少なくよりを RAM にできます。</li><li>エージェント (ウイルス対策、バックアップ、監視)、オペレーティング システムを格納するための十分な RAM が割り当てられていることを確認 NTDS データベースと時間の経過と共に増大します。</li><li>環境が RAM の量を最大化ではない (DIT が大きすぎます) コスト (サテライト オフィス) などに効果的なまたは実現できないことも、その記憶域を確実に [ストレージ] セクションが適切にサイズ設定の参照。</li></ul>|
|ネットワーク|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>一般に、ここまでの DC から送信されるトラフィックは、DC に送信されるトラフィックを超えています。</li><li>スイッチのイーサネット接続は、全二重で受信および送信ネットワーク トラフィックは個別に規模する必要があります。</li><li>数を統合する Dc の各ドメイン コント ローラーのクライアント要求への応答を送信するために使用する帯域幅の容量が増えますが、サイト全体の線形に近づいた。</li><li>サテライトの場所の Dc を削除する場合は、ハブ Dc にサテライト DC の帯域幅を追加するだけでなくになりますが WAN トラフィック量を評価するを使用してください。</li></ul>|
|CPU“Logical Disk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read”descripti"Process(lsass)\\' Processor Time"tors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>ボトルネックとして記憶域を削除した後、必要なコンピューティング能力の量に対処します。</li><li>中に完全に線形ではなく、(サイト) など、特定のスコープ内のすべてのサーバー間で使用されるプロセッサ コアの数がプロセッサの数が合計クライアントの負荷をサポートするために必要な測定に使用できます。 スコープ内のすべてのシステムでサービスの現在のレベルを維持するために必要な最低を追加します。</li><li>プロセッサ速度、電源管理などの変更の関連する変更、現在の環境から派生した影響番号。 一般に、3 GHz プロセッサに 2.5 GHz のプロセッサからの移動が必要な Cpu の数を軽減する方法を正確に評価することはできません。</li></ul>|
|NetLogon|<ul><li>“Netlogon(\*)\Semaphore Acquires”</li><li>“Netlogon(\*)\Semaphore Timeouts”</li><li>“Netlogon(\*)\Average Semaphore Hold Time”</li></ul>|<ul><li>Net Logon のセキュリティで保護されたチャネル/MaxConcurrentAPI には、NTLM 認証や PAC 検証環境のみに影響します。 PAC 検証が Windows Server 2008 より前に、のオペレーティング システムのバージョンで既定でオンにします。 これは、すべてのクライアント システムでこれが無効になるまで、Dc を受けるために設定すると、クライアントです。</li><li>重要な相互の信頼の認証は、フォレスト内の信頼関係が含まれている環境大きいリスクがあるない場合は適切なサイズします。</li><li>サーバーの統合には、間に信頼された認証の同時実行性が向上します。</li><li>急増は、新しいクラスター ノードに、ユーザーを一括再認証、クラスターのフェイル オーバーなど、対応する必要があります。</li><li>(クラスター) などの個々 のクライアント システムでは、チューニングすぎる必要があります。</li></ul>|

## <a name="planning"></a>計画

長時間、AD DS のサイズ調整のコミュニティの推奨するようにしています「、データベースのサイズとして RAM に配置します」 ほとんどの場合、推奨事項がほとんどすべての環境について心配する必要。 AD DS 環境自体は、1999 年以来、非常に大きないるエコシステムの AD DS を使用します。 コンピューティング能力と x86 からスイッチの増加をアーキテクチャには、多数の物理ハードウェアを仮想化の増加を AD DS を実行するお客様に関係のないパフォーマンスがサイズ変更の微妙な側面が行われて x64 のアーキテクチャも前に多くのユーザーにチューニングの問題を再現します。

次のガイダンスを特定し、物理、仮想/物理ミックスでは、または純粋仮想化されたシナリオでデプロイされたかどうかに関係なくサービスとしては、Active Directory の要件を計画する方法の詳細についてはこのため。 そのため、私たちが分割される 4 つの主要なコンポーネントのそれぞれに評価: ストレージ、メモリ、ネットワーク、およびプロセッサ。 つまり、AD DS でのパフォーマンスを最大化するためには、バインド可能なプロセッサの近くに取得するに目標です。

## <a name="ram"></a>RAM

キャッシュして、RAM より簡単に、少なくなり、必要があるディスクに移動します。 RAM の最小量をサーバーのスケーラビリティを最大化には、現在のデータベースのサイズ、SYSVOL の合計サイズ、オペレーティング システムの合計推奨金額をおよびエージェント (ウイルス対策、監視、バックアップ、およびなどのベンダーの推奨事項). サーバーの有効期間にわたって成長に対応する追加の容量を追加する必要があります。 これになります主観的な環境の環境の変化に基づくデータベース サイズの増加の推定に基づいています。

環境が RAM の量を最大化ではない (DIT が大きすぎます) コスト (サテライト オフィス) などに効果的であったり、不可能で参照して、その記憶域ストレージ セクションが適切に設計されています。

メモリのサイズを決定する一般的なコンテキストで表示される結果は、ページファイルのサイズ変更します。 他のすべてと同じコンテキストでメモリ関連、目標は、大幅に速度が低下のディスク移動を最小限に抑えることです。 そのため、質問する必要がありますから移動する、「どのようにページ ファイル サイズを変更するか。」 「RAM の量はページングを最小限に抑える必要でしょうか」。 後者の質問に対する回答は、このセクションの残りの部分に記載されています。 これにより、ほとんどの一般的なオペレーティング システムの推奨事項とメモリ ダンプは、AD DS のパフォーマンスとは無関係のシステムを構成する必要がある領域に、ページファイルのサイズ調整のディスカッションのできます。

### <a name="evaluating"></a>評価します。

ドメイン コント ローラー (DC) が必要な RAM の容量が、これらの理由から、複雑な作業では実際には。

- LSASS は除去メモリの負荷条件下で、必要性を人為的に縮小された RAM の量を計測する既存のシステムを使用するときのエラーの可能性が高くが必要です。
- 個々 の DC のみ必要があることをクライアントに「興味深い」キャッシュの主観的なファクト。 これは、Exchange サーバーのみを使用して、サイトの DC にキャッシュする必要があるデータを非常に異なるのみユーザーを認証する DC にキャッシュする必要があるデータになることを意味します。
- 個別に各 DC の RAM を評価する労働力は桁違いし、環境の変更に応じて変更します。
- 推奨事項の背後にある条件は、情報に基づいた意思に役立ちます。 
- RAM にキャッシュするほど、ディスクに移動する必要が少なくなり、します。 
- ストレージは、コンピューターの最も低速なコンポーネントでは圧倒的です。 アクセス スピンドル ベースのデータを SSD 記憶域メディアは、RAM 内のデータへのアクセスよりも低速 x 1,000,000 順序。

そのため、RAM の最小量、サーバーのスケーラビリティを最大化するために、現在のデータベースのサイズ、SYSVOL の合計サイズ、オペレーティング システムの合計をお勧め金額、およびエージェント (ウイルス対策、監視、バックアップ、ベンダーの推奨事項同様に続きます)。 サーバーの有効期間にわたって成長に対応する追加の金額を追加します。 これは主観的な環境に基づいてされますデータベース サイズの増加の見積もり。 ただし、少数のエンド ユーザーとサテライトの場所、これらの要件を緩和できるこれらのサイトいない必要になるためキャッシュに多くの要求のほとんどのサービスを提供します。

環境が RAM の量を最大化ではない (DIT が大きすぎます) コスト (サテライト オフィス) などに効果的なまたは実現できないことも、その記憶域を確実に [ストレージ] セクションが適切にサイズ設定の参照。

> [!NOTE]
> メモリのサイズ変更中に生じた結果は、ページファイルのサイズ変更します。 質問が「どのようにページ ファイル サイズを変更するか。」から、目標が速度が遅くなるディスクで、大幅に移動を最小限に抑えるため、 「RAM の量はページングを最小限に抑える必要でしょうか」。 後者の質問に対する回答は、このセクションの残りの部分に記載されています。 これにより、ほとんどの一般的なオペレーティング システムの推奨事項とメモリ ダンプは、AD DS のパフォーマンスとは無関係のシステムを構成する必要がある領域に、ページファイルのサイズ調整のディスカッションのできます。

### <a name="virtualization-considerations-for-ram"></a>RAM の仮想化に関する考慮事項

ホストでメモリの過剰コミットしないでください。 RAM の容量の最適化の背後にある基本的な目的は、ディスクに費やされた時間数を最小限に抑えるです。 仮想化では、メモリの過剰コミットの概念をゲストに多くの RAM が割り当てられた場所が存在するを使用し、物理マシン上に存在します。 これで、それ自体の問題には。 すべてのゲストで使用中メモリの合計が、ホスト上の RAM の容量を超えていて、基になるホストがページングを始めたときに問題になります。 パフォーマンスがディスクにバインドされて場合、ドメイン コント ローラーは、データを取得する NTDS.dit しようとしてまたはドメイン コント ローラーがデータを取得するには、ページファイルを移動またはホストがゲストでは、RAM と思われるデータを取得するディスクに移動します。

### <a name="calculation-summary-example"></a>計算の概要の例

|コンポーネント|推定メモリ (例)|
|-|-|
|基本オペレーティング システム (Windows Server 2008) の RAM をお勧めします|2 GB|
|LSASS 内部タスク|200 MB|
|監視エージェント|100 MB|
|ウイルス対策|100 MB|
|データベース (グローバル カタログ)|8.5 GB は確認してください。|
|バックアップを実行、影響を与えずにログオンする管理者のクッション|1 GB|
|Total|12 GB|

**お勧めします。16 GB**

時間の経過と共にことを前提にできることより多くのデータがデータベースに追加され、3 ~ 5 年間運用環境で、サーバーになります。 33% の成長の推定値に基づいて、16 GB は一定の RAM、物理サーバーに配置します。 仮想マシンでは、簡単にする設定を変更できるし、VM に RAM を追加することができますを監視し、将来のアップグレード プランで 12 GB からは妥当です。

## <a name="network"></a>ネットワーク

### <a name="evaluating"></a>評価します。
このセクションでは、WAN を経由するトラフィックにフォーカスがあるし、十分に記載するレプリケーション トラフィックに関するニーズを評価するにはあまり[Active Directory のレプリケーション トラフィック](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10))合計の評価に関するよりも、帯域幅およびネットワーク容量が必要に応じて、クライアントのクエリや、グループ ポリシーのアプリケーションを含むです。 これを既存の環境のパフォーマンス カウンターを使用して収集できます"ネットワーク インターフェイス (\*) \Bytes received/sec は、"と"ネットワーク インターフェイス (\*) \Bytes sent/sec"。 15、30、または 60 分間のネットワーク インターフェイスのカウンターのサンプリング間隔。 何も以下は、一般に適切な測定値; のすぎる揮発性毎日のピークを過度に滑らかも長くは。

> [!NOTE]
> 一般に、DC 上のネットワーク トラフィックの大部分は、DC がクライアントのクエリに応答するよう送信です。 これも受信トラフィックの各環境を評価することをお勧めしている場合、送信トラフィックがフォーカスされた状態の理由です。 解決し、受信ネットワーク トラフィックの要件を確認すると同じアプローチを使用できます。 詳細については、技術情報の記事を参照してください。 [929851。Windows Vista および Windows Server 2008 TCP/IP の既定の動的なポート範囲が変更された](http://support.microsoft.com/kb/929851)します。

### <a name="bandwidth-needs"></a>帯域幅をニーズします。

2 つのカテゴリ ネットワーク スケーラビリティの計画: トラフィックの量と、CPU、ネットワーク トラフィックからロードします。 これらの各シナリオは、この記事では、他のトピックの一部を比較簡単です。

トラフィックの量をサポートする必要がありますを評価するには、2 つの一意のネットワーク トラフィックの観点から AD DS の容量計画のカテゴリがあります。 1 つは、ドメイン コント ローラー間を走査し、参照で徹底的に説明されているレプリケーション トラフィック[Active Directory のレプリケーション トラフィック](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10))は AD DS の現在のバージョンにも関連するとします。 2 番目のサイト内のクライアントからサーバーへのトラフィックです。 サイト内のトラフィックの大部分を計画する簡単なシナリオの 1 つは、基準がクライアントに送信されるデータの大量のクライアントから小さな要求を受信します。 100 MB は、サイト内のサーバーごとに 5,000 ユーザーまでの環境で適切なは、一般にします。 1 GB ネットワーク アダプターと Receive Side Scaling (RSS) を使用してサポートが 5,000 人のユーザーの上のすべてのものを推奨します。 サーバーの統合シナリオの場合は特に、このシナリオを検証するために見てネットワーク インターフェイス (\*) \Bytes/sec サイトでは、すべての Dc 間で同時に、追加し、ことを確認して、ドメイン コント ローラーのターゲット数で除算十分な容量です。 これを行う最も簡単な方法は、Windows 信頼性およびパフォーマンス モニター (旧称パフォーマンス モニター) ではすべてのカウンターを確認します「積み上げ面」ビューを使用するには、同じをスケールします。

次の例を検討してください (とも呼ばれる、実際には、一般的な規則が特定の環境に該当することを検証する方法を非常に複雑な)。 次の仮定が行われます。

- 目標は、できるだけ少ないサーバーに、フット プリントを削減します。 理想的には、負荷がかかるは 1 つのサーバーと、冗長性のため、追加のサーバーが展開されている (*N* + 1 のシナリオ)。 
- このシナリオで、現在のネットワーク アダプターは 100 MB のみをサポートしているし、スイッチの環境では。  
  ターゲットの最大ネットワーク帯域幅使用率は、N シナリオ (DC の損失) では 60% です。
- 各サーバーには約 10,000 のクライアントが接続しています。

グラフ内のデータから得た知識 (ネットワーク インターフェイス (\*) \Bytes sent/sec)。

1. 営業時間は、午後 7時 00分を約 5時 30分と風のランプを開始します。
1. ピーク時の最もビジー期間: 15 AM、8 以上の 25 送信バイト数/秒は最もビジーな DC では 8時 00分 AM からです。  
   > [!NOTE]
   > すべてのパフォーマンス データは履歴です。 したがって 8時 15分にピーク時のデータ ポイントでは、8時 15分に 8時 00分からの負荷を示します。
1. 4時 00分 AM, 20 送信バイト数/秒、最もよく利用される dc の場合よりも多いで異なるタイム ゾーンのいずれかの負荷を示す可能性があります、またはバック グラウンドのバックアップなどのインフラストラクチャのアクティビティの前に、スパイクがあります。 午前 8 時、ピーク時では、このアクティビティを超えているために、関連はありません。
1. サイトには、5 つのドメイン コント ローラーがあります。
1. 最大の負荷は、DC で、100 MB の接続の 44% を表すあたり約 5.5 MB/秒です。 このデータを使用して、その推定できる 8時 00分 AM と 8時 15分 AM の間に必要な帯域幅の合計が 28 MB/秒であります。
   >[!NOTE]
   >バイトにネットワーク インターフェイスの送信/受信カウンターがあり、ネットワーク帯域幅はビット単位で測定することに注意します。 100 MB &divide; 8 = 12.5 MB、1 GB &divide; 8 = 128 MB です。
  
まとめ:

1. この現在の環境では、ターゲット使用率が 60% で、フォールト トレランスの N + 1 レベルを満たしています。 約 5.5 MB/秒 (44%) からサーバーごとの帯域幅をシフトが 1 つのシステムをオフラインにします。約 7 MB/秒 (56%)。
1. ターゲットの最大使用率と理論上は 100 MB の接続の考えられる使用率を超えるこの両方を 1 つのサーバーを統合する前に説明した目標に基づいて。
1. 1 GB 接続で、この合計容量の 22% を表します。
1. 通常の運用状況で、 *N* + 1 のシナリオでは、クライアントの負荷をサーバーまたは 11% の合計容量あたり約 14 MB/秒で比較的均等に分散されます。
1. DC の障害時に容量が十分なは、通常の運用ターゲット サーバーごとに約 30 なります % とネットワーク使用率またはサーバーあたり 38 MB/秒です。 フェールオーバー ターゲットは、ネットワーク使用率が 60% またはサーバーあたり 72 MB/秒になります。  
  
つまり、システムの最終的な配置を使用して、1 GB ネットワーク アダプターがありますと負荷をサポートするネットワーク インフラストラクチャに接続します。 さらに注意は、生成されるネットワーク トラフィックの量を指定するには、ネットワーク通信から、CPU に対する負荷できます大きな影響を与える AD DS の最大限のスケーラビリティの制限です。 この同じプロセスは、DC への受信通信の量を推定できます。 学術的な問題のほとんどの環境基準の受信トラフィックと送信トラフィックの線を指定するには、です。 RSS のハードウェアのサポートを確保することは、サーバーあたり 5,000 人のユーザーよりも大きい環境で重要です。 ネットワーク トラフィックの負荷の高いシナリオでは、割り込み負荷の分散は、ボトルネックになることです。 プロセッサによって検出できます (\*)\%割り込み時間の Cpu 間で均等に分散します。 RSS には、Nic が有効になっているこの制限の緩和し、スケーラビリティを向上させることができます。

> [!NOTE]
> データ センターに統合する場合に必要な追加の容量を見積もるに同様のアプローチを使用できるまたはサテライトの場所にドメイン コント ローラーをインベントリから削除します。 単にクライアントに送信および受信トラフィックを収集し、WAN リンク上に存在するようになりましたトラフィックの量が大きくなります。  
>  
> 場合によっては、トラフィックが遅くなりますが、WAN 上の厳しいタイムアウト時間を満たすために証明書の確認に失敗するとなどのために予想よりも多くのトラフィックが発生する可能性があります。 このため、WAN のサイズと使用率が、反復的な継続的なプロセスをする必要があります。

### <a name="virtualization-considerations-for-network-bandwidth"></a>ネットワーク帯域幅の仮想化に関する考慮事項

物理サーバーの推奨事項に簡単ですから。1 GB の 5000 人のユーザーよりも大きい値をサポートするサーバーです。 複数のゲストが仮想スイッチの基になるインフラストラクチャの共有を開始後、特別な注意はホストが、システム上のすべてのゲストをサポートするために十分なネットワーク帯域幅がその他の厳密さが必要であることを確認する必要があります。 これは、ホスト マシンにネットワーク インフラストラクチャを確保する拡張機能にすぎません。 これは、ネットワーク、仮想スイッチを経由するネットワーク トラフィックがホスト上で仮想マシンのゲストとして実行するドメイン コント ローラーを含むかどうか、または物理スイッチに直接接続されているかどうかに関係なく。 仮想スイッチは、アップリンクが送信されるデータの量をサポートする必要がある 1 つだけの複数コンポーネントです。 したがって、スイッチにリンクされている物理ホストの物理ネットワーク アダプターは、DC の負荷のほか、物理ネットワーク アダプターに接続されている仮想スイッチを共有する他のすべてのゲストをサポートできる必要があります。

### <a name="calculation-summary-example"></a>計算の概要の例

|System|ピーク時の帯域幅|
|-|-|
DC 1|6.5 MB/秒|
DC 2|6.25 MB/秒|
|DC 3|6.25 MB/秒|
|DC 4|5.75 MB/秒|
|DC 5|4.75 MB/秒|
|Total|28.5 MB/秒|

**お勧めします。MB/秒の 72** (28.5 MB/秒が 40% で除算)

|ターゲット システムの数|帯域幅の合計 (上から)|
|-|-|
|2|28.5 MB/秒|
|結果として得られる通常の動作|28.5 &divide; 2 = 14.25 MB/秒|

いつものように時間の経過と共に、想定できるクライアントの負荷が増加して、この成長をできるだけ最適に計画する必要があります。 推奨される量の計画には、ネットワーク トラフィックの 50% の予測成長のによりできます。

## <a name="storage"></a>ストレージ

2 つのコンポーネントを構成する記憶域を計画します。

- 容量、または記憶域のサイズ
- パフォーマンス

大量の時間とドキュメントは、計画の容量、パフォーマンスは多くの場合、完全に見落としてを離れることに費やされました。 ほとんどの環境がないには、現行のハードウェアのコスト、大きな問題では実際には、および"、データベースのサイズとして RAM で put"を推奨されるのに十分なこれらのいずれかが通常では以降では、サテライト オフィスに過剰な処理はありますより大きな環境。

### <a name="sizing"></a>サイズ変更

#### <a name="evaluating-for-storage"></a>記憶域用の評価

13 年前と Active Directory が導入された、最も一般的なドライブのサイズが 4 GB と 9 GB のドライブ時間と比較して、Active Directory のサイズが均等でないすべての考慮事項が、大規模な環境です。 最小使用可能なハード ドライブに 180 GB の範囲、オペレーティング システム全体、SYSVOL、および NTDS.dit のサイズは 1 つのドライブに適合簡単にできます。 そのため、この分野に多額の投資を廃止することをお勧めします。

考慮事項の唯一の推奨事項では、NTDS.dit サイズの 110% が最適化を有効にするために使用できることを確認します。 さらに、ハードウェアの有効期間にわたって成長に対応する必要がありますを作成する必要があります。

最初、最も重要な考慮事項がどのくらい NTDS.dit を評価して、SYSVOL になります。 これらの測定値は、サイズ変更両方固定ディスクとメモリの割り当てになります。 (比較的) 低コストのこれらのコンポーネント、により、数値演算が厳格かつ正確にする必要はありません。 コンテンツの既存および新規の両方の環境では、これを評価する方法について、[データ ストレージ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10))一連の記事。 具体的には、次の記事を参照してください。

- **既存の環境の&ndash;**  、記事「最適化によって解放されるディスク領域のログ記録をアクティブ化"するには"セクション[記憶域の上限](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))します。
- **新しい環境の&ndash;** 記事[Active Directory ユーザーと組織単位に対する拡張推定](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10))します。

  > [!NOTE]
  > 記事は、Windows 2000 Active Directory のリリースの時点で行われたデータ サイズの推定値に基づいています。 環境内でオブジェクトの実際のサイズを反映するオブジェクトのサイズを使用します。

既存の環境に複数のドメインを確認する際にデータベースのサイズのバリエーションである可能性があります。 True の場合は、グローバル カタログ (GC) 最小と非 GC のサイズを使用します。  

データベースのサイズは、オペレーティング システムのバージョンによって異なります。 Dc を Windows Server 2003 は、DC など Windows Server 2008 R2 以降のオペレーティング システムを実行するよりも小さいデータベース サイズなど、以前のオペレーティング システムを実行、特に機能などの Active Directory のごみ箱または資格情報の移動が有効になります。

> [!NOTE]  
  >
>- 新しい環境には、Active Directory ユーザーと組織単位の推定値の増加の推定値が (同じドメイン) で 100,000 人のユーザーが約 450 MB の領域を消費することを示すことに注意してください。 属性が設定された合計量に大きな影響を与えますことに注意してください。 属性は、サード パーティと Microsoft Exchange Server、Lync などのマイクロソフト製品の両方で、多くのオブジェクトに設定されます。 環境では、製品のポートフォリオに基づく評価をお勧め数学アウトの詳細を示すと、すべての正確な見積もりが、大規模な環境のテストの演習いないかもしれません実際には多大な時間と労力の価値です。
>- オフラインを有効にするために空き領域として使用可能なサイズは、NTDS.dit の 110% がデフラグ、および、3 ~ 5 年のハードウェアの寿命経由での成長に対応計画を確認してください。 どの安価なストレージは、300% の記憶域の割り当ては増加との潜在的な必要性をオフラインに対応するために安全では、最適化、DIT のサイズのストレージを推定します。

#### <a name="virtualization-considerations-for-storage"></a>記憶域の仮想化に関する考慮事項

1 つのボリュームに複数の仮想ハード_ディスク (VHD) ファイルが割り当てられている場所のシナリオでは、固定の使用は予約十分な空き領域があることを確認する、DIT のサイズ 210% (DIT + 110% の空き領域の 100%) 以上のディスクをサイズしました。  

#### <a name="calculation-summary-example"></a>計算の概要の例

|評価フェーズから収集されたデータ| |
|-|-|
|NTDS.dit サイズ|送信 35 GB|
|オフラインの許可する修飾子を最適化します。|2.1|
|必要な合計ストレージ|73.5 GB|

> [!NOTE]
> 必要に応じてこのストレージは、SYSVOL、オペレーティング システム、ページのファイル、一時ファイル、(インストーラー ファイルなど)、ローカルのキャッシュされたデータおよびアプリケーションに必要なストレージに加えします。

### <a name="storage-performance"></a>記憶域のパフォーマンス

#### <a name="evaluating-performance-of-storage"></a>記憶域のパフォーマンスを評価します。

内の任意のコンピューターで、最も低速なコンポーネントとして記憶域はクライアントのエクスペリエンスに大きな悪影響があります。 ような大規模な環境で十分な対象の RAM サイズの推奨事項をどれもからはパフォーマンスの記憶域の計画の結果は計り知れません。  また、複雑さとさまざまなストレージ テクノロジをさらには障害のリスクを増やす有用なシナリオでのベスト プラクティスの個別の物理ディスクで「オペレーティング システム、ログ、およびデータベースを配置」長年にわたるの関連性が限られているためです。  これは、長年にわたるベスト プラクティスは、「ディスク」は、専用のスピンドルは、これには、分離する I/O が許可されていることを想定に基づいているためにです。  この想定してこれを true にするは、導入に伴い必要がなくなります。

- 新しい記憶域の種類と仮想化され、共有記憶域のシナリオ
- 記憶域エリア ネットワーク (SAN) 上のスピンドルを共有
- SAN またはネットワーク接続ストレージに VHD ファイル
- ソリッド ステート ドライブ
- 階層型記憶域アーキテクチャ (つまり SSD 記憶域層キャッシュ大きなスピンドル ベース ストレージ)

入力/出力操作あたりの IOPS (秒) の必要な容量があるし、IOPS が、許容される時間枠内が行われることを確認する基になるストレージ アーキテクチャとデザインに関係なく、すべての記憶域パフォーマンス作業の最終的な目標は、簡単に言えば、します. このセクションでは、記憶域ソリューションを確保するために、基になる記憶域のどのような AD DS 要求が適切に設計を評価する方法について説明します。  今日の記憶域テクノロジのばらつきを指定するには、お勧めに十分な IOPS を確実に記憶域ベンダーと連携します。  ローカルに接続された記憶域でこれらのシナリオでは、従来のローカル ストレージのシナリオを設計する方法の基本については付録 C を参照します。  このプリンシパルより複雑な記憶域階層に通常適用されるバックエンド記憶域ソリューションをサポートしているベンダーと、ダイアログにも役立ちます。

- 広範な利用できるストレージ オプションを指定するには、お勧めハードウェア サポート チームや、特定のソリューションが AD DS のニーズを満たしていることを確認するためにベンダの専門知識を対象にします。 次の番号は、記憶域の専門家に指定する情報です。

データベースが大きすぎてメモリに保持される環境で I/O をサポートする必要がある量を決定するのにパフォーマンス カウンターを使用します。

- 論理ディスク (\*) \Avg Disk Sec/read (d: ドライブに NTDS.dit が格納されている場合など、/ドライブの完全なパスの論理ディスク (d:) \Avg ディスク読み取り秒数になります)
- LogicalDisk(\*)\Avg Disk sec/Write
- LogicalDisk(\*)\Avg Disk sec/Transfer
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

これらは、現在の環境の要求のベンチマークに 15/30/60 分間隔でサンプリングする必要があります。

#### <a name="evaluating-the-results"></a>結果を評価します。

> [!NOTE]
> これは最も厳しいコンポーネントでは通常、データベースからの読み取りにフォーカスがある、論理ディスクを置き換えることにより、ログ ファイルへの書き込みを同じロジックを適用できます ( *\<NTDS ログ\>* ) \Avg Disk Sec/write論理ディスクと ( *\<NTDS ログ\>* ) \Writes/sec)。
>  
> - 論理ディスク ( *\<NTDS\>* ) \Avg ディスク読み取り秒数では、現在のストレージが適切なサイズかどうかを示します。  結果が、ディスクの種類の論理ディスクのディスク アクセス時間にほぼ等しい場合 ( *\<NTDS\>* ) \Reads/sec は有効な測定単位です。  バック エンド、上の記憶域の製造元の仕様が論理ディスクの適切な範囲を確認します ( *\<NTDS\>* ) \Avg Disk Sec/read はほぼ同じでは。
>   - 7200 – 9 を 12.5 ミリ秒 (ms)
>   - 10,000 ~ 6 ~ 10 ミリ秒
>   - 15,000 – 4 ~ 6 ミリ秒  
>   - SSD – 1. ~ 3. ms  
>   - >[!NOTE]
>     >(ソース) に応じて使うを 20 に記憶域のパフォーマンスが低下したことを示す推奨事項が存在します。  上記の値とその他のガイダンスの違いは、上記の値が通常の運用範囲であります。  その他の推奨事項はクライアントのエクスペリエンスが大幅に低下しになるときに識別するためのガイダンスをトラブルシューティングします。  詳細については、付録 C を参照します。
> - 論理ディスク ( *\<NTDS\>* ) \Reads/sec が実行される I/O の量。
>   - 場合の論理ディスク ( *\<NTDS\>* ) は、バックエンド ストレージの論理ディスクの最適な範囲内に \Avg Disk Sec/read ( *\<NTDS\>* ) \Reads/1 秒数は、ストレージのサイズを直接使用できます。
>   - If LogicalDisk( *\<NTDS\>* )\Avg Disk sec/Read is not within the optimal range for the backend storage, additional I/O is needed according to the following formula:
>     > (LogicalDisk( *\<NTDS\>* )\Avg Disk sec/Read) &divide; (Physical Media Disk Access Time) &times; (LogicalDisk( *\<NTDS\>* )\Avg Disk sec/Read)

注意点 :

- ある場合、メモリ量が最適で、サーバーを構成すると、これらの値不正確になります計画のために注意してください。  高側に誤ってなるされ、最悪のシナリオとして引き続き使用できます。
- 追加/最適化する RAM は具体的には読み取り I/O の量の減少をドライブが (LogicalDisk ( *\<NTDS\>* ) \Reads/Sec します。 これは、最初に計算された、堅牢であることに、記憶域ソリューションがないことを意味します。  残念ながら、何もこの一般的なステートメントはクライアントの負荷と一般的なガイダンスには依存環境よりも詳細なは指定できません。  最善の方法では、RAM を最適化した後、ストレージのサイズ変更を調整します。

#### <a name="virtualization-considerations-for-performance"></a>パフォーマンスの仮想化に関する考慮事項

キーをここでは基になる共有インフラストラクチャで DC の負荷をサポートできることと、メディアおよびすべての経路を基になるを使用して、その他のリソースが共有すると同様に、すべての仮想化の前のディスカッション。 これが true かどうか、物理ドメイン コント ローラーは、同じ基になるメディアを共有する SAN、NAS、または iSCSI インフラストラクチャとして他のサーバーまたはアプリケーションでは、SAN、NAS、または iSCSI のインフラストラクチャを共有するアクセスにパススルーを使用してゲストがあるかどうか、メディアを基になるか、ゲストが共有メディアをローカルまたは SAN、NAS、または iSCSI のインフラストラクチャ上に存在する VHD ファイルを使用する場合。 計画の手順は、基になるメディアがすべてのコンシューマーの総負荷をサポートできることを確認します。

また、ゲストの観点から走査する必要があります、追加のコード パスがあるは任意のストレージにアクセスするホストを経由する場合に、パフォーマンスに影響します。 当然ながら、記憶域のパフォーマンス テストを示すことは、ホスト システムのプロセッサ使用率を把握する主観的はスループットに影響を与えます、仮想化 (付録 a: を参照してください。CPU サイズ設定基準)、明らかに、ゲストで要求されたホストのリソースを受けますが、します。 これは、仮想化に関する考慮事項、仮想化されたシナリオでの処理ニーズに貢献 (を参照してください[処理の仮想化に関する考慮事項](#virtualization-considerations-for-processing))。

複雑なため、さまざまな種類のパフォーマンスに及ぼす影響があるすべてを利用できるさまざまなストレージ オプションがあることです。 物理から仮想への移行時に、安全な概算、としては、SCSI アダプタ、または IDE にパススルーの記憶域など、HYPER-V 上の仮想化ゲストのオプションの別のストレージを調整する 1.10 の乗数を使用します。 さまざまなストレージ シナリオの間で転送するときに必要な調整は、記憶域がローカルかどうか、SAN、NAS、または iSCSI かは関係ありません。

#### <a name="calculation-summary-example"></a>計算の概要の例

通常の動作条件下で正常なシステムに必要な I/O の量を決定するには。

- LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec during the peak period 15 minute period 
- 基になるストレージの容量を超えたストレージのために必要な I/O の量を判断するには。
  >*Needed IOPS* = (LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read &divide; *\<Target Avg Disk sec/Read\>* ) &times; LogicalDisk( *\<NTDS Database Drive\>* )\Read/sec

|カウンター|値|
|-|-|
|Actual LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Transfer|.02 秒 (20 ミリ秒)|
|Target LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Transfer|.01 秒|
|使用可能な IO で変更するための乗数|0.02 &divide; 0.01 = 2|  
  
|値の名前|値|
|-|-|
|LogicalDisk( *\<NTDS Database Drive\>* )\Transfers/sec|400|
|使用可能な IO で変更するための乗数|2|
|ピーク期間中に必要な合計の IOPS|800|

する活動をキャッシュが必要な速度を決定します。

- キャッシュの準備の最大許容時間を決定します。 データベース全体をディスクから読み込むことができる時間数または RAM を入力する最大時間なりますシナリオ データベース全体をメモリに読み込むことができません。
- 空白文字を除く、データベースのサイズを決定します。  詳細については、次を参照してください。[ストレージ用の評価](#evaluating-for-storage)します。  
- データベースのサイズを 8 KB で除算します。total Io のデータベースを読み込むために必要になります。
- Total Io を定義されているタイム フレーム内の秒数で除算します。

計算され、中に、精度率がならないように正確な固定キャッシュ サイズ、ESE が構成されていないと、既定では、AD DS は、変数のキャッシュ サイズを使用する場合、以前に読み込まれたページが削除されるため、注意してください。

|データ ポイントを収集するには|値
|-|-|
|ウォームする最大許容時間|10 分 (600 秒)
|データベース サイズ|2 GB|  
  
|計算ステップ|[数式]|結果|
|-|-|-|
|ページ内のデータベースのサイズを計算します。|(2 GB &times; 1024 &times; 1024) = *(KB 単位) のデータベースのサイズ*|2,097, 152 KB|
|データベース内のページ数を計算します。|2,097, 152 KB &divide; 8 KB =*ページの数*|262, 144 ページ|
|完全にキャッシュの準備に必要な IOPS を計算します。|262,144 pages &divide; 600 seconds = *IOPS needed*|437 IOPS|

## <a name="processing"></a>処理

### <a name="evaluating-active-directory-processor-usage"></a>Active Directory のプロセッサ使用率を評価します。

ほとんどの環境では、ストレージ、RAM、およびネットワークの計画」セクションで説明されているようにチューニングが正しく処理能力の量を管理するになりますほとんどの注目すべきコンポーネント。 必要な CPU 容量を評価するのには、2 つの課題があります。

- 環境でアプリケーションの共有サービス インフラストラクチャで適切に動作中かどうかとは、情報の記事の"追跡コストおよび非効率的な検索"というタイトルのセクションで説明を作成するより効率的な Microsoft Activeディレクトリ対応アプリケーションや下位 SAM からの移行は、LDAP の呼び出しを呼び出します。  
  
  大規模な環境でこれが重要な理由は適切にコード化されたアプリケーションできます CPU 負荷の変動をドライブ、他のアプリケーションからの CPU 時間の時間を要するを「スティール」、人為的にドライブの容量のニーズをに対する負荷を均等に分散させるDc です。  
- AD DS は、さまざまな潜在的なクライアントでの分散環境で、「1 つのクライアント」の費用を見積もるは使用パターンと型、または AD DS を利用するアプリケーションの数量が原因環境主観的なものです。 つまり、広範な適用性のためのネットワーク セクションと同様にこれより適切に近づくと、環境で必要な合計容量を評価するの観点から。

既存の環境ではストレージのサイズ変更が、先ほど説明したように、前提条件が適用にプロセッサの負荷に関するデータが有効ではそのため、記憶域が適切にサイズ設定ようになりました。 繰り返しますが、システムのボトルネックが、記憶域のパフォーマンスではないことを確実に重要です。 ボトルネックが存在するし、プロセッサが待機している、解消されますが削除されるとボトルネックになっているアイドル状態があります。  定義上、プロセッサの待機状態が解除されると、データでの待機があるなくなったので、CPU 使用率が増加します。 そのため、パフォーマンス カウンターを収集"論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg Disk Sec/read"と"Process(lsass)\\% Processor Time"。 内のデータ"Process(lsass)\\% Processor Time"人工的な少なくなる場合"論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg Disk Sec/read"一般的なしきい値は、10 ~ 15 ミリ秒を超えていますがMicrosoft サポートは、ストレージ関連のパフォーマンスに関する問題のトラブルシューティングに使用します。 同様に、サンプルの間隔が 15、30、または 60 分間にあることをお勧めします。 何も以下は、一般に適切な測定値; のすぎる揮発性毎日のピークを過度に滑らかも長くは。

### <a name="introduction"></a>概要

ドメイン コント ローラーのキャパシティ プランニングを計画するには、処理能力、最も注意と理解が必要です。 ボトルネックであるコンポーネントは常に最大のパフォーマンスを確保するシステムのサイズ変更、および適切なサイズのドメイン コント ローラーで、プロセッサになります。

サイト間接続ごとに、環境の要求を確認する場所のネットワーク セクションと同様に、同じ行う必要がある要求されたコンピューティング能力の。 場所、利用可能なネットワーク テクノロジは、通常のオンデマンドをはるかに超えて、[ネットワーク] セクションとは異なり CPU 容量のサイズを設定する詳細について注意してください。  任意の環境でも中程度のサイズのとしてCPU のいくつか数千の同時実行ユーザーより大きな負荷を配置できます。

残念ながら、AD を利用するクライアント アプリケーションの大きな可変性により CPU あたりのユーザーの一般的な概算ひどく適用可能でないすべての環境にします。 具体的には、コンピューティングの需要は、ユーザーの動作とアプリケーションのプロファイルが適用されます。 そのため、各環境を個別にサイズを設定する必要があります。

#### <a name="target-site-behavior-profile"></a>ターゲット サイトの動作のプロファイル

使用してデザインを対象とする目標は、説明したように、サイト全体の容量を計画するとき、 *N* + 1 容量設計は、ピーク期間中に 1 つのシステムの障害に妥当なサービスの継続を使用すること品質のレベルです。 そのことを意味する"*N*"シナリオでは、すべてのボックス間での負荷は (さらには、80% 未満) 100% 未満をする必要がありますピーク時の期間。

さらに、アプリケーションとサイト内のクライアントには、ドメイン コント ローラーを検索するためのベスト プラクティスを使用する場合 (つまりを使用して、 [DsGetDcName 関数](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx))、クライアントは小さな比較的均等に分散する必要があります任意の数の要素のための一時的なスパイクです。

次の例では、次の仮定が行われます。

- 各サイト内の 5 つの Dc は、Cpu の 4 つがあります。
- ターゲットの業務時間中に CPU 使用率の合計は、通常の動作条件下で 40% ("*N* + 1") とそれ以外の場合の 60% ("*N*")。 非営業時間に、バックアップ ソフトウェアとその他のメンテナンスが使用可能なすべてのリソースを消費する予想されるためはの 80% に対象の CPU 使用率です。

![CPU 使用状況グラフ](media/capacity-planning-considerations-cpu-chart.png)

グラフのデータの分析 (プロセッサ Information(_Total)\%プロセッサ ユーティリティ)、Dc ごと。

- ほとんどの場合、負荷が比較的均等に分散はどのようなクライアントは、DC ロケーターを使用し、検索を正しく書かれているときに予想されます。 
- いくつか大きなとしていくつかの 10% の急増を 5 分間の 20% です。 一般を超えた容量計画のターゲットが発生する場合を除き、これらを調査する必要はありません。  
- すべてのシステムのピーク期間では、約 8時 00分 AM ~ 9時 15分 AM です。 約 5時 00分 AM 約 5時 00分 pm からスムーズな移行、これは、通常のビジネス サイクルを示しています。 容量の懸念事項を計画外のボックスで、シナリオ 5時 00分 PM と午前 4時 00分の間の CPU 使用率よりランダムなスパイクとなります。

  >[!NOTE]
  >適切に管理されたシステムが上述の急増がありますとバックアップ ソフトウェアが実行中、ウイルス対策スキャンの完全なシステム、ハードウェアまたはソフトウェアのインベントリ、ソフトウェアまたは修正プログラムの展開。 ピーク時のユーザーのビジネス サイクル外なったため、ターゲットが超過しません。

- 失敗またはオフラインにする 1 つ、残りのシステムが推定の 53% 実行は各システムが約 40% と、すべてのシステム Cpu の同じ番号を持つ、する必要があります (システム D の 40% の負荷が均等に分割されに追加システム A のおよびシステム C の既存の 40% 負荷)。 線形そうでないはさまざまな理由から、完全に正確ながゲージに十分な精度を提供します。  

  **別のシナリオ –** を 40% で実行されている 2 つのドメイン コント ローラー。1 つのドメイン コント ローラーが失敗した残りの 1 つの推定の CPU を推定の 80% となります。 容量計画の上記で説明したしきい値を超えたし、余裕の 10 ~ 20% は、トラフィックの急増が 90% に設定中に 100%、DC をドライブは、負荷プロファイルでの量が大幅に制限も開始がこれまでに、"*N*"シナリオと応答性を間違いなくが低下します。

### <a name="calculating-cpu-demands"></a>CPU の要求を計算します。

"プロセス\\% プロセッサ時間"パフォーマンス オブジェクト カウンター合計金額の合計時間の CPU に費やすアプリケーションのスレッドのすべてをシステムの合計数で除算の時間を経過します。 このプロパティの効果は、マルチ スレッド アプリケーションのマルチ CPU システムでは、CPU 時間を 100% を超えることができよりも非常に異なる方法で解釈される"プロセッサ情報\\% プロセッサ ユーティリティ"です。 実際には、"Process(lsass)\\% Processor Time"プロセスの要求をサポートするために必要な 100% で実行されている Cpu の数として見なすことができます。 200% の値は、すべての AD DS の読み込みをサポートするために 100%、それぞれ 2 つの Cpu が必要なことを意味します。 100% の容量で実行されている CPU は最もコストの Cpu に費やされるコストの観点から効率とさまざまな理由が記載された付録 A には、マルチ スレッド システムの応答性の向上、電力およびエネルギー消費量は、システムがときに発生します。100% で実行されていません。

クライアントの負荷で一時的なスパイクを対応するために、40% とシステムの容量の 60% の間のピーク期間 CPU を対象とすることをお勧めします。 上記の例を使用ことを意味すること 3.33 (ターゲットの 60%) と 5 (40% ターゲット) の間の Cpu が必要になります、AD DS (lsass プロセス) の負荷。 基本のオペレーティング システムと (ウイルス対策、バックアップ、監視、およびなど) などに必要なその他のエージェントの必要に応じてで追加の容量を追加してください。 エージェントの影響は、環境ごとに評価される必要がありますが 5% から 1 つの CPU の 10% の見積もりを作成できます。 現在の例では、ある 3.43 (ターゲットの 60%) と 5.1 (40% ターゲット) の間の Cpu が必要なピーク期間中にこれはお勧めします。

これを行う最も簡単な方法は、Windows 信頼性およびパフォーマンス モニター (perfmon) ではすべてのカウンターを確認します「積み上げ面」ビューを使用するには、同じをスケールします。

前提:

- 目標は、できるだけ少ないサーバーにフット プリントを削減します。 1 つのサーバーが、ロード テストと冗長性のために追加された追加のサーバーをどのように実行する理想的には、(*N* + 1 のシナリオ)。

![Lsass プロセス (すべてのプロセッサ) 上のプロセッサ時間のグラフ](media/capacity-planning-considerations-proc-time-chart.png)

グラフ内のデータから得た知識 (Process(lsass)\\% Processor Time)。

- 営業時間は、約 7時 00分の急増を起動し、午後 5時 00分に減少します。
- ピーク時の最もビジー期間は、9時 30分 AM から 11時 00分 AM です。 
  > [!NOTE]
  > すべてのパフォーマンス データは履歴です。 9時 15分にピーク時のデータ ポイントでは、9時 00分から 9時 15分への読み込みを示します。
- 7時 00分 AM ことを示すいずれかの異なるタイム ゾーンからの読み込みまたはバックアップなどのバック グラウンド インフラストラクチャ アクティビティの前に、スパイクがあります。 午前 9 時 30 分のピーク時では、このアクティビティを超えているために、関連はありません。
- サイトには、次の 3 つのドメイン コント ローラーがあります。

最大の負荷では、lsass は、1 つの CPU、または 100% で実行されている 4.85 の Cpu の約 485% を消費します。 数学に従って以前では、つまりサイトは、AD DS の約 12.25 Cpu を必要があります。 上記の推奨事項の 5 ~ 10% のバック グラウンド プロセスに追加し、つまり、同じ負荷をサポートする約 12.30 に 12.35 Cpu サーバーを今すぐに置き換える必要があります。 成長を今すぐの環境の見積もりで考慮する必要があります。

### <a name="when-to-tune-ldap-weights"></a>LDAP の重みを調整するタイミング

いくつかのシナリオでチューニング[LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10))見なす必要があります。 容量計画のコンテキスト内ではこれアプリケーションまたはユーザーの負荷が均等に分散されない、または機能の観点から、基になるシステムが均等に分散されないときにします。 容量計画を超えるようにする理由では、この記事の範囲外です。

LDAP の重みを調整する 2 つの一般的な理由があります。

- PDC エミュレーターは、どのユーザーまたはアプリケーションの読み込み時の動作が均等に分散されていないすべての環境に影響する例を示します。 特定のツールとアクションは、グループ ポリシー管理ツール、認証エラー、信頼を確立しての場合は 2 つ目の試行など、PDC エミュレーターをターゲットとしては、PDC エミュレーターでの CPU リソースが他の場所より高い要求された可能性があります。サイトです。
  - のみの負荷をより均等に分散により、PDC エミュレーターの負荷を軽減し、その他のドメイン コント ローラーの負荷を増やすために CPU 使用率によって顕著な相違がある場合は、これをチューニングすると便利です。
  - この場合、PDC エミュレーターの 50 ~ 75 LDAPSrvWeight を設定します。
- Cpu (および速度)、サイト内の異なる数のサーバー。  たとえば、2 つの 8 コア サーバーと 1 つの 4 つのコア サーバーがあるとします。  最後のサーバーには、その他の 2 つのサーバーの半分のプロセッサがあります。  これは、8 コアのボックスの約 2 倍の 4 つのコアでの平均 CPU 負荷を分散ものクライアントの負荷が増加することを意味します。
  - たとえば、40% の 2 つの 8 コア ボックスが実行するし、4 コアのボックスは、80% で実行が。
  - また、4 つのコアのボックスは今すぐオーバー ロードはことファクト具体的には、このシナリオでは、1 つの 8 コア ボックスの損失による影響を検討してください。

#### <a name="example-1---pdc"></a>例 1: PDC

| |既定値を持つ使用率|新しい LdapSrvWeight|新しい使用率の見積もり|
|-|-|-|-|
|DC 1 (PDC エミュレーター)|53%|57|40%|
|DC 2|33%|100|40%|
|DC 3|33%|100|40%|

ここで問題は、PDC エミュレーターの役割を転送または強制して、サイト内の別のドメイン コント ローラーに特に場合がある新しい PDC エミュレーターの劇的に増加します。

セクションの例を使用して[ターゲット サイトの動作のプロファイル](#target-site-behavior-profile)の前提条件が適用されます、サイト内のすべての 3 つのドメイン コント ローラーが 4 基の Cpu を持っています。 場合の動作を通常の状況では、8 つの Cpu がある 1 つのドメイン コント ローラーのでしょうか。 使用率が 40% に 2 つのドメイン コント ローラーとその使用率が 20% に 1 つがあります。 不良が、もう少し向上の負荷を分散する機会がありません。 これを実現する LDAP 重みを活用します。  シナリオの例は次のようになります。

#### <a name="example-2---differing-cpu-counts"></a>例 2: 異なる CPU 数します。

| |プロセッサ情報\\ %&nbsp;プロセッサ Utility(_Total)<br />既定値を持つ使用率|新しい LdapSrvWeight|新しい使用率の見積もり|
|-|-|-|-|
|4-CPU DC 1|40|100|30%|
|4-CPU DC 2|40|100|30%|
|8-CPU DC 3|20|200|30%|

これらのシナリオを十分に注意するただしします。 上記のように、本当にすばらしいと用紙にかなり数学を調べます。 計画、この記事全体では、"*N* + 1" のシナリオにとってきわめて重要です。 すべてのシナリオの 1 つの DC をオフラインに移行の影響を計算する必要があります。 中にロードする負荷分散があっても、60% を保証するためにすぐにこのシナリオでは、"*N*"シナリオでは、すべてのサーバー間で均等に分散する負荷を配布でもかまいません常に比率として。一貫性のあります。 効果は一般的なシナリオでは、チューニング、PDC エミュレーターでどのようなシナリオのユーザーまたはアプリケーションの負荷が不均衡を検索は非常に異なります。

| |チューニングされた使用率|新しい LdapSrvWeight|新しい使用率の見積もり|
|-|-|-|-|
|DC 1 (PDC エミュレーター)|40%|85|47%|
|DC 2|40%|100|53%|
|DC 3|40%|100|53%|

### <a name="virtualization-considerations-for-processing"></a>処理の仮想化に関する考慮事項

これには、仮想化環境で実行する必要がある容量計画の 2 つのレイヤーがあります。 以前は、処理ドメイン コント ローラーの説明、ビジネス サイクルの id と同様に、ホスト レベルでは、ピーク期間中にしきい値を識別する必要があります。 基になるプリンシパルが、CPU、物理マシン上で AD DS のスレッドを取得すると、CPU 上でゲスト スレッドのスケジューリングのホスト コンピューターで同じであるために、同じ目的が 40 ~ 60%、基になるホスト上がお勧めします。 次のレイヤーでは、ゲスト レイヤーでは、スレッドのスケジューリングのプリンシパルから変更されていません、40 ~ 60% の範囲内で、ゲストは内での目標。

直接マップされた場合、ホストごとに、1 つのゲスト、容量計画はすべてこのポイントを基になるホスト オペレーティング システムの要件 (RAM、ディスク、ネットワーク) に追加する必要があります。 共有ホストのシナリオでのテストは、基になるプロセッサの効率性に 10% の影響があることを示します。 つまり、サイトに 40%、仮想 Cpu を割り当てるすべての推奨される量の対象に 10 個の Cpu が必要なかどうかは、"*N*"ゲストは 11 になります。 サイトでの物理サーバーと仮想サーバーの混在の配布、修飾子は、Vm にのみ適用されます。 たとえば、サイトの場合、"*N* + 1" シナリオでは、10 個の Cpu を持つ 1 つのまたは直接マップされた物理サーバーはドメイン コント ローラー用に予約 11 cpu を搭載したホストでは、11 の Cpu を持つ 1 つのゲストと等価の。

分析と必要な CPU 量の計算全体で AD DS の負荷をサポートする用語の物理ハードウェアで何を購入することができますにマップする Cpu の数とは限りませんマップされないクリーンに。 仮想化に切り上げる必要はありません。 仮想化が CPU を VM に追加できる簡単に指定されたサイトにコンピューティング容量を追加するために必要な労力が減少します。 いない Cpu の追加は、ゲストに追加する必要がある場合は、基になるハードウェアを利用できるように必要なコンピューティング能力を正確に評価する必要があります。  いつものように計画や需要の増大の監視に注意してください。

### <a name="calculation-summary-example"></a>計算の概要の例

|System|ピーク時の CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|合計 CPU の使用|485%|  
  
|ターゲット システムの数|帯域幅の合計 (上から)|
|-|-|
|40% のターゲットで必要な Cpu|4.85 &divide; .4 = 12.25|

この時点での重要性のために繰り返し*成長を計画する*します。 次の 3 つの長年にわたって 50% の成長と仮定するとこの環境は 18.375 Cpu を必要があります (12.25 &times; 1.5) 3 年間のマークでします。 代替のプランは、最初の年後に確認し、必要に応じて、追加の容量に追加することです。

### <a name="cross-trust-client-authentication-load-for-ntlm"></a>NTLM の間に信頼されたクライアント認証の負荷

#### <a name="evaluating-cross-trust-client-authentication-load"></a>間に信頼されたクライアント認証の負荷を評価します。

多くの環境には、1 つまたは複数のドメインの信頼によって接続されている可能性があります。 Kerberos 認証を使用しない別のドメインの id の認証要求を別のドメイン コント ローラー、宛先ドメインまたはパスの次のドメインのいずれかのドメイン コント ローラーのセキュリティで保護されたチャネルを使用して信頼を走査する必要があります。変換先のドメイン。 ドメイン コント ローラーが信頼されたドメインにドメイン コント ローラーにすることができますをセキュリティで保護されたチャネルを使用して同時呼び出し数と呼ばれる設定によって制御される**MaxConcurrentAPI**します。 ドメイン コント ローラーのセキュリティで保護されたチャネルが負荷の量を処理できるように 2 つの方法のいずれかによって実現されます。 チューニング**MaxConcurrentAPI**またはショートカットの信頼を作成し、フォレスト内で。 個々 の信頼間でトラフィックの量を測定しを参照してください[MaxConcurrentApi の設定を使用して NTLM 認証のパフォーマンスの調整を行う方法](https://support.microsoft.com/kb/2688798)します。

データの収集中に、他のすべてのシナリオと同様する必要があります収集を使用するデータの 1 日のピーク多忙な期間中です。

> [!NOTE]
> フォレストとフォレスト間のシナリオが複数の信頼を走査する認証生じるし、各ステージはチューニングする必要があります。

#### <a name="planning"></a>計画

既定では、NTLM 認証を使用して、または特定の構成のシナリオで使用するアプリケーションを数多くあります。 アプリケーション サーバーでは、容量を増加し、サービスのアクティブなクライアント数が増加します。 クライアントは、期間限定のセッションを開いておくし、(電子メールのプル同期) など、定期的に再接続ではなく傾向もあります。 NTLM の高負荷の別の一般的な例では、インターネットへのアクセスの認証を必要とする web プロキシ サーバーです。

これらのアプリケーションには、NTLM 認証は、ユーザーおよびリソースは別のドメインにある場合は特に、Dc に大きな負荷を配置できる負荷の高い可能性があります。

実際に使用される、排他的ではなく、組み合わせてか、管理の間に信頼された負荷を複数の方法があります/またはシナリオ。 使用できるオプションは次のとおりです。

- 間に信頼されたクライアント認証を削減するには、ユーザーに常駐しているのと同じドメインにユーザーを使用するサービスを検出します。
- セキュリティで保護されたチャネル使用可能な数を増やします。 これはフォレスト内や、フォレスト間のトラフィックに関連する、ショートカットの信頼と呼ばれます。
- 既定の設定を調整**MaxConcurrentAPI**します。

チューニング**MaxConcurrentAPI**式は、既存のサーバー上。

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires* + *semaphore_time-outs*) &times; *average_semaphore_hold_time* &divide; *time_collection_length*

詳細については、次を参照してください。[サポート技術情報記事 2688798。MaxConcurrentApi の設定を使用して NTLM 認証のパフォーマンスの調整を行う方法](http://support.microsoft.com/kb/2688798)します。

## <a name="virtualization-considerations"></a>仮想化に関する考慮事項

なし、これは、オペレーティング システムの設定をチューニングします。

### <a name="calculation-summary-example"></a>計算の概要の例

|データの種類|[値]|
|-|-|
|セマフォの取得 (最小)|6,161|
|セマフォの取得 (最大)|6,762|
|セマフォのタイムアウト|0|
|ホールド時間の平均のセマフォ|0.012|
|コレクションの継続時間 (秒)|1時 11分分 (71 秒)|
|(KB 2688798) からの数式|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|最小値**MaxConcurrentAPI**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

この期間中、このシステムでは、既定値は許容されます。

## <a name="monitoring-for-compliance-with-capacity-planning-goals"></a>容量計画の目標への準拠の監視

この記事では、全体でが取り上げられてきました計画とスケーリングがターゲットの使用率の方向に移動します。 次に、システムが適切な容量のしきい値内で動作することを確認、監視する必要があります推奨されるしきい値の概要グラフに示します。 これらはいないパフォーマンスのしきい値が容量のしきい値を計画することに注意してください。 これらのしきい値を超える場合、運用サーバーでは、機能しますが、開始を検証するすべてのアプリケーションが適切に動作しないこと。 アプリケーションが正常に動作は言うものの場合に、ハードウェアのアップグレードやその他の構成の変更の評価を開始する時間を勧めします。

|Category|パフォーマンス カウンター|サンプリング間隔/|移行先|警告|
|-|-|-|-|-|
|プロセッサ|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 or earlier)|Memory\Available MB|< 100 MB|N/A|< 100 MB|
|RAM (Windows Server 2012)|Memory\Long-Term Average Standby Cache Lifetime(s)|30 min|Must be tested|Must be tested|
|Network|Network Interface(\*)\Bytes Sent/sec<br /><br />Network Interface(\*)\Bytes Received/sec|30 min|40%|60%|
|Storage|LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read<br /><br />LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write|60 min|10 ms|15 ms|
|AD Services|Netlogon(\*)\Average Semaphore Hold Time|60 min|0|1 second|

## Appendix A: CPU sizing criteria

### Definitions

**Processor (microprocessor) –** a component that reads and executes program instructions  

**CPU –** Central Processing Unit  

**Multi-Core processor –** multiple CPUs on the same integrated circuit  

**Multi-CPU –** multiple CPUs, not on the same integrated circuit  

**Logical Processor –** one logical computing engine from the perspective of the operating system  

This includes hyper-threaded, one core on multi-core processor, or a single core processor.  

As today’s server systems have multiple processors, multiple multi-core processors, and hyper-threading, this information is generalized to cover both scenarios. As such, the term logical processor will be used as it represents the operating system and application perspective of the available computing engines.

### Thread-level parallelism

Each thread is an independent task, as each thread has its own stack and instructions. Because AD DS is multi-threaded and the number of available threads can be tuned by using [How to view and set LDAP policy in Active Directory by using Ntdsutil.exe](http://support.microsoft.com/kb/315071), it scales well across multiple logical processors.

### Data-level parallelism

This involves sharing data across multiple threads within one process (in the case of the AD DS process alone) and across multiple threads in multiple processes (in general). With concern to over-simplifying the case, this means that any changes to data are reflected to all running threads in all the various levels of cache (L1, L2, L3) across all cores running said threads as well as updating shared memory. Performance can degrade during write operations while all the various memory locations are brought consistent before instruction processing can continue.

### CPU speed vs. multiple-core considerations

The general rule of thumb is faster logical processors reduce the duration it takes to process a series of instructions, while more logical processors means that more tasks can be run at the same time. These rules of thumb break down as the scenarios become inherently more complex with considerations of fetching data from shared-memory, waiting on data-level parallelism, and the overhead of managing multiple threads. This is also why scalability in multi-core systems is not linear.

Consider the following analogies in these considerations: think of a highway, with each thread being an individual car, each lane being a core, and the speed limit being the clock speed.

1. If there is only one car on the highway, it doesn’t matter if there are two lanes or 12 lanes. That car is only going to go as fast as the speed limit will allow.
1. Assume that the data the thread needs is not immediately available. The analogy would be that a segment of road is shutdown. If there is only one car on the highway, it doesn’t matter what the speed limit is until the lane is reopened (data is fetched from memory).
1. As the number of cars increase, the overhead to manage the number of cars increases. Compare the experience of driving and the amount of attention necessary when the road is practically empty (such as late evening) versus when the traffic is heavy (such as mid-afternoon, but not rush hour). Also, consider the amount of attention necessary when driving on a two-lane highway, where there is only one other lane to worry about what the drivers are doing, versus a six-lane highway where one has to worry about what a lot of other drivers are doing.
   > [!NOTE]
   > The analogy about the rush hour scenario is extended in the next section: Response Time/How the System Busyness Impacts Performance.

As a result, specifics about more or faster processors become highly subjective to application behavior, which in the case of AD DS is very environmentally specific and even varies from server to server within an environment. This is why the references earlier in the article do not invest heavily in being overly precise, and a margin of safety is included in the calculations. When making budget-driven purchasing decisions, it is recommended that optimizing usage of the processors at 40% (or the desired number for the environment) occurs first, before considering buying faster processors. The increased synchronization across more processors reduces the true benefit of more processors from the linear progression (2&times; the number of processors provides less than 2&times; available additional compute power).

> [!NOTE]
> Amdahl’s Law and Gustafson’s Law are the relevant concepts here.

### Response time/How the system busyness impacts performance

Queuing theory is the mathematical study of waiting lines (queues). In queuing theory, the Utilization Law is represented by the equation:

*U* k = *B* &divide; *T*

Where *U* k is the utilization percentage, *B* is the amount of time busy, and *T* is the total time the system was observed. Translated into the context of Windows, this means the number of 100-nanosecond (ns) interval threads that are in a Running state divided by how many 100-ns intervals were available in given time interval. This is exactly the formula for calculating % Processor Utility (reference [Processor Object](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10)) and [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10))).

Queuing theory also provides the formula: *N* = *U* k &divide; (1 &ndash; *U* k) to estimate the number of waiting items based on utilization ( *N* is the length of the queue). Charting this over all utilization intervals provides the following estimates to how long the queue to get on the processor is at any given CPU load.

![Queue length](media/capacity-planning-considerations-queue-length.png)

It is observed that after 50% CPU load, on average there is always a wait of one other item in the queue, with a noticeably rapid increase after about 70% CPU utilization.

Returning to the driving analogy used earlier in this section:

- The busy times of “mid-afternoon” would, hypothetically, fall somewhere into the 40% to 70% range. There is enough traffic such that one’s ability to pick any lane is not majorly restricted, and the chance of another driver being in the way, while high, does not require the level of effort to “find” a safe gap between other cars on the road.
- One will notice that as traffic approaches rush hour, the road system approaches 100% capacity. Changing lanes can become very challenging because cars are so close together that increased caution must be exercised to do so.

This is why the long term averages for capacity conservatively estimated at 40% allows for head room for abnormal spikes in load, whether said spikes transitory (such as poorly coded queries that run for a few minutes) or abnormal bursts in general load (the morning of the first day after a long weekend).

The above statement regards % Processor Time calculation being the same as the Utilization Law is a bit of a simplification for the ease of the general reader. For those more mathematically rigorous:  
- Translating the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* = The number of 100-ns intervals “Idle” thread spends on the logical processor. The change in the “*X*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation
  - *T* = the total number of 100-ns intervals in a given time range. The change in the “*Y*” variable in the [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10)) calculation.
  - *U* k = The utilization percentage of the logical processor by the “Idle Thread” or % Idle Time.  
- Working out the math:
  - *U* k = 1 – %Processor Time
  - %Processor Time = 1 – *U* k
  - %Processor Time = 1 – *B* / *T*
  - %Processor Time = 1 – *X1* – *X0* / *Y1* – *Y0*

### Applying the concepts to capacity planning

The preceding math may make determinations about the number of logical processors needed in a system seem overwhelmingly complex. This is why the approach to sizing the systems is focused on determining maximum target utilization based on current load and calculating the number of logical processors required to get there. Additionally, while logical processor speeds will have a significant impact on performance, cache efficiencies, memory coherence requirements, thread scheduling and synchronization, and imperfectly balanced client load will all have significant impacts on performance that will vary on a server-by-server basis. With the relatively cheap cost of compute power, attempting to analyze and determine the perfect number of CPUs needed becomes more an academic exercise than it does provide business value.

Forty percent is not a hard and fast requirement, it is a reasonable start. Various consumers of Active Directory require various levels of responsiveness. There may be scenarios where environments can run at 80% or 90% utilization as a sustained average, as the increased wait times for access to the processor will not noticeably impact client performance. It is important to re-iterate that there are many areas in the system that are much slower than the logical processor in the system, including access to RAM, access to disk, and transmitting the response over the network. All of these items need to be tuned in conjunction. Examples:

- Adding more processors to a system running 90% that is disk-bound is probably not going to significantly improve performance. Deeper analysis of the system will probably identify that there are a lot of threads that are not even getting on the processor because they are waiting on I/O to complete.
- Resolving the disk-bound issues potentially means that threads that were previously spending a lot of time in a waiting state will no longer be in a waiting state for I/O and there will be more competition for CPU time, meaning that the 90% utilization in the previous example will go to 100% (because it can not go higher). Both components need to be tuned in conjunction.
  > [!NOTE]
  > Processor Information(*)\\% Processor Utility can exceed 100% with systems that have a "Turbo" mode.  This is where the CPU exceeds the rated processor speed for short periods.  Reference CPU manufacturers documentation and description of the counter for greater insight.  

Discussing whole system utilization considerations also brings into the conversation domain controllers as virtualized guests. [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) applies to both the host and the guest in a virtualized scenario. This is why in a host with only one guest, a domain controller (and generally any system) has near the same performance it does on physical hardware. Adding additional guests to the hosts increases the utilization of the underlying host, thereby increasing the wait times to get access to the processors as explained previously. In short, logical processor utilization needs to be managed at both the host and at the guest levels.

Extending the previous analogies, leaving the highway as the physical hardware, the guest VM will be analogized with a bus (an express bus that goes straight to the destination the rider wants). Imagine the following four scenarios:

- It is off hours, a rider gets on a bus that is nearly empty, and the bus gets on a road that is also nearly empty. As there is no traffic to contend with, the rider has a nice easy ride and gets there just as fast as if the rider had driven instead. The rider’s travel times are still constrained by the speed limit.
- It is off hours so the bus is nearly empty but most of the lanes on the road are closed, so the highway is still congested. The rider is on an almost-empty bus on a congested road. While the rider does not have a lot of competition in the bus for where to sit, the total trip time is still dictated by the rest of the traffic outside.
- It is rush hour so the highway and the bus are congested. Not only does the trip take longer, but getting on and off the bus is a nightmare because people are shoulder to shoulder and the highway is not much better. Adding more busses (logical processors to the guest) does not mean they can fit on the road any more easily, or that the trip will be shortened.
- The final scenario, though it may be stretching the analogy a little, is where the bus is full, but the road is not congested. While the rider will still have trouble getting on and off the bus, the trip will be efficient after the bus is on the road. This is the only scenario where adding more busses (logical processors to the guest) will improve guest performance.

From there it is relatively easy to extrapolate that there are a number of scenarios in between the 0%-utilized and the 100%-utilized state of the road and the 0%- and 100%-utilized state of the bus that have varying degrees of impact.

Applying the principals above of 40% CPU as reasonable target for the host as well as the guest is a reasonable start for the same reasoning as above, the amount of queuing.

## Appendix B: Considerations regarding different processor speeds, and the effect of processor power management on processor speeds

Throughout the sections on processor selection the assumption is made that the processor is running at 100% of clock speed the entire time the data is being collected and that the replacement systems will have the same speed processors. Despite both assumptions in practice being false, particularly with Windows Server 2008 R2 and later, where the default power plan is **Balanced**, the methodology still stands as it is the conservative approach. While the potential error rate may increase, it only increases the margin of safety as processor speeds increase.

- For example, in a scenario where 11.25 CPUs are demanded, if the processors were running at half speed when the data was collected, the more accurate estimate might be 5.125 &divide; 2.
- It is impossible to guarantee that doubling the clock speeds would double the amount of processing that happens for a given time period. This is due to the fact the amount of time that the processors spend waiting on RAM or other system components could stay the same. The net effect is that the faster processors might spend a greater percentage of the time idle while waiting on data to be fetched. Again, it is recommended to stick with the lowest common denominator, being conservative, and avoid trying to calculate a potentially false level of accuracy by assuming a linear comparison between processor speeds.

Alternatively, if processor speeds in replacement hardware are lower than current hardware, it would be safe to increase the estimate of processors needed by a proportionate amount. For example, it is calculated that 10 processors are needed to sustain the load in a site, and the current processors are running at 3.3 Ghz and replacement processors will run at 2.6 Ghz, this is a 21% decrease in speed. In this case, 12 processors would be the recommended amount.

That said, this variability would not change the Capacity Management processor utilization targets. As processor clock speeds will be adjusted dynamically based on the load demanded, running the system under higher loads will generate a scenario where the CPU spends more time in a higher clock speed state, making the ultimate goal to be at 40% utilization in a 100% clock speed state at peak. Anything less than that will generate power savings as CPU speeds will be throttled back during off peak scenarios.

> [!NOTE]
> An option would be to turn off power management on the processors (setting the power plan to **High Performance**) while data is collected. That would give a more accurate representation of the CPU consumption on the target server.

To adjust estimates for different processors, it used to be safe, excluding other system bottlenecks outlined above, to assume that doubling processor speeds doubled the amount of processing that could be performed.  Today, the internal architecture of processors is different enough between processors, that a safer way to gauge the effects of using different processors than data was taken from is to leverage the SPECint_rate2006 benchmark from Standard Performance Evaluation Corporation.

1. Find the SPECint_rate2006 scores for the processor that are in use and that plan to be used.
    1. On the website of the Standard Performance Evaluation Corporation, select **Results**, highlight **CPU2006**, and select **Search all SPECint_rate2006 results**.
    1. Under **Simple Request**, enter the search criteria for the target processor, for example **Processor Matches E5-2630 (baselinetarget)** and **Processor Matches E5-2650 (baseline)**.
    1. Find the server and processor configuration to be used (or something close, if an exact match is not available) and note the value in the **Result** and **# Cores** columns.
1. To determine the modifier use the following equation:
   >((*Target platform per-core score value*) &times; (*MHz per-core of baseline platform*)) &divide; ((*Baseline per-core score value*) &times; (*MHz per-core of target platform*))  

    Using the above example:
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. Multiply the estimated number of processors by the modifier.  In the above case to go from the E5-2650 processor to the E5-2630 processor multiply the calculated 11.25 CPUs &times; 0.92 = 10.35 processors needed.

## Appendix C: Fundamentals regarding the operating system interacting with storage

The queuing theory concepts outlined in [Response time/How the system busyness impacts performance](#response-timehow-the-system-busyness-impacts-performance) are also applicable to storage. Having a familiarity of how the operating system handles I/O is necessary to apply these concepts. In the Microsoft Windows operating system, a queue to hold the I/O requests is created for each physical disk. However, a clarification on physical disk needs to be made. Array controllers and SANs present aggregations of spindles to the operating system as single physical disks. Additionally, array controllers and SANs can aggregate multiple disks into one array set and then split this array set into multiple “partitions”, which is in turn presented to the operating system as multiple physical disks (ref. figure).

![Block spindles](media/capacity-planning-considerations-block-spindles.png)  

In this figure the two spindles are mirrored and split into logical areas for data storage (Data 1 and Data 2). These logical areas are viewed by the operating system as separate physical disks.

Although this can be highly confusing, the following terminology is used throughout this appendix to identify the different entities:

- **Spindle –** the device that is physically installed in the server.
- **Array –** a collection of spindles aggregated by controller.
- **Array partition –** a partitioning of the aggregated array
- **LUN –** an array, used when referring to SANs
- **Disk –** What the operating system observes to be a single physical disk.
- **Partition –** a logical partitioning of what the operating system perceives as a physical disk.

### Operating system architecture considerations

The operating system creates a First In/First Out (FIFO) I/O queue for each disk that is observed; this disk may be representing a spindle, an array, or an array partition. From the operating system perspective, with regard to handling I/O, the more active queues the better. As a FIFO queue is serialized, meaning that all I/Os issued to the storage subsystem must be processed in the order the request arrived. By correlating each disk observed by the operating system with a spindle/array, the operating system now maintains an I/O queue for each unique set of disks, thereby eliminating contention for scarce I/O resources across disks and isolating I/O demand to a single disk. As an exception, Windows Server 2008 introduces the concept of I/O prioritization, and applications designed to use the “Low” priority fall out of this normal order and take a back seat. Applications not specifically coded to leverage the “Low” priority default to “Normal.”

### Introducing simple storage subsystems

Starting with a simple example (a single hard drive inside a computer) a component-by-component analysis will be given. Breaking this down into the major storage subsystem components, the system consists of:

- **1 –** 10,000 RPM Ultra Fast SCSI HD (Ultra Fast SCSI has a 20 MB/s transfer rate)
- **1 –** SCSI Bus (the cable)
- **1 –** Ultra Fast SCSI Adapter
- **1 –** 32-bit 33 MHz PCI bus

Once the components are identified, an idea of how much data can transit the system, or how much I/O can be handled, can be calculated. Note that the amount of I/O and quantity of data that can transit the system is correlated, but not the same. This correlation depends on whether the disk I/O is random or sequential and the block size. (All data is written to the disk as a block, but different applications using different block sizes.) On a component-by-component basis:

- **The hard drive –** The average 10,000-RPM hard drive has a 7-millisecond (ms) seek time and a 3 ms access time. Seek time is the average amount of time it takes the read/write head to move to a location on the platter. Access time is the average amount of time it takes to read or write the data to disk, once the head is in the correct location. Thus, the average time for reading a unique block of data in a 10,000-RPM HD constitutes a seek and an access, for a total of approximately 10 ms (or .010 seconds) per block of data.

  When every disk access requires movement of the head to a new location on the disk, the read/write behavior is referred to as “random.” Thus, when all I/O is random, a 10,000-RPM HD can handle approximately 100 I/O per second (IOPS) (the formula is 1000 ms per second divided by 10 ms per I/O or 1000/10=100 IOPS).

  Alternatively, when all I/O occurs from adjacent sectors on the HD, this is referred to as sequential I/O. Sequential I/O has no seek time because when the first I/O is complete, the read/write head is at the start of where the next block of data is stored on the HD. Thus a 10,000-RPM HD is capable of handling approximately 333 I/O per second (1000 ms per second divided by 3 ms per I/O).

  >[!NOTE]
  >This example does not reflect the disk cache, where the data of one cylinder is typically kept. In this case, the 10 ms are needed on the first I/O and the disk reads the whole cylinder. All other sequential I/O is satisfied from the cache. As a result, in-disk caches might improve sequential I/O performance.
  
  So far, the transfer rate of the hard drive has been irrelevant. Whether the hard drive is 20 MB/s Ultra Wide or an Ultra3 160 MB/s, the actual amount of IOPS the can be handled by the 10,000-RPM HD is ~100 random or ~300 sequential I/O. As block sizes change based on the application writing to the drive, the amount of data that is pulled per I/O is different. For example, if the block size is 8 KB, 100 I/O operations will read from or write to the hard drive a total of 800 KB. However, if the block size is 32 KB, 100 I/O will read/write 3,200 KB (3.2 MB) to the hard drive. As long as the SCSI transfer rate is in excess of the total amount of data transferred, getting a “faster” transfer rate drive will gain nothing. See the following tables for comparison.

  | |7200 RPM 9ms seek, 4ms access|10,000 RPM 7ms seek, 3ms access|15,000 RPM 4ms seek, 2ms access
  |-|-|-|-|
  |Random I/O|80|100|150|
  |Sequential I/O|250|300|500|  
  
  |10,000 RPM drive|8 KB block size (Active Directory Jet)|
  |-|-|
  |Random I/O|800 KB/s|
  |Sequential I/O|2400 KB/s|

- **SCSI backplane (bus) –** Understanding how the “SCSI backplane (bus)”, or in this scenario the ribbon cable, impacts throughput of the storage subsystem depends on knowledge of the block size. Essentially the question would be, how much I/O can the bus handle if the I/O is in 8 KB blocks? In this scenario, the SCSI bus is 20 MB/s, or 20480 KB/s. 20480 KB/s divided by 8 KB blocks yields a maximum of approximately 2500 IOPS supported by the SCSI bus.

  >[!NOTE]
  >The figures in the following table represent an example. Most attached storage devices currently use PCI Express, which provides much higher throughput.  
  
  |I/O supported by SCSI bus per block size|2 KB block size|8 KB block size (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/s|10,000|2,500|
  |40 MB/s|20,000|5,000|
  |128 MB/s|65,536|16,384|
  |320 MB/s|160,000|40,000|

  As can be determined from this chart, in the scenario presented, no matter what the use, the bus will never be a bottleneck, as the spindle maximum is 100 I/O, well below any of the above thresholds.

  >[!NOTE]
  >This assumes that the SCSI bus is 100% efficient.
  
- **SCSI adapter –** For determining the amount of I/O that this can handle, the manufacturer’s specifications need to be checked. Directing I/O requests to the appropriate device requires processing of some sort, thus the amount of I/O that can be handled is dependent on the SCSI adapter (or array controller) processor.

  In this example, the assumption that 1,000 I/O can be handled will be made.

- **PCI bus –** This is an often overlooked component. In this example, this will not be the bottleneck; however as systems scale up, it can become a bottleneck. For reference, a 32 bit PCI bus operating at 33Mhz can in theory transfer 133 MB/s of data. Following is the equation:  
  > 32 bits &divide; 8 bits per byte &times; 33 MHz = 133 MB/s.  

  Note that is the theoretical limit; in reality only about 50% of the maximum is actually reached, although in certain burst scenarios, 75% efficiency can be obtained for short periods.

  A 66Mhz 64-bit PCI bus can support a theoretical maximum of (64 bits &divide; 8 bits per byte &times; 66 Mhz) = 528 MB/sec. Additionally, any other device (such as the network adapter, second SCSI controller, and so on) will reduce the bandwidth available as the bandwidth is shared and the devices will contend for the limited resources.

After analysis of the components of this storage subsystem, the spindle is the limiting factor in the amount of I/O that can be requested, and consequently the amount of data that can transit the system. Specifically, in an AD DS scenario, this is 100 random I/O per second in 8 KB increments, for a total of 800 KB per second when accessing the Jet database. Alternatively, the maximum throughput for a spindle that is exclusively allocated to log files would suffer the following limitations: 300 sequential I/O per second in 8 KB increments, for a total of 2400 KB (2.4 MB) per second.

Now, having analyzed a simple configuration, the following table demonstrates where the bottleneck will occur as components in the storage subsystem are changed or added.

|Notes|Bottleneck analysis|Disk|Bus|Adapter|PCI bus|
|-|-|-|-|-|-|
|This is the domain controller configuration after adding a second disk. The disk configuration represents the bottleneck at 800 KB/s.|Add 1 disk (Total=2)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|200 I/Os total<br />800 KB/s total.| | | |
|After adding 7 disks, the disk configuration still represents the bottleneck at 3200 KB/s.|**Add 7 disks (Total=8)**  <br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD|800 I/Os total.<br />3200 KB/s total| | | |
|After changing I/O to sequential, the network adapter becomes the bottleneck because it is limited to 1000 IOPS.|Add 7 disks (Total=8)<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD| | |2400 I/O sec can be read/written to disk, controller limited to 1000 IOPS| |
|After replacing the network adapter with a SCSI adapter that supports 10,000 IOPS, the bottleneck returns to the disk configuration.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade SCSI adapter (now supports 10,000 I/O)**|800 I/Os total.<br />3,200 KB/s total| | | |
|After increasing the block size to 32 KB, the bus becomes the bottleneck because it only supports 20 MB/s.|Add 7 disks (Total=8)<br /><br />I/O is random<br /><br />**32 KB block size**<br /><br />10,000 RPM HD| |800 I/Os total. 25,600 KB/s (25 MB/s) can be read/written to disk.<br /><br />The bus only supports 20 MB/s| | |
|After upgrading the bus and adding more disks, the disk remains the bottleneck.|**Add 13 disks (Total=14)**<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is random<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />**Upgrade to 320 MB/s SCSI bus**|2800 I/Os<br /><br />11,200 KB/s (10.9 MB/s)| | | |
|After changing I/O to sequential, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI Adapter with 14 disks<br /><br />**I/O is sequential**<br /><br />4 KB block size<br /><br />10,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus|8,400 I/Os<br /><br />33,600 KB\s<br /><br />(32.8 MB\s)| | | |
|After adding faster hard drives, the disk remains the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />4 KB block size<br /><br />**15,000 RPM HD**<br /><br />Upgrade to 320 MB/s SCSI bus|14,000 I/Os<br /><br />56,000 KB/s<br /><br />(54.7 MB/s)| | | |
|After increasing the block size to 32 KB, the PCI bus becomes the bottleneck.|Add 13 disks (Total=14)<br /><br />Add second SCSI adapter with 14 disks<br /><br />I/O is sequential<br /><br />**32 KB block size**<br /><br />15,000 RPM HD<br /><br />Upgrade to 320 MB/s SCSI bus| | | |14,000 I/Os<br /><br />448,000 KB/s<br /><br />(437 MB/s) is the read/write limit to the spindle.<br /><br />The PCI bus supports a theoretical maximum of 133 MB/s (75% efficient at best).|

### Introducing RAID

The nature of a storage subsystem does not change dramatically when an array controller is introduced; it just replaces the SCSI adapter in the calculations. What does change is the cost of reading and writing data to the disk when using the various array levels (such as RAID 0, RAID 1, or RAID 5).

In RAID 0, the data is striped across all the disks in the RAID set. This means that during a read or a write operation, a portion of the data is pulled from or pushed to each disk, increasing the amount of data that can transit the system during the same time period. Thus, in one second, on each spindle (again assuming 10,000-RPM drives), 100 I/O operations can be performed. The total amount of I/O that can be supported is N spindles times 100 I/O per second per spindle (yields 100*N I/O per second).

![Logical d: drive](media/capacity-planning-considerations-logical-d-drive.png)

In RAID 1, the data is mirrored (duplicated) across a pair of spindles for redundancy. Thus, when a read I/O operation is performed, data can be read from both of the spindles in the set. This effectively makes the I/O capacity from both disks available during a read operation. The caveat is that write operations gain no performance advantage in a RAID 1. This is because the same data needs to be written to both drives for the sake of redundancy. Though it does not take any longer, as the write of data occurs concurrently on both spindles, because both spindles are occupied duplicating the data, a write I/O operation in essence prevents two read operations from occurring. Thus, every write I/O costs two read I/O. A formula can be created from that information to determine the total number of I/O operations that are occurring:  

> *Read I/O* + 2 &times; *Write I/O* = *Total available disk I/O consumed*  

When the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array:  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total IOPS*

RAID 1+ 0, behaves exactly the same as RAID 1 regarding the expense of reading and writing. However, the I/O is now striped across each mirrored set. If  

> *Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] = *Total I/O*  

in a RAID 1 set, when a multiplicity (*N*) of RAID 1 sets are striped, the Total I/O that can be processed becomes N &times; I/O per RAID 1 set:  

> *N* &times; {*Maximum IOPS per spindle* &times; 2 spindles &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 2 &times; *%Writes*)] } = *Total IOPS*

In RAID 5, sometimes referred to as *N* + 1 RAID, the data is striped across *N* spindles and parity information is written to the “+ 1” spindle. However, RAID 5 is much more expensive when performing a write I/O than RAID 1 or 1 + 0. RAID 5 performs the following process every time a write I/O is submitted to the array:

1. Read the old data
1. Read the old parity
1. Write the new data
1. Write the new parity

As every write I/O request that is submitted to the array controller by the operating system requires four I/O operations to complete, write requests submitted take four times as long to complete as a single read I/O. To derive a formula to translate I/O requests from the operating system perspective to that experienced by the spindles:  

> *Read I/O* + 4 &times; *Write I/O* = *Total I/O*  

Similarly in a RAID 1 set, when the ratio of reads to writes and the number of spindles are known, the following equation can be derived from the above equation to identify the maximum I/O that can be supported by the array (Note that total number of spindles does not include the “drive” lost to parity):  

> *IOPS per spindle* &times; (*Spindles* – 1) &times; [(*%Reads* + *%Writes*) &divide; (*%Reads* + 4 &times; *%Writes*)] = *Total IOPS*

### Introducing SANs

Expanding the complexity of the storage subsystem, when a SAN is introduced into the environment, the basic principles outlined do not change, however I/O behavior for all of the systems connected to the SAN needs to be taken into account. As one of the major advantages in using a SAN is an additional amount of redundancy over internally or externally attached storage, capacity planning now needs to take into account fault tolerance needs. Also, more components are introduced that need to be evaluated. Breaking a SAN down into the component parts:

- SCSI or Fibre Channel hard drive
- Storage unit channel backplane
- Storage units
- Storage controller module
- SAN switch(es)
- HBA(s)
- The PCI bus

When designing any system for redundancy, additional components are included to accommodate the potential of failure. It is very important, when capacity planning, to exclude the redundant component from available resources. For example, if the SAN has two controller modules, the I/O capacity of one controller module is all that should be used for total I/O throughput available to the system. This is due to the fact that if one controller fails, the entire I/O load demanded by all connected systems will need to be processed by the remaining controller. As all capacity planning is done for peak usage periods, redundant components should not be factored into the available resources and planned peak utilization should not exceed 80% saturation of the system (in order to accommodate bursts or anomalous system behavior). Similarly, the redundant SAN switch, storage unit, and spindles should not be factored into the I/O calculations.

When analyzing the behavior of the SCSI or Fibre Channel hard drive, the method of analyzing the behavior as outlined previously does not change. Although there are certain advantages and disadvantages to each protocol, the limiting factor on a per disk basis is the mechanical limitation of the hard drive.

Analyzing the channel on the storage unit is exactly the same as calculating the resources available on the SCSI bus, or bandwidth (such as 20 MB/s) divided by block size (such as 8 KB). Where this deviates from the simple previous example is in the aggregation of multiple channels. For example, if there are 6 channels, each supporting 20 MB/s maximum transfer rate, the total amount of I/O and data transfer that is available is 100 MB/s (this is correct, it is not 120 MB/s). Again, fault tolerance is a major player in this calculation, in the event of the loss of an entire channel, the system is only left with 5 functioning channels. Thus, to ensure continuing to meet performance expectations in the event of failure, total throughput for all of the storage channels should not exceed 100 MB/s (this assumes load and fault tolerance is evenly distributed across all channels). Turning this into an I/O profile is dependent on the behavior of the application. In the case of Active Directory Jet I/O, this would correlate to approximately 12,500 I/O per second (100 MB/s &divide; 8 KB per I/O).

Next, obtaining the manufacturer’s specifications for the controller modules is required in order to gain an understanding of the throughput each module can support. In this example, the SAN has two controller modules that support 7,500 I/O each. The total throughput of the system may be 15,000 IOPS if redundancy is not desired. In calculating maximum throughput in the case of failure, the limitation is the throughput of one controller, or 7,500 IOPS. This threshold is well below the 12,500 IOPS (assuming 4 KB block size) maximum that can be supported by all of the storage channels, and thus, is currently the bottleneck in the analysis. Still for planning purposes, the desired maximum I/O to be planned for would be 10,400 I/O.

When the data exits the controller module, it transits a Fibre Channel connection rated at 1 GB/s (or 1 Gigabit per second). To correlate this with the other metrics, 1 GB/s turns into 128 MB/s (1 GB/s &divide; 8 bits/byte). As this is in excess of the total bandwidth across all channels in the storage unit (100 MB/s), this will not bottleneck the system. Additionally, as this is only one of the two channels (the additional 1 GB/s Fibre Channel connection being for redundancy), if one connection fails, the remaining connection still has enough capacity to handle all the data transfer demanded.

En route to the server, the data will most likely transit a SAN switch. As the SAN switch has to process the incoming I/O request and forward it out the appropriate port, the switch will have a limit to the amount of I/O that can be handled, however, manufacturers specifications will be required to determine what that limit is. For example, if there are two switches and each switch can handle 10,000 IOPS, the total throughput will be 20,000 IOPS. Again, fault tolerance being a concern, if one switch fails, the total throughput of the system will be 10,000 IOPS. As it is desired not to exceed 80% utilization in normal operation, using no more than 8000 I/O should be the target.

Finally, the HBA installed in the server would also have a limit to the amount of I/O that it can handle. Usually, a second HBA is installed for redundancy, but just like with the SAN switch, when calculating maximum I/O that can be handled, the total throughput of *N* &ndash; 1 HBAs is what the maximum scalability of the system is.

### Caching considerations

Caches are one of the components that can significantly impact the overall performance at any point in the storage system. Detailed analysis about caching algorithms is beyond the scope of this article; however, some basic statements about caching on disk subsystems are worth illuminating:

- Caching does improved sustained sequential write I/O as it can buffer many smaller write operations into larger I/O blocks and de-stage to storage in fewer, but larger block sizes. This will reduce total random I/O and total sequential I/O, thus providing more resource availability for other I/O.
- Caching does not improve sustained write I/O throughput of the storage subsystem. It only allows for the writes to be buffered until the spindles are available to commit the data. When all the available I/O of the spindles in the storage subsystem is saturated for long periods, the cache will eventually fill up. In order to empty the cache, enough time between bursts, or extra spindles, need to be allotted in order to provide enough I/O to allow the cache to flush.

  Larger caches only allow for more data to be buffered. This means longer periods of saturation can be accommodated.

  In a normally operating storage subsystem, the operating system will experience improved write performance as the data only needs to be written to cache. Once the underlying media is saturated with I/O, the cache will fill and write performance will return to disk speed.

- When caching read I/O, the scenario where the cache is most advantageous is when the data is stored sequentially on the disk, and the cache can read-ahead (it makes the assumption that the next sector contains the data that will be requested next).
- When read I/O is random, caching at the drive controller is unlikely to provide any enhancement to the amount of data that can be read from the disk. Any enhancement is non-existent if the operating system or application-based cache size is greater than the hardware-based cache size.

  In the case of Active Directory, the cache is only limited by the amount of RAM.

### SSD considerations

SSDs are a completely different animal than spindle-based hard disks. Yet the two key criteria remain: “How many IOPS can it handle?” and “What is the latency for those IOPS?” In comparison to spindle-based hard disks, SSDs can handle higher volumes of I/O and can have lower latencies. In general and as of this writing, while SSDs are still expensive in a cost-per-Gigabyte comparison, they are very cheap in terms of cost-per-I/O and deserve significant consideration in terms of storage performance.

Considerations:

- Both IOPS and latencies are very subjective to the manufacturer designs and in some cases have been observed to be poorer performing than spindle based technologies. In short, it is more important to review and validate the manufacturer specs drive by drive and not assume any generalities.
- IOPS types can have very different numbers depending on whether it is read or write. AD DS services, in general, being predominantly read-based, will be less affected than some other application scenarios.
- “Write endurance” – this is the concept that SSD cells will eventually wear out. Various manufacturers deal with this challenge different fashions. At least for the database drive, the predominantly read I/O profile allows for downplaying the significance of this concern as the data is not highly volatile.

### Summary

One way to think about storage is picturing household plumbing. Imagine the IOPS of the media that the data is stored on is the household main drain. When this is clogged (such as roots in the pipe) or limited (it is collapsed or too small), all the sinks in the household back up when too much water is being used (too many guests). This is perfectly analogous to a shared environment where one or more systems are leveraging shared storage on an SAN/NAS/iSCSI with the same underlying media. Different approaches can be taken to resolve the different scenarios:

- A collapsed or undersized drain requires a full scale replacement and fix. This would be similar to adding in new hardware or redistributing the systems using the shared storage throughout the infrastructure.
- A “clogged” pipe usually means identification of one or more offending problems and removal of those problems. In a storage scenario this could be storage or system level backups, synchronized antivirus scans across all servers, and synchronized defragmentation software running during peak periods.

In any plumbing design, multiple drains feed into the main drain. If anything stops up one of those drains or a junction point, only the things behind that junction point back up. In a storage scenario, this could be an overloaded switch (SAN/NAS/iSCSI scenario), driver compatibility issues (wrong driver/HBA Firmware/storport.sys combination), or backup/antivirus/defragmentation. To determine if the storage “pipe” is big enough, IOPS and I/O size needs to be measured. At each joint add them together to ensure adequate “pipe diameter.”

## Appendix D - Discussion on storage troubleshooting - Environments where providing at least as much RAM as the database size is not a viable option

It is helpful to understand why these recommendations exist so that the changes in storage technology can be accommodated. These recommendations exist for two reasons. The first is isolation of IO, such that performance issues (that is, paging) on the operating system spindle do not impact performance of the database and I/O profiles. The second is that log files for AD DS (and most databases) are sequential in nature, and spindle-based hard drives and caches have a huge performance benefit when used with sequential I/O as compared to the more random I/O patterns of the operating system and almost purely random I/O patterns of the AD DS database drive. By isolating the sequential I/O to a separate physical drive, throughput can be increased. The challenge presented by today’s storage options is that the fundamental assumptions behind these recommendations are no longer true. In many virtualized storage scenarios, such as iSCSI, SAN, NAS, and Virtual Disk image files, the underlying storage media is shared across multiple hosts, thus completely negating both the “isolation of IO” and the “sequential I/O optimization” aspects. In fact these scenarios add an additional layer of complexity in that other hosts accessing the shared media can degrade responsiveness to the domain controller.

In planning storage performance, there are three categories to consider: cold cache state, warmed cache state, and backup/restore. The cold cache state occurs in scenarios such as when the domain controller is initially rebooted or the Active Directory service is restarted and there is no Active Directory data in RAM. Warm cache state is where the domain controller is in a steady state and the database is cached. These are important to note as they will drive very different performance profiles, and having enough RAM to cache the entire database does not help performance when the cache is cold. One can consider performance design for these two scenarios with the following analogy, warming the cold cache is a “sprint” and running a server with a warm cache is a “marathon.”

For both the cold cache and warm cache scenario, the question becomes how fast the storage can move the data from disk into memory. Warming the cache is a scenario where, over time, performance improves as more queries reuse data, the cache hit rate increases, and the frequency of needing to go to disk decreases. As a result the adverse performance impact of going to disk decreases. Any degradation in performance is only transient while waiting for the cache to warm and grow to the maximum, system-dependent allowed size. The conversation can be simplified to how quickly the data can be gotten off of disk, and is a simple measure of the IOPS available to Active Directory, which is subjective to IOPS available from the underlying storage. From a planning perspective, because warming the cache and backup/restore scenarios happen on an exceptional basis, normally occur off hours, and are subjective to the load of the DC, general recommendations do not exist except in that these activities be scheduled for non-peak hours.

AD DS, in most scenarios, is predominantly read IO, usually a ratio of 90% read/10% write. Read I/O often tends to be the bottleneck for user experience, and with write IO, causes write performance to degrade. As I/O to the NTDS.dit is predominantly random, caches tend to provide minimal benefit to read IO, making it that much more important to configure the storage for read I/O profile correctly.

For normal operating conditions, the storage planning goal is minimize the wait times for a request from AD DS to be returned from disk. This essentially means that the number of outstanding and pending I/O is less than or equivalent to the number of pathways to the disk. There are a variety of ways to measure this. In a performance monitoring scenario, the general recommendation is that LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read be less than 20 ms. The desired operating threshold must be much lower, preferably as close to the speed of the storage as possible, in the 2 to 6 millisecond (.002 to .006 second) range depending on the type of storage.

Example:

![Storage latency chart](media/capacity-planning-considerations-storage-latency.png)

Analyzing the chart:

- **Green oval on the left –** The latency remains consistent at 10 ms. The load increases from 800 IOPS to 2400 IOPS. This is the absolute floor to how quickly an I/O request can be processed by the underlying storage. This is subject to the specifics of the storage solution.
- **Burgundy oval on the right –** The throughput remains flat from the exit of the green circle through to the end of the data collection while the latency continues to increase. This is demonstrating that when the request volumes exceed the physical limitations of the underlying storage, the longer the requests spend sitting in the queue waiting to be sent out to the storage subsystem.

Applying this knowledge:

- **Impact to a user querying membership of a large group –** Assume this requires reading 1 MB of data from the disk, the amount of I/O and how long it takes can be evaluated as follows:
  - Active Directory database pages are 8 KB in size. 
  - A minimum of 128 pages need to be read in from disk. 
  - Assuming nothing is cached, at the floor (10 ms) this is going to take a minimum 1.28 seconds to load the data from disk in order to return it to the client. At 20 ms, where the throughput on storage has long since maxed out and is also the recommended maximum, it will take 2.5 seconds to get the data from disk in order to return it to the end user.  
- **At what rate will the cache be warmed –** Making the assumption that the client load is going to maximize the throughput on this storage example, the cache will warm at a rate of 2400 IOPS &times; 8 KB per IO. Or, approximately 20 MB/s per second, loading about 1 GB of database into RAM every 53 seconds.

> [!NOTE]
> It is normal for short periods to observe the latencies climb when components aggressively read or write to disk, such as when the system is being backed up or when AD DS is running garbage collection. Additional head room on top of the calculations should be provided to accommodate these periodic events. The goal being to provide enough throughput to accommodate these scenarios without impacting normal function.

As can be seen, there is a physical limit based on the storage design to how quickly the cache can possibly warm. What will warm the cache are incoming client requests up to the rate that the underlying storage can provide. Running scripts to “pre-warm” the cache during peak hours will provide competition to load driven by real client requests. That can adversely affect delivering data that clients need first because, by design, it will generate competition for scarce disk resources as artificial attempts to warm the cache will load data that is not relevant to the clients contacting the DC.プロセッサ Information(_Total)\\' プロセッサ ユーティリティ Domain Services
description: Detailed discussion of the factors to consider during capacity planning for AD DS.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; kenbrunf
author: Teresa-Motiv
ms.date: 7/3/2019
---

# Capacity planning for Active Directory Domain Services

This topic is originally written by Ken Brumfield, Senior Premier Field Engineer at Microsoft, and provides recommendations for capacity planning for Active Directory Domain Services (AD DS).

## Goals of capacity planning

Capacity planning is not the same as troubleshooting performance incidents. They are closely related, but quite different. The goals of capacity planning are:  

- Properly implement and operate an environment 
- Minimize the time spent troubleshooting performance issues.  
  
In capacity planning, an organization might have a baseline target of 40% processor utilization during peak periods in order to meet client performance requirements and accommodate the time necessary to upgrade the hardware in the datacenter. Whereas, to be notified of abnormal performance incidents, a monitoring alert threshold might be set at 90% over a 5 minute interval.

The difference is that when a capacity management threshold is continually exceeded (a one-time event is not a concern), adding capacity (that is, adding in more or faster processors) would be a solution or scaling the service across multiple servers would be a solution. Performance alert thresholds indicate that client experience is currently suffering and immediate steps are needed to address the issue.

As an analogy: capacity management is about preventing a car accident (defensive driving, making sure the brakes are working properly, and so on) whereas performance troubleshooting is what the police, fire department, and emergency medical professionals do after an accident. This is about “defensive driving,” Active Directory-style.

Over the last several years, capacity planning guidance for scale-up systems has changed dramatically. The following changes in system architectures have challenged fundamental assumptions about designing and scaling a service:

- 64-bit server platforms  
- Virtualization  
- Increased attention to power consumption  
- SSD storage  
- Cloud scenarios  

Additionally, the approach is shifting from a server-based capacity planning exercise to a service-based capacity planning exercise. Active Directory Domain Services (AD DS), a mature distributed service that many Microsoft and third-party products use as a backend, becomes one the most critical products to plan correctly to ensure the necessary capacity for other applications to run.

### Baseline requirements for capacity planning guidance

Throughout this article, the following baseline requirements are expected:

- Readers have read and are familiar with [Performance Tuning Guidelines for Windows Server 2012 R2](https://docs.microsoft.com/previous-versions//dn529133(v=vs.85)).
- The Windows Server platform is an x64 based architecture. But even if your Active Directory environment is installed on Windows Server 2003 x86 (now beyond the end of the support lifecycle) and has a directory information tree (DIT) that is less 1.5 GB in size and that can easily be held in memory, the guidelines from this article are still applicable.
- Capacity planning is a continuous process and you should regularly review how well the environment is meeting expectations.
- Optimization will occur over multiple hardware lifecycles as hardware costs change. For example, memory becomes cheaper, the cost per core decreases, or the price of different storage options change.
- Plan for the peak busy period of the day. It is recommended to look at this in either 30 minute or hour intervals. Anything greater may hide the actual peaks and anything less may be distorted by “transient spikes.”
- Plan for growth over the course of the hardware lifecycle for the enterprise. This may include a strategy of upgrading or adding hardware in a staggered fashion, or a complete refresh every three to five years. Each will require a “guess” as how much the load on Active Directory will grow. Historical data, if collected, will help with this assessment. 
- Plan for fault tolerance. Once an estimate *N* is derived, plan for scenarios that include *N* &ndash; 1, *N* &ndash; 2, *N* &ndash; *x*.
  - Add in additional servers according to organizational need to ensure that the loss of a single or multiple servers does not exceed maximum peak capacity estimates.
  - Also consider that the growth plan and fault tolerance plan need to be integrated. For example, if one DC is required to support the load, but the estimate is that the load will be doubled in the next year and require two DCs total, there will not be enough capacity to support fault tolerance. The solution would be to start with three DCs. One could also plan to add the third DC after 3 or 6 months if budgets are tight.

    >[!NOTE]
    >Adding Active Directory-aware applications might have a noticeable impact on the DC load, whether the load is coming from the application servers or clients.

### Three-step process for the capacity planning cycle

In capacity planning, first decide what quality of service is needed. For example, a core datacenter supports a higher level of concurrency and requires more consistent experience for users and consuming applications, which requires greater attention to redundancy and minimizing system and infrastructure bottlenecks. In contrast, a satellite location with a handful of users does not need the same level of concurrency or fault tolerance. Thus, the satellite office might not need as much attention to optimizing the underlying hardware and infrastructure, which may lead to cost savings. All recommendations and guidance herein are for optimal performance, and can be selectively relaxed for scenarios with less demanding requirements.

The next question is: virtualized or physical? From a capacity planning perspective, there is no right or wrong answer; there is only a different set of variables to work with. Virtualization scenarios come down to one of two options:

- “Direct mapping” with one guest per host (where virtualization exists solely to abstract the physical hardware from the server)
- “Shared host”

Testing and production scenarios indicate that the “direct mapping” scenario can be treated identically to a physical host. “Shared host,” however, introduces a number of considerations spelled out in more detail later. The “shared host” scenario means that AD DS is also competing for resources, and there are penalties and tuning considerations for doing so.

With these considerations in mind, the capacity planning cycle is an iterative three-step process:

1. Measure the existing environment, determine where the system bottlenecks currently are, and get environmental basics necessary to plan the amount of capacity needed.
1. Determine the hardware needed according to the criteria outlined in step 1.
1. Monitor and validate that the infrastructure as implemented is operating within specifications. Some data collected in this step becomes the baseline for the next cycle of capacity planning.

### Applying the process

To optimize performance, ensure these major components are correctly selected and tuned to the application loads:

1. Memory
1. Network
1. Storage
1. Processor
1. Net Logon

The basic storage requirements of AD DS and the general behavior of well written client software allow environments with as many as 10,000 to 20,000 users to forego heavy investment in capacity planning with regards to physical hardware, as almost any modern server class system will handle the load. That said, the following table summarizes how to evaluate an existing environment in order to select the right hardware. Each component is analyzed in detail in subsequent sections to help AD DS administrators evaluate their infrastructure using baseline recommendations and environment-specific principals.

In general:

- Any sizing based on current data will only be accurate for the current environment.
- For any estimates, expect demand to grow over the lifecycle of the hardware.
- Determine whether to oversize today and grow into the larger environment, or add capacity over the lifecycle.
- For virtualization, all the same capacity planning principals and methodologies apply, except that the overhead of the virtualization needs to be added to anything domain related.
- Capacity planning, like anything that attempts to predict, is NOT an accurate science. Do not expect things to calculate perfectly and with 100% accuracy. The guidance here is the leanest recommendation; add in capacity for additional safety and continuously validate that the environment remains on target.

### Data collection summary tables

#### New environment

| Component | Estimates |
|-|-|
|Storage/Database Size|40 KB to 60 KB for each user|
|RAM|Database Size<br />Base operating system recommendations<br />Third-party applications|
|Network|1 GB|
|CPU|1000 concurrent users for each core|

#### High-level evaluation criteria

| Component | Evaluation criteria | Planning considerations |
|-|-|-|
|Storage/Database size|The section entitled “To activate logging of disk space that is freed by defragmentation” in [Storage Limits](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10))| |
|Storage/ Database performance|<ul><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Write," "LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer"</li><li>"LogicalDisk(*\<NTDS Database Drive\>*)\Reads/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Writes/sec," "LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec"</li></ul>|<ul><li>Storage has two concerns to address<ul><li>Space available, which with the size of today’s spindle based and SSD based storage is irrelevant for most AD environments.</li> <li>Input/Output (IO) Operations available – In many environments, this is often overlooked. But it is important to evaluate only environments where there is not enough RAM to load the entire NTDS Database into memory.</li></ul><li>Storage can be a complex topic and should involve hardware vendor expertise for proper sizing. Particularly with more complex scenarios such as SAN, NAS, and iSCSI scenarios. However, in general, cost per Gigabyte of storage is often in direct opposition to cost per IO:<ul><li>RAID 5 has lower cost per Gigabyte than Raid 1, but Raid 1 has lower cost per IO</li><li>Spindle-based hard drives have lower cost per Gigabyte, but SSDs have a lower cost per IO</li></ul><li>After a restart of the computer or the Active Directory Domain Services service, the Extensible Storage Engine (ESE) cache is empty and performance will be disk bound while the cache warms.</li><li>In most environments AD is read intensive I/O in a random pattern to disks, negating much of the benefit of caching and read optimization strategies.  Plus, AD has a way larger cache in memory than most storage system caches.</li></ul>
|RAM|<ul><li>Database size</li><li>Base operating system recommendations</li><li>Third-party applications</li></ul>|<ul><li>Storage is the slowest component in a computer. The more that can be resident in RAM, the less it is necessary to go to disk.</li><li>Ensure enough RAM is allocated to store the operating system, Agents (antivirus, backup, monitoring), NTDS Database and growth over time.</li><li>For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.</li></ul>|
|Network|<ul><li>“Network Interface(\*)\Bytes Received/sec”</li><li>“Network Interface(\*)\Bytes Sent/sec”|<ul><li>In general, traffic sent from a DC far exceeds traffic sent to a DC.</li><li>As a switched Ethernet connection is full-duplex, inbound and outbound network traffic need to be sized independently.</li><li>Consolidating the number of DCs will increase the amount of bandwidth used to send responses back to client requests for each DC, but will be close enough to linear for the site as a whole.</li><li>If removing satellite location DCs, don’t forget to add the bandwidth for the satellite DC into the hub DCs as well as use that to evaluate how much WAN traffic there will be.</li></ul>|
|CPU|<ul><li>“Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read”</li><li>“Process(lsass)\\% Processor Time”</li></ul>|<ul><li>After eliminating storage as a bottleneck, address the amount of compute power needed.</li><li>While not perfectly linear, the number of processor cores consumed across all servers within a specific scope (such as a site) can be used to gauge how many processors are necessary to support the total client load. Add the minimum necessary to maintain the current level of service across all the systems within the scope.</li><li>Changes in processor speed, including power management related changes, impact numbers derived from the current environment. Generally, it is impossible to precisely evaluate how going from a 2.5 GHz processor to a 3 GHz processor will reduce the number of CPUs needed.</li></ul>|
|NetLogon|<ul><li>“Netlogon(\*)\Semaphore Acquires”</li><li>“Netlogon(\*)\Semaphore Timeouts”</li><li>“Netlogon(\*)\Average Semaphore Hold Time”</li></ul>|<ul><li>Net Logon Secure Channel/MaxConcurrentAPI only affects environments with NTLM authentications and/or PAC Validation. PAC Validation is on by default in operating system versions before Windows Server 2008. This is a client setting, so the DCs will be impacted until this is turned off on all client systems.</li><li>Environments with significant cross trust authentication, which includes intra-forest trusts, have greater risk if not sized properly.</li><li>Server consolidations will increase concurrency of cross-trust authentication.</li><li>Surges need to be accommodated, such as cluster fail-overs, as users re-authenticate en masse to the new cluster node.</li><li>Individual client systems (such as a cluster) might need tuning too.</li></ul>|

## Planning

For a long time, the community’s recommendation for sizing AD DS has been to “put in as much RAM as the database size.” For the most part, that recommendation is all that most environments needed to be concerned about. But the ecosystem consuming AD DS has gotten much bigger, as have the AD DS environments themselves, since its introduction in 1999. Although the increase in compute power and the switch from x86 architectures to x64 architectures has made the subtler aspects of sizing for performance irrelevant to a larger set of customers running AD DS on physical hardware, the growth of virtualization has reintroduced the tuning concerns to a larger audience than before.

The following guidance is thus about how to determine and plan for the demands of Active Directory as a service regardless of whether it is deployed in a physical, a virtual/physical mix, or a purely virtualized scenario. As such, we will break down the evaluation to each of the four main components: storage, memory, network, and processor. In short, in order to maximize performance on AD DS, the goal is to get as close to processor bound as possible.

## RAM

Simply, the more that can be cached in RAM, the less it is necessary to go to disk. To maximize the scalability of the server the minimum amount of RAM should be the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). An additional amount should be added to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth based on environmental changes.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage  section to ensure that storage is properly designed.

A corollary that comes up in the general context in sizing memory is sizing of the page file. In the same context as everything else memory related, the goal is to minimize going to the much slower disk. Thus the question should go from, “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Evaluating

The amount of RAM that a domain controller (DC) needs is actually a complex exercise for these reasons:

- High potential for error when trying to use an existing system to gauge how much RAM is needed as LSASS will trim under memory pressure conditions, artificially deflating the need.
- The subjective fact that an individual DC only needs to cache what is “interesting” to its clients. This means that the data that needs to be cached on a DC in a site with only an Exchange server will be very different than the data that needs to be cached on a DC that only authenticates users.
- The labor to evaluate RAM for each DC on a case-by-case basis is prohibitive and changes as the environment changes.
- The criteria behind the recommendation will help to make informed decisions: 
- The more that can be cached in RAM, the less it is necessary to go to disk. 
- Storage is by far the slowest component of a computer. Access to data on spindle-based and SSD storage media is on the order of 1,000,000x slower than access to data in RAM.

Thus, in order to maximize the scalability of the server, the minimum amount of RAM is the sum of the current database size, the total SYSVOL size, the operating system recommended amount, and the vendor recommendations for the agents (antivirus, monitoring, backup, and so on). Add additional amounts to accommodate growth over the lifetime of the server. This will be environmentally subjective based on estimates of database growth. However, for satellite locations with a small set of end users, these requirements can be relaxed as these sites will not need to cache as much to service most of the requests.

For environments where maximizing the amount of RAM is not cost effective (such as a satellite locations) or not feasible (DIT is too large), reference the Storage section to ensure that storage is properly sized.

> [!NOTE]
> A corollary while sizing memory is sizing of the page file. Because the goal is to minimize going to the much slower disk, the question goes from “how should the page file be sized?” to “how much RAM is needed to minimize paging?” The answer to the latter question is outlined in the rest of this section. This leaves most of the discussion for sizing the page file to the realm of general operating system recommendations and the need to configure the system for memory dumps, which are unrelated to AD DS performance.

### Virtualization considerations for RAM

Avoid memory over-commit at the host. The fundamental goal behind optimizing the amount of RAM is to minimize the amount of time spent going to disk. In virtualization scenarios, the concept of memory over-commit exists where more RAM is allocated to the guests then exists on the physical machine. This in and of itself is not a problem. It becomes a problem when the total memory actively used by all the guests exceeds the amount of RAM on the host and the underlying host starts paging. Performance becomes disk-bound in cases where the domain controller is going to the NTDS.dit to get data, or the domain controller is going to the page file to get data, or the host is going to disk to get data that the guest thinks is in RAM.

### Calculation summary example

|Component|Estimated memory (example)|
|-|-|
|Base operating system recommended RAM (Windows Server 2008)|2 GB|
|LSASS internal tasks|200 MB|
|Monitoring agent|100 MB|
|Antivirus|100 MB|
|Database (Global Catalog)|8.5 GB are you sure ???|
|Cushion for backup to run, administrators to log on without impact|1 GB|
|Total|12 GB|

**Recommended: 16 GB**

Over time, the assumption can be made that more data will be added to the database and the server will probably be in production for 3 to 5 years. Based on an estimate of growth of 33%, 16 GB would be a reasonable amount of RAM to put in a physical server. In a virtual machine, given the ease with which settings can be modified and RAM can be added to the VM, starting at 12 GB with the plan to monitor and upgrade in the future is reasonable.

## Network

### Evaluating
This section is less about evaluating the demands regarding replication traffic, which is focused on traffic traversing the WAN and is thoroughly covered in [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)), than it is about evaluating total bandwidth and network capacity needed, inclusive of client queries, Group Policy applications, and so on. For existing environments, this can be collected by using performance counters “Network Interface(\*)\Bytes Received/sec,” and “Network Interface(\*)\Bytes Sent/sec.” Sample intervals for Network Interface counters in either 15, 30, or 60 分utes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

> [!NOTE]
> Generally, the majority of network traffic on a DC is outbound as the DC responds to client queries. This is the reason for the focus on outbound traffic, though it is recommended to evaluate each environment for inbound traffic also. The same approaches can be used to address and review inbound network traffic requirements. For more information, see Knowledge Base article [929851: The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](http://support.microsoft.com/kb/929851).

### Bandwidth needs

Planning for network scalability covers two distinct categories: the amount of traffic and the CPU load from the network traffic. Each of these scenarios is straight-forward compared to some of the other topics in this article.

In evaluating how much traffic must be supported, there are two unique categories of capacity planning for AD DS in terms of network traffic. The first is replication traffic that traverses between domain controllers and is covered thoroughly in the reference [Active Directory Replication Traffic](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/bb742457(v=technet.10)) and is still relevant to current versions of AD DS. The second is the intrasite client-to-server traffic. One of the simpler scenarios to plan for, intrasite traffic predominantly receives small requests from clients relative to the large amounts of data sent back to the clients. 100 MB will generally be adequate in environments up to 5,000 users per server, in a site. Using a 1 GB network adapter and Receive Side Scaling (RSS) support is recommended for anything above 5,000 users. To validate this scenario, particularly in the case of server consolidation scenarios, look at Network Interface(\*)\Bytes/sec across all the DCs in a site, add them together, and divide by the target number of domain controllers to ensure that there is adequate capacity. The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (formerly known as Perfmon), making sure all of the counters are scaled the same.

Consider the following example (also known as, a really, really complex way to validate that the general rule is applicable to a specific environment). The following assumptions are made:

- The goal is to reduce the footprint to as few servers as possible. Ideally, one server will carry the load and an additional server is deployed for redundancy (*N* + 1 scenario). 
- In this scenario, the current network adapter supports only 100 MB and is in a switched environment.  
  The maximum target network bandwidth utilization is 60% in an N scenario (loss of a DC).
- Each server has about 10,000 clients connected to it.

Knowledge gained from the data in the chart (Network Interface(\*)\Bytes Sent/sec):

1. The business day starts ramping up around 5:30 and winds down at 7:00 PM.
1. The peak busiest period is from 8:00 AM to 8:15 AM, with greater than 25 Bytes sent/sec on the busiest DC.  
   > [!NOTE]
   > All performance data is historical. So the peak data point at 8:15 indicates the load from 8:00 to 8:15.
1. There are spikes before 4:00 AM, with more than 20 Bytes sent/sec on the busiest DC, which could indicate either load from different time zones or background infrastructure activity, such as backups. Since the peak at 8:00 AM exceeds this activity, it is not relevant.
1. There are five Domain Controllers in the site.
1. The max load is about 5.5 MB/s per DC, which represents 44% of the 100 MB connection. Using this data, it can be estimated that the total bandwidth needed between 8:00 AM and 8:15 AM is 28 MB/s.
   >[!NOTE]
   >Be careful with the fact that Network Interface sent/receive counters are in bytes and network bandwidth is measured in bits. 100 MB &divide; 8 = 12.5 MB, 1 GB &divide; 8 = 128 MB.
  
Conclusions:

1. This current environment does meet the N+1 level of fault tolerance at 60% target utilization. Taking one system offline will shift the bandwidth per server from about 5.5 MB/s (44%) to about 7 MB/s (56%).
1. Based on the previously stated goal of consolidating to one server, this both exceeds the maximum target utilization and theoretically the possible utilization of a 100 MB connection.
1. With a 1 GB connection this will represent 22% of the total capacity.
1. Under normal operating conditions in the *N* + 1 scenario, client load will be relatively evenly distributed at about 14 MB/s per server or 11% of total capacity.
1. To ensure that capacity is adequate during unavailability of a DC, the normal operating targets per server would be about 30% network utilization or 38 MB/s per server. Failover targets would be 60% network utilization or 72 MB/s per server.  
  
In short, the final deployment of systems must have a 1 GB network adapter and be connected to a network infrastructure that will support said load. A further note is that given the amount of network traffic generated, the CPU load from network communications can have a significant impact and limit the maximum scalability of AD DS. This same process can be used to estimate the amount of inbound communication to the DC. But given the predominance of outbound traffic relative to inbound traffic, it is an academic exercise for most environments. Ensuring hardware support for RSS is important in environments with greater than 5,000 users per server. For scenarios with high network traffic, balancing of interrupt load can be a bottleneck. This can be detected by Processor(\*)\% Interrupt Time being unevenly distributed across CPUs. RSS enabled NICs can mitigate this limitation and increase scalability.

> [!NOTE]
> A similar approach can be used to estimate the additional capacity necessary when consolidating data centers, or retiring a domain controller in a satellite location. Simply collect the outbound and inbound traffic to clients and that will be the amount of traffic that will now be present on the WAN links.  
>  
> In some cases, you might experience more traffic than expected because traffic is slower, such as when certificate checking fails to meet aggressive time-outs on the WAN. For this reason, WAN sizing and utilization should be an iterative, ongoing process.

### Virtualization considerations for network bandwidth

It is easy to make recommendations for a physical server: 1 GB for servers supporting greater than 5000 users. Once multiple guests start sharing an underlying virtual switch infrastructure, additional attention is necessary to ensure that the host has adequate network bandwidth to support all the guests on the system, and thus requires the additional rigor. This is nothing more than an extension of ensuring the network infrastructure into the host machine. This is regardless whether the network is inclusive of the domain controller running as a virtual machine guest on a host with the network traffic going over a virtual switch, or whether connected directly to a physical switch. The virtual switch is just one more component where the uplink needs to support the amount of data being transmitted. Thus the physical host physical network adapter linked to the switch should be able to support the DC load plus all other guests sharing the virtual switch connected to the physical network adapter.

### Calculation summary example

|System|Peak bandwidth|
|-|-|
DC 1|6.5 MB/s|
DC 2|6.25 MB/s|
|DC 3|6.25 MB/s|
|DC 4|5.75 MB/s|
|DC 5|4.75 MB/s|
|Total|28.5 MB/s|

**Recommended: 72 MB/s** (28.5 MB/s divided by 40%)

|Target system(s) count|Total bandwidth (from above)|
|-|-|
|2|28.5 MB/s|
|Resulting normal behavior|28.5 &divide; 2 = 14.25 MB/s|

As always, over time the assumption can be made that client load will increase and this growth should be planned for as best as possible. The recommended amount to plan for would allow for an estimated growth in network traffic of 50%.

## Storage

Planning storage constitutes two components:

- Capacity, or storage size
- Performance

A great amount of time and documentation is spent on planning capacity, leaving performance often completely overlooked. With current hardware costs, most environments are not large enough that either of these is actually a concern, and the recommendation to “put in as much RAM as the database size” usually covers the rest, though it may be overkill for satellite locations in larger environments.

### Sizing

#### Evaluating for storage

Compared to 13 years ago when Active Directory was introduced, a time when 4 GB and 9 GB drives were the most common drive sizes, sizing for Active Directory is not even a consideration for all but the largest environments. With the smallest available hard drive sizes in the 180 GB range, the entire operating system, SYSVOL, and NTDS.dit can easily fit on one drive. As such, it is recommended to deprecate heavy investment in this area.

The only recommendation for consideration is to ensure that 110% of the NTDS.dit size is available in order to enable defrag. Additionally, accommodations for growth over the life of the hardware should be made.

The first and most important consideration is evaluating how large the NTDS.dit and SYSVOL will be. These measurements will lead into sizing both fixed disk and RAM allocation. Due to the (relatively) low cost of these components, the math does not need to be rigorous and precise. Content about how to evaluate this for both existing and new environments can be found in the [Data Storage](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961771(v=technet.10)) series of articles. Specifically, refer to the following articles:

- **For existing environments &ndash;** The section titled “To activate logging of disk space that is freed by defragmentation” in the article [Storage Limits](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961769(v=technet.10)).
- **For new environments &ndash;** The article titled [Growth Estimates for Active Directory Users and Organizational Units](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961779(v=technet.10)).

  > [!NOTE]
  > The articles are based on data size estimates made at the time of the release of Active Directory in Windows 2000. Use object sizes that reflect the actual size of objects in your environment.

When reviewing existing environments with multiple domains, there may be variations in database sizes. Where this is true, use the smallest global catalog (GC) and non-GC sizes.  

The database size can vary between operating system versions. DCs that run earlier operating systems such as Windows Server 2003 has a smaller database size than a DC that runs a later operating system such as Windows Server 2008 R2, especially when features such Active Directory Recycle Bin or Credential Roaming are enabled.

> [!NOTE]  
  >
>- For new environments, notice that the estimates in Growth Estimates for Active Directory Users and Organizational Units indicate that 100,000 users (in the same domain) consume about 450 MB of space. Please note that the attributes populated can have a huge impact on the total amount. Attributes will be populated on many objects by both third-party and Microsoft products, including Microsoft Exchange Server and Lync. An evaluation based on the portfolio of the products in the environment is preferred, but the exercise of detailing out the math and testing for precise estimates for all but the largest environments may not actually be worth significant time and effort.
>- Ensure that 110% of the NTDS.dit size is available as free space in order to enable offline defrag, and plan for growth over a three to five year hardware lifespan. Given how cheap storage is, estimating storage at 300% the size of the DIT as storage allocation is safe to accommodate growth and the potential need for offline defrag.

#### Virtualization considerations for storage

In a scenario where multiple Virtual Hard Disk (VHD) files are being allocated on a single volume use a fixed sized disk of at least 210% (100% of the DIT + 110% free space) the size of the DIT to ensure that there is adequate space reserved.  

#### Calculation summary example

|Data collected from evaluation phase| |
|-|-|
|NTDS.dit size|35 GB|
|Modifier to allow for offline defrag|2.1|
|Total storage needed|73.5 GB|

> [!NOTE]
> This storage needed is in addition to the storage needed for SYSVOL, operating system, page file, temporary files, local cached data (such as installer files), and applications.

### Storage performance

#### Evaluating performance of storage

As the slowest component within any computer, storage can have the biggest adverse impact on client experience. For those environments large enough for which the RAM sizing recommendations are not feasible, the consequences of overlooking planning storage for performance can be devastating.  Also, the complexities and varieties of storage technology further increase the risk of failure as the relevance of long standing best practices of “put operating system, logs, and database” on separate physical disks is limited in it’s useful scenarios.  This is because the long standing best practice is based on the assumption that is that a “disk” is a dedicated spindle and this allowed I/O to be isolated.  This assumptions that make this true are no longer relevant with the introduction of:

- New storage types and virtualized and shared storage scenarios
- Shared spindles on a Storage Area Network (SAN)
- VHD file on a SAN or network-attached storage
- Solid State Drives
- Tiered storage architectures (i.e. SSD storage tier caching larger spindle based storage)

In short, the end goal of all storage performance efforts, regardless of underlying storage architecture and design, is to ensure the needed amount of Input/Output Operations per Second (IOPS) are available and that those IOPS happen within an acceptable time frame. This section covers how to evaluate what AD DS demands of the underlying storage in order to ensure storage solutions are properly designed.  Given the variability of today’s storage technologies, it is best to work with the storage vendors to ensure adequate IOPS.  For those scenarios with locally attached storage, reference the Appendix C for the basics in how to design traditional local storage scenarios.  This principals are generally applicable to more complex storage tiers and will also help in dialog with the vendors supporting backend storage solutions.

- Given the wide breadth of storage options available, it is recommended to engage the expertise of hardware support teams or vendors to ensure that the specific solution meets the needs of AD DS. The following numbers are the information that would be provided to the storage specialists.

For environments where the database is too large to be held in RAM, use the performance counters to determine how much I/O needs to be supported:

- LogicalDisk(\*)\Avg Disk sec/Read (for example, if NTDS.dit is stored on the D:/ drive, the full path would be LogicalDisk(D:)\Avg Disk sec/Read)
- LogicalDisk(\*)\Avg Disk sec/Write
- LogicalDisk(\*)\Avg Disk sec/Transfer
- LogicalDisk(\*)\Reads/sec
- LogicalDisk(\*)\Writes/sec
- LogicalDisk(\*)\Transfers/sec

These should be sampled in 15/30/60 minute intervals to benchmark the demands of the current environment.

#### Evaluating the results

> [!NOTE]
> The focus is on reads from the database as this is usually the most demanding component, the same logic can be applied to writes to the log file by substituting LogicalDisk(*\<NTDS Log\>*)\Avg Disk sec/Write and LogicalDisk(*\<NTDS Log\>*)\Writes/sec):
>  
> - LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read indicates whether or not the current storage is adequately sized.  If the results are roughly equal to the Disk Access Time for the disk type, LogicalDisk(*\<NTDS\>*)\Reads/sec is a valid measure.  Check the manufacturer specifications for the storage on the back end, but good ranges for LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read would roughly be:
>   - 7200 – 9 to 12.5 milliseconds (ms)
>   - 10,000 – 6 to 10 ms
>   - 15,000 – 4 to 6 ms  
>   - SSD – 1 to 3 ms  
>   - >[!NOTE]
>     >Recommendations exist stating that storage performance is degraded at 15ms to 20ms (depending on source).  The difference between the above values and the other guidance is that the above values are the normal operating range.  The other recommendations are troubleshooting guidance to identify when client experience significantly degrades and becomes noticeable.  Reference Appendix C for a deeper explanation.
> - LogicalDisk(*\<NTDS\>*)\Reads/sec is the amount of I/O that is being performed.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is within the optimal range for the backend storage, LogicalDisk(*\<NTDS\>*)\Reads/sec can be used directly to size the storage.
>   - If LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read is not within the optimal range for the backend storage, additional I/O is needed according to the following formula:
>     > (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read) &divide; (Physical Media Disk Access Time) &times; (LogicalDisk(*\<NTDS\>*)\Avg Disk sec/Read)

Considerations:

- Note that if the server is configured with a sub-optimal amount of RAM, these values will be inaccurate for planning purposes.  They will be erroneously on the high side and can still be used as a worst case scenario.
- Adding/Optimizing RAM specifically will drive a decrease in the amount of read I/O (LogicalDisk(*\<NTDS\>*)\Reads/Sec.  This means the storage solution may not have to be as robust as initially calculated.  Unfortunately, anything more specific than this general statement is environmentally dependent on client load and general guidance cannot be provided.  The best option is to adjust storage sizing after optimizing RAM.

#### Virtualization considerations for performance

Similar to all of the preceding virtualization discussions, the key here is to ensure that the underlying shared infrastructure can support the DC load plus the other resources using the underlying shared media and all pathways to it. This is true whether a physical domain controller is sharing the same underlying media on a SAN, NAS, or iSCSI infrastructure as other servers or applications, whether it is a guest using pass through access to a SAN, NAS, or iSCSI infrastructure that shares the underlying media, or if the guest is using a VHD file that resides on shared media locally or a SAN, NAS, or iSCSI infrastructure. The planning exercise is all about making sure that the underlying media can support the total load of all consumers.

Also, from a guest perspective, as there are additional code paths that must be traversed, there is a performance impact to having to go through a host to access any storage. Not surprisingly, storage performance testing indicates that the virtualizing has an impact on throughput that is subjective to the processor utilization of the host system (see Appendix A: CPU Sizing Criteria), which is obviously influenced by the resources of the host demanded by the guest. This contributes to the virtualization considerations regarding processing needs in a virtualized scenario (see [Virtualization considerations for processing](#virtualization-considerations-for-processing)).

Making this more complex is that there are a variety of different storage options that are available that all have different performance impacts. As a safe estimate when migrating from physical to virtual, use a multiplier of 1.10 to adjust for different storage options for virtualized guests on Hyper-V, such as pass-through storage, SCSI Adapter, or IDE. The adjustments that need to be made when transferring between the different storage scenarios are irrelevant as to whether the storage is local, SAN, NAS, or iSCSI.

#### Calculation summary example

Determining the amount of I/O needed for a healthy system under normal operating conditions:

- LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec during the peak period 15 minute period 
- To determine the amount of I/O needed for storage where the capacity of the underlying storage is exceeded:
  >*Needed IOPS* = (LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read &divide; *\<Target Avg Disk sec/Read\>*) &times; LogicalDisk(*\<NTDS Database Drive\>*)\Read/sec

|Counter|Value|
|-|-|
|Actual LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.02 seconds (20 milliseconds)|
|Target LogicalDisk(*\<NTDS Database Drive\>*)\Avg Disk sec/Transfer|.01 seconds|
|Multiplier for change in available IO|0.02 &divide; 0.01 = 2|  
  
|Value name|Value|
|-|-|
|LogicalDisk(*\<NTDS Database Drive\>*)\Transfers/sec|400|
|Multiplier for change in available IO|2|
|Total IOPS needed during peak period|800|

To determine the rate at which the cache is desired to be warmed:

- Determine the maximum acceptable time to warm the cache. It is either the amount of time that it should take to load the entire database from disk, or for scenarios where the entire database cannot be loaded in RAM, this would be the maximum time to fill RAM.
- Determine the size of the database, excluding white space.  For more information, see [Evaluating for storage](#evaluating-for-storage).  
- Divide the database size by 8 KB; that will be the total IOs necessary to load the database.
- Divide the total IOs by the number of seconds in the defined time frame.

Note that the rate calculated, while accurate, will not be exact because previously loaded pages are evicted if ESE is not configured to have a fixed cache size, and AD DS by default uses variable cache size.

|Data points to collect|Values
|-|-|
|Maximum acceptable time to warm|10 minutes (600 seconds)
|Database size|2 GB|  
  
|Calculation step|Formula|Result|
|-|-|-|
|Calculate size of database in pages|(2 GB &times; 1024 &times; 1024) = *Size of database in KB*|2,097,152 KB|
|Calculate number of pages in database|2,097,152 KB &divide; 8 KB = *Number of pages*|262,144 pages|
|Calculate IOPS necessary to fully warm the cache|262,144 pages &divide; 600 seconds = *IOPS needed*|437 IOPS|

## Processing

### Evaluating Active Directory processor usage

For most environments, after storage, RAM, and networking are properly tuned as described in the Planning section, managing the amount of processing capacity will be the component that deserves the most attention. There are two challenges in evaluating CPU capacity needed:

- Whether or not the applications in the environment are being well-behaved in a shared services infrastructure, and is discussed in the section titled “Tracking Expensive and Inefficient Searches” in the article Creating More Efficient Microsoft Active Directory-Enabled Applications or migrating away from down-level SAM calls to LDAP calls.  
  
  In larger environments, the reason this is important is that poorly coded applications can drive volatility in CPU load, “steal” an inordinate amount of CPU time from other applications, artificially drive up capacity needs, and unevenly distribute load against the DCs.  
- As AD DS is a distributed environment with a large variety of potential clients, estimating the expense of a “single client” is environmentally subjective due to usage patterns and the type or quantity of applications leveraging AD DS. In short, much like the networking section, for broad applicability, this is better approached from the perspective of evaluating the total capacity needed in the environment.

For existing environments, as storage sizing was discussed previously, the assumption is made that storage is now properly sized and thus the data regarding processor load is valid. To reiterate, it is critical to ensure that the bottleneck in the system is not the performance of the storage. When a bottleneck exists and the processor is waiting, there are idle states that will go away once the bottleneck is removed.  As processor wait states are removed, by definition, CPU utilization increases as it no longer has to wait on the data. Thus, collect performance counters “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” and “Process(lsass)\\% Processor Time”. The data in “Process(lsass)\\% Processor Time” will be artificially low if “Logical Disk(*\<NTDS Database Drive\>*)\Avg Disk sec/Read” exceeds 10 to 15 ms, which is a general threshold that Microsoft support uses for troubleshooting storage-related performance issues. As before, it is recommended that sample intervals be either 15, 30, or 60 minutes. Anything less will generally be too volatile for good measurements; anything greater will smooth out daily peeks excessively.

### Introduction

In order to plan capacity planning for domain controllers, processing power requires the most attention and understanding. When sizing systems to ensure maximum performance, there is always a component that is the bottleneck and in a properly sized Domain Controller this will be the processor.

Similar to the networking section where the demand of the environment is reviewed on a site-by-site basis, the same must be done for the compute capacity demanded. Unlike the networking section, where the available networking technologies far exceed the normal demand, pay more attention to sizing CPU capacity.  As any environment of even moderate size; anything over a few thousand concurrent users can put significant load on the CPU.

Unfortunately, due to the huge variability of client applications that leverage AD, a general estimate of users per CPU is woefully inapplicable to all environments. Specifically, the compute demands are subject to user behavior and application profile. Therefore, each environment needs to be individually sized.

#### Target site behavior profile

As mentioned previously, when planning capacity for an entire site, the goal is to target a design with an *N* + 1 capacity design, such that failure of one system during the peak period will allow for continuation of service at a reasonable level of quality. That means that in an “*N*” scenario, load across all the boxes should be less than 100% (better yet, less than 80%) during the peak periods.

Additionally, if the applications and clients in the site are using best practices for locating domain controllers (that is, using the [DsGetDcName function](http://msdn.microsoft.com/en-us/library/windows/desktop/ms675983(v=vs.85).aspx)), the clients should be relatively evenly distributed with minor transient spikes due to any number of factors.

In the next example, the following assumptions are made:

- Each of the five DCs in the site has four of CPUs.
- Total target CPU usage during business hours is 40% under normal operating conditions (“*N* + 1”) and 60% otherwise (“*N*”). During non-business hours, the target CPU usage is 80% because backup software and other maintenance are expected to consume all available resources.

![CPU usage chart](media/capacity-planning-considerations-cpu-chart.png)

Analyzing the data in the chart (Processor Information(_Total)\% Processor Utility) for each of the DCs:

- For the most part, the load is relatively evenly distributed which is what would be expected when clients use DC locator and have well written searches. 
- There are a number of five-minute spikes of 10%, with some as large as 20%. Generally, unless they cause the capacity plan target to be exceeded, investigating these is not worthwhile.  
- The peak period for all systems is between about 8:00 AM and 9:15 AM. With the smooth transition from about 5:00 AM through about 5:00 PM, this is generally indicative of the business cycle. The more randomized spikes of CPU usage on a box-by-box scenario between 5:00 PM and 4:00 AM would be outside of the capacity planning concerns.

  >[!NOTE]
  >On a well-managed system, said spikes are might be backup software running, full system antivirus scans, hardware or software inventory, software or patch deployment, and so on. Because they fall outside the peak user business cycle, the targets are not exceeded.

- As each system is about 40% and all systems have the same numbers of CPUs, should one fail or be taken offline, the remaining systems would run at an estimated 53% (System D's 40% load is evenly split and added to System A's and System C’s existing 40% load). For a number of reasons, this linear assumption is NOT perfectly accurate, but provides enough accuracy to gauge.  

  **Alternate scenario –** Two domain controllers running at 40%: One domain controller fails, estimated CPU on the remaining one would be an estimated 80%. This far exceeds the thresholds outlined above for capacity plan and also starts to severely limit the amount of head room for the 10% to 20% seen in the load profile above, which means that the spikes would drive the DC to 90% to 100% during the “*N*” scenario and definitely degrade responsiveness.

### Calculating CPU demands

The “Process\\% Processor Time” performance object counter sums the total amount of time that all of the threads of an application spend on the CPU and divides by the total amount of system time that has passed. The effect of this is that a multi-threaded application on a multi-CPU system can exceed 100% CPU time, and would be interpreted VERY differently than “Processor Information\\% Processor Utility”. In practice the “Process(lsass)\\% Processor Time” can be viewed as the count of CPUs running at 100% that are necessary to support the process’s demands. A value of 200% means that 2 CPUs, each at 100%, are needed to support the full AD DS load. Although a CPU running at 100% capacity is the most cost efficient from the perspective of money spent on CPUs and power and energy consumption, for a number of reasons detailed in Appendix A, better responsiveness on a multi-threaded system occurs when the system is not running at 100%.

To accommodate transient spikes in client load, it is recommended to target a peak period CPU of between 40% and 60% of system capacity. Working with the example above, that would mean that between 3.33 (60% target) and 5 (40% target) CPUs would be needed for the AD DS (lsass process) load. Additional capacity should be added in according to the demands of the base operating system and other agents required (such as antivirus, backup, monitoring, and so on). Although the impact of agents needs to be evaluated on a per environment basis, an estimate of between 5% and 10% of a single CPU can be made. In the current example, this would suggest that between 3.43 (60% target) and 5.1 (40% target) CPUs are necessary during peak periods.

The easiest way to do this is to use the “Stacked Area” view in Windows Reliability and Performance Monitor (perfmon), making sure all of the counters are scaled the same.

Assumptions:

- Goal is to reduce footprint to as few servers as possible. Ideally, one server would carry the load and an additional server added for redundancy (*N* + 1 scenario).

![Processor time chart for lsass process (over all processors)](media/capacity-planning-considerations-proc-time-chart.png)

Knowledge gained from the data in the chart (Process(lsass)\\% Processor Time):

- The business day starts ramping up around 7:00 and decreases at 5:00 PM.
- The peak busiest period is from 9:30 AM to 11:00 AM. 
  > [!NOTE]
  > All performance data is historical. The peak data point at 9:15 indicates the load from 9:00 to 9:15.
- There are spikes before 7:00 AM which could indicate either load from different time zones or background infrastructure activity, such as backups. Because the peak at 9:30 AM exceeds this activity, it is not relevant.
- There are three domain controllers in the site.

At maximum load, lsass consumes about 485% of one CPU, or 4.85 CPUs running at 100%. As per the math earlier, this means the site needs about 12.25 CPUs for AD DS. Add in the above suggestions of 5% to 10% for background processes and that means replacing the server today would need approximately 12.30 to 12.35 CPUs to support the same load. An environmental estimate for growth now needs to be factored in.

### When to tune LDAP weights

There are several scenarios where tuning [LdapSrvWeight](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc957291(v=technet.10)) should be considered. Within the context of capacity planning, this would be done when the application or user loads are not evenly balanced, or the underlying systems are not evenly balanced in terms of capability. Reasons to do so beyond capacity planning are outside of the scope of this article.

There are two common reasons to tune LDAP Weights:

- The PDC emulator is an example that affects every environment for which user or application load behavior is not evenly distributed. As certain tools and actions target the PDC emulator, such as the Group Policy management tools, second attempts in the case of authentication failures, trust establishment, and so on, CPU resources on the PDC emulator may be more heavily demanded than elsewhere in the site.
  - It is only useful to tune this if there is a noticeable difference in CPU utilization in order  to reduce the load on the PDC emulator and increase the load on other domain controllers will allow a more even distribution of load.
  - In this case, set LDAPSrvWeight between 50 and 75 for the PDC emulator.
- Servers with differing counts of CPUs (and speeds) in a site.  For example, say there are two eight-core servers and one four-core server.  The last server has half the processors of the other two servers.  This means that a well distributed client load will increase the average CPU load on the four-core box to roughly twice that of the eight-core boxes.
  - For example, the two eight-core boxes would be running at 40% and the four-core box would be running at 80%.
  - Also, consider the impact of loss of one eight-core box in this scenario, specifically the fact that the four-core box would now be overloaded.

#### Example 1 - PDC

| |Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|53%|57|40%|
|DC 2|33%|100|40%|
|DC 3|33%|100|40%|

The catch here is that if the PDC emulator role is transferred or seized, particularly to another domain controller in the site, there will be a dramatic increase on the new PDC emulator.

Using the example from the section [Target site behavior profile](#target-site-behavior-profile), an assumption was made that all three domain controllers in the site had four CPUs. What should happen, under normal conditions, if one of the domain controllers had eight CPUs? There would be two domain controllers at 40% utilization and one at 20% utilization. While this is not bad, there is an opportunity to balance the load a little bit better. Leverage LDAP weights to accomplish this.  An example scenario would be:

#### Example 2 - Differing CPU counts

| |Processor Information\\ %&nbsp;Processor Utility(_Total)<br />Utilization with defaults|New LdapSrvWeight|Estimated new utilization|
|-|-|-|-|
|4-CPU DC 1|40|100|30%|
|4-CPU DC 2|40|100|30%|
|8-CPU DC 3|20|200|30%|

Be very careful with these scenarios though. As can be seen above, the math looks really nice and pretty on paper. But throughout this article, planning for an “*N* + 1” scenario is of paramount importance. The impact of one DC going offline must be calculated for every scenario. In the immediately preceding scenario where the load distribution is even, in order to ensure a 60% load during an “*N*” scenario, with the load balanced evenly across all servers, the distribution will be fine as the ratios stay consistent. Looking at the PDC emulator tuning scenario, and in general any scenario where user or application load is unbalanced, the effect is very different:

| |Tuned Utilization|New LdapSrvWeight|Estimated New Utilization|
|-|-|-|-|
|DC 1 (PDC emulator)|40%|85|47%|
|DC 2|40%|100|53%|
|DC 3|40%|100|53%|

### Virtualization considerations for processing

There are two layers of capacity planning that need to be done in a virtualized environment. At the host level, similar to the identification of the business cycle outlined for the domain controller processing previously, thresholds during the peak period need to be identified. Because the underlying principals are the same for a host machine scheduling guest threads on the CPU as for getting AD DS threads on the CPU on a physical machine, the same goal of 40% to 60% on the underlying host are recommended. At the next layer, the guest layer, since the principals of thread scheduling have not changed, the goal within the guest remains in the 40% to 60% range.

In a direct mapped scenario, one guest per host, all the capacity planning done to this point needs to be added to the requirements (RAM, disk, network) of the underlying host operating system. In a shared host scenario, testing indicates that there is 10% impact on the efficiency of the underlying processors. That means if a site needs 10 CPUs at a target of 40%, the recommended amount of virtual CPUs to allocate across all the “*N*” guests would be 11. In a site with a mixed distribution of physical servers and virtual servers, the modifier only applies to the VMs. For example, if a site has an “*N* + 1” scenario, one physical or direct-mapped server with 10 CPUs would be about equivalent to one guest with 11 CPUs on a host, with 11 CPUs reserved for the domain controller.

Throughout the analysis and calculation of the CPU quantities necessary to support AD DS load, the numbers of CPUs that map to what can be purchased in terms physical hardware do not necessarily map cleanly. Virtualization eliminates the need to round up. Virtualization decreases the effort necessary to add compute capacity to a site, given the ease with which a CPU can be added to a VM. It does not eliminate the need to accurately evaluate the compute power needed so that the underlying hardware is available when additional CPUs need to be added to the guests.  As always, remember to plan and monitor for growth in demand.

### Calculation summary example

|System|Peak CPU|
|-|-|-|
|DC 1|120%|
|DC 2|147%|
|Dc 3|218%|
|Total CPU being used|485%|  
  
|Target system(s) count|Total bandwidth (from above)|
|-|-|
|CPUs needed at 40% target|4.85 &divide; .4 = 12.25|

Repeating due to the importance of this point, *remember to plan for growth*. Assuming 50% growth over the next three years, this environment will need 18.375 CPUs (12.25 &times; 1.5) at the three-year mark. An alternate plan would be to review after the first year and add in additional capacity as needed.

### Cross-trust client authentication load for NTLM

#### Evaluating cross-trust client authentication load

Many environments may have one or more domains connected by a trust. An authentication request for an identity in another domain that does not use Kerberos authentication needs to traverse a trust using the domain controller’s secure channel to another domain controller either in the destination domain or the next domain in the path to the destination domain. The number of concurrent calls using the secure channel that a domain controller can make to a domain controller in a trusted domain is controlled by a setting known as **MaxConcurrentAPI**. For domain controllers, ensuring that the secure channel can handle the amount of load is accomplished by one of two approaches: tuning **MaxConcurrentAPI** or, within a forest, creating shortcut trusts. To gauge the volume of traffic across an individual trust, refer to [How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](https://support.microsoft.com/kb/2688798).

During data collection, this, as with all the other scenarios, must be collected during the peak busy periods of the day for the data to be useful.

> [!NOTE]
> Intraforest and interforest scenarios may cause the authentication to traverse multiple trusts and each stage would need to be tuned.

#### Planning

There are a number of applications that use NTLM authentication by default, or use it in a certain configuration scenario. Application servers grow in capacity and service an increasing number of active clients. There is also a trend that clients keep sessions open for a limited time and rather reconnect on a regular basis (such as email pull sync). Another common example for high NTLM load is web proxy servers that require authentication for Internet access.

These applications can cause a significant load for NTLM authentication, which can put significant stress on the DCs, especially when users and resources are in different domains.

There are multiple approaches to managing cross-trust load, which in practice are used in conjunction rather than in an exclusive either/or scenario. The possible options are:

- Reduce cross-trust client authentication by locating the services that a user consumes in the same domain that the user is resident in.
- Increase the number of secure-channels available. This is relevant to intraforest and cross-forest traffic and are known as shortcut trusts.
- Tune the default settings for **MaxConcurrentAPI**.

For tuning **MaxConcurrentAPI** on an existing server, the equation is:

> *New_MaxConcurrentApi_setting* &ge; (*semaphore_acquires* + *semaphore_time-outs*) &times; *average_semaphore_hold_time* &divide; *time_collection_length*

For more information, see [KB article 2688798: How to do performance tuning for NTLM authentication by using the MaxConcurrentApi setting](http://support.microsoft.com/kb/2688798).

## Virtualization considerations

None, this is an operating system tuning setting.

### Calculation summary example

|Data type|Value|
|-|-|
|Semaphore Acquires (Minimum)|6,161|
|Semaphore Acquires (Maximum)|6,762|
|Semaphore Timeouts|0|
|Average Semaphore Hold Time|0.012|
|Collection Duration (seconds)|1:11 minutes (71 seconds)|
|Formula (from KB 2688798)|((6762 &ndash; 6161) + 0) &times; 0.012 /|
|Minimum value for **MaxConcurrentAPI**|((6762 &ndash; 6161) + 0) &times; 0.012 &divide; 71 = .101|

For this system for this time period, the default values are acceptable.

## Monitoring for compliance with capacity planning goals

Throughout this article, it has been discussed that planning and scaling go towards utilization targets. Here is a summary chart of the recommended thresholds that must be monitored to ensure the systems are operating within adequate capacity thresholds. Keep in mind that these are not performance thresholds, but capacity planning thresholds. A server operating in excess of these thresholds will work, but is time to start validating that all the applications are well behaved. If said applications are well behaved, it is time to start evaluating hardware upgrades or other configuration changes.

|Category|Performance counter|Interval/Sampling|Target|Warning|
|-|-|-|-|-|
|Processor|Processor Information(_Total)\\% Processor Utility|60 min|40%|60%|
|RAM (Windows Server 2008 R2 またはそれ以前)|Memory\Available MB|< 100 MB|なし|< 100 MB|
|RAM (Windows Server 2012)|Memory\Long 用語の平均スタンバイ キャッシュ Lifetime(s)|30 分|テストする必要があります。|テストする必要があります。|
|ネットワーク|Network Interface(\*)\Bytes Sent/sec<br /><br />Network Interface(\*)\Bytes Received/sec|30 分|40%|60%|
|ストレージ|LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Read<br /><br />LogicalDisk( *\<NTDS Database Drive\>* )\Avg Disk sec/Write|60 分|10 ミリ秒|15 ミリ秒|
|AD サービス|Netlogon(\*)\Average Semaphore Hold Time|60 分|0|1 秒|

## <a name="appendix-a-cpu-sizing-criteria"></a>付録 A:CPU のサイズ設定基準

### <a name="definitions"></a>定義

**プロセッサ (マイクロプロセッサ) –** コンポーネントを読み取り、プログラムの命令を実行します。  

**CPU:** 中央処理装置  

**マルチコア プロセッサ-** 同じ integrated 回線上の複数の Cpu  

**マルチ CPU –** 同じ integrated 回線ではなく、複数の Cpu  

**論理プロセッサ-** オペレーティング システムの観点から、1 つの論理コンピューティング エンジン  

これは、ハイパー スレッドが含まれています。 マルチコア プロセッサ、または 1 つのコア プロセッサで 1 つのコア。  

現在のサーバー システムでは、複数のプロセッサ、複数のマルチコア プロセッサ、およびハイパー スレッディングがある、この情報は両方のシナリオをカバーする一般化します。 そのため、オペレーティング システムと利用可能なコンピューティング エンジンのアプリケーションの観点を表しているため、用語の論理プロセッサが使用されます。

### <a name="thread-level-parallelism"></a>スレッド レベルの並列処理

各スレッドは、各スレッドで独自のスタックと手順については、独立したタスク、です。 AD DS は、マルチ スレッドを使用して、利用可能なスレッドの数をチューニングできるため、[表示し、Ntdsutil.exe を使用して、Active Directory での LDAP ポリシーを設定する方法](http://support.microsoft.com/kb/315071)、複数の論理プロセッサにわたる拡大または縮小します。

### <a name="data-level-parallelism"></a>データ レベルの並列処理

これは、データの共有 (AD DS プロセスだけでも) の場合は 1 つのプロセス内で複数のスレッドと複数のプロセスで複数のスレッド (一般) が含まれます。 過剰な場合は、簡略化する問題である、つまりデータに対する変更が反映されるキャッシュ (l1 正規化、L2、L3) すべてのコアのすべてのさまざまなレベルで実行中のスレッドとスレッドを実行して、共有メモリを更新します。 命令の処理を続行するには、さまざまなすべてのメモリ ロケーションを一貫性のある起動するときに、書き込み操作中には、パフォーマンスが低下することができます。

### <a name="cpu-speed-vs-multiple-core-considerations"></a>CPU の速度と複数コアの考慮事項

一般則は高速の論理プロセッサは、一連の手順については、タスクの詳細については、同時に実行できる以上の論理プロセッサ手段中の処理に要する期間を短縮します。 これらの経験則は、シナリオは、共有メモリ、データのレベルの並列処理と複数のスレッドを管理するオーバーヘッドを待機してからデータをフェッチする場合の考慮事項と本質的に複雑になるように分解します。 これは、マルチコア システムでのスケーラビリティが線形理由もします。

これらの考慮事項では、以下の比喩を検討してください。 各スレッドが、コアとクロック速度をされている速度制限されている各レーンを個々 の車の中で、幹線道路を考えてみてください。

1. 1 つだけの車が高速道路を使用する場合は、2 つのレーンまたは 12 のレーンがある場合もかまいません。 車がのみ、速度制限で許可されている高速になります。
1. スレッドが必要なデータがすぐに使用できないことを想定しています。 道路のセグメントがシャット ダウン、類推となります。 1 つだけの車が高速道路を使用する場合は、速度の制限とは関係ありませんレーンを再び開くまで (メモリからデータをフェッチします)。
1. 車の台数を増やす、車の台数を管理するオーバーヘッドが増加します。 運転のエクスペリエンスを比較し、注意が必要な量、道路が実質的には、空 (など、深夜) トラフィックが負荷の高い (中間の午後、ラッシュ時間ありませんなど) の場合とします。 また、大きさを考慮注意の必要な 2 レーンの高速道路に動かす場合は、ドライバーに何を行っている気にするその他の 1 つだけのレーンでは、どのような多くの他のドライバーについて心配する必要があります、6 レーン幹線道路との比較を行っています。
   > [!NOTE]
   > 類推ラッシュ時間のシナリオの詳細については、次のセクションの拡張します。応答時間]、[システム Busyness がパフォーマンスに与える影響します。

その結果より高速なプロセッサについての詳細はアプリケーションの動作の場合は AD DS 環境では非常に固有であり、環境内でサーバーからサーバーをも異なりますに高主観的なものになります。 これは、が過度に正確には、記事の前半に参照が大きな投資しないと、計算での安全性の余白が含まれているためにです。 予算ドリブンに購買決定を行うときに、ことを 40% (または、環境に必要な数) でプロセッサの使用率の最適化、高速のプロセッサの購入を検討する前に最初に、発生をお勧めします。 多くのプロセッサ間で、増加の同期が直線的からより多くのプロセッサの真のメリットを削減 (2&times;プロセッサの数が 2 より小さい値を提供します&times;使用可能な追加のコンピューティング能力)。

> [!NOTE]
> アムダールの法則とグスタフソンの法則は、関連する概念は、ここには。

### <a name="response-timehow-the-system-busyness-impacts-performance"></a>応答時間]、[システム busyness がパフォーマンスに与える影響

キューの理論上は、待機している行 (キュー) の数学的な研究です。 キューの理論上は、使用率の法律は次の式で表されます。

*U* k = *B* &divide; *T*

場所*U* k は、使用率、 *B*ビジー時間と*T*は、システムが検出された合計時間です。 Windows のコンテキストに変換、つまり、100 ナノ秒 (ns) の数実行中の状態が 100 ナノ秒間隔の数が所定の時間間隔で使用可能で割った値に含まれる間隔のスレッド。 これは、ユーティリティのプロセッサの % を計算する式では正確に (参照[プロセッサ オブジェクト](https://docs.microsoft.com/previous-versions/ms804036(v=msdn.10))と[PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/previous-versions/windows/embedded/ms901169(v=msdn.10)))。

理論上はキューには、数式も用意されています。*N* = *U* k &divide; (1 &ndash; *U* k) の使用率に基づく待機している項目の数を見積もる ( *N*が、キューの長さ)。 使用率の全期間を通じてこのグラフを作成する、指定された CPU 負荷でプロセッサの取得するキューの長さが次の見積もりを提供します。

![キューの長さ](media/capacity-planning-considerations-queue-length.png)

50% の CPU 負荷後の平均が常に待機時間は、キュー内の他の 1 つの項目が見られる、著しく高速で約 70% の後に CPU 使用率の向上します。

このセクションでは以前に使用、運転の類推を返します。

- 「中間午後」のビジー状態の時間は、40 ~ 70% の範囲に、どこかに分類されます。 任意のレーンを取得する 1 つの機能が majorly 制限ならないように十分なトラフィックがあるし、されるように、高、中に別のドライバーが発生する可能性が「検索」道路上の他の自動車のギャップを安全に工数のレベルを必要としません。
- トラフィックが近づくラッシュ時間は、道路システム容量が 100% とアプローチをいずれかがわかります。 レーンを変更するは、車が閉じるようにしてこれを行うに増加の注意を実行する必要がありますので、非常に困難なことができますなります。

これが、長期的な平均容量を 40% で推定控えめに異常な急増の余裕をにより、読み込むには、数分の実行が不十分なコード化されたクエリ) などの一時的なスパイクと言うかどうか、または異常は (朝の負荷で急増一般の理由最初より後の日付、長い週末)。

上記のステートメントは、% プロセッサ時間の計算に使用率の法律が少し、容易にするため、一般的なリーダーの簡略化したものと一致していることです。 その数学的にはより厳格です。  
- 変換、 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))
  - *B* ="Idle"スレッドが論理プロセッサに費やした 100 ナノ秒間隔の数。 変更、"*X*"の変数、 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))計算
  - *T* = 指定された時間範囲内の 100 ナノ秒間隔の合計数。 変更、"*Y*"の変数、 [PERF_100NSEC_TIMER_INV](https://docs.microsoft.com/en-us/previous-versions/windows/embedded/ms901169(v=msdn.10))計算します。
  - *U* k「アイドル スレッド」または % で、論理プロセッサの使用率の割合を = アイドル時間。  
- 計算に対処します。
  - *U* k = 1 – % Processor Time
  - % Processor Time = 1 – *U* k
  - % Processor Time = 1 – *B* / *T*
  - % Processor Time = 1 – *X1* – *X0* / *Y1* – *Y0*

### <a name="applying-the-concepts-to-capacity-planning"></a>容量計画に概念を適用します。

上記の数値演算を行うことがあります、システムで必要な論理プロセッサの数に関する決定はそれほど複雑なようです。 これは、システムのサイズを変更する方法は、フォーカスが現在に基づいてターゲットの最大使用率を決定するため負荷とそれを入手するために必要な論理プロセッサの数を計算します。 さらに、論理プロセッサの速度はパフォーマンス、キャッシュの効率性、一貫性のメモリ要件、スレッドのスケジューリングと同期に大きな影響を持ち、まったくバランスの取れたクライアントの読み込み中にはすべてに大きな影響を与えますサーバー間ごとに変化するパフォーマンス。 コンピューティング能力の比較的低コスト、分析し、必要な Cpu の完璧な数値を決定しようとしています。 詳細について、学術的な問題よりも、ビジネス価値を提供してになります。

40% は絶対厳守の決まり要件ではありませんが、適切な開始します。 Active Directory のさまざまなコンシューマーには、さまざまなレベルの応答性が必要です。 プロセッサへのアクセスのため、待機時間はクライアントのパフォーマンスに著しく影響しません、持続的な平均値、として率が 80% または 90% に環境を実行できるシナリオがかかることがあります。 RAM へのアクセスなど、システムの論理プロセッサよりもかなり遅くなりますのシステムで多くの領域があることを再反復処理、ディスク、およびネットワーク経由で応答を送信へのアクセスに重要です。 これらすべての項目は、連携してチューニングする必要があります。 例 :

- 多くのプロセッサを追加するディスクの制限は、90% を実行するシステムには大幅にパフォーマンスを向上させるは移動いない可能性があります。 システムの詳細な分析があってもされないプロセッサの I/O 完了を待機しているため、スレッドの多くがあることはおそらく特定します。
- ディスクの制限の問題を解決する I/O の待機状態で待機状態で多くの時間を費やす前のスレッドが不要になったことを意味が可能性があるし、CPU 時間、前の使用率の 90% を意味するで複数の競合があります。例は、(これにより高いならないことができます) ために、100% に移動します。 両方のコンポーネントが連携してチューニングする必要があります。
  > [!NOTE]
  > プロセッサ Information(*)\\% プロセッサ ユーティリティは、"Turbo"モードのシステムとの 100% を超えることができます。  これは、CPU が短期間の評価済みのプロセッサの速度を超えています。  リファレンス CPU の製造元のドキュメントについての情報のカウンターの説明.  

仮想化されたゲストとして、メッセージ交換のドメイン コント ローラーに統合もシステム全体の使用率に関する考慮事項について説明します。 [応答時間]、[システム busyness がパフォーマンスに与える影響](#response-timehow-the-system-busyness-impacts-performance)ホストと仮想化されたシナリオでは、ゲストの両方に適用されます。 ゲストの 1 つだけ使用すると、ホストでその理由は、同等のパフォーマンスは、物理ハードウェア上の近くのドメイン コント ローラー (および一般に任意のシステム) ができます。 ホストに他のゲストを追加すると、前の説明は、プロセッサにアクセスを取得する待機時間を増やすことが、基になるホストの使用率が増加します。 つまり、論理プロセッサ使用率は、両方のホストとゲスト レベルで管理する必要があります。

物理ハードウェア、ゲストとして前の比喩を拡張する、高速道路 VM が (が高速バス、rider を先に直接移動する必要がある) バス analogized されます。 次の 4 つのシナリオを考えてみましょう。

- 業務時間外は、rider がほぼ空では、バスの取得およびはほぼ何も道路上のバスを取得します。 取り組むへのトラフィックがないと、rider が優れた簡単な乗り物、rider が代わりに駆動型であるかのように、高速取得できないだけです。 Rider の出張の時刻は、速度の制限によっても制限されます。
- 業務時間外バスがほぼ空が外出レーンのほとんどが終了すると、高速道路がまだ混雑しています。 混雑している外出がほぼ空バスは、rider です。 Rider には、配置先のバス内での多数の競合がない、トリップの合計時間は引き続き外部のトラフィックの残りの部分によって決まります。
- 高速道路とバスが混雑しているためラッシュ時間になります。 だけでなくは、乗車時間が長く、人は肩をショルダーと高速道路のほうがないため、非常に厄介は、オンとオフ、バスを取得します。 複数のバス (ゲストに論理プロセッサ) を追加してが収まる外出先でいずれかのより簡単にまたは、トリップが短縮されることは限りません。
- 最終的なシナリオでは、その可能性がありますが伸縮例え少し、ただし、バスは、完全なが外出先でないが輻輳します。 Rider では、問題がオンとオフ、バスを取得することがあります、中には、外出先で、バスは、後に、乗車が効率的なされます。 これは、複数バス (ゲストに論理プロセッサ) を追加してゲストのパフォーマンスを向上は、唯一のシナリオです。

そこからは、比較的簡単には、多くの 0% 使用率の間のシナリオと道路の 100% 使用率の低い状態と影響のレベルが異なるバスの 0% と 100% 活用の状態を推測します。

キューの使用量を超えると、同じ理論の妥当なスタートをホストとゲストの適切なターゲットとしての CPU 40% の上のプリンシパルを適用することです。

## <a name="appendix-b-considerations-regarding-different-processor-speeds-and-the-effect-of-processor-power-management-on-processor-speeds"></a>付録 B:別のプロセッサ速度、およびプロセッサ速度のプロセッサの電源管理の効果に関する考慮事項

プロセッサの選択項目のセクションでは、全体では、時間全体で、データが収集されて、100% のクロック速度、プロセッサが実行されていると、交換システムが同じ速度のプロセッサにあると想定が行われます。 実際には既定の電源プランのどこが false の場合、特に Windows Server 2008 R2 以降、されている両方の前提条件に関係なく**バランス**、保守的なアプローチは引き続き、方法論を意味します。 潜在的なエラー率が増加すると、中にのみ、プロセッサ速度の向上と安全性のマージンが増加します。

- たとえば、11.25 Cpu が要求されるたび、データの収集時に、プロセッサが半分の速度で実行されていた場合のシナリオより正確に見積もる場合があります 5.125 &divide; 2。
- クロック速度を 2 倍、一定時間内に発生する処理の 2 倍の容量をよう保証することはできません。 これは原因プロセッサ、RAM 待機に費やされた時間数または他のシステム コンポーネントには、同じままできます。 実際の効果は、高速のプロセッサがより多くのデータをフェッチで待機中にアイドル状態の時間の割合を費やす可能性があります。 ここでも、中、保守的な最小公分母を使用し、プロセッサ速度の間で直線的な比較を想定して精度の可能性がある場合は false レベルを計算しようとしてを避けることことをお勧めします。

または、代替ハードウェアでプロセッサの速度が現在のハードウェアよりも低い場合は、安全に比例した量で必要なプロセッサの推定量の増加がなります。 たとえばを 10 個のプロセッサがサイトでは、負荷を維持するために必要なし、3.3 Ghz で実行している現在のプロセッサと 2.6 ghz プロセッサの置換が実行されますこれは、速度が 21% 減少計算されます。 この場合、12 プロセッサは、推奨される量になります。

ただし、このように、容量管理のプロセッサ使用率のターゲットは変化しません。 プロセッサのクロック速度は負荷が高いシステムを実行して要求を負荷に基づいて動的に調整されるように、CPU 時間を費やしている上位のクロック速度状態で、40% 使用率が 100% である、最終的な目標を行うシナリオを生成します。ピーク時のクロック速度の状態。 何もよりも短くなって CPU の速度は遅くなります中にオフ ピーク時のシナリオと省電力が生成されます。

> [!NOTE]
> オプションは、プロセッサの電源管理を無効になります (電源プラン設定**高パフォーマンス**) データを収集中にします。 ターゲット サーバーの CPU 使用量のより正確な表現が目的です。

異なるプロセッサの見積もりを調整するには、安全では、プロセッサ速度の 2 倍と、実行できる処理の量が 2 倍に想定する、上記で説明した他のシステムのボトルネックを除外するために使用します。  今日では、プロセッサの内部アーキテクチャが異なるのに十分なプロセッサ、ゲージのデータの取得元よりも、異なるプロセッサを使用しての効果をより安全な方法は、標準的なパフォーマンス評価から SPECint_rate2006 ベンチマークを活用するにはCorporation.

1. 使用されていると、使用する計画をプロセッサの SPECint_rate2006 スコアを検索します。
    1. 標準のパフォーマンス評価 Corporation の web サイトで、次のように選択します。**結果**、強調表示**CPU2006**、選択と**SPECint_rate2006 のすべての結果を検索**します。
    1. **単純な要求**、たとえば、ターゲットのプロセッサに検索条件を入力**プロセッサ一致 E5-2630 (baselinetarget)** と**プロセッサ一致 E5-2650 (ベースライン)** .
    1. 使用するサーバーおよびプロセッサの構成が見つかりません (または完全一致が使用できない場合、何か閉じます) で値を確認し、**結果**と **# コア**列。
1. 判断には、修飾子は、次の式を使用します。
   >((*ターゲット プラットフォームのコアごとのスコア値*) &times; (*MHz コアごとのベースライン プラットフォーム*)) &divide; ((*ベースライン コアごとのスコアの値*) &times;(*MHz コアごとのターゲット プラットフォームの*))  

    上記の例を使用します。
   >(35.83 &times; 2000) &divide; (33.75 &times; 2300) = 0.92
1. 修飾子は、プロセッサの推定数を乗算します。  E5 2650 から移動するのには、上記の場合、E5 2630 プロセッサのプロセッサが計算 11.25 Cpu を乗算&times;0.92 = 10.35 プロセッサが必要です。

## <a name="appendix-c-fundamentals-regarding-the-operating-system-interacting-with-storage"></a>付録 C記憶域と対話するオペレーティング システムに関する基本事項

記載されている、キューの理論的概念[応答時間]、[システム busyness がパフォーマンスに与える影響](#response-timehow-the-system-busyness-impacts-performance)記憶域にも適用されます。 オペレーティング システム ハンドルの I/O がこれらの概念を適用する必要がどのようにの習熟度を持ちます。 Microsoft Windows オペレーティング システムで各物理ディスクの I/O 要求を保持するキューが作成されます。 ただし、物理ディスクで問題を明確にする必要があります。 配列コント ローラーと San は、1 つの物理ディスクのスピンドルにオペレーティング システムの集計を提示します。 さらに、配列コント ローラーと San 配列が 1 つのセットに複数のディスクを集約できし、さらに複数の物理ディスク (図を参照) として、オペレーティング システムに提示するは複数の「パーティション」に設定するこの配列に分割できます。

![スピンドルのブロック](media/capacity-planning-considerations-block-spindles.png)  

この図では 2 つのスピンドルがミラー化され、データ ストレージ (Data 1、Data 2) の論理領域に分割します。 これらの論理領域は、オペレーティング システムによって個別の物理ディスクとして表示されます。

これは、高混乱を招くことは、この付録で、さまざまなエンティティを識別するために、次の用語が使用します。

- **スピンドル –** サーバーに物理的にインストールされているデバイス。
- **配列 –** スピンドルのコレクションは、コント ローラーによって集計されます。
- **配列のパーティション –** 集計された配列のパーティション分割
- **LUN –** を参照するときに使用する、配列の San
- **ディスク –** オペレーティング システムが 1 つの物理ディスクを監視します。
- **パーティション –** 物理ディスクとして認識するオペレーティング システムの論理パーティション分割します。

### <a name="operating-system-architecture-considerations"></a>オペレーティング システムのアーキテクチャに関する考慮事項

オペレーティング システムが監視; するディスクごとに最初 In/First 先出し (FIFO) I/O キューを作成しますスピンドル、配列、または配列のパーティションをこのディスクを表すことがあります。 I/O の処理に関して、オペレーティング システムの観点から、複数のアクティブなキューのパフォーマンスは向上。 FIFO キューがシリアル化の順序で、記憶域サブシステムに発行されたすべての I/o を処理する必要がある、要求を受信しました。 スピンドル/配列で、オペレーティング システムで監視される各ディスクを関連付けることによって、オペレーティング システムようになりました、I/O のキュー管理ディスク、それによってをディスク間で不足している I/O リソースの競合を排除し、1 つの I/O 要求を分離するの各一意のセットディスク。 例外として、Windows Server 2008 が I/O の優先順位付け、概念を紹介し、「低」優先度を使用するように設計するアプリケーションは通常この順序どおり分類され、バック シートを実行します。 "Normal"を「低」優先度の既定の利用を特にコード化されたアプリケーション

### <a name="introducing-simple-storage-subsystems"></a>単純な記憶域サブシステムの概要

以降では、単純な例では、(、コンピューター内部の単一のハード ドライブ) コンポーネントの分析が与えられます。 これに分解、主要な記憶域サブシステムのコンポーネント、システムで構成されます。

- **1 –** 10,000 RPM 超高速 SCSI HD (超高速な SCSI が 20 MB/秒の転送速度)
- **1 –** SCSI バス (ケーブル)
- **1 –** 超高速な SCSI アダプター
- **1 –** 33 MHz PCI バスの 32 ビット

コンポーネントを特定すると、データの量は、システムを通過できますか、どの程度の I/O を処理することができますのアイデアを計算できます。 I/O の量と、システムを通過できるデータの量が関連付けられて、注意が同じではありません。 この関連付けは、ディスク I/O は、ランダムかシーケンシャルかどうかとブロックのサイズによって異なります。 (すべてのデータをブロックとしてディスクに書き込まれますが、ブロック サイズの異なるさまざまなアプリケーション)。コンポーネントに。

- **ハード ドライブ:** 平均 10,000 RPM のハード ドライブが 7 ミリ秒 (ms) シークの時刻と 3 ミリ秒のアクセス時刻。 シーク時間はプラッターを場所に移動する読み取り/書き込みヘッドにかかる平均時間。 アクセス時間は、読み取りまたはヘッドが、正しい位置になると、ディスクにデータの書き込みにかかる時間の平均です。 したがって、10,000 RPM HD 内のデータの一意のブロックの読み取りの平均時間を構成、シーク、合計で約 10 ミリ秒 (または.010 秒) のアクセスをごとのデータ ブロックします。

  ディスクのすべてのアクセスには、先頭、ディスク上の新しい場所への移動が必要とする場合、読み取り/書き込みの動作と呼びます「ランダムです」 したがって、すべての I/O がランダムな 10,000 RPM のハード ディスクを処理できる約 100/秒 (IOPS) I/O (数式は、I/O または 1000/10/10 ミリ秒未満で割った値の 1 秒あたり 1000 ミリ秒 = 100 IOPS)。

  また、ハード ディスク上の隣接するセクターからすべての I/O が発生したときにこれと呼びますシーケンシャル I/O。 シーケンシャル I/O を使用するため、最初の I/O が完了したら、読み取り/書き込みヘッド、HD に次のデータ ブロックを格納する場所の開始時のシーク時間にない。 10,000 RPM のハード ディスク、つまり約 333 を処理できる I/O/秒 (1 秒間の I/O あたり 3 ミリ秒で割った値は 1000 ミリ秒)。

  >[!NOTE]
  >この例では、通常 1 つの円柱のデータが保存されている、ディスク キャッシュは反映されません。 この場合、最初の I/O で 10 ミリ秒が必要ですし、ディスクが全体の円柱を読み取ります。 その他のすべてのシーケンシャル I/O は、キャッシュから満たされます。 その結果、ディスクのキャッシュでは、シーケンシャル I/O パフォーマンスを向上させる可能性があります。
  
  ここまでは、転送速度、ハード ドライブの非が関連します。 かどうか、ハード ドライブは、20 MB/秒超ワイドか、Ultra3 160 MB/秒、iops は、実際の量によって処理される 10,000 RPM HD は 100 ~ ランダムまたは順次 I/O の最大 300 です。 ドライブへの書き込みアプリケーションをサイズ変更ブロック ベース I/O ごとに取り込まれたデータの量は異なります。 たとえば、ブロック サイズが 8 KB である場合は、100 個の I/O 操作をからの読み取りまたは 800 KB の合計をハード ドライブに書き込みます。 ただし、ブロック サイズが 32 KB、100 の場合 I/O は読み取り/書き込み 3,200 KB 3.2 MB、ハード ドライブにします。 SCSI の転送速度は、転送されるデータの合計額を超える場合は、「高速化」の転送率のドライブを取得するが獲得何もできません。 比較については、次の表を参照してください。

  | |7200 RPM 9ms seek, 4ms access|10,000 RPM 7ms シーク、ミリ秒をアクセスします。|15,000 RPM 4ms シークでは、2 ミリ秒へのアクセスします。
  |-|-|-|-|
  |ランダム I/O|80|100|150|
  |シーケンシャル I/O|250|300|500|  
  
  |10,000 RPM のドライブ|8 KB のブロック サイズ (Active Directory Jet)|
  |-|-|
  |ランダム I/O|800 KB/秒|
  |シーケンシャル I/O|2400 KB/秒|

- **SCSI バック プレーン (バス) –** 理解する方法「SCSI バック プレーン (バス)」、または、このシナリオでは、リボン ケーブル、記憶域サブシステムのスループットの影響はブロック サイズの知識に依存します。 基本的に、質問がある場合場合、I/O は 8 KB ブロック単位で、I/O がバス ハンドルをできるはどの程度はでしょうか。 このシナリオでは、SCSI バスは、20 MB/秒、または 20480 KB/秒です。 20480 KB/秒の 8 KB のブロック単位で割った値には、最大約 2500 IOPS の SCSI バスでサポートされているが生成されます。

  >[!NOTE]
  >次の表の図は、例を表します。 接続されている記憶域デバイスでは最もは現在、PCI Express、多くのより高いスループットを提供するを使用します。  
  
  |I/O ブロック サイズごとの SCSI バスでサポートされています。|2 KB のブロック サイズ|8 KB のブロック サイズ (AD Jet) (SQL Server 7.0/SQL Server 2000)
  |-|-|-|
  |20 MB/秒|10,000|2,500|
  |40 MB/秒|20,000|5,000|
  |128 MB/秒|65,536|16,384|
  |320 MB/秒|160,000|40,000|

  スピンドルとしてように、どのような使用に関係なく、バスは決して、ボトルネック、提示されたシナリオでは、このグラフから判断と、最大値は 100 より上のしきい値のいずれかの I/O。

  >[!NOTE]
  >これは、SCSI バスが 100% の効率的であると仮定します。
  
- **SCSI アダプター –** これを処理できる I/O の量を決定するには、製造元の仕様をチェックする必要です。 適切なデバイスへの I/O 要求を送信するには、何らかの処理が必要です、したがって処理できる I/O の量は、SCSI アダプタ (または配列コント ローラー) に依存するプロセッサ。

  この例では、という前提で 1,000 I/O できる処理になります。

- **PCI バス –** これは、見落とされがちなコンポーネントです。 この例では、この操作がボトルネックになっています。ただし、システムはスケール アップ、ボトルネックになります。 リファレンスについては、33 Mhz で動作する 32 ビットの PCI バスは、133 MB/秒のデータを理論的に転送できます。 数式を次に示します。  
  > 32 ビット&divide;バイトあたり 8 ビット&times;33 MHz = 133 MB/秒。  

  理論上の制限があるに注意してください。実際には最大の約 50% 実際に達するが、特定のバーストのシナリオで短時間の 75% の効率性を取得できます。

  66 Mhz の 64 ビットの PCI バスは、理論上最大をサポートできます (64 ビット&divide;バイトあたり 8 ビット&times;66 Mhz) 528 MB/秒をさらに、= その他のデバイス (ネットワーク アダプター、2 番目の SCSI コント ローラーなど) が使用可能な帯域幅を減らす帯域幅を共有し、デバイスは限られたリソースの競合が発生します。

この記憶域サブシステムのコンポーネントの分析、スピンドルが制限要因の量を要求することができます、I/O とその結果、システムを通過できるデータの量。 8 KB 単位で 1 秒あたり 100 のランダム I/O は、このシナリオでは、AD DS、具体的には、2 番目の when あたり 800 KB の合計の Jet データベースへのアクセスします。 または、ログ ファイルを排他的に割り当てられているスピンドルの最大のスループットでは、次の制限事項が低下します。2400 KB (2.4 MB) の 1 秒あたりの合計の 8 KB 単位で 1 秒あたり 300 シーケンシャル I/O。

次に、単純な構成を分析すると、次の表に示します記憶域サブシステムのコンポーネントが変更または追加されると、ボトルネックの発生します。

|メモ|ボトルネックの分析|Disk|Bus|[アダプター]|PCI バス|
|-|-|-|-|-|-|
|これは、2 番目のディスクを追加した後、ドメイン コント ローラーの構成です。 ディスク構成は、800 kb/s でボトルネックを表します。|1 つのディスクの追加 (合計 = 2)<br /><br />I/O はランダム<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク|200 I/o の合計<br />800 KB/秒の合計です。| | | |
|7 つのディスクを追加した後、ディスク構成はまだ 3200 kb/s でボトルネックを表します。|**7 つのディスクの追加 (合計 = 8)**  <br /><br />I/O はランダム<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク|800 I/o の合計。<br />3200 KB/秒の合計| | | |
|シーケンシャル I/O を変更した後、ネットワーク アダプターがボトルネックになるため 1000 IOPS に制限されます。|7 つのディスクの追加 (合計 = 8)<br /><br />**I/O は順次**<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク| | |2400 I/O 秒書き込むことのできる読み取り/ディスク、コント ローラーが 1000 IOPS に制限されています| |
|10,000 IOPS をサポートする、SCSI アダプターを使用したネットワーク アダプターを交換した後、ボトルネックは、ディスク構成を返します。|7 つのディスクの追加 (合計 = 8)<br /><br />I/O はランダム<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク<br /><br />**SCSI アダプター (今すぐサポート 10,000 I/O) をアップグレードします。**|800 I/o の合計。<br />3,200 KB/秒の合計| | | |
|32 KB のブロック サイズを増やすと、バスがボトルネックになる 20 MB/秒だけがサポートされます。|7 つのディスクの追加 (合計 = 8)<br /><br />I/O はランダム<br /><br />**32 KB のブロック サイズ**<br /><br />10,000 RPM のハード ディスク| |800 I/o の合計。 25,600 KB/秒 (25 MB/秒) がディスクに読み取り/書き込みを指定できます。<br /><br />バスは、20 MB/秒のみがサポートされます。| | |
|ディスクはバスをアップグレードすると、ディスクの追加、ボトルネックのままです。|**13 のディスクを追加 (合計 = 14)**<br /><br />14 個のディスクを備えた 2 つ目の SCSI アダプターを追加します。<br /><br />I/O はランダム<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク<br /><br />**320 MB/秒の SCSI バスへのアップグレードします。**|2800 I/o<br /><br />11,200 KB/秒 (10.9 MB/秒)| | | |
|シーケンシャル I/O を変更した後、ディスクは、ボトルネックのままです。|13 のディスクを追加 (合計 = 14)<br /><br />14 個のディスクを備えた 2 つ目の SCSI アダプターを追加します。<br /><br />**I/O は順次**<br /><br />4 KB のブロック サイズ<br /><br />10,000 RPM のハード ディスク<br /><br />320 MB/秒の SCSI バスへのアップグレードします。|8,400 I/o<br /><br />33,600 KB\s<br /><br />(32.8 MB\s)| | | |
|高速なハード ドライブを追加すると、ディスクは、ボトルネックのままです。|13 のディスクを追加 (合計 = 14)<br /><br />14 個のディスクを備えた 2 つ目の SCSI アダプターを追加します。<br /><br />I/O は順次<br /><br />4 KB のブロック サイズ<br /><br />**15,000 RPM のハード ディスク**<br /><br />320 MB/秒の SCSI バスへのアップグレードします。|14,000 I/o<br /><br />56,000 KB/秒<br /><br />(54.7 MB/秒)| | | |
|32 KB のブロック サイズを増やすと、PCI バスは、ボトルネックになります。|13 のディスクを追加 (合計 = 14)<br /><br />14 個のディスクを備えた 2 つ目の SCSI アダプターを追加します。<br /><br />I/O は順次<br /><br />**32 KB のブロック サイズ**<br /><br />15,000 RPM のハード ディスク<br /><br />320 MB/秒の SCSI バスへのアップグレードします。| | | |14,000 I/o<br /><br />448,000 KB/秒<br /><br />(437 MB/秒) は、スピンドルに読み取り/書き込み制限です。<br /><br />PCI バスには、理論上最大 133 MB/秒 (75% が最良で効率的な) がサポートしています。|

### <a name="introducing-raid"></a>RAID の概要

配列コント ローラーが導入される; 記憶域サブシステムの性質が大幅に変更されません。SCSI アダプターは、計算だけ置き換えられます。 読み取りおよび (RAID 0 の場合、RAID 1 または RAID 5) などさまざまな配列のレベルを使用する場合、ディスクにデータの書き込みのコストは、変更とは。

RAID 0 で、データをすべての raid ディスクの設定にストライピングします。 つまり、読み取りまたは書き込み操作中に、データの一部はからプルまたは各ディスクは、同じ期間中に、システムを通過できるデータの量の増加にプッシュします。 そのため、秒の 1 つで (もう一度仮定 10,000 RPM のドライブ)、各スピンドルに 100 個の I/O 操作実行できます。 サポートされる I/O の合計金額が 100 倍 N スピンドル スピンドル (1 秒あたり 100 * N 生成 I/O) ごとに 1 秒あたりの I/O。

![D: の論理ドライブ](media/capacity-planning-considerations-logical-d-drive.png)

RAID 1 で (複製) の冗長性のスピンドルのペアの間でデータがミラー化します。 したがって、読み取り I/O 操作が実行されると、データのセット内のスピンドルの両方から読み取り可能です。 これにより、両方のディスクからの I/O 容量使用可能な読み取り操作中にします。 注意事項は、RAID 1 で操作の向上もパフォーマンスのメリットを記述します。 これは、同じデータの冗長性のために両方のドライブに書き込む必要があるためにです。 ならないなくなり、データの書き込みが発生すると同時に両方のスピンドル上のデータを複製する両方のスピンドルが占有されるためが書き込み I/O 操作は基本的に 2 つの読み取り操作が発生を防ぎます。 そのため、すべての書き込み I/O コスト 2 つの読み取り I/O。 発生している I/O 操作の合計数を決定するには、その情報からは、数式を作成できます。  

> *読み取り I/O* + 2 &times; *書き込み I/O* = *消費される使用可能なディスク I/O の合計*  

書き込みの読み取りの割合とスピンドルの数がわかったら、次の式は配列でサポートされる最大 I/O を識別するために上記の式から派生できます。  

> *スピンドルごとの最大 IOPS* &times; 2 スピンドル&times;[( *% の読み取り* +  *% が書き込み*) &divide; ( *% の読み取り*+ 2 &times; *% が書き込み*)] = *IOPS の合計*

RAID 1 + 0、読み取りと書き込みのコストに関する RAID 1 とまったく同じ動作です。 ただし、I/O はミラー化された各セットでストライピングようになりました。 If  

> *スピンドルごとの最大 IOPS* &times; 2 スピンドル&times;[( *% の読み取り* +  *% が書き込み*) &divide; ( *% の読み取り*+ 2 &times; *% が書き込み*)] = *I/O の合計*  

多重度のときに、RAID 1 セットで (*N*) 処理できる I/O の合計数になりますのセットをストライプ、RAID 1 N &times; RAID 1 セットあたりの i/o 率。  

> *N* &times; {*スピンドルごとの最大 IOPS* &times; 2 スピンドル&times;[( *% の読み取り* +  *% が書き込み*) &divide;( *% の読み取り*+ 2 &times; *% が書き込み*)]} = *IOPS の合計*

RAID 5 でとも呼ば*N* 1 RAID は、データにストライピングされます + *N*スピンドルとパリティ情報は「+ 1」のスピンドルに書き込まれます。 ただし、RAID 1 または 1 + 0 よりも書き込み I/O を実行するときに、RAID 5 ははるかに高くなります。 RAID 5 は、配列に書き込み I/O が送信されるたびに、次のプロセスを実行します。

1. 古いデータを読み取る
1. 古いパリティを読み取る
1. 新しいデータを書き込む
1. 新しいパリティを書き込む

必要な 4 つの I/O 操作が完了するため、オペレーティング システムによって、配列コント ローラーに送信されるすべての書き込み I/O 要求、書き込み要求の送信時間がかかり 4 回として 1 つの I/O の読み取りを完了します。 スピンドルが経験するには、オペレーティング システムの観点から I/O 要求を変換するための式を派生します。  

> *読み取り I/O* + 4 &times; *書き込み I/O の* = *I/O の合計*  

同様に、RAID 1 セットの読み取り先の書き込みとスピンドルの数の比率がわかっている場合、次の式から派生できるスピンドルの合計数は含まれません (注の配列でサポートされる最大 I/O を識別するために、上記の式e「ドライブ」失わパリティに)。  

> *スピンドルごとの IOPS* &times; (*スピンドル*– 1) &times; [( *% の読み取り* +  *% が書き込み*) &divide; ( *% の読み取り*は + 4 &times; *% が書き込み*)] = *IOPS の合計*

### <a name="introducing-sans"></a>San の概要

SAN は、環境に導入するときに、記憶域サブシステムの複雑さを拡張に説明した基本的な原則は変更しないでくださいのすべてのシステムの I/O 動作が SAN に接続するただしことを考慮する必要があります。 冗長性の追加の量は、内部または外部接続された記憶域上で SAN を使用する主な利点の 1 つは、容量計画する必要がアカウントのフォールト トレランスのニーズを考慮します。 ある またより多くのコンポーネントが導入されたを評価する必要があります。 SAN を分割して、コンポーネントに。

- SCSI またはファイバー チャネルのハード ドライブ
- ストレージ ユニットのチャネルのバック プレーン
- 記憶域ユニット
- 記憶域コント ローラー モジュール
- SAN スイッチの設定
- HBA(s)
- PCI バス

冗長性実現のための任意のシステムを設計するときに他のコンポーネントは障害の可能性を対応するために含まれています。 ときに非常に重要では容量計画、使用可能なリソースから冗長コンポーネントを除外します。 たとえば、SAN に 2 つのコント ローラー モジュールがある場合は、1 つのコント ローラー モジュールの I/O 容量はすべてのシステムで使用可能な合計の I/O スループットのために使用する必要があります。 これは、1 つのコント ローラーが失敗した場合、接続されているすべてのシステムで必要な全体の I/O 負荷が残っているコント ローラーによって処理される必要がありますという事実が原因です。 使用量ピーク期間のすべての容量計画が完了したら、使用可能なリソースに冗長コンポーネントを組み込むことがない必要があります、計画的なピーク使用率 (急激な増加や異常なシステムに対応するために、システムの鮮やかさを 80% を超えない動作)。 同様に、冗長な SAN スイッチ、記憶域ユニット、およびスピンドルされませんするのに組み込む必要が I/O 計算あるします。

ハード_ディスクの SCSI またはファイバー チャネルの動作を分析するときに、メソッドの説明に従って動作を分析の以前は変更されません。 特定の長所と短所の各プロトコルにはありますが、ディスクあたりの単位で制限要因は、ハード ドライブの機械的な制限です。

記憶域ユニット上のチャネルの分析は、SCSI バス、または (8 KB) などのブロック サイズで割った値帯域幅 (20 MB/秒) などに使用できるリソースを計算すると同じでは正確にします。 単純な前の例からの逸脱この場所は複数のチャネルの集計です。 たとえば、6 チャネルがある場合は、それぞれ 20 MB/秒の最大転送速度をサポートしている I/O とデータの転送が使用可能な量の合計は 100 MB/秒 (この情報が正しいはいない 120 MB/秒)。 ここでも、フォールト トレランスの主力チャンネル全体の損失が発生した場合、この計算では、システムが唯一の左側に機能している 5 つのチャネルにします。 したがって、障害発生時のパフォーマンス目標を満たすために継続させるには、すべての記憶域のチャネルのスループットの合計が超えないように 100 MB/秒 (すべてのチャネルでの負荷とフォールト トレランスが均等に分散を想定)。 アプリケーションの動作に依存では、I/O プロファイルにこの機能を有効です。 Active の Directory Jet I/O の場合、約標高 12,500 に関連付けるためこれは 1 秒あたりの I/O (100 MB/秒&divide;I/O あたり 8 KB)。

次に、コント ローラー モジュールの製造元の仕様を取得するが各モジュールがサポートできるスループットを理解するために必要です。 この例では、その SAN はそのサポート 7,500 I/O 各 2 つのコント ローラー モジュールが。 システムのスループットの合計は、冗長性が必要でない場合、15,000 IOPS にすることがあります。 失敗した場合の最大のスループットを計算するには、1 つのコント ローラーまたは 7,500 IOPS のスループットはという制限が。 このしきい値がすべての記憶域のチャネルでサポートできる 12,500 の IOPS (4 KB のブロック サイズを想定) 最大値よりも、したがって、分析のボトルネックは、現在します。 まだ計画のために計画する場合は、必要な最大 I/O になります。 10,400 I/O。

データは、コント ローラー モジュールを終了すると、1 GB/秒 (または 1 ギガ ビット/秒) に評価されたファイバー チャネル接続がそれと同じです。 1 GB/秒が 128 MB/秒に変換する他のメトリックでは、これを関連付け、(1 GB/秒&divide;8 ビット/バイト)。 これは、記憶域ユニット (100 MB/秒) 内のすべてのチャネルで帯域幅の合計を超える場合は、このシステムがボトルネックされません。 さらに、これは、1 つだけの 2 つのチャネル (追加 1 GB/秒のファイバー チャネル接続の冗長性確保されている)、残りの接続が必要なすべてのデータ転送を処理するために十分な容量をまだ 1 つの接続に失敗した場合。

データは、サーバーに送信は、SAN スイッチを通過ほとんどの場合は。 SAN スイッチは、受信の I/O 要求を処理する必要があり、転送を適切なポート、スイッチが処理できる I/O の量に制限、ただし、製造元の仕様が必要になりますこの制限には、対象を決定します。 たとえば、2 つのスイッチがある各スイッチは、10,000 IOPS を処理できる場合は、合計スループットは 20,000 IOPS になります。 スイッチは 1 つの失敗した場合、システムの合計スループットが 10,000 IOPS の場合フォールト トレランスの中の問題にならなければをもう一度。 通常の運用で使用率が 80% を超えないことが必要な 8000 以下を使用して I/O が対象になります。

最後に、サーバーにインストールされている HBA は、処理できる I/O の量に制限もがあります。 通常、冗長性のため、2 つ目の HBA がインストールされているが、最大 I/O 処理できるのスループットの合計を計算するときに、SAN スイッチと同様*N* &ndash; 1 Hba は、システムの最大限のスケーラビリティとは何です。

### <a name="caching-considerations"></a>キャッシュに関する考慮事項

キャッシュは、ストレージ システムで任意の時点の全体的なパフォーマンスに大きく影響するコンポーネントの 1 つです。 キャッシュのアルゴリズムについての詳細な分析が; この記事の範囲を超えていますただし、ディスク サブシステム上のキャッシュに関するいくつかの基本的なステートメントは、照明価値は。

- ほどは持続的な改善のシーケンシャル書き込み I/O のキャッシュ、I/O の大きなブロックに多数の小さな書き込み操作をバッファーし、少数の大きなブロック サイズのストレージにステージング解除できます。 これは、ランダム I/O の合計数と他の I/O の複数リソースの可用性を提供するため、順次 I/O の合計数が減少します。
- キャッシュでは、記憶域サブシステムの持続的書き込み I/O のスループットは向上しません。 スピンドルがある、データをコミットするまでバッファリングされますへの書き込みことのみできます。 記憶域サブシステム内のスピンドルの使用可能なすべての I/O が飽和状態に長期にわたって、ときに、キャッシュいっぱいになってしまいます。 急激な増加、または追加のスピンドル間の十分な時間、キャッシュを空にするには、キャッシュをフラッシュを許可するための十分な I/O を提供するために割り当てることが必要があります。

  サイズの大きいキャッシュは、詳細データをバッファーにのみ許可します。 つまり、彩度の長期間に対応することができます。

  正常に動作の記憶域サブシステムでのみデータをキャッシュに書き込む必要があるために、オペレーティング システムは書き込みパフォーマンスの向上を体験します。 基になるメディアは、I/O が飽和状態とキャッシュがいっぱい書き込みのパフォーマンスはディスクの速度に戻ります。

- キャッシュには、I/O が読み取られる、キャッシュが最も便利なシナリオは、ディスク上のデータが順番に格納されているし、キャッシュが先読み (、[次へ] のセクターが次に要求されたデータが含まれているという前提です) ことができます。
- 読み取るときに I/O がランダムにキャッシュをドライブ コント ローラーでは、ディスクから読み取ることができるデータの量の拡張機能を提供する可能性はありません。 任意の拡張機能は、オペレーティング システムまたはアプリケーション ベースのキャッシュ サイズがハードウェア ベースのキャッシュ サイズよりも大きい場合は存在しません。

  Active Directory の場合、キャッシュは RAM の量によってのみ制限されます。

### <a name="ssd-considerations"></a>SSD の考慮事項

SSDs は、ハード ディスクのスピンドルに基づくよりもまったく異なる動物です。 まだ、2 つの主な基準が残ります。「数の IOPS が処理できますか。」 「これらの IOPS の待機時間は何でしょうか。」 ハード ディスクのスピンドルに基づく Ssd の I/O の高いボリュームを処理できるし、比較低待機時間を持つことができます。 一般に、本稿執筆 Ssd はギガバイトあたりのコスト比較にまだコストがかかりますが、コストあたりの I/o の観点から非常に安価であり記憶域のパフォーマンスの観点から重要な検討事項があります。

注意点 :

- IOPS と待機時間の両方が製造元の設計に非常に主観的なと、場合によってはベースのテクノロジのスピンドルよりも低下パフォーマンス観測されました。 つまり、確認のうえ、ドライブのドライブの製造元の仕様を検証し、時系列を想定する方が。
- IOPS の種類は読み取り専用または書き込みにするかどうかに応じて数が非常に異なることができます。 AD DS サービスでは、一般に、主に読み取りに基づくされているなります他のアプリケーションのシナリオよりも低い影響を受ける。
- SSD のセルの摩耗は最終的に概念は、「書き込みの耐久性」の場合 – します。さまざまな製造元は、異なる方法で、この課題を扱います。 少なくともデータベース ドライブでは、主に読み取り I/O プロファイルは、データが揮発性が高いではないために、この問題の重要度をそのできます。

### <a name="summary"></a>Summary

記憶域について考慮する方法の 1 つは、家庭用のプラミング割り振ってくれとします。 データが格納されているメディアの IOPS、世帯のメインのドレインを想像してください。 (パイプでルート) などが目詰まりこれは、または場合 limited (は折りたたまれている、または小さすぎる)、バックアップが多すぎる水がいる場合、家族のすべてのシンクが (ゲストが多すぎます) を使用します。 これは、1 つまたは複数のシステムが、SAN/NAS/iSCSI を基になるのと同じメディア上の共有ストレージを利用している、共有環境に完全に似ています。 さまざまなシナリオを解決するのには、さまざまなアプローチを行えます。

- 折りたたまれた、またはサイズが小さすぎるドレインでは、スケールの完全な置換と修正プログラムが必要です。 これは、新しいハードウェアを追加するか、インフラストラクチャ全体で共有記憶域を使用して、システムの再配布するようになります。
- 通常、「かすれたり」パイプは、1 つ以上の問題が発生した問題の識別とそれらの問題の削除を意味します。 記憶域のシナリオでは、ストレージまたはシステム レベルのバックアップ、サーバー、およびピーク時同期の最適化ソフトウェアが実行中のすべての間で同期済みのウイルス対策スキャンこの可能性があります。

任意のプラミング設計では、複数の消費はメインのドレインにフィードです。 これらの消費または接合ポイントのいずれかを何も停止すると、その分岐点の背後にあるものだけはバックアップをポイントします。 記憶域のシナリオでは、オーバー ロードされたスイッチ (SAN または NAS/iSCSI シナリオ)、ドライバーの互換性の問題 (正しくないドライバー/HBA Firmware/storport.sys 組み合わせ)、またはバックアップとウイルス対策/最適化このできます。 「パイプ」記憶域が十分に大きいかどうかを確認するのには、IOPS と I/O のサイズを測定する必要があります。 各ジョイントに十分なことを確認してそれらを追加「パイプの直径します」。

## <a name="appendix-d---discussion-on-storage-troubleshooting---environments-where-providing-at-least-as-much-ram-as-the-database-size-is-not-a-viable-option"></a>付録 D - storage のトラブルシューティングについては、環境の場所を提供する多くの部分には少なくとも RAM ように、データベースのサイズは現実的ではありません。

これらの推奨事項が存在ストレージ テクノロジの変更を確保できるようにする理由を理解することをお勧めします。 これらの推奨事項は、2 つの理由が存在します。 最初は、パフォーマンスの問題 (ページング) オペレーティング システムのスピンドルをデータベースとプロファイルの I/O のパフォーマンスに影響しないように、IO の分離です。 2 つ目は、AD DS (およびほとんどのデータベース) のログ ファイルは、本質的にシーケンシャル スピンドル ベースのハード ドライブとキャッシュのオペレーティング システムとほぼよりランダムな I/O パターンと比較してシーケンシャル I/O を使用すると大きなパフォーマンス上の利点があります。AD DS の純粋なランダム I/O パターンはデータベースのドライブです。 別の物理ドライブにシーケンシャル I/O を分離することにより、スループットを増やすことができます。 今日の記憶域オプションによって提示される課題では、これらの推奨事項の背後にある基本的な前提条件が true で不要になったことです。 多くでは、iSCSI SAN、NAS、および仮想ディスクのイメージ ファイル、メディアが複数のホスト間で共有記憶域を基になる、つまり「IO の分離」と「シーケンシャル I/O 最適化」面の両方が完全に否定など、記憶域のシナリオを仮想化します。 実際にこれらのシナリオは、その他のホストが共有メディアへのアクセスには、ドメイン コント ローラーへの応答性が低下する可能性が複雑さの追加レイヤーを追加します。

記憶域のパフォーマンスを計画するには、考慮すべき 3 つのカテゴリ: コールド キャッシュの状態、キャッシュを使って、およびバックアップ/復元します。 コールド キャッシュの状態が最初に、ドメイン コント ローラーが再起動されるときなどのシナリオで発生しますまたは、Active Directory サービスの再起動し、RAM で Active Directory データはありません。 ウォーム キャッシュの状態とは、ドメイン コント ローラーが安定した状態では、データベースのキャッシュです。 これらは、非常にさまざまなパフォーマンスのプロファイルをいくし、データベース全体をキャッシュするための十分な RAM を持つに役立たないためにパフォーマンス キャッシュがコールドの場合に注意してください。 コールド キャッシュをウォーム次の例は、これら 2 つのシナリオのパフォーマンスの設計は、「スプリント」と"marathon"は、サーバーを実行するウォーム キャッシュを使用して 1 つ考えることができます。

コールド キャッシュとキャッシュのウォーム シナリオの両方での質問は、速度、ストレージ データを移動できますディスクからメモリになります。 キャッシュをウォームは、ここで、時間の経過と共にパフォーマンスが向上しより多くのクエリがデータを再利用、キャッシュ ヒット率が増えるとのディスクに移動する必要がある頻度を減らすシナリオです。 その結果しようとしてディスクのパフォーマンス低下の影響が小さくなります。 パフォーマンスの低下は、キャッシュをウォーム、許可されているサイズが最大値、システムに依存するまで拡張するのには待機中に一時的なのみです。 メッセージ交換では、データを取得して、ディスクから速度に簡略化することができ、、Active Directory で利用できる IOPS のシンプルな測定これは主観的な使用可能な IOPS を基になるストレージから。 計画の観点から通常業務時間外に発生して、DC の負荷を把握する主観的には、例外的な単位でキャッシュとバックアップ/復元のシナリオが発生するウォームため、一般的な推奨事項はありませんを除くこれらのアクティビティをスケジュールすることでピーク時以外の時間。

ほとんどのシナリオでの AD DS には主に 90 %read/10% 書き込みの比率は、通常、IO が読み取られます。 多くの場合、読み取り I/O をユーザー エクスペリエンスのボトルネックになる傾向があり、書き込みの IO エラーの原因書き込みパフォーマンスが低下します。 キャッシュは読み取り IO、するために最小限の特典を提供する傾向があります、NTDS.dit に I/O は主にランダムでさらに構成する重要のストレージは、I/O プロファイルを正しく読み取る。

通常の動作条件では、記憶域の計画の目標はディスクから返される AD DS からの要求の待機時間を最小限に抑えます。 本質的にはつまり、未処理の保留中の I/O 数が未満か、ディスクへの経路の数に相当します。 これを測定する方法のさまざまながあります。 パフォーマンスの監視シナリオ、一般的な推奨事項は、その論理ディスク ( *\<NTDS データベース ドライブ\>* ) \Avg ディスク読み取り秒数が 20 ミリ秒未満です。 目的の動作のしきい値は、可能であれば、記憶域の種類に応じて 2 ~ 6 ミリ秒 (.002 に.006 秒) の範囲として非常に低く、可能であればとして記憶域の速度の近くにである必要があります。

例:

![ストレージの待機時間のグラフ](media/capacity-planning-considerations-storage-latency.png)

グラフを分析するには。

- **左側の緑色の楕円**待機時間が 10 ミリ秒未満で変わらない。 負荷の増加は 800 IOPS 2400 IOPS にします。 これは、基になるストレージでの I/O 要求の処理速度を絶対 floor です。 これは、ストレージ ソリューションの詳細によって異なります。
- **右側 – バーガンディ楕円**スループットがデータ コレクションの末尾を緑色の円の終了からフラットである間、待機時間が増加し続けます。 これには、要求のボリュームが基になるストレージの物理的な制限を超えた場合に、長い時間の要求に費やす記憶域サブシステムに送信するを待機しているキューに格納されていますが示すことです。

この知識を適用するには。

- **大規模なグループのユーザー クエリ メンバーシップへの影響**I/O の量、ディスクから 1 MB のデータを読み取る必要があり、次のように評価されるのにかかるを前提としています。
  - Active Directory データベース ページが、サイズ 8 KB です。 
  - 128 のページの最小値でディスクから読み取られる必要があります。 
  - 何も仮定にキャッシュされて、これ以上を要します。 これをクライアントに返すためにディスクからデータを読み込むに 1.28 秒をフロア (10 ミリ秒)。 20 ミリ秒で記憶域のスループットは限界が昔とも推奨される最大値はのことをエンドユーザーに返すためにディスクからデータを取得する 2.5 秒かかります。  
- **どのような料金では、キャッシュがウォーム –** クライアントの負荷がこのストレージの例でスループットを最大にいると想定をして、2400 IOPS の速度でキャッシュをウォームは&times;IO ごとの 8 KB です。 または、2 つ目は、約 1 GB のデータベースに読み込む RAM 53 秒ごとあたり約 20 MB/秒。

> [!NOTE]
> 観察する短期間に通常は積極的にコンポーネントの読み取りまたはをシステムにバックアップされている場合や、AD DS がガベージ コレクションを実行している場合など、ディスクに書き込むときに、待機時間が上昇します。 これらの定期的なイベントを対応するために、計算上に追加の余裕を指定する必要があります。 これらのシナリオを通常の関数の影響を与えずに対応するために十分なスループットを提供することが目標です。

ように、どの程度の速度、キャッシュのウォームできます可能性がありますするストレージの設計に基づいて、物理的な制限があります。 受信は、キャッシュをウォーム何が基になるストレージを提供できるレートまでクライアントの要求。 "事前キャッシュの準備に"ピーク時にスクリプトを実行する実際のクライアントの要求で駆動型の読み込みに競合が提供されます。 キャッシュの準備に人為的な試行は負荷のないドメイン コント ローラーにアクセスするクライアントに関連するデータを仕様では、不足しているディスク リソースの競合を生成、されるため、クライアントが最初に必要なデータの提供に悪影響をします。
