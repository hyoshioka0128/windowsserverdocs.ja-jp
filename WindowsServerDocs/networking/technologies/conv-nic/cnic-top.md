---
title: 収束ネットワーク インターフェイス カード (NIC) の構成ガイド
description: このトピックでは、集約型の NIC 構成ガイドの Windows Server 2016 の一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 42f7ef674da1754253ad72ae30ad505f29ba6a7d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="converged-network-interface-card-nic-configuration-guide"></a>収束ネットワーク インターフェイス カード \(NIC\) 構成ガイド

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

収束ネットワーク インターフェイス カード \(NIC\) を使用すると、パーティションのサービスをホストに Hyper-V ゲストは、TCP/IP のトラフィックを使用している同じ Nic でのリモート ダイレクト メモリ アクセス \(RDMA\) がアクセスできるように、host\ パーティション仮想 NIC \(vNIC\) を通じて RDMA を公開できます。

収束の NIC の機能の前に RDMA を使用したい management \(host partition\) のサービス必要がある、専用 RDMA\ に対応した Nic を使用する場合でも、帯域幅が Hyper-V 仮想スイッチにバインドされた Nic でご確認いただけます。

収束の NIC、2 つのワークロードで \ (管理ユーザーは RDMA とゲスト traffic\ の) は、サーバーで以下の Nic をインストールすることが、同じ物理 Nic を共有できます。

収束の NIC で Windows Server 2016 の Hyper-V ホストと Hyper-V 仮想スイッチを展開するときに Vnic を Hyper-V ホストでは、RDMA over を使用して任意の RDMA の Ethernet\ ベース テクノロジを介してホスト プロセスに RDMA サービスを公開します。

>[!NOTE]
>収束の NIC テクノロジを使用するには、サーバーで、認定済みのネットワーク アダプターで RDMA をサポートする必要があります。

このガイドには、手順については、収束の NIC の基本的な展開である単一のネットワーク アダプターがインストールされている場合、サーバーのある展開の 1 つの 2 つのセットが用意されています集約型の NIC の RDMA\ 対応ネットワーク アダプターのチームがスイッチ埋め込みチーミング \(SET\) 経由の展開には、サーバーがインストールされている場合、2 つ以上のネットワーク アダプターをある命令の別のセットです。

このガイドには、次のトピックが含まれています。

- [単一のネットワーク アダプターに収束の NIC 構成](cnic-single.md)
- [収束の NIC チーム化された NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型の NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)

## <a name="prerequisites"></a>前提条件

次に、収束の NIC の基本およびデータ センター展開の前提条件

>[!NOTE]
>このガイドの例については、Mellanox connectx-3 Pro 40 Gbps イーサネット アダプターを使用するがこの機能をサポートする RDMA\ 対応のネットワーク アダプターの認定、Windows Server のいずれかを使用することができます。 互換性のあるネットワーク アダプターに関する詳細については、トピックを参照して、Windows Server Catalog [LAN カード](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)します。

### <a name="basic-converged-nic-prerequisites"></a>収束の NIC の基本的な前提条件

収束の NIC の基本設定は、このガイドの手順を実行するには、次の操作が必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard エディションのいずれかを実行している 2 台のサーバー。
- 1 つ RDMA 対応では、各サーバーにインストールされているネットワーク アダプターを認定されています。
- Hyper-V サーバーの役割は、各サーバーにインストールする必要があります。

### <a name="datacenter-converged-nic-prerequisites"></a>データ センターの集約型の NIC の前提条件

データ センターの NIC の集約型の構成は、このガイドの手順を実行するには、次の操作が必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard エディションのいずれかを実行している 2 台のサーバー。
- 次の 2 つ RDMA 対応では、各サーバーにインストールされているネットワーク アダプターを認定されています。
- Hyper-V サーバーの役割は、各サーバーにインストールする必要があります。
- おく必要があります \(SET\)、スイッチ埋め込みチーミングを理解して Hyper-v ホストと、ソフトウェアによるネットワーク制御 (SDN) スタックを Windows Server 2016 に含まれる環境で使用できる、NIC チーミング ソリューションの代わりします。 セットは、Hyper-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

