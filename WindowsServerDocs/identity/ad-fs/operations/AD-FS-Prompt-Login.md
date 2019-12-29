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
ms.openlocfilehash: ba43d591d429e589a990dfdfc4a4992ffa4a6ef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358547"
---
# <a name="active-directory-federation-services-promptlogin-parameter-support"></a>Active Directory フェデレーションサービス (AD FS) prompt = ログインパラメーターのサポート

次のドキュメントでは、AD FS で使用できる prompt = login パラメーターのネイティブサポートについて説明します。

## <a name="what-is-promptlogin"></a>Prompt = login とは

アプリケーションが Azure AD からの新しい認証を要求する必要がある場合は、ユーザーが既に認証されている場合でもユーザーを再認証する Azure AD `prompt=login`必要があることを意味するために、認証の一部として Azure AD にパラメーターを送信することができます。申請.

フェデレーションユーザーの要求である場合、Azure AD は、要求が新規認証用であることを、AD FS のように通知する必要があります。

既定では、Azure AD `prompt=login`は、 `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`この種類の認証要求をフェデレーション IdP に送信するときにとに`wfresh=0`変換されます。

これらのパラメーターの意味は次のとおりです。

- `wfresh=0`: 新しい認証を行います。
- `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`: 新しい認証要求にユーザー名とパスワードを使用します。

これにより、 `wauth`パラメーターで要求された認証の種類 (ユーザー名とパスワード以外) が必要になる企業イントラネットおよび multi-factor authentication のシナリオで問題が発生する可能性があります。  

Windows Server 2012 R2 では、2016年7月の更新プログラムのロールアップ`prompt=login`で AD FS、パラメーターのネイティブサポートが導入されました。 これは、Azure AD が Azure AD および Office 365 認証要求の一部として AD FS サービスにこのパラメーターをそのように送信できるようになったことを意味します。

## <a name="ad-fs-versions-that-support-promptlogin"></a>Prompt = login をサポートするバージョンの AD FS

パラメーターを`prompt=login`サポートする AD FS バージョンの一覧を次に示します。

- Windows Server 2012 R2 の AD FS (2016 年7月の更新プログラムのロールアップ)
- Windows Server 2016 の AD FS

## <a name="how-to-configure-a-federated-domain-to-send-promptlogin-to-ad-fs"></a>プロンプトを送信するフェデレーションドメインを構成する方法 = ログイン AD FS

Azure AD PowerShell モジュールを使用して、設定を構成します。

> [!NOTE]
> 現在、この `prompt=login` 機能は、(`PromptLoginBehavior` プロパティにより有効にされ) [Azure AD Powershell モジュールのバージョン1.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185) でのみ使用できます。このコマンドレットには、set-msoldomainfederationsettings などの "msol" を含む名前が付いています。  現時点では、Azure AD PowerShell モジュールの ' version 2.0 ' 経由では使用できません。このコマンドレットには\*、"AzureAD" のような名前が付いています。

1. まず、次の PowerShell コマンド`PreferredAuthenticationProtocol`を`SupportsMfa`実行し`PromptLoginBehavior`て、フェデレーションドメインの、、およびの現在の値を取得します。

```powershell
    Get-MsolDomainFederationSettings -DomainName <your_domain_name> | Format-List *
```

> [!NOTE]
> 既定での`Get-MsolDomainFederationSettings`の出力では、コンソールに特定のプロパティは表示されません。 すべてのプロパティを表示するには、`|`パイプを使用し`Format-List *`て出力をに渡し ()、オブジェクトのすべてのプロパティの出力を強制的に適用する必要があります。

![Get-MsolDomainFederationSettings](media/AD-FS-Prompt-Login/GetMsol.png)

> [!NOTE]
> プロパティが空の場合 (`$null`) は、の`TranslateToFreshPasswordAuth`既定の動作を意味します。 `PreferredAuthenticationMethod`

2. 次のコマンドを実行`PromptLoginBehavior`して、の目的の値を構成します。

```powershell
    Set-MsolDomainFederationSettings –DomainName <your_domain_name> -PreferredAuthenticationProtocol <current_value_from_step1> -SupportsMfa <current_value_from_step1> -PromptLoginBehavior <TranslateToFreshPasswordAuth|NativeSupport|Disabled>
```

パラメーターの`PromptLoginBehavior`使用可能な値とその意味は次のとおりです。

- **TranslateToFreshPasswordAuth**: および`prompt=login` へ`wfresh=0`の変換の既定の Azure AD 動作を意味します。 `wauth=http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`
- **NativeSupport**: `prompt=login`パラメーターが AD FS にそのように送信されることを意味します。 これは、2012年 7 2016 月の更新プログラムのロールアップ以降を使用して AD FS が Windows Server R2 に存在する場合に推奨される値です。
- **Disabled**: のみ`wfresh=0`が AD FS に送信されることを意味します。
