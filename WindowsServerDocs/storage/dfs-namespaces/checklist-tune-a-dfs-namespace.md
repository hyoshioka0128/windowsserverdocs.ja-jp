---
title: "チェックリスト: DFS 名前空間を調整する"
description: "この記事では、DFS 名前空間が紹介を処理し、AD DS から更新された名前空間データをポーリングする方法を最適化する方法について説明します。"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 827484c2ffcbb2617626129011a8b510473fe669
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="checklist-tune-a-dfs-namespace"></a>チェックリスト: DFS 名前空間を調整する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間を作成してフォルダーとターゲットを追加した後、次のチェックリストを使って、DFS 名前空間が紹介を処理し、Active Directory Domain Services (AD DS) から更新された名前空間データをポーリングする方法を調整または最適化します。

-   ユーザーがアクセス許可を持たない名前空間のフォルダーを参照できないようにします。 [名前空間でアクセス ベースの列挙を有効にする](enable-access-based-enumeration-on-a-namespace.md) 
-   ユーザーが名前空間内のフォルダーにアクセスするときの名前空間またはフォルダー ターゲットへの紹介を有効または無効にします。 [紹介とクライアント フェールバックを有効または無効にする](enable-or-disable-referrals-and-client-failback.md) 
-   クライアントが紹介をキャッシュしてから新しい紹介を要求するまでの時間を調整します。 [クライアントが紹介をキャッシュする時間の長さを変更する](change-the-amount-of-time-that-clients-cache-referrals.md)
-   名前空間サーバーが AD DS をポーリングして最新の名前空間データを取得する方法を最適化します。 [名前空間のポーリングを最適化する](optimize-namespace-polling.md)
-   継承されたアクセス許可を使って、アクセス ベースの列挙が有効になっている名前空間のフォルダーを表示できるユーザーを制御します。 [継承されたアクセス許可とアクセス ベースの列挙を使う](using-inherited-permissions-with-access-based-enumeration.md)

加えて、ターゲット優先順位と呼ばれる DFS 名前空間の拡張機能を使うことで、クライアントが名前空間内のターゲットを含むフォルダーにアクセスするときに受け取るサーバーの一覧 (紹介と呼ばれます) の先頭または末尾に特定のサーバーが常に配置されるように、サーバーの優先順位を指定できます。

-   ユーザーがフォルダー ターゲットに紹介される順序を指定します。 [紹介におけるターゲットの順序指定方法を設定する](set-the-ordering-method-for-targets-in-referrals.md)
-   特定の名前空間サーバーまたはフォルダー ターゲットの紹介順序を上書きします。 [ターゲット優先順位を設定して紹介順序を上書きする](set-target-priority-to-override-referral-ordering.md)

## <a name="see-also"></a>関連項目

-   [名前空間](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [チェックリスト: DFS 名前空間を展開する](checklist-deploy-dfs-namespaces.md)
-   [DFS 名前空間を調整する](tuning-dfs-namespaces.md)


