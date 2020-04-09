---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: パスワードの有効期限クレームを送信するように AD FS を構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0c04f42cbe29b1ea36d09f1f148fb28280d7fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859895"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>パスワードの有効期限クレームを送信するように AD FS を構成する


ADFS によって保護されている証明書利用者信頼 (アプリケーション) にパスワードの有効期限要求を送信するように Active Directory フェデレーションサービス (AD FS) (AD FS) を構成できます。 これらの要求がどのように使用されるかは、アプリケーションによって異なります。 たとえば、証明書利用者として Office 365 を使用している場合、間もなく期限切れになるパスワードをフェデレーション ユーザーに通知できる更新プログラムが Exchange および Outlook に実装されました。

証明書利用者信頼にパスワードの有効期限要求を送信するように AD FS を構成するには、この証明書利用者信頼に次の要求規則を追加する必要があります。

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> パスワードの有効期限要求は、ユーザー名とパスワード、および Microsoft Passport for Work 認証の種類に対してのみ使用できます。  ユーザーが Windows 統合認証を使用して認証され、Passport が構成されていない場合、要求は使用できず、ユーザーにはパスワードの有効期限の通知は表示されません。

> [!NOTE]
> 14日間の期間があるため、パスワードの有効期限が14日以内に切れる場合にのみ、送信された要求に値が設定されます。

## <a name="see-also"></a>参照
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
