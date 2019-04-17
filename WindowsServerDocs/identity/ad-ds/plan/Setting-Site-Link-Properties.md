---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: "サイト リンクのプロパティの設定"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 495ed006ecac5458877191a14060c5fd4b746d96
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="setting-site-link-properties"></a>サイト リンクのプロパティの設定

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイト間レプリケーションは、接続オブジェクトのプロパティに基づいて発生します。 知識整合性チェッカー (KCC) は、接続オブジェクトを作成するときは、サイト リンク オブジェクトのプロパティから、レプリケーション スケジュールを派生します。 各サイト リンク オブジェクトは、次の 2 つまたは複数のサイト間のワイド エリア ネットワーク (WAN) 接続を表します。  
  
サイト リンク オブジェクトのプロパティを設定すると、次の手順が含まれています。  
  
-   そのレプリケーション パスに関連付けられているコストを決定します。 KCC は、コストを使用して、同じディレクトリ パーティションをレプリケートする 2 つのサイト間のレプリケーションには、少なくとも高価なルートを決定します。  
  
-   サイト間レプリケーション中に時間を定義するスケジュールを決定が発生することができます。  
  
-   レプリケーションする必要がありますレプリケーションが許可されて時間中に発生する、スケジュールに定義されているどの程度の間隔を定義するレプリケーション間隔を決定します。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [コストを決定します。](../../ad-ds/plan/Determining-the-Cost.md)  
  
-   [スケジュールを決定します。](../../ad-ds/plan/Determining-the-Schedule.md)  
  
-   [間隔を決定します。](../../ad-ds/plan/Determining-the-Interval.md)  
  


