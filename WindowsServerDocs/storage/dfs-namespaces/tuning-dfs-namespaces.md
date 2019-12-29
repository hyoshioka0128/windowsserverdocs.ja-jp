---
title: DFS 名前空間を調整する
description: この記事では、DFS 名前空間を調整または最適化する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 011512deaeb99ded7d0bfc32a48f19ab3b622475
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386155"
---
# <a name="tuning-dfs-namespaces"></a>DFS 名前空間を調整する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成し、フォルダーとターゲットを追加した後、次のセクションを参照して、DFS 名前空間が更新された名前空間データに対して Active Directory Domain Services (AD DS) の参照とポーリングを処理する方法を調整または最適化します。

-   [名前空間でアクセスベースの列挙を有効にする](enable-access-based-enumeration-on-a-namespace.md)
-   [紹介とクライアント フェールバックを有効または無効にする](enable-or-disable-referrals-and-client-failback.md)
-   [クライアントが参照をキャッシュする時間の長さを変更する](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [紹介におけるターゲットの順序指定方法を設定する](set-the-ordering-method-for-targets-in-referrals.md)
-   [ターゲット優先順位を設定して紹介順序を上書きする](set-target-priority-to-override-referral-ordering.md)
-   [名前空間のポーリングを最適化する](optimize-namespace-polling.md)
-   [アクセスベースの列挙で継承されたアクセス許可を使用する](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> フォルダーまたはフォルダー ターゲットを検索するには、名前空間を選択して **[検索]** タブをクリックし、テキスト ボックスに検索文字列を入力して **[検索]** をクリックします。