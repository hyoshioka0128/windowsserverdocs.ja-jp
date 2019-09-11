---
title: MultiPoint Services のシステム パフォーマンスに影響を与える変数
description: MultiPoint Services のパフォーマンス情報
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f3e8875-1b5e-4789-b16c-d06d6e31f38e
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 23bde4a65e3bf41d8968d55bf9641ca6a44b7d96
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871490"
---
# <a name="variables-affecting-multipoint-services-system-performance"></a>MultiPoint Services のシステム パフォーマンスに影響を与える変数
MultiPoint サービス システムの全体的なパフォーマンスに影響を与える多くの変数があります。 システムの設計時にこれらを考慮することがあります。  
  
## <a name="usage"></a>使用方法  
  
-   **アプリケーション** 型と同時に、特にグラフィックを実行しているアプリケーション数\-高負荷またはメモリの負荷の高いアプリケーションは、システムの全体的なパフォーマンスに影響を与えます。 詳細については、次を参照してください。 [アプリケーションやインターネット コンテンツ](hardware-and-performance-recommendations.md#applications-and-internet-content)します。  
  
-   **インターネットの使用** マルチ メディア コンテンツまたはフルモーション ビデオを使用する web ページに、ユーザーを表示するかどうかを検討してください。 この種類のコンテンツは、多数のユーザーが同時に表示する場合、システムをオーバー ロードできます。  
  
    > [!NOTE]  
    > フルモーション ビデオをプロジェクトには、モニターを学生に各自の画面を射影する教師が許可されている MultiPoint Services で投影機能は設計されていません。 プロジェクションの機能は、プロシージャを表示するなどのデモンストレーションの目的で設計されています。  
  
-   **高速デバイス** web カメラや DVD プレーヤーなどの高速のデバイスが同時に多数のユーザーを使用している場合、システムの全体のパフォーマンスに影響します。  
  
## <a name="configuration"></a>構成  
  
-   **CPU、GPU、および RAM** を参照してください [MultiPoint サービスのシステム パフォーマンスの最適化](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance) CPU、GPU、および RAM の推奨事項は、このガイドにします。  
-   **ネットワーク帯域幅**RDP over LAN 接続ステーションの場合、特にビデオがユーザーのセッションで実行されている場合は、ネットワーク帯域幅とクライアントの機能 (たとえば、シンクライアント、デスクトップ PC、ラップトップなど) が重要です。 USB over Ethernet 0 クライアントを使用している場合は、そのネットワークの帯域幅が重要な考慮事項できる必要があります。 これらのデバイスを使用する場合は、別のギガビット イーサネット ネットワークの設定を考慮することも、同じのイーサネット接続経由でのすべてのデバイスのビデオ データが送信されます。  
-   **RemoteFX** RDP over LAN 接続されたステーションできる場合があります RemoteFX を使用して、高品位のマルチ メディア コンテンツの配信を大幅に向上させる。  
-   **画面の解像度** 多量の全画面表示のビデオ使用した場合は、パフォーマンスを最適化するモニターの解像度を減らす場合します。  
-   **USB ゼロ クライアント数** サーバー上の単一のルート ハブでの USB ゼロ クライアントの合計数、ビデオのパフォーマンスに直接影響します。 詳細については、次を参照してください。 [USB ゼロ クライアント接続ステーションのレイアウト](MultiPoint-services-Site-Planning.md#layout-for-usb-zero-client-connected-stations)します。 使用可能な USB over Ethernet 0 クライアント局の数は USB ゼロ クライアントの数より若干少なくなります。  
-   **USB の帯域幅** 、システムを設計する際に、USB の帯域幅を検討してください。  これは、USB ゼロ クライアントは、USB 接続経由でのビデオ データを送信するために特に重要です。 帯域幅を最適化するには、サーバー上の単一の USB ポートに接続されているデバイスの数を最小限に抑えます。 これは、デイジー チェーン ステーションと中間ハブに適用されます。 詳細については、次を参照してください。 [ステーション ハブ](MultiPoint-services-Site-Planning.md#station-hubs) と [中間ハブ](MultiPoint-services-Site-Planning.md#intermediate-hubs)します。  
  
-   **USB の種類**Usb 2.0 ではなく USB 3.0 を使用すると、3台以上の USB ゼロクライアントをハブに接続している場合、または高帯域幅の USB デバイスを使用している場合に、サーバーと中間ハブの間で使用可能な帯域幅が増加します。  
  
-   **ステーション** ステーションの合計数がパフォーマンスに影響します。 大量のグラフィックス、処理、またはビデオのニーズがある場合は、場合は、ステーションの全体的な数を制限します。 詳細については、次を参照してください。 [最適化 MultiPoint サービス システムのパフォーマンス](hardware-and-performance-recommendations.md#optimize-multipoint-services-system-performance)します。