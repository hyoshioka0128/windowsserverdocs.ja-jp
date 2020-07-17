---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: Windows Server 2016 での AD FS のカスタマイズ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3f46ea97034c382d1846ff95bb0974307943bbc5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860095"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016 での AD FS のカスタマイズ


AD FS を使用した組織からのフィードバックに応じて、AD FS によって保護されている個々のアプリケーションのユーザーサインインエクスペリエンスをカスタマイズするためのツールが追加されました。  
説明テキストやリンクなど、アプリケーションごとの web コンテンツを指定するだけでなく、アプリケーションごとに web テーマ全体を指定することもできます。  これには、ロゴ、イラスト、スタイルシート、または onload ファイル全体が含まれます。  
  
## <a name="global-settings"></a>グローバル設定    
全般的なグローバル設定については、Windows Server 2012 R2 の AD FS に付属している[AD FS サインインページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)に関するページを参照してください。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントで説明されている手順を実行する前に、次の前提条件が必要です。  
  
-   Windows Server 2016 TP4 以降の AD FS  
  
## <a name="configure-ad-fs-relying-parties"></a>AD FS 証明書利用者を構成する  
証明書利用者ごとのサインイン web 要素とテーマは、次の PowerShell の例を使用して構成できます。  
  
### <a name="customize-messages"></a>メッセージのカスタマイズ  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>会社名、ロゴ、画像をカスタマイズする  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>ページ全体のカスタマイズ  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>カスタムテーマと高度なカスタムテーマ  
  
カスタムテーマについて[は、AD FS サインインページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)と[AD FS サインインページの高度なカスタマイズ](https://technet.microsoft.com/library/dn636121.aspx)に関するページを参照してください。  
  
## <a name="assigning-custom-web-themes-per-rp"></a>RP ごとにカスタム web テーマを割り当てる  
  
RP ごとにカスタムテーマを割り当てるには、次の手順を使用します。  
  
1. の既定のグローバルテーマのコピーとして新しいテーマを作成し AD FS  
`New-AdfsWebTheme -Name AppSpecificTheme -SourceName default`  
2. カスタマイズ用のテーマをエクスポートする  
`Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme`  
3. 好みのエディターで、またはファイルを置き換えるテーマファイル (画像、css、または onload) をカスタマイズします。  
4. カスタマイズしたファイルをファイルシステムから AD FS にインポートする (新しいテーマをターゲットにする)  
`Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}`  
5. カスタマイズした新しいテーマを特定の RP (または RP) に適用する  
`Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme`  
  
## <a name="home-realm-discovery"></a>ホーム領域検出  
ホーム領域検出のカスタマイズについて[は、「AD FS サインインページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)」を参照してください。  
  
## <a name="updated-password-page"></a>更新されたパスワードページ  
[パスワードの更新] ページのカスタマイズの詳細については、「 [AD FS サインインページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)」を参照してください。  
  
## <a name="customizing-and-alternate-ids"></a>カスタマイズと代替 Id  
ユーザーは、Active Directory Domain Services (AD DS) で受け入れられる任意の形式のユーザー識別子を使用して、Active Directory フェデレーションサービス (AD FS) (AD FS) 対応のアプリケーションにサインインできます。 これには、ユーザープリンシパル名 (Upn) (johndoe@contoso.com) またはドメイン修飾 sam アカウント名 (contoso\johndoe または com\johndoe) が含まれます。  詳細については、「[代替ログイン ID の構成](Configuring-Alternate-Login-ID.md)」を参照してください。  
  
また、AD FS サインインページをカスタマイズして、代替ログイン ID に関するヒントをエンドユーザーに与えることもできます。 カスタマイズしたサインインページの説明を追加することによってこれを行うことができます。詳細については[、「AD FS サインインページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)」を参照してください。   
  
これを行うには、[ユーザー名] フィールドの上にある [組織のアカウントでサインインする] をカスタマイズします。  詳細については[、AD FS サインインページの高度なカスタマイズ](https://technet.microsoft.com/library/dn636121.aspx)に関するページを参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
