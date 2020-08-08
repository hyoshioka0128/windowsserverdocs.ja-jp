---
title: AD FS prompt = login
description: AD FS 2016 に関してよく寄せられる質問
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/27/2017
ms.topic: article
ms.custom: it-pro
ms.openlocfilehash: 0af0d71ad2b373f755653898ab0697b0308faa4b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940305"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory フェデレーション サービスの prompt=login パラメーターのサポート

次のドキュメントでは、AD FS で使用できる prompt = login パラメーターのネイティブサポートについて説明します。

## <a name="what-is-promptlogin"></a>Prompt = login とは

アプリケーションが Azure AD からの新しい認証を要求する必要がある場合は、ユーザーが既に認証されている場合でもユーザーを再認証する Azure AD 必要があることを意味するために、 `prompt=login` 認証要求の一部として Azure AD にパラメーターを送信できます。

フェデレーションユーザーの要求である場合、Azure AD は、要求が新規認証用であることを、AD FS のように通知する必要があります。

既定では、Azure AD は、 `prompt=login` `wfresh=0` `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` この種類の認証要求をフェデレーション IdP に送信するときにとに変換されます。

これらのパラメーターの意味は次のとおりです。

- `wfresh=0`: 新しい認証を行います。
- `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: 新しい認証要求にユーザー名とパスワードを使用します。

これにより、パラメーターで要求された認証の種類 (ユーザー名とパスワード以外) が必要になる企業イントラネットおよび multi-factor authentication のシナリオで問題が発生する可能性があり `wauth` ます。

Windows Server 2012 R2 では、2016年7月の更新プログラムのロールアップで AD FS、パラメーターのネイティブサポートが導入されました `prompt=login` 。 これは、Azure AD が Azure AD および Office 365 認証要求の一部として AD FS サービスにこのパラメーターをそのように送信できるようになったことを意味します。

## <a name="ad-fs-versions-that-support-promptlogin"></a>Prompt = login をサポートするバージョンの AD FS

パラメーターをサポートする AD FS バージョンの一覧を次に示し `prompt=login` ます。

- Windows Server 2012 R2 の AD FS (2016 年7月の更新プログラムのロールアップ)
- Windows Server 2016 の AD FS

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>プロンプトを送信するフェデレーションドメインを構成する方法 = ログイン AD FS

Azure AD PowerShell モジュールを使用して、設定を構成します。

> [!NOTE]
> `prompt=login`現在、この機能は、 `PromptLoginBehavior` [Azure AD Powershell モジュールのバージョン 1.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)でのみ使用できます。このコマンドレットには、Set-msoldomainfederationsettings などの "msol" を含む名前が付いています。  現時点では、Azure AD PowerShell モジュールの ' version 2.0 ' 経由では使用できません。このコマンドレットには、"AzureAD" のような名前が付いてい \* ます。

1. まず `PreferredAuthenticationProtocol` 、 `SupportsMfa` 次の `PromptLoginBehavior` PowerShell コマンドを実行して、フェデレーションドメインの、、およびの現在の値を取得します。

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> 既定でのの出力で `Get-MsolDomainFederationSettings` は、コンソールに特定のプロパティは表示されません。 すべてのプロパティを表示するには、パイプを使用して `|` 出力をに渡し ()、 `Format-List *` オブジェクトのすべてのプロパティの出力を強制的に適用する必要があります。

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> プロパティの値 `PromptLoginBehavior` が空 () の場合 `$null` は、の動作 `TranslateToFreshPasswordAuth` が使用されます。

2. 次のコマンドを実行して、の目的の値を構成し `PromptLoginBehavior` ます。

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

パラメーターの使用可能な値 `PromptLoginBehavior` とその意味は次のとおりです。

- **TranslateToFreshPasswordAuth**: およびへの変換の既定の Azure AD 動作を意味し `prompt=login` `wauth=https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` `wfresh=0` ます。
- **NativeSupport**: `prompt=login` パラメーターが AD FS にそのように送信されることを意味します。 これは、2012年 7 2016 月の更新プログラムのロールアップ以降を使用して AD FS が Windows Server R2 に存在する場合に推奨される値です。
- **Disabled**: のみが AD FS に送信されることを意味 `wfresh=0` します。
