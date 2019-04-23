---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: AD FS サインイン ページのカスタム エラー メッセージ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a015c27f784d5b1f488f984450612820d4a06b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828983"
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>AD FS サインイン ページのカスタム エラー メッセージ  

>適用先:Windows Server 2016、Windows Server 2012 R2

組織の要件に合わせてカスタム エラー メッセージを構成できます。 次の図に、カスタマイズしたエラー ページの説明と一般エラー メッセージを示します。 エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットを使用します。  
  
![カスタム エラー](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>エラー ページの説明のカスタマイズ  
エラー ページの説明をカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>一般エラー メッセージのカスタマイズ  
一般的なエラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>承認エラー メッセージのカスタマイズ  
承認エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>デバイス認証エラー メッセージのカスタマイズ  
デバイス認証のエラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>サポート電子メール エラー メッセージのカスタマイズ  
AD FS では、サポートの電子メール アドレスを構成できます。 構成される場合は、AD FS でエラーの詳細を電子メールで送信するエンドユーザーへのリンクが自動的に表示されます。  
  
サポート電子メール エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>証明書利用者の承認メッセージのカスタマイズ  
AD FS では、証明書利用者のパーティ承認エラー メッセージを構成できます。  
  
パーティの証明書利用者のエラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)    
