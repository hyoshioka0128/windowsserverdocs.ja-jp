---
title: Data Center Bridging (DCB)
description: このトピックでは、Windows Server 2016 のデータセンターブリッジングの概要について説明します。
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 646660c1371b592670737b7d7d208b62208bfec9
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993942"
---
# <a name="data-center-bridging-dcb"></a>データ センター ブリッジング\(DCB\)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、データセンターブリッジング DCB の概要について説明し \( \) ます。

DCB は、データセンター内の集約型ファブリックを有効にする米国国立電気技術研究所の IEEE 標準のスイートであり \( \) 、記憶域、データネットワーク、クラスターの \- プロセス間通信 \( IPC \) 、および管理トラフィックはすべて同じイーサネットネットワークインフラストラクチャを共有します。

>[!NOTE]
>このトピックに加えて、次の DCB のドキュメントも参照できます。
>
>- [Windows Server 2016 または Windows 10 で DCB をインストールする](dcb-install.md)
>- [データセンターブリッジング (DCB) の管理](dcb-manage.md)

DCB は \- 、特定の種類のネットワークトラフィックに対してハードウェアベースの帯域幅割り当てを提供し、優先順位ベースのフロー制御を使用して、イーサネットトランスポートの信頼性を強化し \- ます。

\-トラフィックがオペレーティングシステムをバイパスし、インターネットスモールコンピューターシステムインターフェイス \( iSCSI \) 、リモートダイレクトメモリアクセス \( RDMA \) Over Ethernet、またはイーサネット Fcoe 経由のファイバーチャネル \( \) をサポートする収束ネットワークアダプターにオフロードされる場合は、ハードウェアベースの帯域幅割り当てが不可欠です。

\-ファイバーチャネルなどの上位層プロトコルで、基になる転送が無損失であることが前提となっている場合は、優先順位ベースのフロー制御が不可欠です。

## <a name="dcb-protocols-and-management-options"></a>DCB のプロトコルと管理オプション

DCB は、次の一連のプロトコルで構成されています。

- \( \) 802.1 p と 802.1 q 標準を基にした、高度な転送サービスの作成– IEEE 802.1 qaz
- 優先順位フロー制御 \( PFS \) 、IEEE 802.1 qbb
- DCB Exchange Protocol \( dcbx \) 、IEEE 802.1 ab。 802.1 qaz standard で拡張されています。

DCBX プロトコルを使用すると、スイッチで DCB を構成して、Windows Server 2016 を実行しているコンピューターなどのエンドデバイスを自動的に構成することができます。

スイッチから DCB を管理する場合、Windows Server 2016 の機能として DCB をインストールする必要はありませんが、この方法にはいくつかの制限があります。

DCBX は、クラスサイズと PFC を使用できるようにホストネットワークアダプターに通知するだけなので、通常、Windows Server ホストは DCB をインストールして、トラフィックが送信クラスにマップされるようにする必要があります。

通常、Windows アプリケーションは、DCBX 交換に参加するように設計されていません。 このため、ホストはネットワークスイッチとは別に構成する必要がありますが、同じ設定を使用します。

スイッチから DCB を管理することを選択した場合でも、windows PowerShell コマンドを使用して Windows Server 2016 で構成を表示できます。

##  <a name="important-dcb-functionality"></a>重要な DCB 機能

DCB には、次のような機能があります。

1. DCB \- 対応のネットワークアダプターと DCB 対応のスイッチ間の相互運用性を提供 \- します。

2. ネットワークアダプターの優先順位に基づくフロー制御を有効にすることによって、Windows Server 2016 を実行しているコンピューターとその近隣ノードスイッチとの間で無損失のイーサネット転送を提供し \- ます。

3. \( \) 802.1 p traffic クラスの \( 優先度インジケーターによって区別される1つまたは複数のクラスで構成される場合があるため、トラフィック制御 tc に割合を割り当てることができます \) 。

4. サーバー管理者またはネットワーク管理者が、アプリケーションで使われるウェルノウン プロトコル、ウェルノウン TCP/UDP ポート、または NetworkDirect ポートに基づいて、特定のトラフィック クラスまたは優先度をアプリケーションに割り当てることのできる機能。

