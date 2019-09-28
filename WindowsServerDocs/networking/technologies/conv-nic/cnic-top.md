---
title: 収束ネットワークインターフェイスカード (NIC) の構成ガイダンス
description: 収束ネットワークインターフェイスカード (NIC) を使用すると、ホストパーティションの仮想 NIC (vNIC) を介して RDMA を公開できます。これにより、ホストパーティションサービスは、Hyper-v ゲストが TCP/IP トラフィックに使用しているのと同じ Nic でリモートダイレクトメモリアクセス (RDMA) にアクセスできるようになります。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: d791e0d51278d1f83f344250d38b1c7005c1a14a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355441"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>収束ネットワークインターフェイスカード \(NIC @ no__t 構成ガイダンス

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

収束ネットワークインターフェイスカード \(NIC @ no__t-1 を使用すると、ホストパーティションサービスが同じ Nic のリモートダイレクトメモリアクセス \(RDMA @ no__t にアクセスできるように、ホスト @ no__t-2partition 仮想 NIC \(vNIC @ no__t-4 を介して RDMA を公開できます。Hyper-v ゲストが TCP/IP トラフィックに使用している。

収束 NIC 機能の前に、Hyper-v 仮想スイッチにバインドされている Nic で帯域幅が使用可能であったとしても、RDMA を使用する必要がある管理 \(host パーティション @ no__t サービスでは、専用の RDMA @ no__t 対応 Nic を使用する必要がありました。

収束 NIC を使用すると、RDMA トラフィックとゲストトラフィックの2つのワークロード @no__t (RDMA とゲストトラフィック @ no__t) で同じ物理 Nic を共有でき、サーバーにインストールできる Nic の数を減らすことができます。

Windows Server 2016 の Hyper-v ホストと Hyper-v 仮想スイッチを使用して収束 NIC を展開すると、Hyper-v ホストの vNICs は、イーサネット @ no__t-0based の RDMA テクノロジを使用して rdma を使用してプロセスをホストする RDMA サービスを公開します。

>[!NOTE]
>収束 NIC テクノロジを使用するには、サーバーの認定されたネットワークアダプターで RDMA がサポートされている必要があります。

このガイドでは、サーバーに単一のネットワークアダプターがインストールされている展開用の2つの手順について説明します。これは、収束 NIC の基本的な展開です。また、サーバーに2つ以上のネットワークアダプターがインストールされています。これは、スイッチ埋め込みチーミングに対する収束 NIC の展開であり、RDMA @ no__t に対応したネットワークアダプターの @no__t 0SET @ no__t チームです。


## <a name="prerequisites"></a>前提条件

収束 NIC の基本およびデータセンターの展開の前提条件を次に示します。

>[!NOTE]
>提供される例については、Mellanox/3 Pro 40 Gbps イーサネットアダプターを使用しますが、この機能をサポートする Windows Server 認定 RDMA @ no__t 対応ネットワークアダプターを使用することもできます。 互換性のあるネットワークアダプターの詳細については、Windows Server Catalog のトピック「 [LAN カード](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)」を参照してください。

### <a name="basic-converged-nic-prerequisites"></a>基本的な収束 NIC の前提条件

基本的な集約型 NIC の構成について、このガイドの手順を実行するには、次のものが必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard edition を実行する2台のサーバー。
- 各サーバーに1つの RDMA 対応の認定済みネットワークアダプターがインストールされていること。
- 各サーバーにインストールされている hyper-v サーバーロール。

### <a name="datacenter-converged-nic-prerequisites"></a>データセンターの集約型 NIC の前提条件

データセンターの集約型 NIC の構成に関するこのガイドの手順を実行するには、次のものが必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard edition を実行する2台のサーバー。
- 各サーバーにインストールされている、RDMA 対応の2つのネットワークアダプター。
- 各サーバーにインストールされている hyper-v サーバーロール。
- スイッチ埋め込みチーミング \(SET @ no__t-1 (Hyper-v を含む環境で使用される代替の NIC チーミングソリューション、および Windows Server 2016 のソフトウェア定義ネットワーク (SDN) スタックについて理解している必要があります。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 詳細については、「[リモートダイレクトメモリアクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
- [単一のネットワークアダプターを使用した収束 NIC 構成](cnic-single.md)
- [収束 NIC チーミング NIC 構成](cnic-datacenter.md)
- [収束 NIC の物理スイッチ構成](cnic-app-switch-config.md)
- [収束 NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)

---