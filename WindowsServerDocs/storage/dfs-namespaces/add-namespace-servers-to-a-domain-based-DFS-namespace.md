---
title: ドメインベースの DFS 名前空間に名前空間サーバーを追加する
description: この記事では、DFS 管理を使って名前空間をホストする追加の名前空間サーバーを指定する方法について説明します。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ada742f53435b8b3894fc1a19eee4dd69d3777d6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957810"
---
# <a name="add-namespace-servers-to-a-domain-based-dfs-namespace"></a>ドメインベースの DFS 名前空間に名前空間サーバーを追加する

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

名前空間をホストする追加の名前空間サーバーを指定することによって、ドメイン ベース名前空間の可用性を高めることができます。

## <a name="to-add-a-namespace-server-to-a-domain-based-namespace"></a>ドメインベースの名前空間に名前空間サーバーを追加するには

DFS の管理を使ってドメイン ベース名前空間に名前空間サーバーを追加するには、次の手順に従います。

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、ドメインベースの名前空間を右クリックし、**[名前空間を追加]** をクリックします。

3.  別のサーバーのパスを入力するか、**[参照]** をクリックしてサーバーを見つけます。

> [!NOTE]
> スタンドアロン名前空間では単一の名前空間サーバーのみサポートされるため、この手順は適用されません。 スタンドアロン名前空間の可用性を高めるには、名前空間の新規作成ウィザードで名前空間サーバーとしてフェールオーバー クラスターを指定します。


> [!TIP]
> Windows PowerShell を使って名前空間サーバーを追加するには、[New-DfsnRootTarget コマンドレット](/powershell/module/dfsn/new-dfsnroottarget)を使います。 DFSN Windows PowerShell モジュールは、Windows Server 2012 で導入されました。

## <a name="additional-references"></a>その他の参照情報

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [DFS 名前空間サーバーの要件を確認する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753448(v=ws.11))
-   [DFS 名前空間を作成する](create-a-dfs-namespace.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
