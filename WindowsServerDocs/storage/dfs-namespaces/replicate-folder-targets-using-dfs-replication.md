---
title: DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする
description: この記事は、DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 3a4f76e43c2dbf5296afd163055adeafb36a5576
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474399"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする

> 適用対象: Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008

DFS レプリケーションを使うと、フォルダー ターゲットの内容を同期された状態に維持し、クライアント コンピューターが紹介されるフォルダー ターゲットに関係なくユーザーに同じファイルが表示されるようにすることができます。

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>DFS レプリケーションを使ってフォルダー ターゲットをレプリケートするには

1.  [**スタート**] をクリックし、[**管理ツール**] をポイントして、[**DFS 管理**] をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、複数のターゲットを持つフォルダーを右クリックし、**[フォルダーのレプリケート]** をクリックします。

3.  フォルダーのレプリケート ウィザードの指示に従います。

> [!NOTE]
> [Suspend-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) および [Sync-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup) コマンドレットを使う場合を除き、構成の変更はすぐにすべてのメンバーに適用されるわけではありません。 新しい構成は、すべてのドメイン コントローラーにレプリケートされる必要があります。レプリケーション グループ内の各メンバーは、最も近いドメイン コントローラーをポーリングして変更内容を取得する必要があります。 この処理にかかる時間は、Active Directory ディレクトリ サービス (AD DS) のレプリケーションの待機時間と、各メンバーの長いポーリング間隔 (60 分) によって決まります。 変更内容をすぐにポーリングをするには、コマンド プロンプト ウィンドウを開き、レプリケーション グループのメンバーごとに、 <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
これを Windows PowerShell セッションから行うには、Windows Server 2012 R2 で導入された [Update-DfsrConfigurationFromAD](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad) コマンドレットを使います。

## <a name="additional-references"></a>その他のリファレンス

-   [DFS 名前空間を展開する](deploying-dfs-namespaces.md)
-   [DFS 名前空間の管理アクセス許可を委任する](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS レプリケーション](../dfs-replication/dfsr-overview.md)