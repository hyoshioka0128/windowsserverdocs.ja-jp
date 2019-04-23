---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: スケジュールを決定する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dee63ce0fb687b2b722ce64614c54388fc544433
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839003"
---
# <a name="determining-the-schedule"></a>スケジュールを決定する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイト リンクのスケジュールを設定して、サイト リンクの可用性を制御できます。 2 つのサイト間のレプリケーションでは、複数のサイト リンクを通過、すべての関連リンクのレプリケーション スケジュールの積集合は 2 つのサイト間の接続スケジュールを決定します。  
  
サイト リンク スケジュールを設定するための計画、相互に直接レプリケートするドメイン コント ローラーを含むサイト リンクの間の 2 つの重複するスケジュールを作成します。 ピーク時間帯にレプリケーション トラフィックをブロックする場合、これらのリンクで、(100% 使用可能な) 既定のスケジュールを使用します。 ブロックのレプリケーションによってもレプリケーションの待機時間を増やすことが、その他のトラフィックに優先順位を設定します。  
  
ドメイン コント ローラーは、世界協定時刻 (UTC) 時刻を格納します。 サイト リンク オブジェクトのスケジュールの時刻の設定は、サイトと、スケジュールが設定されているコンピューターのローカル時刻に準拠しています。 ドメイン コント ローラーには、別のサイトおよびタイム ゾーンにあるコンピューターが取引先担当者、ドメイン コント ローラー上のスケジュールはコンピューターのサイトのローカル時刻に従って、時刻設定を表示します。  
  


