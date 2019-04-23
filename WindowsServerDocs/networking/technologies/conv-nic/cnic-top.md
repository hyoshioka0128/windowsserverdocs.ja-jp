---
title: 収束ネットワーク インターフェイス カード (NIC) の構成ガイド
description: 収束ネットワーク インターフェイス カード (NIC) ホスト サービスのパーティション分割はリモート ダイレクト メモリ アクセス (RDMA)、HYPER-V ゲストが TCP/IP トラフィックを使用している同じ Nic 上でアクセスできるように、を通じてパーティションのホスト仮想 NIC (vNIC) RDMA を公開することができます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d7642338-9b33-4dce-8100-8b2c38d7127a
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: e9f5180285dda790e11cec543a109d0cb58edd2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838843"
---
# <a name="converged-network-interface-card-nic-configuration-guidance"></a>集約型のネットワーク インターフェイス カード\(NIC\)構成ガイド

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

収束ネットワーク インターフェイス カード\(NIC\)ホストから RDMA を公開できる\-仮想 NIC をパーティション分割\(vNIC\)ホスト サービスのパーティション分割は、リモート ダイレクト メモリ アクセスをアクセスできるように\(RDMA\) TCP/IP トラフィックを HYPER-V でゲストを使用している同じ Nic でします。

コンバージド NIC 機能を管理する前に\(パーティションがホスト\)RDMA を使用したいサービス専用の RDMA を使用する必要がある\-帯域幅は Hyper-v ホストにバインドされている Nic で利用可能だった場合でも対応の Nic仮想スイッチ。

収束の NIC、2 つのワークロードで\(RDMA とゲスト トラフィックの管理ユーザー\)サーバーの数の Nic をインストールすることができます、同じ物理 Nic を共有することができます。

Vnic で HYPER-V ホストがすべてイーサネット経由で RDMA を使用してホスト プロセスに RDMA のサービスを公開収束の NIC を Windows Server 2016 の HYPER-V ホストと HYPER-V 仮想スイッチを展開するときに\-RDMA テクノロジに基づいています。

>[!NOTE]
>コンバージド NIC テクノロジを使用するには、サーバーで、認定済みのネットワーク アダプターで RDMA をサポートする必要があります。

このガイドには、手順については、コンバージド NIC; の基本的な展開である単一のネットワーク アダプターがインストールされている、サーバーがある展開のいずれかの 2 つのセットが用意されていますコンバージド NIC の展開をスイッチ埋め込みチーミング経由では、サーバーがインストールされている場合、2 つ以上のネットワーク アダプターにある命令の別のセットと\(設定\)RDMA のチーム\-対応のネットワーク アダプター。


## <a name="prerequisites"></a>前提条件

次に、収束の NIC の Basic、およびデータ センターの展開の前提条件

>[!NOTE]
>提供された例で、Mellanox connectx-3 Pro 40 Gbps のイーサネット アダプターを使用しますが、RDMA の認定、Windows Server のいずれかを使用する\-この機能をサポートする対応のネットワーク アダプター。 互換性のあるネットワーク アダプターの詳細については、Windows Server Catalog トピックを参照してください。 [LAN カード](https://www.windowsservercatalog.com/results.aspx?&bCatID=1468&cpID=0&avc=85&ava=0&avt=0&avq=46&OR=1)します。

### <a name="basic-converged-nic-prerequisites"></a>収束の NIC の基本的な前提条件

収束の NIC の基本的な構成は、このガイドで、手順を実行するには、次の操作が必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard edition を実行する 2 つのサーバー。
- 1 つ rdma 対応、各サーバーにインストールされているネットワーク アダプターを認定します。
- 各サーバーにインストールされている HYPER-V サーバー ロール。

### <a name="datacenter-converged-nic-prerequisites"></a>データ センターの収束の NIC の前提条件

データ センターの収束の NIC の構成は、このガイドで、手順を実行するには、次の操作が必要です。

- Windows Server 2016 Datacenter edition または Windows Server 2016 Standard edition を実行する 2 つのサーバー。
- 2 つ rdma 対応には、各サーバーにインストールされているネットワーク アダプターが認定されています。
- 各サーバーにインストールされている HYPER-V サーバー ロール。
- スイッチ埋め込みチーミング理解しておく必要があります\(設定\)、代替 NIC チーミング ソリューションの Hyper-v ホストと、ソフトウェア定義ネットワーク (SDN) スタックを Windows Server 2016 に含まれる環境で使用します。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。 詳細については、次を参照してください。[リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)します。

## <a name="related-topics"></a>関連トピック
- [1 つのネットワーク アダプターに収束の NIC の構成](cnic-single.md)
- [収束の NIC チーミングされた NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型のない NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)

---