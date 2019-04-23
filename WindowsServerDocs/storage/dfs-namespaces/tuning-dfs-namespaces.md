---
title: DFS 名前空間を調整する
description: この記事では、DFS 名前空間を調整または最適化する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c11bbf65c3baebebe1e5143a5e694ca752500aca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844633"
---
# <a name="tuning-dfs-namespaces"></a>DFS 名前空間を調整する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成し、フォルダーとターゲットを追加した後は、調整や DFS Namespace が紹介を処理する方法と Active Directory Domain Services (AD DS) の名前空間の更新されたデータのポーリングを最適化するのには、次のセクションを参照してください。

-   [Namespace アクセス ベースの列挙を有効にします。](enable-access-based-enumeration-on-a-namespace.md)
-   [有効または無効の参照とクライアントのフェールバック](enable-or-disable-referrals-and-client-failback.md)
-   [クライアントが紹介をキャッシュする時間を変更します。](change-the-amount-of-time-that-clients-cache-referrals.md)
-   [紹介内のターゲットの順序付け方法を設定します。](set-the-ordering-method-for-targets-in-referrals.md)
-   [紹介順序を上書きするターゲットの優先順位を設定します。](set-target-priority-to-override-referral-ordering.md)
-   [Namespace ポーリングを最適化します。](optimize-namespace-polling.md)
-   [アクセス ベースの列挙で継承されたアクセス許可の使用](using-inherited-permissions-with-access-based-enumeration.md)

> [!NOTE]
> フォルダーまたはフォルダー ターゲットを検索するには、名前空間を選択して **[検索]** タブをクリックし、テキスト ボックスに検索文字列を入力して **[検索]** をクリックします。