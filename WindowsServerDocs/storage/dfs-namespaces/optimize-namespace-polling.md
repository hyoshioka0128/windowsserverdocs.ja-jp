---
title: 名前空間のポーリングを最適化する
description: この記事では、名前空間のポーリングを最適化して、名前空間サーバー間で一貫性のあるドメイン ベースの名前空間を維持する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 995b01604b680746c4b0d6502b3b3968503d4210
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878273"
---
# <a name="optimize-namespace-polling"></a>名前空間のポーリングを最適化する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間サーバー全体でドメイン ベースの名前空間の整合性を保つには、それぞれの名前空間のサーバーが定期的に Active Directory Domain Services (AD DS) をポーリングして、最新の名前空間データを取得する必要があります。 

## <a name="to-optimize-namespace-polling"></a>名前空間のポーリングを最適化するには

次の手順に従って、名前空間のポーリングの実行方法を最適化できます。

1.  **[スタート]** をクリックし、**[管理ツール]** をポイントして、**[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、ドメインベースの名前空間を右クリックし、**[プロパティ]** をクリックします。

3.  **[詳細設定]** タブで、整合性とスケーラビリティのどちらのために名前空間を最適化するのかを選択します。

    -   名前空間をホストする名前空間サーバーが 16 台以下の場合は、**[整合性の最適化]** を選択します。
    -   名前空間サーバーが 17 台以上ある場合は **[スケーラビリティの最適化]** を選択します。 これにより、プライマリ ドメイン コントローラー (PDC) エミュレーターへの負荷が軽減されますが、名前空間に加えられた変更をすべての名前空間サーバーに対してレプリケートするために要する時間は長くなります。 変更がすべてのサーバーに対してレプリケートされるまで、ユーザーには名前空間が不整合な状態で表示される場合があります。

> [!NOTE]
> Windows PowerShell を使用して、名前空間のポーリング モードを設定するには、使用、[セット DfsnRoot EnableRootScalability](https://technet.microsoft.com/library/jj884281.aspx)コマンドレットで、Windows Server 2012 で導入されました。

## <a name="see-also"></a>関連項目

-   [DFS 名前空間のチューニング](tuning-dfs-namespaces.md)
-   [Delegate Management Permissions for DFS 名前空間](delegate-management-permissions-for-dfs-namespaces.md)