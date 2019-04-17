---
title: "AD FS プロンプト ログインを ="
description: "AD FS 2016 についてよく寄せられる質問"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8b98cdc27c9bd01d9855e98965f59ebe5257ed5c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory フェデレーション サービスのプロンプト = ログイン パラメーターのサポート
次のドキュメントでは、AD FS で使用できる = ログイン パラメーターのネイティブ サポートについて説明します。

## <a name="what-is-promptlogin"></a>プロンプトはログインを = ですか?  

一部の Office 365 アプリケーション (最新の認証が有効になっている) では、各認証要求の一部として Azure AD に = ログイン パラメーターを送信します。  By default, Azure AD translates this into two parameters: <code><b>wauth</b>=urn:oasis:names:tc:SAML:1.0:am:password</code>, and <code><b>wfresh</b>=0</code>.

これにより、企業イントラネットと multi-factor authentication シナリオ以外のユーザー名とパスワードの認証の種類が必要な問題が発生することができます。  

2016 年 7 月更新プログラムのロールアップを Windows Server 2012 R2 の AD FS には、プロンプト = ログイン パラメーターのネイティブ サポートが導入されました。  つまり、としてこのパラメーターを送信する Azure AD を構成するオプションがあるようになりました-は、AD FS サービスを Azure AD の一部として、Office 365 の認証要求します。

### <a name="ad-fs-versions-that-support-promptlogin"></a>プロンプトをサポートしている AD FS バージョン ログインを =
= ログイン パラメーターをサポートしている AD FS のバージョンの一覧を次に示します。

- 2016 年 7 月 Windows Server 2012 R2 の AD FS の更新プログラムのロールアップ

- Windows Server 2016 の AD FS

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>プロンプトを送信する Azure AD テナントを構成する方法の AD FS へのログを =

設定を構成するのにには、Azure AD PowerShell モジュールを使用します。

> [!NOTE]
> The prompt=login capability (enabled by the PromptLoginBehavior property) is currently available only in the [‘version 1.0’ Azure AD Powershell module](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185), in which the cmdlets have names that include “Msol”, such as Set-MsolDomainFederationSettings.  経由で現在利用可能なは ' バージョン 2.0' Azure AD PowerShell モジュールのコマンドレットは、名前を持つように"設定-AzureAD\ *"です。

プロンプトを構成するログイン動作では、次のコマンドレットの構文を =。

例 1:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PreferredAuthenticationProtocol <your current protocol setting> 
```

例 2:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -SupportsMfa <$True|$False>
```

例 3:
```powershell
    Set-MsolDomainFederationSettings –DomainName <your domain name> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

 
 コマンドレットからの出力を表示することによって、PreferredAuthenticationProtocol、SupportsMfa、および PromptLoginBehavior プロパティの値が見つかりません: ![Get-msoldomainfederationsettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> 既定で Get-MsolDomainFederationSettings を実行しているときに、特定のプロパティは、コンソールでは表示されません。  これらのパラメーターを使用することをお勧めを表示する、|fl * をすべてのオブジェクトのプロパティの出力を強制します。


詳細については、PromptLoginBehavior パラメーターとその設定を次に示します。
   
   - <b>TranslateToFreshPasswordAuth</b>既定 Azure AD の動作を送信することを意味<b>wauth</b>と<b>wfresh</b> = ログイン プロンプトではなく、AD FS に
   - <b>NativeSupport</b>の AD FS には、プロンプト = ログイン パラメーターは送信されることを意味
   - <b>無効になっている</b>何が AD FS に送信されることを意味

