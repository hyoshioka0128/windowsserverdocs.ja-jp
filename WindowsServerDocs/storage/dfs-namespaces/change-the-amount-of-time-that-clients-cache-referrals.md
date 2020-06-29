---
title: クライアントが紹介をキャッシュする時間の長さを変更する
description: この記事では、クライアントが紹介をキャッシュする時間の長さを変更する方法について説明します
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: d421a14c2a6021d45cd16f30c526ff1670ae62e3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475199"
---
# <a name="change-the-amount-of-time-that-clients-cache-referrals"></a>クライアントが紹介をキャッシュする時間の長さを変更する

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

紹介とは、ユーザーが名前空間のルートにアクセスするか、名前空間内のターゲットを持つフォルダーにアクセスしたときに、クライアント コンピューターがドメイン コントローラーまたは名前空間サーバーから受信する、順序付きのターゲット一覧です。 クライアントが紹介をキャッシュしてから新しい紹介を要求するまでの時間を調整できます。

## <a name="to-change-the-amount-of-time-that-clients-cache-namespace-root-referrals"></a>クライアントが名前空間のルートの紹介をキャッシュする時間の長さを変更するには

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、名前空間を右クリックし、**[プロパティ]** をクリックします。

3.  **[紹介]** タブの **[キャッシュ時間 (秒)]** ボックスに、クライアントが名前空間のルートの紹介をキャッシュする時間の長さを秒単位で入力します。 既定値は 300 秒 (5 分) です。

> [!TIP]
> Windows PowerShell を使ってクライアントが名前空間ルート紹介をキャッシュする時間の長さを変更するには、[Set-DfsnRoot TimeToLiveSec](https://technet.microsoft.com/library/jj884281.aspx) コマンドレットを使います。 これらのコマンドレットは、Windows Server 2012 で導入されました。

## <a name="to-change-the-amount-of-time-that-clients-cache-folder-referrals"></a>クライアントがフォルダーの紹介をキャッシュする時間の長さを変更するには

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、ターゲットを持つフォルダーを右クリックし、**[プロパティ]** をクリックします。

3.  **[紹介]** タブの **[キャッシュ時間 (秒)]** ボックスに、クライアントがフォルダーの紹介をキャッシュする時間の長さを秒単位で入力します。 既定値は 1800 秒 (30 分) です。

## <a name="additional-references"></a>その他のリファレンス

-   [DFS 名前空間を調整する](tuning-dfs-namespaces.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)


