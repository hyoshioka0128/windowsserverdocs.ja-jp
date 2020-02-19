---
title: AD FS prompt = login
description: AD FS 2016 に関してよく寄せられる質問
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a80678f5d2773e3fcd7a95032853249dc36d5616
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465526"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory フェデレーションサービス (AD FS) prompt = ログインパラメーターのサポート

次のドキュメントでは、AD FS で使用できる prompt = login パラメーターのネイティブサポートについて説明します。

## <a name="what-is-promptlogin"></a>Prompt = login とは

アプリケーションが Azure AD からの新しい認証を要求する必要がある場合は、ユーザーが既に認証されている場合でもユーザーを再認証する Azure AD 必要があることを意味するために、`prompt=login` パラメーターを認証要求の一部として Azure AD に送信することができます。

フェデレーションユーザーの要求である場合、Azure AD は、要求が新規認証用であることを、AD FS のように通知する必要があります。

既定では、Azure AD は `prompt=login` を `wfresh=0` に変換し、この種類の認証要求をフェデレーション IdP に送信するときに `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` します。

これらのパラメーターの意味は次のとおりです。

- `wfresh=0`: 新しい認証を行う
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: 新しい認証要求にユーザー名とパスワードを使用します

これにより、`wauth` パラメーターによって要求されたユーザー名とパスワード以外の認証の種類が必要になる企業イントラネットおよび multi-factor authentication シナリオで問題が発生する可能性があります。  

Windows Server 2012 R2 では、2016年7月の更新プログラムのロールアップで AD FS、`prompt=login` パラメーターのネイティブサポートが導入されました。 これは、Azure AD が Azure AD および Office 365 認証要求の一部として AD FS サービスにこのパラメーターをそのように送信できるようになったことを意味します。

## <a name="ad-fs-versions-that-support-promptlogin"></a>Prompt = login をサポートするバージョンの AD FS

`prompt=login` パラメーターをサポートする AD FS バージョンの一覧を次に示します。

- Windows Server 2012 R2 の AD FS (2016 年7月の更新プログラムのロールアップ)
- Windows Server 2016 の AD FS

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>プロンプトを送信するフェデレーションドメインを構成する方法 = ログイン AD FS

Azure AD PowerShell モジュールを使用して、設定を構成します。

> [!NOTE]
> `prompt=login` 機能 (`PromptLoginBehavior` プロパティによって有効) は現在、 [Azure AD Powershell モジュールのバージョン 1.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)でのみ使用できます。このコマンドレットには、set-msoldomainfederationsettings などの "msol" を含む名前が付いています。  現在、Azure AD PowerShell モジュールの ' version 2.0 ' 経由では使用できません。このコマンドレットには、"AzureAD\*" のような名前が付いています。

1. まず、次の PowerShell コマンドを実行して、フェデレーションドメインの `PreferredAuthenticationProtocol`、`SupportsMfa`、および `PromptLoginBehavior` の現在の値を取得します。

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> 既定で `Get-MsolDomainFederationSettings` の出力は、コンソールに特定のプロパティを表示しません。 すべてのプロパティを表示するには、パイプを使用してその出力を `Format-List *` に`|`し、オブジェクトのすべてのプロパティの出力を強制的に適用する必要があります。

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> プロパティ `PromptLoginBehavior` の値が空 (`$null`) の場合、`TranslateToFreshPasswordAuth` の動作が使用されます。

2. 次のコマンドを実行して、`PromptLoginBehavior` の目的の値を構成します。

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

`PromptLoginBehavior` パラメーターの有効な値とその意味は次のとおりです。

- **TranslateToFreshPasswordAuth**: `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` および `wfresh=0`に `prompt=login` を変換する既定の Azure AD 動作を意味します。
- **NativeSupport**: `prompt=login` パラメーターが AD FS にそのように送信されることを意味します。 これは、2012年 7 2016 月の更新プログラムのロールアップ以降を使用して AD FS が Windows Server R2 に存在する場合に推奨される値です。
- **Disabled**: `wfresh=0` のみが AD FS に送信されることを意味します。
