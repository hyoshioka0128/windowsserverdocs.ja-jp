---
title: データ センター ブリッジング (DCB)
description: Windows Server 2016 でのデータ センター ブリッジングの概要については、このトピックの「を使用することができます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d465e855adc387d7136919ac11fbab56c792c34
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="data-center-bridging-dcb"></a>データ センター ブリッジング \(DCB\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックは、データ センター ブリッジング \(DCB\) に関する基本的な情報を使用できます。

DCB は、データ センターで、記憶域、データ ネットワーク、クラスター Inter\ プロセス通信 \(IPC\)、および管理のトラフィックはすべてが同じのイーサネット ネットワーク インフラストラクチャを共有するには、[ファブリックの集約を有効にする Institute of Electrical and Electronics Engineers の \(IEEE\) 標準のスイートです。

>[!NOTE]
>このトピックに加え、次の DCB ドキュメントは使用
>
>- [Windows Server 2016 または Windows 10 での DCB をインストールします。](dcb-install.md)
>- [データ センター ブリッジング (DCB) の管理します。](dcb-manage.md)

DCB は、特定の種類のネットワーク トラフィックを hardware\ ベースの帯域幅の割り当てを提供しの priority\ に基づくフロー制御でイーサネット トランスポートの信頼性が向上します。

トラフィックは、オペレーティング システムをバイパスし、可能性がありますをサポートする Internet Small Computer System Interface \(iSCSI\)、リモート ダイレクト メモリ アクセス \(RDMA\) over Ethernet、またはファイバー チャネル イーサネット \(FCoE\) 経由で、収束ネットワーク アダプターにオフロードされる場合、Hardware\ ベースの帯域幅の割り当てが不可欠です。

Priority\ に基づくフロー制御は、必須の場合は、ファイバー チャネルなどの上層のプロトコルには、ロスレス基になるトランスポートが前提としています。

## <a name="dcb-protocols-and-management-options"></a>DCB のプロトコルと管理オプション

DCB は、次のプロトコルのセットで構成されます。 

- 拡張伝送サービス \(ETS\) – IEEE 802.1 qaz、802.1 P および 802.1 q 標準をビルドします。
- 優先度のフロー制御 \(PFS\)、IEEE 802.1 qbb 
- DCB Exchange プロトコル \(DCBX\)、IEEE 802.1AB、として 802.1 qaz 標準に拡張します。

DCBX プロトコルでは、Windows Server 2016 を実行しているコンピューターなど、終端のデバイスを自動的に構成し、スイッチ、DCB を構成することができます。

スイッチで DCB を管理する場合は、必要はありません DCB を Windows Server 2016 での機能としてインストールするが、このアプローチには、いくつかの制限が含まれています。

DCBX クラス サイズの ETS と PFC の有効化のホスト ネットワーク アダプタを通知のみことができます、ため、Windows Server ホスト通常必要トラフィックは ETS クラスにマップされるように DCB がインストールされていることです。

Windows アプリケーションは通常限りません DCBX 交換に参加します。 このため、ホストする必要があります構成とは別に、ネットワーク スイッチからが同一の設定。

スイッチで DCB を管理する場合は、Windows PowerShell コマンドを使用して、構成 Windows Server 2016 で引き続き表示できます。

##  <a name="important-dcb-functionality"></a>DCB の重要な機能

DCB によって提供される機能をまとめた一覧を次に示します。

1. DCB\ 対応ネットワーク アダプターと DCB\ 対応のスイッチ間の相互運用性を提供します。

2. ネットワーク アダプターで priority\ に基づくフロー制御を有効にして、Windows Server 2016 とその近隣のスイッチを実行するコンピューター間でロスレス イーサネット転送を提供します。

3. トラフィック制御 \(TC\) に tc は通常、可能性があります 802.1p トラフィック クラス \(priority\) インジケーターが異なるトラフィックの 1 つまたは複数のクラスを成りますパーセンテージで帯域幅を割り当てることができるを提供します。

4. アプリケーションを特定のトラフィック クラスまたはれるウェルノウン プロトコル、よく知られている TCP または UDP ポート、またはそのアプリケーションで使われる NetworkDirect ポートに基づいて優先順位を割り当てるには、サーバー管理者またはネットワーク管理者を使用できます。

5. Windows Server 2016 Windows Management Instrumentation \(WMI\) と Windows PowerShell による DCB 管理を提供します。 詳細については、セクションを参照して[DCB 用の Windows PowerShell コマンド](#bkmk_wps)、次のトピックに加え、このトピックで後述します。
    - [システムが提供 DCB コンポーネント](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [データ センター ブリッジングの NDIS QoS 要件](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Windows Server 2016 のグループ ポリシーを使った DCB 管理を提供します。

7. Windows Server 2016 のサービスの品質 \(QoS\) ソリューションの共存をサポートしています。

>[!NOTE]
>RDMA の Converged Ethernet \(RoCE\) バージョン経由で任意の RDMA を使用する前に、DCB を有効にする必要があります。 インターネット ワイド エリア RDMA プロトコル \(iWARP\) ネットワークは必要ありません、テストが判別されましたすべて RDMA の Ethernet\ ベースのテクノロジが DCB でうまく機能します。 このため、DCB を使用して、iWARP RDMA の展開を検討してください。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

##  <a name="practical-applications-of-dcb"></a>DCB の実際の適用

多くの組織では、大規模なファイバー チャネル \(FC\) 記憶域エリア ネットワーク \(SAN\) インストール記憶域サービスがあります。 FC SAN では、サーバーおよびネットワークには FC スイッチ上の特殊なネットワーク アダプターが必要です。 通常も使用して、組織のイーサネット ネットワーク アダプターとスイッチ。

ほとんどの場合、FC のハードウェアはイーサネットのハードウェアは、大規模な設備投資が小さいの結果よりも展開に大幅に高額です。 さらに、独立したと FC SAN のイーサネット ネットワーク アダプターとスイッチ ハードウェアの要件は、追加の空き領域、電力、および運用コストを追加、継続的な結果データ センター内の容量を冷却が必要です。

コストの観点から、多くの組織の Ethernet\ ベースのハードウェア ソリューションを記憶域とデータ ネットワーク サービスの両方を提供すると、FC テクノロジをマージすることをお勧めします。

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>記憶域とデータ ネットワークの Ethernet\ ベースの収束ファブリックの DCB を使用します。

組織で既に大規模な FC san 移行はしたいもの、FC テクノロジにそれ以上投資から離れた場所は、DCB を使用すると、ビルドしたイーサネット ベースの収束ファブリック記憶域とデータ ネットワークの両方をします。 DCB の集中型ファブリックは、将来の総保有コストを削減できます \(TCO\) および管理を簡略化します。

ホスト側は既に採用している、またはを採用する場合は、DCB、記憶域ソリューションとして iSCSI は hardware\ による帯域幅予約を iSCSI トラフィックにパフォーマンスの分離を提供できます。 DCB は standards\ ベース - してしたがって比較的簡単に展開および管理ネットワーク異機種混在環境でその他の独自技術のソリューションとは異なりします。

Windows Server 2016\ ベースの DCB の実装は、多くのファブリック ソリューションが複数の相手先ブランド供給 \(OEMs\) によって提供される集約型のときに発生する問題を軽減します。

複数の Oem によって提供される独自技術のソリューションの実装が互いに相互運用されない、するが難しい場合があります、管理、さまざまなソフトウェアの保守スケジュールは通常します。 

これに対し、Windows Server 2016 の DCB standards\ ベースを展開し、異種ネットワークにおいて DCB を管理することができます。

## <a name="bkmk_wps"></a>DCB の Windows PowerShell コマンド

Windows Server 2016 および Windows Server 2012 R2 の両方の DCB の Windows PowerShell コマンドもあります。 Windows Server 2016 での Windows Server 2012 R2 のすべてのコマンドを使用することができます。

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB の Windows PowerShell コマンドを Windows Server 2016

Windows Server 2016 用の次のトピックでは、Windows PowerShell コマンドレットの説明と構文すべてのデータ センター ブリッジング \(DCB\) Quality of Service \ (QoS\) \-specific コマンドレット。 先頭のコマンドレットの動詞に基づいてアルファベット順でコマンドレットが一覧表示します。

- [DcbQoS モジュール](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB の Windows Server 2012 R2 の Windows PowerShell コマンド

Windows Server 2012 R2 の次のトピックでは、Windows PowerShell コマンドレットの説明と構文すべてのデータ センター ブリッジング \(DCB\) Quality of Service \ (QoS\) \-specific コマンドレット。 先頭のコマンドレットの動詞に基づいてアルファベット順でコマンドレットが一覧表示します。

- [データ センター ブリッジング (DCB) サービスの品質 (QoS) コマンドレットでは、Windows PowerShell](https://technet.microsoft.com/library/hh967440.aspx)
