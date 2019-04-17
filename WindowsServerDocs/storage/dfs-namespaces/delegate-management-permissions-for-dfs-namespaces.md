---
title: "DFS 名前空間の管理アクセス許可を委任する"
description: "この記事では、DFS 名前空間の管理アクセス許可を委任する方法と、名前空間タスクを既定で実行できるグループについて説明します。"
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e584b49639a83e4ab1da142a999741ae4ac7ff84
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="delegate-management-permissions-for-dfs-namespaces"></a>DFS 名前空間の管理アクセス許可を委任する

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

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

\*ユーザーが名前空間サーバーでローカル Administrators グループのメンバーとなっている場合を除き、スタンドアロン名前空間を管理する管理アクセス許可を委任しても、ユーザーは **[委任]** タブを使ってセキュリティを表示および管理できるようになりません。 この問題は、DFS 管理スナップインがスタンドアロン名前空間の随意アクセス制御リスト (DACL) をレジストリから取得できないために発生します。 スナップインに委任情報を表示できるようにするには、Microsoft<sup>®</sup> サポート技術情報「[KB314837: レジストリへのリモート アクセスを管理する方法](http://go.microsoft.com/fwlink?linkid=46803)」の手順に従う必要があります。