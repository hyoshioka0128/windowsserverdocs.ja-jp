---
title: 必要に応じてデバイス ドライバーを更新およびインストールする
description: MultiPoint Services でデバイスドライバーを確認および更新する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16be3ef9-a05b-4621-a431-5806b567e997
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 94c06e6d33577c5542358e1244ea5a9b3331f1cd
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871511"
---
# <a name="update-and-install-device-drivers-if-needed"></a>必要に応じてデバイス ドライバーを更新およびインストールする
USB ゼロクライアントまたはドライバーを必要とする周辺機器を使用している場合は、現時点でドライバーをインストールする必要があります。 また、ドライバーアラートの**デバイスマネージャー**を確認し、それらのデバイスのドライバーをインストールすることもお勧めします。  
  
一般に、次の種類のデバイスには最新のドライバーが必要です。  
  
-   USB ゼロ クライアント  
  
-   USB over Ethernet 0 クライアント  
  
-   ディスクコントローラー  
  
-   ネットワーク アダプター  
  
-   サウンドコントローラー  
  
-   USB ホストコントローラー

-   グラフィックカード


## <a name="to-check-for-driver-alerts-in-device-manager"></a>デバイスマネージャーでドライバーのアラートを確認するには  
  
1.  スタート画面を開きます。  
  
2.  「**コンピューターの管理**」と入力し、結果で **[コンピューターの管理]** をクリックします。  
  
3.  コンピュータの管理 コンソールツリーで、**デバイスマネージャー** をクリックします。  
  
4.  右側のシステムデバイスで、MultiPoint Server に影響する可能性のあるドライバーのアラートがないかどうかを確認します。  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>MultiPoint マネージャーにデバイスドライバーをインストールするには  
  
1.  MultiPoint マネージャーを開くには、"MultiPoint マネージャー" を検索し、結果で **[Multipoint マネージャー]** をクリックします。  
  
2.  MultiPoint マネージャーで、 **[ホーム]** タブをクリックし、 **[コンソールモードへの切り替え]** をクリックします。  
  
3.  デバイスドライバーをインストールするには、ドライバーファイルをダブルクリックし、指示に従ってドライバーをインストールします。  
  
4.  前の手順を繰り返して、必要なすべてのドライバーをインストールします。  
  
    > [!NOTE]  
    > インストールでコンピューターの再起動が必要な場合は、次のドライバーをインストールする前に、コンソールモードに戻す必要があります。 MultiPoint server は、常にステーションモードで起動します。 コンソールモードに切り替えるには、MultiPoint マネージャーの **[ホーム]** タブに移動し、 **[コンソールモードへの切り替え]** をクリックします。