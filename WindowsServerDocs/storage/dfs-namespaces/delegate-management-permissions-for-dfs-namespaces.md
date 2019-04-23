---
title: DFS 名前空間の管理アクセス許可を委任する
description: この記事では、DFS 名前空間の管理アクセス許可を委任する方法と、名前空間タスクを既定で実行できるグループについて説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7895432ca16dd13c6425d966f99104fc03db100d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829493"
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>DFS 名前空間の管理アクセス許可を委任する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

次の表では、基本的な名前空間タスクを既定で実行できるグループと、それらのタスクを実行する権限を委任する方法について説明します。

|タスク | このタスクを既定で実行できるグループ | 委任方法 |
|---|---|---|
|ドメイン ベースの名前空間を作成する|名前空間が構成されているドメインの Domain Admins グループ|コンソール ツリーで **[名前空間]** ノードを右クリックし、**[管理アクセス許可の委任]** をクリックします。 または、[Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) および [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) を使います。 Windows PowerShell コマンドレット (Windows Server 2012 で導入)。 名前空間サーバー上のローカル Administrators グループにもユーザーを追加する必要があります。|
|ドメインベースの名前空間に名前空間サーバーを追加する|名前空間が構成されているドメインの Domain Admins グループ| コンソール ツリーでドメイン ベースの名前空間を右クリックし、**[管理アクセス許可の委任]** をクリックします。 または、[Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) および [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) を使います。 Windows PowerShell コマンドレット (Windows Server 2012 で導入)。 追加する名前空間サーバー上のローカル Administrators グループにもユーザーを追加する必要があります。|
|ドメイン ベースの名前空間を管理する|各名前空間サーバー上のローカル Administrators グループ| コンソール ツリーでドメイン ベースの名前空間を右クリックし、**[管理アクセス許可の委任]** をクリックします。 |
|スタンドアロン名前空間を作成する|名前空間サーバー上のローカル Administrators グループ| 名前空間サーバー上のローカル Administrators グループにもユーザーを追加します。 |
|スタンドアロン名前空間を管理する*|名前空間サーバー上のローカル Administrators グループ| コンソール ツリーでスタンドアロン名前空間を右クリックし、**[管理アクセス許可の委任]** をクリックします。 または、[Set-DfsnRoot GrantAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) および [Set-DfsnRoot RevokeAdminAccounts](https://technet.microsoft.com/itpro/powershell/windows/dfsn/set-dfsnroot) を使います。 Windows PowerShell コマンドレット (Windows Server 2012 で導入)。|
|レプリケーション グループを作成するか、フォルダーで DFS レプリケーションを有効にする|名前空間が構成されているドメインの Domain Admins グループ| コンソール ツリーでレプリケーション ノードを右クリックし、**[管理アクセス許可の委任]** をクリックします。 |

<br />

\*スタンドアロンの名前空間を管理する管理アクセス許可の委任は付与されませんユーザーを表示およびを使用してセキュリティを管理する機能、**委任**タブ、ユーザーのローカルの Administrators グループのメンバーである場合を除き、名前空間サーバー。 この問題は、DFS 管理スナップインがスタンドアロン名前空間の随意アクセス制御リスト (DACL) をレジストリから取得できないために発生します。 委任情報を表示するスナップインを有効にするには、Microsoft では手順に従って必要があります<sup>®</sup>サポート技術情報の記事。[KB314837:レジストリへのリモート アクセスを管理する方法](https://go.microsoft.com/fwlink?linkid=46803)