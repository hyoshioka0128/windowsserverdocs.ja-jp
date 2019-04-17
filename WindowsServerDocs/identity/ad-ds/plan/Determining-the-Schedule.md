---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: "スケジュールを決定します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0ec953b34475c50e62553a9ba95e4d45d9904bf3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-schedule"></a>スケジュールを決定します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイト リンクの可用性を制御するには、サイト リンク スケジュールを設定します。 2 つのサイト間のレプリケーションは、複数のサイト リンクを経由する、すべての関連リンク上のレプリケーション スケジュールの共通部分は、2 つのサイト間の接続スケジュールを決定します。  
  
サイト リンク スケジュールを設定するための計画、相互に直接レプリケートするドメイン コントローラーを含むサイト リンクの間で 2 つの重複するスケジュールを作成します。 ピーク時にレプリケーション トラフィックをブロックする必要がない限り、これらのリンクで (100% 使用可能な) の既定のスケジュールを使用します。 ブロックの複製によって、その他のトラフィックに優先順位を設定が、レプリケーションの潜在期間を増やすこともします。  
  
ドメイン コントローラーは、世界協定時刻 (UTC) で時間を格納します。 サイト リンク オブジェクトのスケジュールの時刻の設定は、サイトおよびスケジュールが設定されているコンピューターのローカル時刻に準拠しています。 ドメイン コントローラーは、別のサイトとタイム ゾーンにあるコンピューターを接続、ドメイン コントローラー上のスケジュールは、サイトのコンピューターのローカル時刻に従って、[時間] 設定を表示します。  
  


