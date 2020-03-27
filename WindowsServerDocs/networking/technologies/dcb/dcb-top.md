---
title: データ センター ブリッジング (DCB)
description: このトピックでは、Windows Server 2016 のデータセンターブリッジングの概要について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5401f0409ce46e5b7a6da32e1e0a914581956279
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312747"
---
# <a name="data-center-bridging-dcb"></a>データセンターブリッジング \(DCB\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、データセンターブリッジング \(DCB\)の概要について説明します。

DCB は、IEEE\) 標準 \(IEEE 標準のセットであり、記憶域、データネットワーク、クラスター間\-通信 \(IPC\)、および管理トラフィックがすべて同じイーサネットネットワークインフラストラクチャを共有する、データセンター内の集約型ファブリックを有効にします。

>[!NOTE]
>このトピックに加えて、次の DCB のドキュメントも参照できます。
>
>- [Windows Server 2016 または Windows 10 で DCB をインストールする](dcb-install.md)
>- [データセンターブリッジング (DCB) の管理](dcb-manage.md)

DCB は、特定の種類のネットワークトラフィックに対してハードウェア\-ベースの帯域幅割り当てを提供し、優先順位\-ベースのフロー制御を使用してイーサネットトランスポートの信頼性を強化します。

トラフィックがオペレーティングシステムをバイパスし、インターネットのスモールコンピューターシステムインターフェイス \(iSCSI\)、リモートダイレクトメモリアクセス \(RDMA\) over Ethernet、またはイーサネット経由のファイバーチャネル \(FCoE\)をサポートする収束ネットワークアダプターにオフロードされる場合は、ハードウェア\-ベースの帯域幅割り当てが不可欠です。

ファイバーチャネルなどの上層のプロトコルで、基になる転送が無損失と想定されている場合は、優先順位\-ベースのフロー制御が不可欠です。

## <a name="dcb-protocols-and-management-options"></a>DCB のプロトコルと管理オプション

DCB は、次の一連のプロトコルで構成されています。 

- 802.1 P および 802.1 Q 標準に基づいている、強化された伝送サービス \(の\) – IEEE 802.1 Qaz
- PFS\)\(優先順位フロー制御、IEEE 802.1 Qbb 
- 802.1 Qaz standard で拡張された DCB Exchange プロトコル \(DCBX\)、IEEE 802.1 AB。

DCBX プロトコルを使用すると、スイッチで DCB を構成して、Windows Server 2016 を実行しているコンピューターなどのエンドデバイスを自動的に構成することができます。

スイッチから DCB を管理する場合、Windows Server 2016 の機能として DCB をインストールする必要はありませんが、この方法にはいくつかの制限があります。

DCBX は、クラスサイズと PFC を使用できるようにホストネットワークアダプターに通知するだけなので、通常、Windows Server ホストは DCB をインストールして、トラフィックが送信クラスにマップされるようにする必要があります。

通常、Windows アプリケーションは、DCBX 交換に参加するように設計されていません。 このため、ホストはネットワークスイッチとは別に構成する必要がありますが、同じ設定を使用します。

スイッチから DCB を管理することを選択した場合でも、windows PowerShell コマンドを使用して Windows Server 2016 で構成を表示できます。

##  <a name="important-dcb-functionality"></a>重要な DCB 機能

DCB には、次のような機能があります。

1. DCB\-対応のネットワークアダプターと DCB\-対応のスイッチ間の相互運用性を提供します。

2. Windows Server 2016 を実行しているコンピューターとその近隣スイッチとの間で無損失のイーサネット転送を実現するために、ネットワークアダプターで優先\-ベースのフロー制御を有効にします。

3. 802.1 p traffic クラス \(priority\) インジケーターによって区別される1つまたは複数のクラスで構成される場合がありますが、\(TC\) のトラフィック制御に帯域幅を割り当てることができます。

4. サーバー管理者またはネットワーク管理者が、アプリケーションで使われるウェルノウン プロトコル、ウェルノウン TCP/UDP ポート、または NetworkDirect ポートに基づいて、特定のトラフィック クラスまたは優先度をアプリケーションに割り当てることのできる機能。

5. では、Windows Server 2016 Windows Management Instrumentation \(WMI\) および Windows PowerShell を使用して DCB を管理できます。 詳細については、このトピックで後述する「 [Windows PowerShell Commands FOR DCB](#bkmk_wps) 」を参照してください。
    - [システム指定の DCB コンポーネント](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [データセンターブリッジングの NDIS QoS 要件](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. では、Windows Server 2016 グループポリシーによる DCB 管理が提供されます。

7. は、Windows Server 2016 のサービス品質 \(QoS\) ソリューションの共存をサポートしています。

>[!NOTE]
>Rdma の \(RoCE\) バージョンの RDMA を使用する前に、DCB を有効にする必要があります。 インターネットワイドエリア RDMA プロトコル \(iWARP\) ネットワークには必要ありませんが、テストでは、すべてのイーサネット\-ベースの RDMA テクノロジが DCB で機能していると判断しました。 このため、iWARP RDMA のデプロイには DCB を使用することを検討してください。 詳細については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」を参照してください。

##  <a name="practical-applications-of-dcb"></a>DCB の実用的なアプリケーション

多くの組織では、大規模なファイバーチャネル \(FC\) ストレージエリアネットワーク \(ストレージサービス用の SAN\) インストールがあります。 FC SAN を利用するには、サーバーに特殊なネットワーク アダプターが、また、ネットワークには FC スイッチが必要となります。 これらの組織は通常、イーサネットネットワークアダプターとスイッチも使用します。

ほとんどの場合、FC ハードウェアの方がイーサネットハードウェアよりも負荷が大きくなり、資本投資が大きくなります。 さらに、個別のイーサネットおよび FC SAN ネットワークアダプターとスイッチハードウェアの要件によって、データセンターに追加の領域、電力、冷却能力が必要になります。これにより、継続的な運用コストが増加します。

コストの観点からは、多くの組織は、FC テクノロジとイーサネット\-ベースのハードウェアソリューションを統合して、記憶域とデータネットワークサービスの両方を提供することをお勧めします。

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>ストレージおよびデータネットワーク用のイーサネット\-ベースの収束型ファブリックに対して DCB を使用する

既に大規模な FC SAN を所有していて、FC テクノロジによる追加投資から移行する必要がある組織では、DCB を使用して、記憶域とデータネットワークの両方に対してイーサネットベースの集約型ファブリックを構築することができます。 DCB 収束ファブリックを使用すると、\) TCO \(将来の総保有コストを削減し、管理を簡略化することができます。

記憶域ソリューションとして iSCSI を既に導入している場合、または導入を計画している場合、DCB は、パフォーマンスの分離を確保するために、iSCSI トラフィックに対してハードウェア\-支援による帯域幅の予約を提供できます。 他の独自のソリューションとは異なり、DCB は標準\-ベースであるため、異種ネットワーク環境では比較的簡単に展開および管理できます。

Windows Server 2016\-ベースの DCB の実装により、\(Oem\)の複数の相手先ブランド供給メーカーによって集約型ファブリックソリューションが提供されるときに発生する可能性がある多くの問題を軽減できます。

複数の Oem によって提供される独自のソリューションの実装は相互運用できない場合があり、管理が困難な場合があり、通常はソフトウェアメンテナンススケジュールが異なります。 

これに対して、Windows Server 2016 DCB は標準\-基づいているため、異種ネットワークに DCB を展開して管理することができます。

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>DCB 用の Windows PowerShell コマンド

Windows Server 2016 と Windows Server 2012 R2 の両方に対応する DCB Windows PowerShell コマンドがあります。 Windows server 2016 では、Windows Server 2012 R2 のすべてのコマンドを使用できます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 DCB 用の Windows PowerShell コマンド

Windows Server 2016 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供します。すべてのデータセンターのブリッジング \(DCB\) のサービス品質 \(QoS\)\-特定のコマンドレットを使用します。 コマンドレットは、それぞれの先頭の動詞に使用されているアルファベットの順に並んでいます。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB 用の windows Server 2012 R2 Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文を提供します。すべてのデータセンターのブリッジング \(DCB\) のサービス品質 \(QoS\)\-特定のコマンドレットを使用します。 コマンドレットは、それぞれの先頭の動詞に使用されているアルファベットの順に並んでいます。

- [Windows PowerShell のデータセンターブリッジング (DCB) のサービス品質 (QoS) コマンドレット](https://technet.microsoft.com/library/hh967440.aspx)
