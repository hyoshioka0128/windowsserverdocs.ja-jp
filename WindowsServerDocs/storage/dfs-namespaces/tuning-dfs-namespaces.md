---
title: DFS 名前空間を調整する
description: この記事では、DFS 名前空間を調整または最適化する方法について説明します。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 348a34e24cf7d22dc376df37607f21f1dceea74a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939398"
---
# <a name="tuning-dfs-namespaces"></a>DFS 名前空間を調整する

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成し、フォルダーとターゲットを追加できたら、次のセクションを参照し、DFS 名前空間が紹介を処理する方法を調整します。さらに、名前空間データが更新されていないかどうかを確認するために DFS 名前空間が Active Directory Domain Services (AD DS) に対してポーリングする方法も調整します。

-   [名前空間でアクセスベースの列挙を有効にする](enable-access-based-enumeration-on-a-namespace.md)
-   [紹介とクライアント フェールバックを有効または無効にする](enable-or-disable-referrals-and-client-failback.md)
-   [クライアントが参照をキャッシュする時間の長さを変更する](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [紹介におけるターゲットの順序指定方法を設定する](set-the-ordering-method-for-targets-in-referrals.md)
-   [ターゲット優先順位を設定して紹介順序を上書きする](set-target-priority-to-override-referral-ordering.md)
-   [名前空間のポーリングを最適化する](optimize-namespace-polling.md)
-   [アクセスベースの列挙で継承されたアクセス許可を使用する](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> フォルダーまたはフォルダー ターゲットを検索するには、名前空間を選択して **[検索]** タブをクリックし、テキスト ボックスに検索文字列を入力して **[検索]** をクリックします。