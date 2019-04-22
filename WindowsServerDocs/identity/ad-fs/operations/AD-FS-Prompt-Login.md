---
title: プロンプトの AD FS ログインを =
description: AD FS 2016 のよく寄せられる質問
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6a4b6cfe98064181824e210be9031a0f67cb4b75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824633"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory フェデレーション サービスの要求パラメーターのログインのサポートを =
次のドキュメントでは、AD FS で使用できる prompt = login パラメーターのネイティブ サポートについて説明します。

## <a name="what-is-promptlogin"></a>プロンプトはログインを = ですか?  

(先進認証を有効になっている) を使用する Office 365 アプリケーションでは、各認証要求の一部として Azure AD に prompt = login パラメーターを送信します。  2 つのパラメーターにこの Azure AD によって既定では、変換: <code> <b> wauth </b> =urn:oasis:names:tc:SAML:1.0:am:password </code>、および<code> <b> wfresh </b> =0 </code>.

これにより、企業のイントラネットとユーザー名とパスワード以外の認証タイプが必要な多要素認証のシナリオで問題が発生することができます。  

2016 年 7 月更新プログラムのロールアップの Windows Server 2012 R2 で AD FS では、prompt = login パラメーターに対するネイティブ サポートが導入されました。  つまり、としては、このパラメーターを送信する Azure AD を構成するオプションがあるようになりました-Azure AD の一部として、AD FS サービスには、Office 365 認証の要求。

### <a name="ad-fs-versions-that-support-promptlogin"></a>プロンプトをサポートする AD FS のバージョンのログインを =
次には、prompt = login パラメーターをサポートする AD FS のバージョンの一覧を示します。

- 2016 年 7 月 Windows Server 2012 R2 で AD FS の更新プログラムのロールアップ

- Windows Server 2016 の AD FS

## <a name="how-do-to-configure-your-azure-ad-tenant-to-send-promptlogin-to-ad-fs"></a>メッセージを送信する Azure AD テナントを構成する方法: AD FS へのログインを =

設定を構成するのにには、Azure AD PowerShell モジュールを使用します。

> [!NOTE]
> (PromptLoginBehavior プロパティで有効) = ログイン機能は現時点でのみには、 [' Azure AD Powershell モジュール バージョン 1.0'](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)コマンドレットがなど"Msol"を含む名前があります。Set-msoldomainfederationsettings します。  使用して、現在ご利用いただけません ' バージョン 2.0' Azure AD PowerShell モジュールのコマンドレットは、名前を持つように"セット AzureAD\*"。

プロンプトを構成するログインの動作を次のコマンドレットの構文を =。

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

 
 PreferredAuthenticationProtocol、SupportsMfa、および PromptLoginBehavior プロパティの値は、コマンドレットからの出力を表示してあります。![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)
```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | fl *
 ```
> [!NOTE]
> 既定で次のように Get-msoldomainfederationsettings を実行するときに、特定のプロパティは、コンソールでは表示されません。  これらのパラメーターを使用することをお勧めの表示、|fl * すべてのオブジェクトのプロパティの出力を強制的にします。


PromptLoginBehavior パラメーターとその設定の詳細については、次のです。
   
   - <b>TranslateToFreshPasswordAuth</b>送信の既定の Azure AD の動作のことを意味<b>wauth</b>と<b>wfresh</b>プロンプトではなく、AD fs ログインを =
   - <b>NativeSupport</b> AD FS には、prompt = login パラメーターが送信されることを意味
   - <b>無効になっている</b>AD FS に何も送信されることを意味します

