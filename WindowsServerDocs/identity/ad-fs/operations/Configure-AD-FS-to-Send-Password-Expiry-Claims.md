---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: パスワードの有効期限クレームを送信するように AD FS を構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 080e8cc81949df3bf74ae846eee7f32c5e145f53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834363"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>パスワードの有効期限クレームを送信するように AD FS を構成する

>適用先:Windows Server 2016、Windows Server 2012 R2

ADFS で保護されている証明書利用者のパーティ信頼 (アプリケーション) にパスワードの有効期限クレームを送信する Active の Directory フェデレーション サービス (AD FS) を構成することができます。 これらの要求を使用する方法は、アプリケーションによって異なります。 たとえば、証明書利用者として Office 365 を更新プログラムが実装されましたがすぐに-する-有効期限切れのパスワードのフェデレーション ユーザーに通知するには、Exchange と Outlook に。

パスワードを送信する AD FS を構成するには、有効期限は、証明書利用者信頼を要求する必要があります追加する次の要求規則にこの証明書利用者信頼。

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("http://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "http://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "http://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> パスワードの有効期限クレームでは、作業の認証の種類のユーザー名とパスワード、および Microsoft Passport を使用できるのみです。  ユーザーを認証する場合は、Windows 統合認証と Passport を使用してが構成されていないと要求は使用できません、ユーザーがパスワードの有効期限通知に表示されません。

> [!NOTE]
> 14 日間のウィンドウがあるため、送信された要求は、パスワードは 14 日以内は期限切れにならない場合のみ設定されます。

## <a name="see-also"></a>関連項目
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
