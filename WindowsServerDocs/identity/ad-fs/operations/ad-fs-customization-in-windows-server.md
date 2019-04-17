---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: "Windows Server 2016 の AD FS のカスタマイズ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: a2699e93a0a19cb138c1fde0c9af36774a12f865
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016 の AD FS のカスタマイズ

>Windows Server 2016 の適用対象:

AD FS を使用して組織からのフィードバックに応えて、ユーザーをカスタマイズするその他のツールは、AD FS によって保護されている個々 のアプリケーション エクスペリエンスにログインを追加しました。  
今すぐ説明のテキストとリンクなどのアプリケーションごとの Web コンテンツを指定するだけでなくは、アプリケーションあたりの全体の Web テーマを指定できます。  これには、ロゴ、イラスト、スタイル シート、または、全体 onload.js ファイルが含まれます。  
  
## <a name="global-settings"></a>[グローバルな設定    
一般的なグローバル設定することができますを参照してください[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)Windows Server 2012 R2 の AD FS に付属します。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントで説明されている手順を実行する前に、次の前提条件が必要です。  
  
-   Windows Server 2016 TP4 またはそれ以降の AD FS  
  
## <a name="configure-ad-fs-relying-parties"></a>AD FS 証明書利用者を構成します。  
証明書利用者のパーティ サインイン Web ごとの要素とテーマを使って構成できます以下の PowerShell の例。  
  
### <a name="customize-messages"></a>メッセージをカスタマイズします。  
  
```  
PS C:\>Set-AdfsRelyingPartyWebContent  
    -TargetRelyingPartyName "<RP trust Name>"  
    -CompanyName "This text appears in place of the federation service display name"  
    -OrganizationalNameDescriptionText "This text appears right below the company name"  
    -SignInPageDescription "This text appears below the credential prompt"  
```  
  
### <a name="customize-company-name-logo-and-image"></a>会社名、ロゴ、およびイメージをカスタマイズします。  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -Logo @{path="C:\Images\applogo.png"}  
    -Illustration @{path="C:\Images\appillustration.jpg"}  
```  
  
### <a name="customize-entire-page"></a>全体のページをカスタマイズします。  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>カスタム テーマと高度なカスタム テーマ  
  
カスタム テーマを参照してください[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)と[Advanced Customization of AD FS サインイン ページ。](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>RP ごとのカスタム Web テーマを割り当てる  
  
RP ごとのカスタム テーマを割り当てるには、次の手順を使用します。  
  
1. 既定では、AD FS でのグローバルのテーマをコピーとして新しいテーマを作成します。  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code>  
2.  カスタマイズのテーマをエクスポート<code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code>3.、好みのエディターで (イメージ、css、onload.js) - テーマ ファイルをカスタマイズしたり、4、ファイルを置き換えます。 (新しいテーマを対象とする) の AD FS へのファイル システムからカスタマイズされたファイルをインポート<code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code>5.特定 RP (または RP の) に、カスタマイズした新しいテーマを適用します。
<code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>ホーム領域検出  
ホーム領域検出のカスタマイズを参照してください[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。  
  
## <a name="updated-password-page"></a>パスワード更新ページ  
パスワード更新ページをカスタマイズする方法の詳細についてを参照してください。[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。  
  
## <a name="customizing-and-alternate-ids"></a>カスタマイズと代替の Id  
Active Directory フェデレーション サービス (AD FS) にログインできるユーザーの Active Directory ドメイン サービス (AD DS) によって承認されたユーザーの識別子の任意の形式を使用してアプリケーションを有効になっています。 ユーザー プリンシパル名 (Upn) が含まれます (johndoe@contoso.com) またはドメイン (contoso\johndoe または contoso.com\johndoe) の sam アカウント名を修飾します。  この参照の詳細については[を構成する代替ログイン ID です。](Configuring-Alternate-Login-ID.md)  
  
代替ログイン ID に関するいくつかのヒントをエンド ユーザーに提供する AD FS サインイン ページをカスタマイズすることもまた 詳細については「カスタマイズされたサインイン ページ説明を追加することによって行うことができます[AD FS サインイン ページのカスタマイズします。](https://technet.microsoft.com/library/dn280950.aspx)   
  
ユーザー名] フィールドの上に「組織のアカウントでログイン」文字列をカスタマイズすることでこれを実行できます。  この参照について[Advanced Customization of AD FS Sign-in Pages](https://technet.microsoft.com/library/dn636121.aspx)します。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
