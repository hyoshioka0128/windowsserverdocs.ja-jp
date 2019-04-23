---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: 表示名と認証方法の説明をカスタマイズします。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 699622a8a075dd6c78ab1b536dce2abfee642e9e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855193"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>表示名と認証方法の説明をカスタマイズします。 

>適用先:Windows Server 2016、Windows Server 2012 R2

認証方法の表示名と説明をカスタマイズするには、 `Set-AdfsAuthenticationProviderWebContent` PowerShell コマンドレットを使用します。  このコマンドレットを使用するには、まず、カスタマイズする認証方法の名前を取得する必要があります。  これは、 `Get-AdfsGlobalAuthenticationPolicy`を使って実行できます。  次の例を見る、サインオン\- ページで、次が表示されます。"X.509 証明書を使ってサインインしてください"  これをユーザー向けに簡素化します。  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
まず、認証方法の名前を取得し、表示されたテキストを編集します。  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
これで、表示メッセージが変更されました。  
  
![displayname をカスタマイズします。](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
