---
ms.assetid: de054ac2-a386-43ec-a537-c0de21549741
title: サイト リンクのプロパティを設定する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4fa9a1fa8d2a463fe5f361a5a27ee2b9e3edc0f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870363"
---
# <a name="setting-site-link-properties"></a>サイト リンクのプロパティを設定する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

接続オブジェクトのプロパティに従って、サイト間レプリケーションが発生します。 知識整合性チェッカー (KCC) は、接続オブジェクトを作成するとき、レプリケーション スケジュールをサイト リンク オブジェクトのプロパティから派生します。 各サイト リンク オブジェクトは、2 つまたは複数のサイト間のワイド エリア ネットワーク (WAN) 接続を表します。  
  
サイト リンク オブジェクトのプロパティを設定するには、次の手順が含まれています。  
  
-   そのレプリケーション パスに関連付けられているコストを決定します。 KCC は、コストを使用して、同じディレクトリ パーティションをレプリケートする 2 つのサイト間のレプリケーションで最も安価なルートを決定します。  
  
-   発生する可能性がどのサイト間のレプリケーション中に時間を定義するスケジュールを決定します。  
  
-   スケジュールで定義されている複製がレプリケーションを許可すると、時間帯に行われる頻度を定義するレプリケーション間隔を決定します。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [コストを決定します。](../../ad-ds/plan/Determining-the-Cost.md)  
  
-   [スケジュールを決定します。](../../ad-ds/plan/Determining-the-Schedule.md)  
  
-   [間隔を決定します。](../../ad-ds/plan/Determining-the-Interval.md)  
  


