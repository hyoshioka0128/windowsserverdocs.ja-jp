---
title: ネットワーク サブシステムのパフォーマンス チューニング
description: このトピックは、Windows Server 2016 のネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c7ef50335a6dcc7dc5187cc30ff1b2dc2c5cdfed
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-subsystem-performance-tuning"></a>ネットワーク サブシステムのパフォーマンス チューニング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ネットワーク サブシステムの概要については、このガイドでは、その他のトピックへのリンクについては、このトピックを使用できます。

>[!NOTE]
>このガイドの次のセクションでは、このトピックに加え、ネットワーク デバイスのパフォーマンス チューニングの推奨事項と、ネットワーク スタックを提供します。
> - [ネットワーク アダプターを選択します。](net-sub-choose-nic.md)
> - [ネットワーク インターフェイスの順序を構成します。](net-sub-interface-metric.md)
> - [パフォーマンス チューニングのネットワーク アダプター](net-sub-performance-tuning-nics.md)
> - [ネットワーク関連のパフォーマンス カウンター](net-sub-performance-counters.md)
> - [ネットワーク ワークロードに関するパフォーマンス ツール](net-sub-performance-tools.md)

パフォーマンス チューニング特に、ネットワーク負荷が高いワークロードの場合、ネットワーク サブシステムには、ネットワーク スタックとも呼ばれるネットワーク アーキテクチャの各層が含まれます。 これらの層は、次のセクションに広く分類されます。

1. **ネットワーク インターフェイス**します。 これは、ネットワーク スタックの最下位の層であり、ネットワーク アダプターと直接通信するネットワーク ドライバーが含まれています。

2. **ネットワーク ドライバー Interface Specification (NDIS)**します。 NDIS 下にある、ドライバー、およびなど、プロトコル スタック上にある、レイヤー インターフェイスを公開します。
  
3. **プロトコル スタック**します。 プロトコル スタックは、TCP/IP および UDP/IP などのプロトコルを実装します。 これらの層は、上位のレイヤーのトランスポート層のインターフェイスを公開します。
  
4. **システム ドライバー**します。 これらは、インターフェイス ユーザー モード アプリケーションを公開するトランスポート データ拡張機能 (TDX) または Winsock カーネル (WSK) インターフェイスを使用するクライアントでは通常です。 WSK インターフェイスは、Windows Server 2008 および Windows で導入された&reg;Vista、およびそれが AFD.sys によって公開されています。 インターフェイスは、ユーザー モードとカーネル モードの切り替えを排除することによって、パフォーマンスを向上させます。
  
5. **ユーザー モード アプリケーション**します。 これらは通常 Microsoft ソリューションやカスタム アプリケーションです。

次の表は、各レイヤーで実行されている項目の例を含む、ネットワーク スタックの各層の垂直方向の図を示します。  

![ネットワーク スタック レイヤー](../../media/Network-Subsystem/network-layers.jpg)

