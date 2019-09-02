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
ms.openlocfilehash: 8a3743d1ce430f605244408dc6b26779965aa99f
ms.sourcegitcommit: d83933c6a2e180b747c2db910392117569348901
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68807876"
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>キー配布サービス KDS ルート キーの作成

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、windows PowerShell を使用してドメインコントローラーに Microsoft キー配布サービス (kdssvc.dll) のルートキーを作成し、Windows Server 2012 以降でグループの管理されたサービスアカウントのパスワードを生成する方法について説明します。

GMSA パスワードの生成を開始するには、ドメインコントローラー (DC) にルートキーが必要です。 ドメイン コントローラーは作成時点から最大で 10 時間待機します。これにより、すべてのコントローラーは gMSA の作成を許可する前に AD レプリケーションを収束させることができます。 この 10 時間というのは、環境内のすべての DC が gMSA 要求に応答できるようになる前にパスワードの生成が行われるのを防止するための安全対策です。  すぐに gMSA を使用しようとすると、キーがすべてのドメインコントローラーにレプリケートされていない可能性があるため、gMSA ホストがパスワードを取得しようとすると、パスワードの取得が失敗する可能性があります。 また、DC を制限付きのレプリケーション スケジュールで使用する際に、またはレプリケーションに関する問題がある場合に、gMSA パスワードを取得できない可能性があります。

> [!NOTE]
> ルートキーを削除して再作成すると、キーのキャッシュによって古いキーが削除後も引き続き使用される問題が発生する可能性があります。 ルートキーが再作成された場合、すべてのドメインコントローラーでキー配布サービス (KDC) を再起動する必要があります。

この手順を完了するには、 **[Domain Admins]** または **[Enterprise Admins]** グループのメンバーシップ、あるいはそれと同等のメンバーシップが最低限必要です。 適切なアカウントおよびグループ メンバーシップの使用方法の詳細については、「 [ローカルおよびドメインの既定のグループ](https://technet.microsoft.com/library/dd728026(WS.10).aspx)」を参照してください。

> [!NOTE]
> グループの管理されたサービス アカウントを管理するために使用する Windows PowerShell コマンドを実行するには、64 ビット アーキテクチャが必要です。

#### <a name="to-create-the-kds-root-key-using-the-add-kdsrootkey-cmdlet"></a>Add-kdsrootkey コマンドレットを使用して KDS ルートキーを作成するには

1.  Windows Server 2012 以降のドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **Add-kdsrootkey-EffectiveImmediately**

    > [!TIP]
    > Effective 時間パラメータを使用すれば、使用前にすべての DC にキーを伝達する時刻を指定できます。 Add-kdsrootkey-EffectiveImmediately を使用すると、KDS サービスによって直ちに使用されるターゲット DC にルートキーが追加されます。 ただし、他のドメインコントローラーは、レプリケーションが成功するまでルートキーを使用できません。

DC が 1 つしか存在しないテスト環境では、次の手順を実行して KDS ルート キーを作成し、開始時刻を過去の時刻に設定することで、キー生成における待機を回避することができます。 4004 イベントが kds イベント ログにログ記録されていることを検証します。

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>テスト環境で KDS ルート キーを作成してすぐに有効にするには

1.  Windows Server 2012 以降のドメインコントローラーで、タスクバーから Windows PowerShell を実行します。

2.  Windows PowerShell Active Directory モジュールのコマンド プロンプトで、次のコマンドを入力し、ENTER キーを押します。

    **$a=Get-Date**

    **$b=$a.AddHours(-10)**

    **Add-KdsRootKey -EffectiveTime $b**

    または、単一のコマンドを使用します。

    **Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))**

## <a name="see-also"></a>関連項目
[グループの管理されたサービス アカウントの概要](getting-started-with-group-managed-service-accounts.md)


