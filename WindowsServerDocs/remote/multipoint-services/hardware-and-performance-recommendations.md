---
title: ハードウェア要件とパフォーマンスの推奨事項
description: ハードウェアとパフォーマンスの要件と MultiPoint サービスの推奨事項を提供します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b47f4c224d4a4f6f4aa104b6d5ee5d93590ac0c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823393"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>ハードウェア要件とパフォーマンスの推奨事項
このトピックでは、MultiPoint Services システムを実行し、ユーザーのアプリケーション シナリオをサポートするために必要なハードウェアについて説明します。 ユーザーのシナリオは、CPU、RAM、およびネットワーク帯域幅の要件に直接影響します。  

## <a name="optimize-multipoint-services-system-performance"></a>MultiPoint Services システムのパフォーマンスを最適化します。  
MultiPoint Services システムのパフォーマンスは、CPU、GPU、および MultiPoint Services を実行しているコンピューターで利用可能な RAM の容量の機能によって直接影響されます。  
  
### <a name="applications-and-internet-content"></a>アプリケーションとインターネットのコンテンツ  
MultiPoint Services は、共有リソースのコンピューティング ソリューションであるため、MultiPoint Services システムのパフォーマンスが種類のステーションで実行されているアプリケーションの数により影響します。 重要、システムを計画するときに定期的に使用されるプログラムの種類になります。 たとえば、グラフィックを多用するアプリケーションでは、ワード プロセッサなどのアプリケーションよりもより強力なコンピューターが必要です。 グラフィックを多用するアプリケーションを使用してコンピューターをオーバー ロードしても、システム全体にわたって遅延の問題が発生可能性があります。  
  
アプリケーションによってアクセスされるコンテンツの種類では、システムのパフォーマンスも影響します。 複数のステーションは、フルモーション ビデオなどのマルチ メディア コンテンツにアクセスする web ブラウザーを使用している場合は、システム パフォーマンスが低下する前に少ないステーションを接続できます。 逆に、複数のステーションでは、静的 web コンテンツにアクセスする web ブラウザーを使用している場合、ステーションはパフォーマンスに大きな影響を及ぼすことがなく接続できます。  
  
### <a name="hardware-recommendations"></a>ハードウェアの推奨事項  
さまざまな負荷の下で、MultiPoint Services システムに良好なパフォーマンスを実現するために計画、システムをテストするときに、次の表のガイドラインを使用します。 これらの基本的な要件を forMultiPoint サービスには。 実際の構成のサイズ変更は、システム構成を実行しているワークロードとハードウェアの機能によって異なります。 常に、アプリケーションおよびハードウェアをテストして検証する必要があります。  
  
> [!NOTE]  
> 2 C = 2 コア、4 C = 4 コア、6 C = 6 コア、MT = マルチ スレッドです。 プロセッサ速度、少なくとも 2.0 ギガヘルツ (GHz) があります。  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>既定の MultiPoint Server ステーションを実行するためのハードウェア (推奨)  
  
|アプリケーションのシナリオ|最大 5 つのステーション|6 ~ 8 ステーション|9-12 ステーション|13 ~ 16 ステーション|17 ~ 20 ステーション|21 ~ 24 ステーション|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**生産性**<br /><br />Office、web の閲覧、基幹業務アプリケーション|CPU:2 つの C<br /><br />RAM:2 GB|CPU:2 つの C<br /><br />RAM:4 GB|CPU:4C<br /><br />RAM:6 GB|CPU:4C<br /><br />RAM:8 GB|CPU:C + MT が 4 または 6 C<br /><br />RAM:10 GB| CPU:6C+MT<br /><br />RAM:12 GB|
|**混合**<br /><br />Office、web 閲覧、基幹業務アプリケーション、および一部のユーザーがビデオ不定期の使用|CPU:2 つの C<br /><br />RAM:2 GB|CPU:2 つの C<br /><br />RAM:4 GB|CPU:4C<br /><br />RAM:6 GB|CPU:C + MT が 4 または 6 C<br /><br />RAM:8 GB|CPU:6C+MT<br /><br />RAM:10 GB| CPU:6C+MT<br /><br />RAM:12 GB| 
|**ビデオの処理を要する**<br /><br />Office、web 閲覧、基幹業務アプリケーション、およびすべてのユーザーがビデオの使用頻度が高く**に注意してください。** ビデオのテストには、360 p H.264 のビデオを使用して、ネイティブの解像度で実行されました。|CPU:4C+MT<br /><br />RAM:2 GB|CPU:6C+MT<br /><br />RAM:4 GB|CPU:8C+MT<br /><br />RAM:6 GB|CPU:12C+MT<br /><br />RAM:8 GB|CPU:16 C + MT<br /><br />RAM:10 GB<br /><br />-シン クライアント:RemoteFX<br />USB ビデオをお勧めしません| CPU:C + MT の 20<br /><br />RAM:12 GB<br /><br />-シン クライアント:RemoteFX<br />USB ビデオをお勧めしません|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>完全な Windows 10 仮想デスクトップを実行するためのハードウェア (推奨)  
各ステーションのオペレーティング システムの完全な仮想インスタンスを実行すると、ステーションごとのホストのハードウェア要件が高いために、既定の MultiPoint デスクトップ セッションを実行するよりも多くのコンピューティング リソースを消費は。  
  
1.  CPU:1 つのコアまたはステーションごとにスレッド  
  
2.  ソリッド ステート ドライブ (SSD)  
  
    1.  容量 > = ステーションあたり 20 GB + 40 GB、WMS のホスト オペレーティング システム  
  
    2.  ランダムな読み取り/書き込み IOPS > ステーションごとに 3 つの K を =  
  
3.  RAM > WMS ホスト オペレーティング システムのステーションごとに 2 GB + 2 GB を =  
  
仮想化 – Second Level Address Translation (SLAT) を有効にする BIOS の CPU 設定が構成されました  
  
ニーズに最適な MultiPoint Services のハードウェアの選択の詳細については、ハードウェア ベンダーにお問い合わせください。  