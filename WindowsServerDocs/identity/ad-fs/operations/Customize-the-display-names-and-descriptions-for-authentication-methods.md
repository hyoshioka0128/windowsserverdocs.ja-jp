---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: "表示名と認証方法の説明をカスタマイズします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 699622a8a075dd6c78ab1b536dce2abfee642e9e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>表示名と認証方法の説明をカスタマイズします。 

>適用対象: Windows Server 2016、Windows Server 2012 R2

表示名と使用できる認証方法の説明をカスタマイズする、 `Set-AdfsAuthenticationProviderWebContent` PowerShell コマンドレット。  このコマンドレットを使用するためにカスタマイズする認証方法の名前をまず取得する必要があります。  これを行うを使用して`Get-AdfsGlobalAuthenticationPolicy`します。  お次の例では、[サインイン] ページで、次が表示されることを参照してください。"X.509 証明書を使用してサインインとしています"。  これが、ユーザーの簡略化します。  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
まず、認証方法の名前を取得し、表示されるテキストを編集します。  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
これで、表示メッセージが変更されている参照してください。  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
