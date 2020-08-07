---
title: ネットワークのサブシステムのパフォーマンス チューニング
description: このトピックは、Windows Server 2016 のネットワークサブシステムのパフォーマンスチューニングガイドに含まれています。
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.openlocfilehash: 40819f850788192f9057f8fd73c6c63f9d61dc0c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953908"
---
# <a name="network-subsystem-performance-tuning"></a>ネットワークのサブシステムのパフォーマンス チューニング

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークサブシステムの概要と、このガイドの他のトピックへのリンクについて説明します。

>[!NOTE]
>このトピックに加えて、このガイドの次のセクションでは、ネットワークデバイスとネットワークスタックのパフォーマンスチューニングに関する推奨事項について説明します。
> - [ネットワークアダプターの選択](net-sub-choose-nic.md)
> - [ネットワークインターフェイスの順序を構成する](net-sub-interface-metric.md)
> - [ネットワークアダプターのパフォーマンスチューニング](net-sub-performance-tuning-nics.md)
> - [ネットワーク関連のパフォーマンスカウンター](net-sub-performance-counters.md)
> - [ネットワーク ワークロードに関するパフォーマンス ツール](net-sub-performance-tools.md)

ネットワークサブシステムのパフォーマンスチューニング (特にネットワーク集中型のワークロードの場合) には、ネットワークスタックとも呼ばれるネットワークアーキテクチャの各層が関係します。 これらのレイヤーは、次のセクションに広範囲に分かれています。

1. **ネットワークインターフェイス**。 これはネットワークスタックの最下位層であり、ネットワークアダプターと直接通信するネットワークドライバーが含まれています。

2. **Network Driver Interface Specification (NDIS)**。 NDIS は、その下にあるドライバーのインターフェイスと、プロトコルスタックなどの上位層のインターフェイスを公開します。

3. **プロトコルスタック**。 プロトコルスタックは、TCP/IP や UDP/IP などのプロトコルを実装します。 これらのレイヤーは、その上にあるレイヤーのトランスポート層インターフェイスを公開します。

4. **システムドライバー**。 これらは通常、トランスポートデータ拡張機能 (TDX) または Winsock カーネル (WSK) インターフェイスを使用して、インターフェイスをユーザーモードアプリケーションに公開するクライアントです。 WSK インターフェイスは、Windows Server 2008 および Windows Vista で導入され、 &reg; AFD.sys によって公開されています。 インターフェイスにより、ユーザーモードとカーネルモードの切り替えが不要になるため、パフォーマンスが向上します。

5. **ユーザーモードアプリケーション**。 これらは通常、Microsoft ソリューションまたはカスタムアプリケーションです。

次の表は、各レイヤーで実行される項目の例を含む、ネットワークスタックのレイヤーを示しています。

![ネットワークスタックレイヤー](../../media/Network-Subsystem/network-layers.jpg)

