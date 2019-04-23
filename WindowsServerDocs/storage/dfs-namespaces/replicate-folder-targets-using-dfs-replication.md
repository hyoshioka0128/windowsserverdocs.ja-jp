---
title: DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする
description: この記事は、DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 098ffd1a47891d2355742682a002f80dcfc59650
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878083"
---
# <a name="replicate-folder-targets-using-dfs-replication"></a>DFS レプリケーションを使ってフォルダー ターゲットをレプリケートする

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008

DFS レプリケーションを使うと、フォルダー ターゲットの内容を同期された状態に維持し、クライアント コンピューターが紹介されるフォルダー ターゲットに関係なくユーザーに同じファイルが表示されるようにすることができます。

## <a name="to-replicate-folder-targets-using-dfs-replication"></a>DFS レプリケーションを使ってフォルダー ターゲットをレプリケートするには

1.  **[スタート]** をクリックし、**[管理ツール]** をポイントして、**[DFS 管理]** をクリックします。

2.  コンソール ツリーの **[名前空間]** ノードで、複数のターゲットを持つフォルダーを右クリックし、**[フォルダーのレプリケート]** をクリックします。

3.  フォルダーのレプリケート ウィザードの指示に従います。

> [!NOTE]
> [Suspend-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/suspend-dfsreplicationgroup) および [Sync-DfsReplicationGroup](https://technet.microsoft.com/itpro/powershell/windows/dfsr/sync-dfsreplicationgroup) コマンドレットを使う場合を除き、構成の変更はすぐにすべてのメンバーに適用されるわけではありません。 新しい構成は、すべてのドメイン コントローラーにレプリケートされる必要があります。レプリケーション グループ内の各メンバーは、最も近いドメイン コントローラーをポーリングして変更内容を取得する必要があります。 これにかかる時間量は、Active Directory ディレクトリ サービス (AD DS) レプリケーションの待機時間と、時間の長いによって異なります。 各メンバーのポーリング間隔 (60 分)。 変更内容をすぐにポーリングをするには、コマンド プロンプト ウィンドウを開き、レプリケーション グループのメンバーごとに、 <br /> dfsrdiag.exe PollAD /Member:DOMAIN\Server1
<br />
Windows PowerShell セッションから、その場合は、使用、 [Update DfsrConfigurationFromAD](https://technet.microsoft.com/itpro/powershell/windows/dfsr/update-dfsrconfigurationfromad)コマンドレットで、Windows Server 2012 R2 で導入されました。

## <a name="see-also"></a>関連項目

-   [DFS 名前空間を展開します。](deploying-dfs-namespaces.md)
-   [Delegate Management Permissions for DFS 名前空間](delegate-management-permissions-for-dfs-namespaces.md)
-   [DFS レプリケーション](../dfs-replication/dfsr-overview.md)