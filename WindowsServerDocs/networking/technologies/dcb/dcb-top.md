---
title: データ センター ブリッジング (DCB)
description: Windows Server 2016 でのデータ センター ブリッジングの概要については、このトピックを使用できます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb488192a873743db27d9c1d09c5912bc810bb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834183"
---
# <a name="data-center-bridging-dcb"></a>データ センター ブリッジング\(DCB\)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、データ センター ブリッジングの概要については\(DCB\)します。

DCB は、一連の Institute の Electrical and Electronics Engineers \(IEEE\)ストレージ、ネットワーク、データのクラスター間、データ センターにおいてファブリックの集約を有効にする標準\-プロセス通信\(IPC\)、すべての管理トラフィックで同じイーサネット ネットワーク インフラストラクチャを共有するとします。

>[!NOTE]
>このトピックに加え、次の DCB ドキュメントは使用可能です
>
>- [Windows Server 2016 または Windows 10 での DCB をインストールします。](dcb-install.md)
>- [データ センター ブリッジング (DCB) の管理します。](dcb-manage.md)

DCB はハードウェア\-に特定の種類のネットワーク トラフィックの帯域幅の割り当てをベースし、優先度の使用でイーサネット トランスポートの信頼性を高めます\-ベースのフロー制御します。

ハードウェア\-トラフィックが、オペレーティング システムをバイパスし、Internet Small Computer System Interface をサポートする収束ネットワーク アダプターにオフロードされる場合は、ベースの帯域幅の割り当てが欠かせません\(iSCSI\)、リモート ダイレクト メモリ アクセス\(RDMA\) over Ethernet、または Fiber Channel over Ethernet \(FCoE\)します。

優先順位\-ベースのフロー制御が不可欠の場合は、ファイバー チャネルなどの上層のプロトコルには、下層の転送が前提としています。

## <a name="dcb-protocols-and-management-options"></a>DCB のプロトコル、および管理オプション

DCB は、次の一連のプロトコルで構成されます。 

- 転送サービスを強化\(ETS\) -IEEE 802.1 qaz、802.1 P、802.1 q 標準に組み込まれました。
- 優先度のフロー制御\(PFS\)、IEEE 802.1 qbb 
- DCB 交換プロトコル\(DCBX\)、IEEE 802.1AB、802.1 qaz 標準の拡張として。

DCBX プロトコルは Windows Server 2016 を実行しているコンピューターなど、エンド デバイスを自動的に構成し、スイッチで DCB を構成することができます。

スイッチで DCB を管理する場合は、このアプローチには、いくつかの制限が含まれています。 ただし、Windows Server 2016 の機能として、DCB をインストールする必要はありません。

DCBX はクラスのサイズを ETS と PFC の有効化のホスト ネットワーク アダプターに通知のみ、ため、ただし、Windows Server ホストは、通常必要 ETS クラスにトラフィックをマップに DCB がインストールされていることです。

Windows アプリケーションは通常限りません DCBX 交換に参加します。 このため、ホストする必要がありますは個別に構成を同じ設定が、ネットワーク スイッチから。

スイッチで DCB を管理する場合は、Windows PowerShell コマンドを使用して、構成で Windows Server 2016 も表示できます。

##  <a name="important-dcb-functionality"></a>DCB の重要な機能

DCB には、次のような機能があります。

1. DCB の間の相互運用性を提供します。\-対応のネットワーク アダプターと DCB\-対応のスイッチ。

2. 優先度を有効にして、Windows Server 2016 とその隣接するスイッチを実行しているコンピューターの間で無損失のイーサネット転送を提供します。\-ベースのネットワーク アダプターのフロー制御します。

3. トラフィック制御の帯域幅を割り当てる機能を提供します\(TC\)パーセント、802.1 p トラフィック クラスによって区別されるトラフィックの 1 つまたは複数のクラスの TC はで構成されます\(優先度\)。インジケーター。

4. サーバー管理者またはネットワーク管理者が、アプリケーションで使われるウェルノウン プロトコル、ウェルノウン TCP/UDP ポート、または NetworkDirect ポートに基づいて、特定のトラフィック クラスまたは優先度をアプリケーションに割り当てることのできる機能。

