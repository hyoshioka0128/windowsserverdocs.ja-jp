---
title: 'チェックリスト: DFS 名前空間を調整する'
description: この記事では、DFS 名前空間が紹介を処理し、AD DS から更新された名前空間データをポーリングする方法を最適化する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5e2d43f75a64a6a7950539c14386c6a037bc3c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872643"
---
# <a name="checklist-tune-a-dfs-namespace"></a>チェックリスト:DFS 名前空間を調整します。

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成し、フォルダーとターゲットの追加は、次のチェックリストを使用して、調整や最適化を後、DFS 名前空間が紹介を処理し、更新された名前空間データを Active Directory Domain Services (AD DS) をポーリングします。

-   ユーザーがアクセス許可を持たない名前空間のフォルダーを参照できないようにします。 [Namespace アクセス ベースの列挙を有効にします。](enable-access-based-enumeration-on-a-namespace.md) 
-   ユーザーが名前空間内のフォルダーにアクセスするときの名前空間またはフォルダー ターゲットへの紹介を有効または無効にします。 [有効または無効の参照とクライアントのフェールバック](enable-or-disable-referrals-and-client-failback.md) 
-   クライアントが紹介をキャッシュしてから新しい紹介を要求するまでの時間を調整します。 [クライアントが紹介をキャッシュする時間を変更します。](change-the-amount-of-time-that-clients-cache-referrals.md)
-   名前空間サーバーが AD DS をポーリングして最新の名前空間データを取得する方法を最適化します。 [Namespace ポーリングを最適化します。](optimize-namespace-polling.md)
-   継承されたアクセス許可を使って、アクセス ベースの列挙が有効になっている名前空間のフォルダーを表示できるユーザーを制御します。 [アクセス ベースの列挙で継承されたアクセス許可の使用](using-inherited-permissions-with-access-based-enumeration.md)

さらに、ターゲットの優先順位と呼ばれる DFS 名前空間の拡張機能を使用して指定できますサーバーの優先順位、特定のサーバーには、必ず最初または最 (紹介と呼ばれる) サーバーの一覧で、フォルダーにアクセスするときに、クライアントが受信するように名前空間内のターゲット。

-   ユーザーがフォルダー ターゲットに紹介される順序を指定します。 [紹介内のターゲットの順序付け方法を設定します。](set-the-ordering-method-for-targets-in-referrals.md)
-   特定の名前空間サーバーまたはフォルダー ターゲットの紹介順序を上書きします。 [紹介順序を上書きするターゲットの優先順位を設定します。](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>関連項目

-   [名前空間](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [チェックリスト:DFS 名前空間をデプロイします。](checklist-deploy-dfs-namespaces.md)
-   [DFS 名前空間のチューニング](tuning-dfs-namespaces.md)


