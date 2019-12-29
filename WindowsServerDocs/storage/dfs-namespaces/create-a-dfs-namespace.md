---
title: DFS 名前空間を作成する
description: この記事では、DFS 名前空間を作成する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f4d4b86dd1a105576ac4d1749213696b319ba528
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402209"
---
# <a name="create-a-dfs-namespace"></a>DFS 名前空間を作成する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

新しい名前空間を作成するには、DFS 名前空間の役割サービスをインストールするときに、サーバー マネージャーを使って名前空間を作成できます。 Windows PowerShell セッションから [New-DfsnRoot コマンドレット](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot)を使うこともできます。 

DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。 

または、次の手順を使って、役割サービスをインストールした後に名前空間を作成することができます。

## <a name="to-create-a-namespace"></a>名前空間を作成するには

1.  **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードを右クリックし、 **[新しい名前空間]** をクリックします。

3.  **名前空間の新規作成ウィザード**の手順に従います。

    フェールオーバー クラスターでスタンドアロン名前空間を作成するには、**名前空間の新規作成ウィザード**の **[名前空間サーバー]** でクラスター化されたファイル サーバー インスタンスの名前を指定します。

> [!IMPORTANT]
> フォレストの機能レベルが Windows Server 2003 以上の場合を除き、Windows Server 2008 モードを使用してドメインベースの名前空間を作成しないでください。 このようにすると、DFS フォルダーを削除できない名前空間が生成されるため、次のエラーメッセージが表示されます。"フォルダーを削除できません。 このファンクションを完了できません" というエラー メッセージが生成される可能性があります。

## <a name="see-also"></a>関連項目

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [名前空間の種類を選択する](choose-a-namespace-type.md)
-   [ドメインベースの DFS 名前空間に名前空間サーバーを追加する](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)。


