---
title: キー配布サービス KDS ルート キーの作成
description: Windows Server のセキュリティ
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
ms.openlocfilehash: 3d5f7b46b28e6a2fbfafb664b69aebc8d34886fe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867213"
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>キー配布サービス KDS ルート キーの作成

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナルは、このトピックでは、ドメイン コント ローラーで Windows Server 2012 でのグループ管理されたサービス アカウントのパスワードを生成する Windows PowerShell を使用して Microsoft キー配布サービス (kdssvc.dll) のルート キーを作成する方法について説明します。

 Windows Server 2012 ドメイン コント ローラー (DC) には、gMSA パスワードの生成を開始するルート キーが必要です。 ドメイン コントローラーは作成時点から最大で 10 時間待機します。これにより、すべてのコントローラーは gMSA の作成を許可する前に AD レプリケーションを収束させることができます。 この 10 時間というのは、環境内のすべての DC が gMSA 要求に応答できるようになる前にパスワードの生成が行われるのを防止するための安全対策です。  GMSA を使用しようとする場合が早すぎる、キーがレプリケートされていないすべての Windows Server 2012 Dc にし、パスワードの取得がそのため、gMSA ホストがパスワードを取得しようとすると失敗します。 また、DC を制限付きのレプリケーション スケジュールで使用する際に、またはレプリケーションに関する問題がある場合に、gMSA パスワードを取得できない可能性があります。

この手順を完了するには、**[Domain Admins]** または **[Enterprise Admins]** グループのメンバーシップ、あるいはそれと同等のメンバーシップが最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「 [ローカルおよびドメインの既定のグループ](https://technet.microsoft.com/library/dd728026(WS.10).aspx)」を参照してください。

> [!NOTE]
> グループの管理されたサービス アカウントを管理するために使用する Windows PowerShell コマンドを実行するには、64 ビット アーキテクチャが必要です。

#### <a name="to-create-the-kds-root-key-using-the-add-kdsrootkey-cmdlet"></a>Add-kdsrootkey コマンドレットを使用して、KDS ルート キーを作成するには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **追加 KdsRootKey EffectiveImmediately**

    > [!TIP]
    > Effective 時間パラメータを使用すれば、使用前にすべての DC にキーを伝達する時刻を指定できます。 Add-kdsrootkey を使用して、EffectiveImmediately はすぐに、KDS サービスで使用されるターゲット DC にルート キーを追加します。 ただし、他の Windows Server 2012 Dc はレプリケーションが成功するまでルート キーを使用することができません。

DC が 1 つしか存在しないテスト環境では、次の手順を実行して KDS ルート キーを作成し、開始時刻を過去の時刻に設定することで、キー生成における待機を回避することができます。 4004 イベントが kds イベント ログにログ記録されていることを検証します。

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>テスト環境で KDS ルート キーを作成してすぐに有効にするには

1.  Windows Server 2012 ドメイン コント ローラーには、タスク バーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **$a=Get-Date**

    **$b=$a.AddHours(-10)**

    **追加 KdsRootKey EffectiveTime $b**

    または、単一のコマンドを使用します。

    **Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))**

## <a name="see-also"></a>関連項目
[管理されたサービス アカウント グループの概要](getting-started-with-group-managed-service-accounts.md)


