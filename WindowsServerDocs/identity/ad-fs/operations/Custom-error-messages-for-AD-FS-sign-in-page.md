---
ms.assetid: 1df78c2a-5054-4b54-8310-c48ea62e6e0b
title: "AD FS サインイン ページのカスタム エラー メッセージ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3a015c27f784d5b1f488f984450612820d4a06b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="custom-error-messages-for-ad-fs-sign-in-page"></a>AD FS サインイン ページのカスタム エラー メッセージ  

>適用対象: Windows Server 2016、Windows Server 2012 R2

組織に合わせてカスタム エラー メッセージを構成できます。 次の図は、カスタマイズしたエラー ページの説明と一般エラー メッセージを示します。 エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットを使用します。  
  
![カスタム エラー](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom3.png)  
  
## <a name="customize-the-error-page-description"></a>エラー ページの説明をカスタマイズします。  
エラー ページの説明をカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" ` 

  
## <a name="customize-a-generic-error-message"></a>一般的なエラー メッセージをカスタマイズします。  
一般的なエラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsGlobalWebContent -ErrorPageGenericErrorMessage "This is a generic error message.  Contact Contoso IT for assistance." ` 

  
## <a name="customize-an-authorization-error-message"></a>承認エラー メッセージをカスタマイズします。  
承認エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -ErrorPageAuthorizationErrorMessage "You have received an Authorization error.  Contact Contoso IT for assistance."  

  
## <a name="customize-a-device-authentication-error-message"></a>デバイス認証エラー メッセージをカスタマイズします。  
デバイス認証エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsGlobalWebContent -ErrorPageDeviceAuthenticationErrorMessage "Your device is not authorized.  Contact Contoso IT for assistance."`  
 
  
## <a name="customize-a-support-email-error-message"></a>サポート電子メール エラー メッセージをカスタマイズします。  
AD FS では、サポートの電子メール アドレスを構成できます。 構成されている、AD FS は自動的にエンド ユーザーが電子メールで送信エラーの詳細へのリンクを示します。  
  
サポート電子メール エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

    Set-AdfsGlobalWebContent -ErrorPageSupportEmail  "admin@contoso.com"  

  
## <a name="customize-a-relying-party-authorization-message"></a>証明書利用者のパーティ承認メッセージをカスタマイズします。  
AD FS で、証明書利用者の承認エラー メッセージを構成することができます。  
  
証明書利用者のパーティ エラー メッセージをカスタマイズするには、次の Windows PowerShell コマンドレットと構文を使用します。  

    Set-AdfsRelyingPartyWebContent -Name fedpassive -ErrorPageAuthorizationErrorMessage "<p> You need to be a member of Security Auditors to access this site. Click <A href='http://accessrequest/'>here</A> for more information.</p>“  


## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)    
