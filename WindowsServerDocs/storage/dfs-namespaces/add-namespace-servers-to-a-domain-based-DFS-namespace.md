---
title: ドメインベースの DFS 名前空間に名前空間サーバーを追加する
description: この記事では、DFS 管理を使って名前空間をホストする追加の名前空間サーバーを指定する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f00a6419bae1951a7c1597212d3c37676a4db90e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961254"
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

## <a name="additional-references"></a>その他のリファレンス

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [DFS 名前空間サーバーの要件を確認する](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753448(v=ws.11))
-   [DFS 名前空間を作成する](create-a-dfs-namespace.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
