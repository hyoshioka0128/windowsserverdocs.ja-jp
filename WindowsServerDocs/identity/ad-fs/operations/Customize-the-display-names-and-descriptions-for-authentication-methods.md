---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: 認証方法の表示名と説明をカスタマイズする
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 679f60d1328795ef4f272f0159c6be5185428d59
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954268"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>認証方法の表示名と説明をカスタマイズする

認証方法の表示名と説明をカスタマイズするには、 `Set-AdfsAuthenticationProviderWebContent` PowerShell コマンドレットを使用します。  このコマンドレットを使用するには、まず、カスタマイズする認証方法の名前を取得する必要があります。  これは、 `Get-AdfsGlobalAuthenticationPolicy`を使って実行できます。  次の例では、サインイン \- ページに "x.509 証明書を使用してサインイン" と表示されています。  これをユーザー向けに簡素化します。

![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)

まず、認証方法の名前を取得し、表示されたテキストを編集します。

```powershell
Get-AdfsGlobalAuthenticationPolicy

AdditionalAuthenticationProvider  : {}
DeviceAuthenticationEnabled   : False
PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}
WindowsIntegratedFallbackEnabled  : True

Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"
 ```

![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)

これで、表示メッセージが変更されました。

![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)

## <a name="additional-references"></a>その他の参照情報

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
