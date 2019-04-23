---
title: ネットワーク サブシステムのパフォーマンスの調整
description: このトピックでは、Windows Server 2016 は、ネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c0706c6ddbb678eacd3e609cfad3ccdda943fbd3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857413"
---
# <a name="network-subsystem-performance-tuning"></a>ネットワーク サブシステムのパフォーマンスの調整

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、ネットワーク サブシステムの概要については、このガイドの他のトピックへのリンクを使用できます。

>[!NOTE]
>このトピックに加え、このガイドの次のセクションではネットワーク デバイスのパフォーマンス チューニングの推奨事項とネットワーク スタックを提供します。
> - [ネットワーク アダプターを選択します。](net-sub-choose-nic.md)
> - [ネットワーク インターフェイスの順序を構成します。](net-sub-interface-metric.md)
> - [パフォーマンス チューニングのネットワーク アダプター](net-sub-performance-tuning-nics.md)
> - [ネットワーク関連のパフォーマンス カウンター](net-sub-performance-counters.md)
> - [ネットワーク ワークロードのパフォーマンス ツール](net-sub-performance-tools.md)

パフォーマンス チューニングの特にネットワーク集中型のワークロードの場合、ネットワーク サブシステムには、ネットワーク スタックとも呼ばれるネットワーク アーキテクチャの各レイヤーが含まれます。 これらの層は、次のセクションに大きく分類します。

1. **ネットワーク インターフェイス**します。 これは、ネットワーク スタックの最下位の層であり、ネットワーク アダプターと直接通信するネットワーク ドライバーが含まれています。

2. **Network Driver Interface Specification (NDIS)** します。 NDIS は、下にある、ドライバー、およびプロトコル スタックなど、上位層インターフェイスを公開します。
  
3. **プロトコル スタック**します。 プロトコル スタックは、TCP/IP や UDP/IP などのプロトコルを実装します。 これらの層は、それらの上に層のトランスポート レイヤー インターフェイスを公開します。
  
4. **システム ドライバー**します。 これらは、通常、インターフェイス ユーザー モード アプリケーションを公開する、トランスポートのデータ拡張機能 (TDX) や Winsock カーネル (WSK) インターフェイスを使用するクライアントです。 WSK インターフェイスは、Windows Server 2008 および Windows で導入された&reg;AFD.sys によって、Vista、およびが公開されます。 インターフェイスでは、ユーザー モードとカーネル モードの切り替えを排除することによってパフォーマンスが向上します。
  
5. **ユーザー モード アプリケーション**します。 これらは通常、Microsoft ソリューションまたはカスタム アプリケーションです。

次の表は、各レイヤーで実行されている項目の例を含む、ネットワーク スタックの各層の垂直方向の図を示します。  

![ネットワーク スタック レイヤー](../../media/Network-Subsystem/network-layers.jpg)

