---
title: 必要に応じてデバイス ドライバーを更新およびインストールする
description: 確認し、MultiPoint Services でのデバイス ドライバーを更新する方法について説明します
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
ms.openlocfilehash: 66477634e06df217656876b084ae37be8cb311c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829133"
---
# <a name="update-and-install-device-drivers-if-needed"></a>必要に応じてデバイス ドライバーを更新およびインストールする
USB ゼロ クライアントまたはドライバーが必要な周辺機器を使用している場合は、この時点で、ドライバーをインストールする必要があります。 チェックもすることをお勧め**デバイス マネージャー**は、ドライバーのアラートとそれらのデバイス ドライバーをインストールします。  
  
一般に、最新のドライバーは、次の種類のデバイスの必要があります。  
  
-   USB ゼロ クライアント  
  
-   USB over Ethernet 0 クライアント  
  
-   ディスク コント ローラー  
  
-   ネットワーク アダプター  
  
-   サウンドのコント ローラー  
  
-   USB ホスト コント ローラー

-   グラフィック カード


## <a name="to-check-for-driver-alerts-in-device-manager"></a>デバイス マネージャーで警告のドライバーを確認するには  
  
1.  スタート画面を開きます。  
  
2.  型**コンピュータの管理**、 をクリックし、**コンピュータの管理**結果にします。  
  
3.  コンピューターの管理コンソール ツリーで、クリックして**デバイス マネージャー**します。  
  
4.  右側のシステム デバイス で MultiPoint Server に影響を与える可能性がありますドライバー アラートを確認します。  
  
## <a name="to-install-device-drivers-in-multipoint-manager"></a>MultiPoint マネージャーでデバイス ドライバーをインストールするには  
  
1.  MultiPoint マネージャーを開くには、"MultiPoint Manager"を検索し、クリックして**MultiPoint マネージャー**結果にします。  
  
2.  MultiPoint マネージャーで、をクリックして、**ホーム**タブをクリックし、をクリックし、**コンソール モードに切り替える**します。  
  
3.  デバイス ドライバーをインストールするには、ドライバー ファイルをダブルクリックし、ドライバーをインストールする手順についてに従います。  
  
4.  すべての必要なドライバーをインストールする前の手順を繰り返します。  
  
    > [!NOTE]  
    > インストールには、コンピューターの再起動が必要とする場合は、次のドライバーをインストールする前に、コンソール モードに切り替える必要があります。 MultiPoint server は、常に、ステーション モードで起動します。 移動するコンソール モードに切り替える、**ホーム**MultiPoint マネージャー タブでをクリックし、**コンソール モードに切り替える**します。