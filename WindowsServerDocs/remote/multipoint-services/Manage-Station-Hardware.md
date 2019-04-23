---
title: ステーション ハードウェアの管理
description: MultiPoint ステーションのハードウェアを管理する方法の概要を説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 429b8539-b17a-4e01-9576-860600466451
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 3a1cdfd12c9bd6a21fec9cbfffae04573ef5ea98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841633"
---
# <a name="manage-station-hardware"></a>ステーション ハードウェアの管理
MultiPoint Services システムから成る単一のコンピューターと少なくとも 1 つのステーションです。 ステーション ハードウェアは通常、ステーション ハブ、マウス、キーボード、およびビデオ モニターで構成されます。 ステーションは通常、コンピューターにケーブルで物理的に接続されます。  
  
4 つのステーションで構成される MultiPoint Services システムのレイアウトの例を次の図に示します。 各ステーションは、USB ハブおよびマルチ モニター ビデオ カードを使用して MultiPoint Services コンピューターに接続されます。 この図は、多機能ハブを使用して接続されているステーションを表していません。  
   
![MultiPoint サービス USB ベース システム レイアウトのイメージ](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
このセクションのトピックでは、MultiPoint Services システムに接続されているハードウェアの状態を表示する方法を説明します。また、MultiPoint Services ステーションのセットアップに使用できる USB デバイスの種類とその他の周辺機器についても詳しく説明します。 以下では、ハードウェアの選択と MultiPoint Services ステーションのセットアップに役立つ、このセクションのトピックの概要を説明します。  
  
## <a name="view-hardware-status"></a>ハードウェアの状態を表示する  
MultiPoint マネージャーで、使用することができます、**ステーション**タブには、ステーションと MultiPoint Services コンピューターに接続されているハードウェア デバイスの状態を表示します。 MultiPoint Services コンピューターやそれに接続されているハードウェア デバイスの状態を表示する方法については、「[ハードウェアの状態の表示](View-Hardware-Status.md)」トピックを参照してください。  
  
## <a name="work-with-usb-devices"></a>USB デバイスを使用する  
USB デバイスとその他の周辺機器が MultiPoint Services システムに接続されている場合、MultiPoint Services コンピューターに接続されている場合と、MultiPoint Services ステーションに接続されている場合では、その動作が異なります。 「[USB デバイスの使用](Work-with-USB-Devices.md)」トピックでは、これらのシナリオでハードウェア デバイスの動作がどのように異なるのかを説明し、ステーション ハブとの連携について詳細な情報を提供します。  
  
## <a name="work-with-video-devices"></a>ビデオ デバイスを使用する  
「[ビデオ デバイスの使用](Work-with-Video-Devices.md)」トピックでは、モニターやプロジェクターなどのビデオ デバイスが MultiPoint Services システムのコンピューターまたは MultiPoint Services ステーションに接続されているときに、ビデオ デバイスがどのように機能するかについて説明します。  
  
## <a name="set-up-a-station"></a>ステーションをセットアップする  
「[ステーションのセットアップ](Set-Up-a-Station.md)」トピックでは、MultiPoint Services ステーションを作成するために MultiPoint Services ステーション ハブに周辺機器を接続する方法について説明します。 MultiPoint Services では、次の 2 種類のステーション ハブがサポートされています。  
  
-   外部電源またはバス供給のマルチ ポート*USB ハブ*マウス、キーボード、およびその他の USB 周辺機器をサポートすることができます  
  
-   統合ビデオ コントローラーと、マウス、キーボード、およびオーディオ周辺機器のためのポートを備えた*多機能ハブ*  
  
どちらの種類のステーション ハブも、USB ケーブルによってコンピューターに接続します。 「[ステーションのセットアップ](Set-Up-a-Station.md)」トピックの手順では、ハードウェア デバイスと各タイプのステーション ハブとの接続方法を示しています。  
  
## <a name="see-also"></a>関連項目  
[ハードウェアの状態の表示](View-Hardware-Status.md)  
[USB デバイスを使用します。](Work-with-USB-Devices.md)  
[ビデオ デバイスを使用します。](Work-with-Video-Devices.md)  
[ステーションをセットアップします。](Set-Up-a-Station.md)