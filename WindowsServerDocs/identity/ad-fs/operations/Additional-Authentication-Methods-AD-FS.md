---
title: AD FS 2019 での追加の認証方法
description: このドキュメントでは、AD FS 2019 の新しい認証方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8a53a4cfca4f34459102b8edc8e6af82f36be70d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358369"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>AD FS 2019 でサードパーティの認証プロバイダーをプライマリ認証として構成する


組織では、パスワードベースの認証要求を送信することによって、ブルートフォース、侵害、またはユーザーアカウントのロックアウトを試みる攻撃が発生しています。  組織のセキュリティ侵害を防ぐために、AD FS には、エクストラネットの "スマート" ロックアウトや IP アドレスベースのブロックなどの機能が導入されました。  

ただし、これらの軽減策はリアクティブです。  このような攻撃の重要度を軽減するために、AD FS では、パスワードを収集する前にパスワード以外の要素を要求することができます。  

たとえば、AD FS 2016 では、認証アプリからの OTP コードを最初の要素として使用できるように、プライマリ認証として Azure MFA が導入されました。
AD FS 2019 を使用して構築すると、外部認証プロバイダーをプライマリ認証要素として構成できます。

これにより、次の2つの主要なシナリオが可能になります。

## <a name="scenario-1-protect-the-password"></a>シナリオ 1: パスワードを保護する
追加の外部因子を要求することによって、ブルートフォース攻撃やロックアウトからパスワードベースのログインを保護します。  外部認証が正常に完了した場合にのみ、ユーザーにパスワードの入力を求めるメッセージが表示されます。  これにより、攻撃者がアカウントを侵害または無効にしようとする便利な方法を排除できます。

このシナリオは、次の2つのコンポーネントで構成されています。
- プライマリ認証として Azure MFA または外部認証要素を要求する
- AD FS での追加認証としてのユーザー名とパスワード

## <a name="scenario-2-password-free"></a>シナリオ 2: パスワードを無料でご利用いただけます。
パスワードを完全に排除しますが、パスワードベースではないメソッドを完全に使用して、強力な多要素認証を完了し AD FS
- Azure MFA と Authenticator アプリ
- Windows 10 Hello for Business
- 証明書の認証
- 外部認証プロバイダー

## <a name="concepts"></a>概念
**プライマリ認証**とは、特に、追加の要因の前にユーザーが最初に要求する方法であるということです。  以前は、AD FS で使用できる唯一の主要な方法は、Active Directory または Azure MFA のメソッド、またはその他の LDAP 認証ストアに組み込まれています。  外部メソッドは、プライマリ認証が正常に完了した後に行われる "追加" 認証として構成できます。

AD FS 2019 では、外部認証は主な機能として、AD FS ファームに登録されている外部認証プロバイダー (Register-adfsauthenticationprovider を使用) がプライマリ認証に使用できるようになります。また、"追加" することもできます。認証. これらは、フォーム認証や証明書認証などの組み込みプロバイダーと同じ方法で、イントラネットまたはエクストラネットで使用できます。

![認証 (authentication)](media/Additional-Authentication-Methods-AD-FS/auth1.png)

外部プロバイダーがエクストラネット、イントラネット、またはその両方に対して有効になると、ユーザーが使用できるようになります。  複数の方法が有効になっている場合、ユーザーは選択肢ページを表示し、追加の認証の場合と同様に、主要な方法を選択できます。

## <a name="pre-requisites"></a>前提条件
外部認証プロバイダーをプライマリとして構成する前に、次の前提条件が整っていることを確認してください。
- AD FS ファーム動作レベル (FBL) が ' 4 ' に発生しました (この値は AD FS 2019 に変換されます)
    - これは、新しい AD FS 2019 ファームの既定の FBL 値です
    - Windows Server 2012 R2 または2016に基づく AD FS ファームの場合は、PowerShell コマンドレット AdfsFarmBehaviorLevelRaise を使用して FBL を発生させることができます。  AD FS ファームのアップグレードの詳細については、SQL ファームまたは WID ファームのファームアップグレードに関する記事を参照してください。 
    - コマンドレット AdfsFarmInformation を使用して、FBL 値を確認できます。
- AD FS 2019 ファームは、新しい2019の [改ページ調整されたユーザー向けページ] を使用するように構成されています。
    - これは、新しい AD FS 2019 ファームの既定の動作です。
    - Windows Server 2012 R2 または2016からアップグレードされた AD FS ファームの場合は、次に示すように、プライマリとしての外部認証 (このドキュメントで説明されている機能) が有効になっていると、改ページ調整されたフローが自動的に有効になります。

## <a name="enable-external-authentication-methods-as-primary"></a>外部認証方法をプライマリとして有効にする
前提条件を確認したら、次の2つの方法で AD FS 追加の認証プロバイダーをプライマリとして構成できます。

### <a name="using-powershell"></a>PowerShell を使用する


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


追加の認証をプライマリとして有効または無効にした後、AD FS サービスを再起動する必要があります。

### <a name="using-the-ad-fs-management-console"></a>AD FS 管理コンソールの使用
AD FS 管理コンソールで [**サービス** -> **認証方法** **プライマリ認証方法**編集] をクリックして

**[追加の認証プロバイダーをプライマリとして許可する]** チェックボックスをオンにします。

追加の認証をプライマリとして有効または無効にした後、AD FS サービスを再起動する必要があります。

## <a name="enable-username-and-password-as-additional-authentication"></a>追加の認証としてユーザー名とパスワードを有効にする
"パスワードを保護する" シナリオを完了するには、PowerShell または AD FS 管理コンソールを使用して、追加の認証としてユーザー名とパスワードを有効にします。
### <a name="using-powershell"></a>PowerShell を使用する



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>AD FS 管理コンソールの使用
AD FS 管理コンソールの [**サービス** -> の**認証方法**] で、 **[追加の認証方法]** の **[編集]** をクリックします。

**[フォーム認証]** のチェックボックスをオンにして、追加の認証としてユーザー名とパスワードを有効にします。
