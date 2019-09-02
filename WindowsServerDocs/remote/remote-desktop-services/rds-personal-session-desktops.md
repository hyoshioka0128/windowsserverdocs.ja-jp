---
title: リモート デスクトップ サービスで個人用セッション デスクトップを使用する
description: RDS から、個人用に設定された割り当て済みデスクトップを共有する方法について説明します。
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
ms.openlocfilehash: 723e68bad79e7723aaa0690c312e20ccf47c47b0
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743503"
---
# <a name="use-personal-session-desktops-with-remote-desktop-services"></a>リモート デスクトップ サービスで個人用セッション デスクトップを使用する

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

個人用セッション デスクトップを使用して、クラウド コンピューティング環境でサーバー ベースの個人用デスクトップを展開できます。  (クラウド コンピューティング環境では、ファブリック Hyper-V サーバーと、Microsoft Azure クラウドや Microsoft クラウド プラットフォームなどのゲスト仮想マシンとが区別されます)。個人用セッション デスクトップ機能は、各ユーザーが管理者特権を持つ自身の個人用セッション ホストに割り当てられている新しい種類のセッション コレクションを作成するように、リモート デスクトップ サービスのセッション ベースのデスクトップ展開シナリオを拡張します。 

作成および個人用セッション デスクトップ コレクションを管理するには、次の情報を使用します。

## <a name="create-a-personal-session-desktop-collection"></a>個人用セッション デスクトップ コレクションを作成する

個人用セッション デスクトップ コレクションを作成するには、New-RDSessionCollection コマンドレットを使用します。 次の 3 つのパラメーターは、個人用セッション デスクトップに必要な構成情報を提供します。

- **-PersonalUnmanaged** - 個人用セッション ホスト サーバーにユーザーを割り当てられようにするセッション コレクションの種類を指定します。 このパラメーターを指定しない場合、コレクションは従来の RD セッション ホスト コレクションとして作成されます。ここではユーザーは、サインインしたときに、次に使用可能なセッション ホストに割り当てられます。
- **-GrantAdministrativePrivilege** - **-PersonalUnmanaged** を使用する場合、セッション ホストに割り当てられているユーザーに管理者特権を与えられることを指定します。 このパラメーターを使用しない場合、ユーザーは、標準のユーザー特権のみが付与されます。
- **-AutoAssignUser** - **-PersonalUnmanaged** を使用する場合、RD 接続ブローカーを通じて接続する新しいユーザーが、割り当てられていないセッション ホストに自動的に割り当てられることを指定します。 割り当てられていないセッション ホストがコレクションにない場合は、エラー メッセージが表示されます。 このパラメーターを使用しない場合は、サインインする前に、[ユーザーをセッション ホストに手動で割り当てる](#manually-assign-a-user-to-a-personal-session-host)必要があります。

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

## <a name="hardware-accelerated-graphics"></a>ハードウェア アクセラレータに対応したグラフィックス
Windows Server 2016 では、OpenGL をサポートするように RemoteFX 3D グラフィックス アダプター (vGPU) テクノロジを拡張し、シングル ユーザー Windows Server 2016 ゲスト VM をサポートします。 個人用セッション デスクトップと新しい vGPU 機能とを組み合わせて、アクセラレータに対応したグラフィックスを必要とするホステッド アプリケーションのサポートを提供できます。 または、個人用セッション デスクトップと新しい個別のデバイスの割り当て (DDA) 機能とを組み合わせて、アクセラレータに対応したグラフィックスを必要とするホステッド アプリケーションのサポートを提供することもできます。
