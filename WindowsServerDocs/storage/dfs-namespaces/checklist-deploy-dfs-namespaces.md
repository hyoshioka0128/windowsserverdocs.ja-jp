---
title: 'チェックリスト: DFS 名前空間を展開する'
description: この記事では、DFS 名前空間を構成して展開する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7f7cca6b67ff6fa8d81e88323381866315f07f33
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842123"
---
# <a name="checklist-deploy-dfs-namespaces"></a>チェックリスト:DFS 名前空間をデプロイします。

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

ドキュメント、ソフトウェア、および基幹業務データを組織全体のユーザーに発行するのには、分散ファイル システム (DFS) 名前空間と DFS レプリケーションを使用できます。 DFS レプリケーション単独ではデータを配布するのにだけで十分ですが、フォルダーが、フォルダーの更新されたコピーを保持するそれぞれの複数のサーバーによってホストされているように、名前空間を構成するのに DFS 名前空間を使用できます。 これにより、データの可用性が向上し、サーバー間でクライアントの負荷が分散されます。

名前空間内のフォルダーを参照するとき、ユーザーからはフォルダーが複数のサーバーによってホストされていることがわかりません。 ユーザーがフォルダーを開くと、クライアント コンピューターがそのサイトのサーバーに自動的に紹介されます。 同じサイト サーバーが使用できない場合は、コストの Active Directory ディレクトリ サービス (AD DS) で定義されている最も低い接続されているサーバーにクライアントが参照する名前空間を構成できます。

DFS 名前空間を展開するには、次のタスクを実行できます。

-   DFS 名前空間の概念と要件を確認します。
[DFS 名前空間の概要](dfs-overview.md)
-   [名前空間の種類を選択します。](choose-a-namespace-type.md)
-   [DFS 名前空間を作成します。](create-a-dfs-namespace.md) 
-   Windows Server 2008 モードのドメイン ベース名前空間に既存のドメイン ベース名前空間を移行します。 [ドメイン ベースの Namespace を Windows Server 2008 モードに移行します。](migrate-a-domain-based-namespace-to-windows-server-2008-mode.md) 
-   ドメイン ベースの名前空間に名前空間サーバーを追加することで可用性を高めます。 [ドメイン ベース DFS Namespace に Namespace サーバーを追加します。](add-namespace-servers-to-a-domain-based-dfs-namespace.md)
-   名前空間にフォルダーを追加します。 [DFS Namespace にフォルダーを作成します。](create-a-folder-in-a-dfs-namespace.md)
-   名前空間内のフォルダーにフォルダー ターゲットを追加します。 [フォルダー ターゲットを追加します。](add-folder-targets.md)
-   DFS レプリケーション (オプション) を使ってフォルダー ターゲット間でコンテンツをレプリケートします。 [DFS レプリケーションを使用してフォルダー ターゲットをレプリケートします。](replicate-folder-targets-using-dfs-replication.md)


## <a name="see-also"></a>関連項目

-   [名前空間](https://technet.microsoft.com/library/cc771914(v=ws.11).aspx)
-   [チェックリスト:DFS Namespace を調整します。](checklist-tune-a-dfs-namespace.md)
-   [レプリケーション](https://technet.microsoft.com/library/cc770278(v=ws.11).aspx)