5. Windows Server 2016 の Windows Management Instrumentation による DCB 管理\(WMI\)と Windows PowerShell。 詳細については、セクションをご覧ください。 [DCB 用 Windows PowerShell コマンド](#bkmk_wps)、次のトピックに加えて、このトピックで後述します。
    - [システム指定の DCB コンポーネント](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [データ センター ブリッジングの NDIS QoS の要件](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Windows Server 2016 のグループ ポリシーによる DCB 管理を提供します。

7. Windows Server 2016 サービス品質の共存をサポートしている\(QoS\)ソリューション。

>[!NOTE]
>Over Converged Ethernet、RDMA を使用する前に\(RoCE\)バージョン RDMA の DCB を有効にする必要があります。 インターネット ワイド エリア RDMA プロトコルは必要ありません、 \(iWARP\)テスト ネットワークがあると判断されるすべてイーサネット\-RDMA テクノロジは、うまくが DCB をベースします。 このため、DCB を使用して、iWARP RDMA の展開を検討してください。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

##  <a name="practical-applications-of-dcb"></a>DCB の実際の適用

多くの組織がある大規模なファイバー チャネル\(FC\)記憶域エリア ネットワーク\(SAN\)ストレージ サービスをインストールします。 FC SAN を利用するには、サーバーに特殊なネットワーク アダプターが、また、ネットワークには FC スイッチが必要となります。 このような組織通常もイーサネット ネットワーク アダプターとスイッチを使用します。

ほとんどの場合、FC のハードウェアはイーサネットのハードウェアは、大規模な資本支出の結果よりもデプロイを大幅に高くします。 さらに、独立したイーサネットと FC SAN、ネットワーク アダプターとスイッチ ハードウェアの要件は、追加の領域、電力、冷却結果、追加の進行中の運用経費、データ センターの容量が必要です。

コストの観点からは、イーサネット、FC テクノロジに多くの組織にとって便利な\-ベースの記憶域とデータ ネットワーク サービスの両方を提供するハードウェア ソリューション。

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>DCB を使用して、イーサネットの\-ベースの記憶域やネットワークのデータの収束ファブリック

組織は、既に大規模な FC SAN をいるが、FC テクノロジで追加の投資から移行する場合は、DCB を使用すると、ビルド、イーサネット ベースの収束ファブリックの記憶域とデータ ネットワークの両方。 DCB の集中型ファブリックは、将来の総保有コストを削減できます\(TCO\)および管理を簡略化します。

DCB、記憶域ソリューションとして iSCSI ホスト側ユーザー既に採用しているかを採用する場合は、ハードウェアを提供できる\-帯域幅予約を iSCSI トラフィックにパフォーマンスの分離を支援します。 DCB は標準を他の独自技術のソリューションとは異なり、\-ベース、およびそのため、異種ネットワーク環境で展開および管理を比較的簡単です。

Windows Server 2016\-ベースの DCB 実装がファブリック ソリューションが複数の相手先ブランド供給によって提供される集約型のときに発生する問題の軽減\(Oem\)します。

複数の Oem から提供される独自技術のソリューションの実装と他のいずれかの相互運用可能性がありますできません、難しい可能性がある管理、および通常はさまざまなソフトウェア メンテナンス スケジュールになります。 

これに対し、Windows Server 2016 の DCB は、標準\-し、デプロイおよび異種ネットワークにおいて DCB を管理することができます。

## <a name="bkmk_wps"></a>DCB の Windows PowerShell コマンド

Windows Server 2016 と Windows Server 2012 R2 の両方の DCB Windows PowerShell コマンドもあります。 Windows Server 2016 での Windows Server 2012 R2 のすべてのコマンドを使用できます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2016 の Windows PowerShell のコマンド

Windows Server 2016 の次のトピックでは、すべてのデータ センター ブリッジングの Windows PowerShell コマンドレットの説明と構文を提供します。 \(DCB\)サービスの品質\(QoS\)\-固有コマンドレット。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2012 R2 の Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、すべてのデータ センター ブリッジングの Windows PowerShell コマンドレットの説明と構文を提供します。 \(DCB\)サービスの品質\(QoS\)\-固有コマンドレット。 コマンドレットの先頭の動詞に基づいて、アルファベット順に記載しています。

- [データ センター ブリッジング (DCB) サービスの品質 (QoS) コマンドレットでは、Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
