---
ms.assetid: 25f5aff1-6abf-4dea-b531-f1d9943bc181
title: Windows Server 2016 で AD FS のカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e4d463f5f25fe85dc95d767c9c75b722e60b012
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852033"
---
# <a name="ad-fs-customization-in-windows-server-2016"></a>Windows Server 2016 で AD FS のカスタマイズ

>適用先:Windows Server 2016

AD FS を使用して組織からのフィードバックに応答して、ユーザーをカスタマイズするその他のツールは、AD FS によって保護されている個々 のアプリケーションのエクスペリエンスにサインインを追加されています。  
今すぐ説明のテキストとリンクなど、アプリケーションごとの web コンテンツを指定するだけでなくは、1 つのアプリケーション全体の web テーマを指定できます。  これには、ロゴ、図、スタイル シート、または、全体の onload.js ファイルが含まれます。  
  
## <a name="global-settings"></a>グローバル設定    
一般的なグローバル設定を参照することができます[Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx) Windows Server 2012 R2 で AD FS に付属します。  
  
## <a name="pre-requisites"></a>前提条件  
このドキュメントで説明した手順を試行する前に、次の前提条件が必要です。  
  
-   Windows Server 2016 TP4 以降の AD FS  
  
## <a name="configure-ad-fs-relying-parties"></a>AD FS 証明書利用者のパーティを構成します。  
Web サインインのパーティの証明書利用者ごとの要素とテーマを使って構成できます以下の PowerShell の例。  
  
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
  
### <a name="customize-entire-page"></a>ページ全体のカスタマイズします。  
  
```  
PS C:\>Set-AdfsRelyingPartyWebTheme  
    -TargetRelyingPartyName "<RP trust Name>"  
    -OnLoadScriptPath @{path="c:\scripts\adfstheme\onload.js"}  
```  
  
## <a name="custom-themes-and-advanced-custom-themes"></a>カスタム テーマと高度なカスタム テーマ  
  
カスタム テーマを参照してください[Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)と[Advanced Customization of AD FS サインイン ページ。](https://technet.microsoft.com/library/dn636121.aspx)  
  
## <a name="assigning-custom-web-themes-per-rp"></a>RP ごとのカスタム web テーマを割り当てる  
  
RP ごとのカスタム テーマを割り当てるには、次の手順を使用します。  
  
1. 既定では、AD FS でグローバルにテーマのコピーとして新しいテーマを作成します。  
<code>New-AdfsWebTheme -Name AppSpecificTheme -SourceName default</code> 2.  カスタマイズ用のテーマをエクスポートします。 <code>Export-AdfsWebTheme -Name AppSpecificTheme -DirectoryPath c:\appspecifictheme</code>  
3. お気に入りのエディターでテーマ ファイル (イメージ、css、onload.js) をカスタマイズまたは 4 ファイルを置換します。 AD FS の (新しいテーマを対象とする) をファイル システムからカスタマイズされたファイルをインポートします。 <code>Set-AdfsWebTheme -TargetName AppSpecificTheme -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';Path="c:\appspecifictheme\script\onload.js"}</code>  
5. 特定の RP (または RP の) に、カスタマイズされた新しいテーマを適用します。 <code>Set-AdfsRelyingPartyWebTheme -TargetRelyingPartyName urn:app1 -SourceWebThemeName AppSpecificTheme</code>  
  
## <a name="home-realm-discovery"></a>ホーム領域検出  
ホーム領域検出のカスタマイズを参照してください[Customizing the AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)します。  
  
## <a name="updated-password-page"></a>パスワードの更新されたページ  
パスワード更新ページのカスタマイズに関する情報を参照してください。 [AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。  
  
## <a name="customizing-and-alternate-ids"></a>カスタマイズと代替 Id  
ユーザーが Active Directory フェデレーション サービス (AD FS) にサインインできます-その Active Directory Domain Services (AD DS) によって承認されたユーザー識別子の形式を使用してアプリケーションを有効にします。 ユーザー プリンシパル名 (Upn) が含まれます (johndoe@contoso.com) またはドメインが sam アカウント名 (contoso \johndoe または contoso.com\johndoe) を修飾します。  この参照の詳細については[構成の代替ログイン id です。](Configuring-Alternate-Login-ID.md)  
  
代替ログイン ID に関するいくつかのヒントをエンドユーザーに提供する AD FS サインイン ページをカスタマイズすることもさらに 詳細については「カスタマイズされたサインイン ページ説明を追加することで行うことができます[AD FS サインイン ページのカスタマイズ。](https://technet.microsoft.com/library/dn280950.aspx)   
  
ユーザー名 フィールド上に「組織アカウントでサインイン」の文字列をカスタマイズすることでこれを行うことができます。  この参照は[Advanced Customization of AD FS サインイン ページ](https://technet.microsoft.com/library/dn636121.aspx)します。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
