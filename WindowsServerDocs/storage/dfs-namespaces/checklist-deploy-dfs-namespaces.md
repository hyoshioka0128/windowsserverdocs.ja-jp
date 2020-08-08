---
title: 'チェックリスト: DFS 名前空間を展開する'
description: この記事では、DFS 名前空間を構成して展開する方法について説明します。
ms.date: 6/5/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 43cb085eb8af627609371f37f61eab22be91d606
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957720"
---
# <a name="checklist-deploy-dfs-namespaces"></a>チェックリスト: DFS 名前空間を展開する

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

分散ファイル システム (DFS) の名前空間と DFS レプリケーションを使うと、組織全体のユーザーにドキュメント、ソフトウェア、基幹業務データを発行できます。 DFS レプリケーション単独でもデータを配布するには十分ですが、DFS 名前空間を使用すると、フォルダーが複数のサーバーによってホストされるように名前空間を構成できます。これらの各サーバーでは、そのフォルダーの更新されたコピーが保持されます。 これにより、データの可用性が向上し、サーバー間でクライアントの負荷が分散されます。

名前空間内のフォルダーを参照するとき、ユーザーからはフォルダーが複数のサーバーによってホストされていることがわかりません。 ユーザーがフォルダーを開くと、クライアント コンピューターがそのサイトのサーバーに自動的に紹介されます。 同じサイトのサーバーがない場合、Active Directory ディレクトリ サービス (AD DS) で定義された接続コストが最も低いサーバーにクライアントが紹介されるように名前空間を構成できます。

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


## <a name="additional-references"></a>その他の参照情報

-   [名前空間](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771914(v=ws.11))
-   [チェックリスト:DFS 名前空間を調整する](checklist-tune-a-dfs-namespace.md)
-   [レプリケーション](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770278(v=ws.11))
