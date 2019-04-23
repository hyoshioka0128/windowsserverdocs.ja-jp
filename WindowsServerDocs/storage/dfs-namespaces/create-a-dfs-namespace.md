---
title: DFS 名前空間を作成する
description: この記事では、DFS 名前空間を作成する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4256e124e75be72f94cbd35c182edfe38e92bc90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847503"
---
# <a name="create-a-dfs-namespace"></a>DFS 名前空間を作成する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

新しい名前空間を作成するには、DFS 名前空間の役割サービスをインストールするときに、サーバー マネージャーを使って名前空間を作成できます。 Windows PowerShell セッションから [New-DfsnRoot コマンドレット](https://docs.microsoft.com/powershell/module/dfsn/new-dfsnroot)を使うこともできます。 

DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。 

または、次の手順を使って、役割サービスをインストールした後に名前空間を作成することができます。

## <a name="to-create-a-namespace"></a>名前空間を作成するには

1.  **[スタート]** をクリックし、**[管理ツール]** をポイントして、**[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードを右クリックし、**[新しい名前空間]** をクリックします。

3.  **名前空間の新規作成ウィザード**の手順に従います。

    フェールオーバー クラスターでスタンドアロン名前空間を作成するには、**名前空間の新規作成ウィザード**の **[名前空間サーバー]** でクラスター化されたファイル サーバー インスタンスの名前を指定します。

> [!IMPORTANT]
> フォレストの機能レベルが Windows Server 2003 以上でない限り、Windows Server 2008 モードを使用してドメイン ベースの名前空間を作成しようとしないでください。 そうと、名前空間を削除できません DFS フォルダーでは、次のエラー メッセージを生成することができます。"フォルダーを削除できません。 このファンクションを完了できません" というエラー メッセージが生成される可能性があります。

## <a name="see-also"></a>関連項目

-   [DFS 名前空間を展開します。](deploying-dfs-namespaces.md)
-   [Namespace の種類を選択します。](choose-a-namespace-type.md)
-   [ドメイン ベース DFS Namespace に Namespace サーバーを追加します。](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)。


