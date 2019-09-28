---
title: ターゲット優先順位を設定して紹介順序を上書きする
description: この記事では、ターゲット優先順位を指定して紹介順序を上書きする方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f0a6496802d2be16e84ef62c41fea6f0ae9f6438
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386119"
---
# <a name="set-target-priority-to-override-referral-ordering"></a>ターゲット優先順位を設定して紹介順序を上書きする

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

紹介とは、ユーザーが名前空間のルートにアクセスするか、名前空間内のターゲットを持つフォルダーにアクセスしたときに、クライアント コンピューターがドメイン コントローラーまたは名前空間サーバーから受信する、順序付きのターゲット一覧です。 紹介内の各ターゲットは、名前空間のルートまたはフォルダーの順序指定方法に従って順序付けられています。 

ターゲットの順序付け方法を調整するには、個別のターゲットに優先順位を設定します。 たとえば、特定のターゲットをすべてのターゲットの先頭として指定したり、すべてのターゲットの末尾として指定したり、同じコストのすべてのターゲットの先頭 (または末尾) として指定したりできます。

## <a name="to-set-target-priority-on-a-root-target-for-a-domain-based-namespace"></a>ドメインベースの名前空間のルート ターゲットにターゲット優先順位を設定するには

ドメインベースの名前空間のルート ターゲットにターゲット優先順位を設定するには、次の手順を実行します。

1.  **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、優先順位を設定するルート ターゲットのドメインベースの名前空間をクリックします。

3.  **[詳細]** ウィンドウの **[名前空間サーバー]** タブで、優先順位を変更するルート ターゲットを右クリックし、 **[プロパティ]** をクリックします。

4.  **[詳細設定]** タブで、 **[紹介順序を上書きする]** をクリックし、希望する優先順位をクリックします。

    -   **[すべてのターゲットのうち最初のターゲット]**  このターゲットを使用できる場合は、ユーザーが常にこのターゲットを参照するよう指定します。
    -   **[すべてのターゲットのうち最後のターゲット]**  他のすべてのターゲットを使用できない場合にのみ、ユーザーがこのターゲットを参照するよう指定します。
    -   **[コストが等しいターゲットのうち最初のターゲット]**  コストが同じ他のターゲット (通常、同じサイトに含まれる他のターゲット) に優先して、ユーザーがこのターゲットを参照するよう指定します。
    -   **[コストが等しいターゲットのうち最後のターゲット]**  コストが同じターゲット (通常、同じサイトに含まれる他のターゲット) を使用できない場合にのみ、ユーザーがこのターゲットを参照するよう指定します。

## <a name="to-set-target-priority-on-a-folder-target"></a>フォルダー ターゲットにターゲット優先順位を設定するには

フォルダー ターゲットにターゲット優先順位を設定するには、次の手順を実行します。

1.  **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、優先順位を設定するターゲットのフォルダーをクリックします。

3.  **[詳細]** ウィンドウの **[フォルダー ターゲット]** タブで、優先順位を変更するフォルダー ターゲットを右クリックし、 **[プロパティ]** をクリックします。

4.  **[詳細設定]** タブで、 **[紹介順序を上書きする]** をクリックし、希望する優先順位をクリックします。

> [!NOTE]
> Windows PowerShell を使ってターゲット優先順位を設定するには、**ReferralPriorityClass** および **ReferralPriorityRank** パラメーターを指定して [Set-DfsnRootTarget](https://technet.microsoft.com/library/jj884266.aspx) および [Set-DfsnFolderTarget](https://technet.microsoft.com/library/jj884264.aspx) コマンドレットを使います。 これらのコマンドレットは、Windows Server 2012 で導入されました。

## <a name="see-also"></a>関連項目

-   [DFS 名前空間を調整する](tuning-dfs-namespaces.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)