5. Windows Server 2016 Windows Management Instrumentation \( WMI \) および windows PowerShell を使用した DCB の管理を提供します。 詳細については、このトピックで後述する「 [Windows PowerShell Commands FOR DCB](#bkmk_wps) 」を参照してください。
    - [システムが提供する DCB コンポーネント](/windows-hardware/drivers/network/system-provided-dcb-components)
    - [NDIS のデータ センター ブリッジングの QoS 要件](/windows-hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. では、Windows Server 2016 グループポリシーによる DCB 管理が提供されます。

7. は、Windows Server 2016 のサービス品質 QoS ソリューションの共存をサポートしてい \( \) ます。

>[!NOTE]
>Rdma の集約型イーサネット roce バージョンを使用する前に \( \) 、DCB を有効にする必要があります。 インターネットワイドエリア RDMA プロトコルの iwarp ネットワークには必要ありません \( \) が、テストでは、すべてのイーサネット \- ベースの RDMA テクノロジが DCB で動作しやすくなっていると判断しました。 このため、iWARP RDMA のデプロイには DCB を使用することを検討してください。 詳細については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」を参照してください。

##  <a name="practical-applications-of-dcb"></a>DCB の実用的なアプリケーション

多く \( \) の組織では \( \) 、ストレージサービス用に大規模なファイバーチャネル FC ストレージエリアネットワーク SAN がインストールされています。 FC SAN を利用するには、サーバーに特殊なネットワーク アダプターが、また、ネットワークには FC スイッチが必要となります。 これらの組織は通常、イーサネットネットワークアダプターとスイッチも使用します。

ほとんどの場合、FC ハードウェアの方がイーサネットハードウェアよりも負荷が大きくなり、資本投資が大きくなります。 さらに、個別のイーサネットおよび FC SAN ネットワークアダプターとスイッチハードウェアの要件によって、データセンターに追加の領域、電力、冷却能力が必要になります。これにより、継続的な運用コストが増加します。

コストの観点からは、多くの組織は、FC テクノロジとイーサネットベースのハードウェアソリューションを統合して、 \- 記憶域とデータネットワークサービスの両方を提供することをお勧めします。

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>\-ストレージとデータネットワーク用のイーサネットベースの収束ファブリックに DCB を使用する

既に大規模な FC SAN を所有していて、FC テクノロジによる追加投資から移行する必要がある組織では、DCB を使用して、記憶域とデータネットワークの両方に対してイーサネットベースの集約型ファブリックを構築することができます。 DCB 収束ファブリックを使用すると、将来の総所有コストを削減 \( \) し、管理を簡素化できます。

記憶域ソリューションとして iSCSI を既に導入している場合、または導入を計画している場合、DCB は、 \- パフォーマンスの分離を確保するために iscsi トラフィックに対してハードウェアによる帯域幅の予約を提供できます。 他の独自のソリューションとは異なり、DCB は標準ベースである \- ため、異種ネットワーク環境において比較的簡単に展開および管理できます。

Windows Server 2016 \- ベースの DCB の実装では、複数の相手先ブランド供給メーカーによって集約型ファブリックソリューションが提供される場合に発生する可能性がある多くの問題を軽減 \( \) します。

複数の Oem によって提供される独自のソリューションの実装は相互運用できない場合があり、管理が困難な場合があり、通常はソフトウェアメンテナンススケジュールが異なります。

これに対して、Windows Server 2016 DCB は標準ベースであるため、 \- 異種ネットワークに DCB を展開して管理することができます。

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>DCB 用の Windows PowerShell コマンド

Windows Server 2016 と Windows Server 2012 R2 の両方に対応する DCB Windows PowerShell コマンドがあります。 Windows server 2016 では、Windows Server 2012 R2 のすべてのコマンドを使用できます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 DCB 用の Windows PowerShell コマンド

Windows Server 2016 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供しており、すべてのデータセンターブリッジング \( DCB Quality Of Service QoS 固有のコマンドレットについて説明して \) \( \) \- います。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [DcbQoS モジュール](/powershell/module/dcbqos/?view=win10-ps)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB 用の windows Server 2012 R2 Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供しており、すべてのデータセンターブリッジング \( DCB \) Quality of Service QoS 固有のコマンドレットについて説明し \( \) \- ます。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [Windows PowerShell のデータ センター ブリッジング (DCB) サービス品質 (QoS) コマンドレット](/powershell/module/dcbqos/?view=win10-ps&viewFallbackFrom=winserverr2-ps)