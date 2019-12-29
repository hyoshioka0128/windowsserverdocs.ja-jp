---
title: ハードウェア要件とパフォーマンスの推奨事項
description: MultiPoint サービスのハードウェアとパフォーマンスの要件と推奨事項について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 284131028b308ee86389f25102d934390ba2f16d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389113"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>ハードウェア要件とパフォーマンスの推奨事項
このトピックでは、MultiPoint Services システムを実行し、ユーザーアプリケーションのシナリオをサポートするために必要なハードウェアについて説明します。 ユーザーシナリオは、CPU、RAM、およびネットワーク帯域幅の要件に直接影響します。  

## <a name="optimize-multipoint-services-system-performance"></a>MultiPoint サービスのシステムパフォーマンスを最適化する  
MultiPoint Services システムのパフォーマンスは、CPU、GPU、および MultiPoint サービスを実行しているコンピューターで使用可能な RAM の容量によって直接影響を受けます。  
  
### <a name="applications-and-internet-content"></a>アプリケーションとインターネットコンテンツ  
MultiPoint Services は共有リソースコンピューティングソリューションであるため、ステーションで実行されているアプリケーションの種類と数が MultiPoint Services システムのパフォーマンスに影響を与える可能性があります。 システムを計画するときに、定期的に使用されるプログラムの種類を考慮することが重要です。 たとえば、グラフィックを多用するアプリケーションでは、ワードプロセッサなどのアプリケーションよりも強力なコンピューターが必要です。 グラフィックスを多用するアプリケーションでコンピューターを過負荷にすると、システム全体で遅延の問題が発生する可能性があります。  
  
アプリケーションによってアクセスされるコンテンツの種類は、システムのパフォーマンスにも影響します。 複数のステーションがフルモーションビデオなどのマルチメディアコンテンツにアクセスするために web ブラウザーを使用している場合、システムのパフォーマンスに悪影響を及ぼす前に接続できるステーションが減少します。 逆に、複数のステーションが web ブラウザーを使用して静的 web コンテンツにアクセスする場合、パフォーマンスに大きな影響を与えることなく、より多くのステーションを接続できます。  
  
### <a name="hardware-recommendations"></a>ハードウェアの推奨事項  
さまざまな負荷下で MultiPoint Services システムのパフォーマンスを向上させるには、システムを計画およびテストするときに、次の表のガイドラインを使用します。 これらは、forMultiPoint サービスの基本的な要件です。 実際の構成サイズは、システム構成、実行しているワークロード、およびハードウェア機能によって異なります。 アプリケーションとハードウェアをテストすることで、常に検証する必要があります。  
  
> [!NOTE]  
> 2C = 2 コア、4C = 4 コア、6C = 6 コア、MT = マルチスレッド。 プロセッサ速度は2.0 ギガヘルツ (GHz) 以上である必要があります。  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>既定の MultiPoint Server ステーションを実行するための最小推奨ハードウェア  
  
|アプリケーションのシナリオ|最大5つのステーション|6-8 ステーション|9-12 ステーション|13-16 ステーション|17-20 ステーション|21-24 ステーション|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**力**<br /><br />Office、web 閲覧、基幹業務アプリケーション|CPU:B<br /><br />RAM:2 GB|CPU:B<br /><br />RAM:4 GB|CPU:4C<br /><br />RAM:6 GB|CPU:4C<br /><br />RAM:8 GB|CPU:4C + MT または6C<br /><br />RAM:10 GB| CPU:6C + MT<br /><br />RAM:12 GB|
|**多**<br /><br />一部のユーザーが Office、web 閲覧、基幹業務アプリケーション、および不定期に使用するビデオ|CPU:B<br /><br />RAM:2 GB|CPU:B<br /><br />RAM:4 GB|CPU:4C<br /><br />RAM:6 GB|CPU:4C + MT または6C<br /><br />RAM:8 GB|CPU:6C + MT<br /><br />RAM:10 GB| CPU:6C + MT<br /><br />RAM:12 GB| 
|**ビデオ集中型**<br /><br />Office、web 閲覧、基幹業務アプリケーション、およびすべてのユーザーが頻繁に使用するビデオの**メモ:** ビデオテストは、ネイティブ解像度で 360p h.264 ビデオを使用して実行されました。|CPU:4C + MT<br /><br />RAM:2 GB|CPU:6C + MT<br /><br />RAM:4 GB|CPU:8C + MT<br /><br />RAM:6 GB|CPU:12C + MT<br /><br />RAM:8 GB|CPU:16C + MT<br /><br />RAM:10 GB<br /><br />-シンクライアント:RemoteFX<br />-USB ビデオは推奨されません| CPU:20C + MT<br /><br />RAM:12 GB<br /><br />-シンクライアント:RemoteFX<br />-USB ビデオは推奨されません|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>Windows 10 仮想デスクトップ全体を実行するための最小推奨ハードウェア  
各ステーションに対して完全な仮想オペレーティングシステムインスタンスを実行することは、既定の MultiPoint desktop セッションを実行するよりもコンピューティングリソースが多くなるため、ステーションあたりのホストハードウェア要件は高くなります。  
  
1.  CPU:ステーションあたり1コアまたはスレッド  
  
2.  ソリッドステートドライブ (SSD)  
  
    1.  容量 > = 1 ステーションあたり 20 gb + WMS ホストオペレーティングシステム用  
  
    2.  ランダム読み取り/書き込み IOPS > ステーションあたり 3 k  
  
3.  RAM > = ステーションあたり 2 GB + WMS ホストオペレーティングシステム用に 2 GB  
  
仮想化–第2レベルのアドレス変換 (SLAT) を有効にするように BIOS CPU 設定が構成されています  
  
ニーズに最も適した MultiPoint Services ハードウェアを選択する方法の詳細については、ハードウェアベンダーにお問い合わせください。  