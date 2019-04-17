---
title: "キー配布サービス KDS ルート キーを作成します。"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e5db8f-1516-4d42-be0a-fa932f5588e9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 30075e56f3ca8e90a0655508efeacfcf2aaa0337
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>キー配布サービス KDS ルート キーを作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

This topic for the IT professional describes how to create a Microsoft Key Distribution Service (kdssvc.dll) root key on the domain controller using Windows PowerShell to generate group Managed Service Account passwords in Windows Server 2012.

 Windows Server 2012 ドメイン コントローラー (DC) では、gMSA パスワードの生成を開始するためにルート キーが必要です。 ドメイン コントローラーでは、すべてのドメイン コントローラーは gMSA の作成を許可する前に、AD レプリケーションの収束を許可するように作成時点から最大で 10 時間を待機します。 10 時間では、環境内のすべての Dc が gMSA 要求に応答できる前に発生しているからパスワードの生成されないようにする安全対策です。  GMSA を使用しようとする場合が早すぎる、キーがレプリケートされていないすべての Windows Server 2012 Dc と、gMSA ホストがパスワードを取得しようとするとパスワードの取得が失敗するためです。 gMSA パスワードを取得できないは、制限付きのレプリケーション スケジュールまたはレプリケーションの問題があるかどうかにドメイン コントローラーを使用する場合にも発生します。

内のメンバーシップ、**Domain Admins**または**Enterprise Admins**はこの手順を完了するために必要な最低限のグループ、またはそれと同等です。 For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

> [!NOTE]
> グループ管理サービス アカウントの管理に使用される Windows PowerShell コマンドを実行するには、64 ビット アーキテクチャが必要です。

#### <a name="to-create-the-kds-root-key-using-the-new-kdsrootkey-cmdlet"></a>New-KdsRootKey コマンドレットを使用して KDS ルート キーを作成するには

1.  Windows Server 2012 ドメイン コントローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **Add-KdsRootKey -EffectiveImmediately**

    > [!TIP]
    > キーを使用する前にすべての Dc に伝達するための時間を提供する時間の有効なパラメーターを使用できます。 Using Add-KdsRootKey -EffectiveImmediately will add a root key to the target DC which will be used by the KDS service immediately. ただし、その他の Windows Server 2012 Dc はレプリケーションが成功するまでルート キーを使用できません。

1 つだけの DC とテスト環境では、KDS ルート キーを作成し、以前は、次の手順を使用してキーの生成における待機を回避する開始時刻を設定します。 4004 イベントが kds イベント ログに記録されたことを検証します。

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>すぐに有効にするためのテスト環境で KDS ルート キーを作成するには

1.  Windows Server 2012 ドメイン コントローラーで、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell の Active Directory モジュールのコマンド プロンプトで次のコマンドを入力し、Enter キーを押します。

    **$、Get-date を =**

    **$b=$a.AddHours(-10)**

    **Add-KdsRootKey -EffectiveTime $b**

    1 つのコマンドを使用して、または

    **Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))**

## <a name="see-also"></a>参照してください。
[管理されたサービス アカウントをグループの概要](getting-started-with-group-managed-service-accounts.md)


