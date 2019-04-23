---
title: 個人用セッション デスクトップを使用して、リモート デスクトップ サービス
description: Rds. によってデスクトップを割り当てられている個人に合わせたを共有する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/16/2016
manager: dongill
ms.openlocfilehash: 41f6a28c1b754a5277a0966a87dae08a6aa34e08
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875953"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>個人用セッション デスクトップを使用して、リモート デスクトップ サービス

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

個人用セッション デスクトップを使用して、クラウド コンピューティング環境でのサーバー ベースのパーソナル デスクトップを展開できます。  (クラウド コンピューティング環境があるファブリックで HYPER-V サーバーと Microsoft Azure のクラウドまたは Microsoft のクラウド プラットフォームなど、ゲストの仮想マシンを区別します。)個人用セッション デスクトップ機能は、各ユーザーが管理者権限を持つ自分個人のセッション ホストに割り当てられている、新しい種類のセッション コレクションを作成するリモート デスクトップ サービス セッション ベースのデスクトップ展開シナリオを拡張します。 

作成および個人用セッション デスクトップ コレクションを管理するには、次の情報を使用します。

## <a name="create-a-personal-session-desktop-collection"></a>個人用セッション デスクトップ コレクションを作成します。

個人用セッション デスクトップ コレクションを作成するのにには、新規 RDSessionCollection コマンドレットを使用します。 次の 3 つのパラメーターは、個人用セッション デスクトップに必要な構成情報を提供します。

- **-PersonalUnmanaged** -個人のセッション ホスト サーバーにユーザーの割り当てできるようにする、セッション コレクションの型を指定します。 このパラメーターを指定しない場合、コレクションは、[次へ] の使用可能なセッションのホストにユーザーが割り当てられているサインインしたときに、従来の RD セッション ホスト コレクションとして作成されます。
- **-GrantAdministrativePrivilege**を使用する場合 - **- PersonalUnmanaged**セッションのホストに割り当てられているユーザーが管理者特権を与えられることを指定します。 このパラメーターを使用しない場合、ユーザーは、標準ユーザー特権のみが付与されます。
- **-AutoAssignUser** - を使用する場合は、 **- PersonalUnmanaged**、RD 接続ブローカーを接続する新しいユーザーが、割り当てられていないセッションのホストに自動的に割り当てられているを指定します。 コレクションに割り当てられていないセッション ホストがない、エラー メッセージが表示されます。 必要がある場合、このパラメーターを使用しない[セッション ホストにユーザーを手動で割り当てる](#manually-assign-a-user-to-a-personal-session-host)サインインします。

## <a name="manually-assign-a-user-to-a-personal-session-host"></a>ユーザーを手動で個人のセッション ホストを割り当てる
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
 
## <a name="removing-a-user-assignment-from-a-personal-session-host"></a>個人のセッション ホストからユーザーの割り当てを削除します。
使用して、**削除 RDPersonalSessionDesktopAssignment**コマンドレットを個人用セッション デスクトップとユーザー間の関連付けを削除します。 コマンドレットには、次のパラメーターがサポートされています。

-CollectionName \<string\>

-ConnectionBroker \<string\>

-Force

-Name \<string\>

-User \<string\>

**– 強制**コマンドを強制的にユーザーの確認を要求せずに実行します。

## <a name="query-user-assignments"></a>クエリのユーザーの割り当て
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

## <a name="hardware-accelerated-graphics"></a>ハードウェアの高速グラフィック
Windows Server 2016 では、OpenGL をサポートする RemoteFX 3D グラフィックス アダプター (vGPU) テクノロジを拡張し、シングル ユーザーの Windows Server 2016 ゲスト Vm をサポートします。 高速化されたグラフィックスを必要とする、ホスト アプリケーションのサポートを提供する新しい vGPU 機能では、個人用セッション デスクトップを組み合わせることができます。 またはも高速化されたグラフィックスを必要とする、ホスト アプリケーションのサポートを提供する新しい独立したデバイスの割り当て (DDA) 機能を持つ個人用セッション デスクトップを組み合わせることができます。
