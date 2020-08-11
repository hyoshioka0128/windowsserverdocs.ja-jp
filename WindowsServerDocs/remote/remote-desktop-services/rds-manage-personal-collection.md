---
title: RDS で個人用デスクトップ セッション コレクションを管理する
description: RDS の展開に、RDSH および RemoteApp プログラムを追加する方法について説明します。
ms.author: elizapo
ms.date: 11/08/2016
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: bd6c91b7f022e60e488c90776e0981523da7bccb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961656"
---
# <a name="manage-your-personal-desktop-session-collections"></a>個人用デスクトップ セッション コレクションを管理する

以下の情報を使用して、リモート デスクトップ サービスで個人用デスクトップ セッション コレクションを管理します。

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>ユーザーを個人用セッション ホストに手動で割り当てる
コレクション内の個人用セッション ホスト サーバーにユーザーを手動で割り当てるには、**Set-RDPersonalSessionDesktopAssignment** コマンドレットを使用します。 このコマンドレットは、次のパラメーターをサポートしています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

- **–CollectionName** - 個人用セッション デスクトップ コレクションの名前を指定します。 このパラメーターは必須です。
- **– ConnectionBroker** - リモート デスクトップの展開のためのリモート デスクトップ接続ブローカー (RD 接続ブローカー) サーバーを指定します。 値を指定しない場合、コマンドレットではローカル コンピューターの完全修飾ドメイン名 (FQDN) が使用されます。
- **–User** - 個人用セッション デスクトップに関連付けるユーザー アカウントを DOMAIN\User の形式で指定します。 このパラメーターは必須です。
- **–Name** - セッション ホスト サーバーの名前を指定します。 このパラメーターは必須です。 ここで識別されるセッション ホストは、 **-CollectionName** パラメーターで指定するコレクションのメンバーである必要があります。

**Import-RDPersonalSessionDesktopAssignment** コマンドレットは、ユーザー アカウントと個人用セッション デスクトップとの関連付けをテキスト ファイルからインポートします。 このコマンドレットは、次のパラメーターをサポートしています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string>

**–Path** は、インポートするファイルのパスとファイル名を指定します。

## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>個人用セッション ホストからのユーザー割り当ての削除
個人用セッション デスクトップとユーザー間の関連付けを削除するには、**Remove-RDPersonalSessionDesktopAssignment** コマンドレットを使用します。 このコマンドレットは、次のパラメーターをサポートしています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

-User \<string\>

**–Force** を指定すると、ユーザーへの確認なしにコマンドが強制的に実行されます。

## <a name="query-user-assignments"></a>ユーザー割り当てをクエリする
個人用セッション デスクトップおよび関連付けられているユーザー アカウントの一覧を取得するには、**Get-RDPersonalSessionDesktopAssignment** コマンドレットを使用します。 このコマンドレットは、次のパラメーターをサポートしています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

このコマンドレットを実行すると、コレクション名、ユーザー名、またはセッション デスクトップ名によるクエリが可能です。 **–CollectionName** パラメーターだけを指定した場合、コマンドレットは、セッション ホストおよび関連付けられているユーザーの一覧を返します。 **–User** パラメーターも指定した場合、そのユーザーに関連付けられているセッション ホストが返されます。 **–Name** パラメーターを指定した場合、そのセッション ホストに関連付けられているユーザーが返されます。


**Export-RDPersonalPersonalDesktopAssignment** コマンドレットは、ユーザーと個人用仮想デスクトップとの現在の関連付けをテキスト ファイルにエクスポートします。 このコマンドレットは、次のパラメーターをサポートしています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string\>


新しいコマンドレットはすべて、共通パラメーターの -Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer、および -OutVariable をサポートしています。 詳細については、「[about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216)」を参照してください。
