---
title: RDS で個人用デスクトップ セッション コレクションを管理します。
description: RDS デプロイに RDSH および RemoteApp プログラムおよび追加する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 286c7ba4bd4428669d135c35c825033d22b8f40e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865723"
---
## <a name="manage-your-personal-desktop-session-collections"></a>個人用デスクトップ セッション コレクションを管理します。

リモート デスクトップ サービスで個人のデスクトップ セッション コレクションを管理するのにには、次の情報を使用します。

### <a name="manually-assign-a-user-to-a-personal-session-host"></a>ユーザーを手動で個人のセッション ホストを割り当てる
使用して、**セット RDPersonalSessionDesktopAssignment**コマンドレットを手動でユーザーをコレクション内の個人のセッション ホスト サーバーを割り当てます。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\> 

-User \<string\>

-Name \<string\>

- **– CollectionName** -個人用セッション デスクトップ コレクションの名前を指定します。 このパラメーターは必須です。
- **– ConnectionBroker** -リモート デスクトップ接続ブローカー (RD 接続ブローカー) サーバー、リモート デスクトップの展開を指定します。 値を指定しない場合、コマンドレットは、ローカル コンピューターの完全修飾ドメイン名 (FQDN) を使用します。
- **– ユーザー** -に関連付ける個人用セッション デスクトップで、domain \user 形式でユーザー アカウントを指定します。 このパラメーターは必須です。
- **– 名前**-セッション ホスト サーバーの名前を指定します。 このパラメーターは必須です。 ここで識別されるセッションのホストは、コレクションのメンバーである必要がありますが、 **- CollectionName**パラメーターを指定します。

**インポート RDPersonalSessionDesktopAssignment**コマンドレットは、テキスト ファイルからユーザー アカウントと個人用セッション デスクトップ間の関連付けをインポートします。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string>

**– パス**インポートするファイルのパスとファイル名を指定します。
 
### <a name="removing-a-user-assignment-from-a-personal-session-host"></a>個人のセッション ホストからユーザーの割り当てを削除します。
使用して、**削除 RDPersonalSessionDesktopAssignment**コマンドレットを個人用セッション デスクトップとユーザー間の関連付けを削除します。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

-User \<string\>

**– 強制**コマンドを強制的にユーザーの確認を要求せずに実行します。

### <a name="query-user-assignments"></a>クエリのユーザーの割り当て
使用して、 **Get RDPersonalSessionDesktopAssignment**個人用セッション デスクトップと関連付けられているユーザー アカウントの一覧を取得するコマンドレットです。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-User \<string\>

-Name \<string\>

コレクション名、ユーザー名、またはセッション デスクトップの名前では、クエリに、コマンドレットを実行できます。 のみを指定する場合、 **– CollectionName**パラメーター、コマンドレットは、セッションのホストと関連付けられているユーザーの一覧を返します。 指定する場合、 **– ユーザー**パラメーター、そのユーザーに関連付けられているセッションのホストが返されます。 指定した場合、 **– 名前**パラメーター、そのセッションのホストに関連付けられているユーザーが返されます。 


**エクスポート RDPersonalPersonalDesktopAssignment**コマンドレットでは、現在のユーザーと個人用仮想デスクトップの間の関連付けをテキスト ファイルにエクスポートします。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Path \<string\>


すべての新しいコマンドレットは共通のパラメーターのサポート:-Verbose、--debug、-erroraction、-errorvariable、-OutBuffer、および - OutVariable します。 詳細については、「[about_CommonParameters](https://go.microsoft.com/fwlink/p/?LinkID=113216)」を参照してください。
