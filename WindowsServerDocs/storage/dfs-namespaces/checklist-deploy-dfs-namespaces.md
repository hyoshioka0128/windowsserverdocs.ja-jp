---
title: 'チェックリスト: DFS 名前空間を展開する'
description: この記事では、DFS 名前空間を構成して展開する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: ab38c41c32ec88285a69fb94e62abc1453ddc3d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402267"
---
# <a name="checklist-deploy-dfs-namespaces"></a>チェックリスト:DFS 名前空間を展開する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

分散ファイルシステム (DFS) 名前空間と DFS レプリケーションを使用すると、組織全体のユーザーにドキュメント、ソフトウェア、および基幹業務データを発行できます。 データの配布には DFS レプリケーションだけで十分ですが、DFS 名前空間を使用すると、フォルダーが複数のサーバーによってホストされるように名前空間を構成できます。各サーバーは、フォルダーの更新されたコピーを保持します。 これにより、データの可用性が向上し、サーバー間でクライアントの負荷が分散されます。

名前空間内のフォルダーを参照するとき、ユーザーからはフォルダーが複数のサーバーによってホストされていることがわかりません。 ユーザーがフォルダーを開くと、クライアント コンピューターがそのサイトのサーバーに自動的に紹介されます。 同じサイトサーバーが使用できない場合は、Active Directory Directory Services (AD DS) で定義されているように、接続コストが最も低いサーバーをクライアントが参照するように名前空間を構成できます。

DFS 名前空間を展開するには、次のタスクを実行できます。

-   DFS 名前空間の概念と要件を確認します。
[DFS 名前空間の概要](dfs-overview.md)
-   [名前空間の種類の選択](choose-a-namespace-type.md)
-   [DFS 名前空間を作成する](create-a-dfs-namespace.md) 
-   Windows Server 2008 モードのドメイン ベース名前空間に既存のドメイン ベース名前空間を移行します。 [ドメインベースの名前空間を Windows Server 2008 モードに移行する](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   ドメイン ベースの名前空間に名前空間サーバーを追加することで可用性を高めます。 [ドメインベースの DFS 名前空間に名前空間サーバーを追加する](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   名前空間にフォルダーを追加します。 [DFS 名前空間でフォルダーを作成する](create-a-folder-in-a-dfs-namespace.md)
-   名前空間内のフォルダーにフォルダー ターゲットを追加します。 [フォルダー ターゲットの追加](add-folder-targets.md)
-   DFS レプリケーション (オプション) を使ってフォルダー ターゲット間でコンテンツをレプリケートします。 [DFS レプリケーションを使用してフォルダーターゲットをレプリケートする](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>関連項目

-   [名前空間](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [チェックリスト:DFS 名前空間を調整する](checklist-tune-a-dfs-namespace.md)
-   [レプリケーション](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


