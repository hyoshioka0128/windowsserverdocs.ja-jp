---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: "パスワードの有効期限クレームを送信する AD FS を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 386a5ac921ba609c371121b8657351667628951b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>パスワードの有効期限クレームを送信する AD FS を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス (AD FS) を ad FS で保護されている証明書利用者のパーティ信頼 (アプリケーション) にパスワードの有効期限クレームを送信するように構成することができます。 これらの要求を使用する方法は、アプリケーションに依存します。 たとえばと、証明書利用者として Office 365、更新プログラムを早くに-する-有効期限の切れてパスワードのフェデレーション ユーザーに通知するには、Exchange と Outlook に実装されています。

パスワードを送信する AD FS を構成するには、証明書利用者信頼、要求の有効期限必要があります追加する次の要求規則この証明書利用者信頼。

```
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
=> issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> パスワードの有効期限クレームでは、作業の認証の種類のユーザー名とパスワード、および Microsoft Passport の使用のみです。  ユーザーを認証する場合は、統合 Windows 認証および Passport を使用してが構成されていないと、信頼性情報は使用できませんユーザーでは、パスワードの有効期限の通知が表示されません。

> [!NOTE]
> 14 日間のウィンドウがあるため、送信要求は、パスワードが 14 日以内に期限切れの場合のみ表示されます。

## <a name="see-also"></a>参照してください。
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)
