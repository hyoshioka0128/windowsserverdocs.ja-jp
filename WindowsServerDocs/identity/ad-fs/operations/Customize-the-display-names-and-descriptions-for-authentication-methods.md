---
ms.assetid: 309d6358-777d-496a-856d-728246c7d9a1
title: 認証方法の表示名と説明をカスタマイズする
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cc0da10858ca6924a516fbf825206e376294209d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407566"
---
# <a name="customize-the-display-names-and-descriptions-for-authentication-methods"></a>認証方法の表示名と説明をカスタマイズする 


認証方法の表示名と説明をカスタマイズするには、 `Set-AdfsAuthenticationProviderWebContent` PowerShell コマンドレットを使用します。  このコマンドレットを使用するには、まず、カスタマイズする認証方法の名前を取得する必要があります。  これは、 `Get-AdfsGlobalAuthenticationPolicy`を使って実行できます。  次の例では、sign @ no__t-0in ページに次のように表示されています。"X.509 証明書を使ってサインインしてください"  これをユーザー向けに簡素化します。  
  
![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update1.PNG)  
  
まず、認証方法の名前を取得し、表示されたテキストを編集します。  
  
 
    Get-AdfsGlobalAuthenticationPolicy  
      
    AdditionalAuthenticationProvider  : {}  
    DeviceAuthenticationEnabled   : False  
    PrimaryIntranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    PrimaryExtranetAuthenticationProvider : {FormsAuthentication, CertificateAuthentication}  
    WindowsIntegratedFallbackEnabled  : True  
      
    Set-AdfsAuthenticationProviderWebContent -Name CertificateAuthentication -DisplayName "Sign in with a certificate"  
  
  
![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update2.PNG)  
  
これで、表示メッセージが変更されました。  
  
![displayname のカスタマイズ](media/AD-FS-user-sign-in-customization/ADFS_Customize_Update3.PNG)  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md) 
