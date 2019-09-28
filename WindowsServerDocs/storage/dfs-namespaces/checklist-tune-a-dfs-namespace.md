---
title: 'チェックリスト: DFS 名前空間を調整する'
description: この記事では、DFS 名前空間が紹介を処理し、AD DS から更新された名前空間データをポーリングする方法を最適化する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8a4c581801cbb1dcfe3db2813fb66fb4514d6434
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402188"
---
# <a name="checklist-tune-a-dfs-namespace"></a>チェックリスト:DFS 名前空間のチューニング

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成し、フォルダーとターゲットを追加したら、次のチェックリストを使用して、DFS 名前空間が参照を処理し、更新された名前空間データの Active Directory Domain Services (AD DS) をポーリングする方法を調整または最適化します。

-   ユーザーがアクセス許可を持たない名前空間のフォルダーを参照できないようにします。 [名前空間でアクセスベースの列挙を有効にする](enable-access-based-enumeration-on-a-namespace.md) 
-   ユーザーが名前空間内のフォルダーにアクセスするときの名前空間またはフォルダー ターゲットへの紹介を有効または無効にします。 [紹介とクライアント フェールバックを有効または無効にする](enable-or-disable-referrals-and-client-failback.md) 
-   クライアントが紹介をキャッシュしてから新しい紹介を要求するまでの時間を調整します。 [クライアントが参照をキャッシュする時間の長さを変更する](change-the-amount-of-time-that-clients-cache-referrals.md)
-   名前空間サーバーが AD DS をポーリングして最新の名前空間データを取得する方法を最適化します。 [名前空間のポーリングを最適化する](optimize-namespace-polling.md)
-   継承されたアクセス許可を使って、アクセス ベースの列挙が有効になっている名前空間のフォルダーを表示できるユーザーを制御します。 [アクセスベースの列挙で継承されたアクセス許可を使用する](using-inherited-permissions-with-access-based-enumeration.md)

さらに、ターゲット優先順位と呼ばれる DFS 名前空間の拡張機能を使用することにより、サーバーの優先順位を指定できます。これにより、特定のサーバーが常に、フォルダーにアクセスするときにクライアントが受信するサーバーの一覧 (参照と呼ばれます) に配置されるようになります。名前空間のターゲットを使用します。

-   ユーザーがフォルダー ターゲットに紹介される順序を指定します。 [紹介におけるターゲットの順序指定方法を設定する](set-the-ordering-method-for-targets-in-referrals.md)
-   特定の名前空間サーバーまたはフォルダー ターゲットの紹介順序を上書きします。 [ターゲット優先順位を設定して紹介順序を上書きする](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>関連項目

-   [名前空間](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [チェックリスト:DFS 名前空間を展開する](checklist-deploy-dfs-namespaces.md)
-   [DFS 名前空間を調整する](tuning-dfs-namespaces.md)


