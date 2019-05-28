---
title: AD FS 2019 で追加の認証方法
description: このドキュメントでは、AD FS 2019 で新しい認証方法を説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b0d5754a4622df9ca26a80bd4e32c355dda0f684
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190064"
---
# <a name="configure-3rd-party-authentication-providers-as-primary-authentication-in-ad-fs-2019"></a>AD FS 2019 でプライマリ認証としてサード パーティの認証プロバイダーを構成します。


ブルート フォース攻撃をしようとする攻撃が発生している組織、侵害、またはそれ以外の場合、パスワード ベースの認証要求を送信してユーザー アカウントをロックします。  セキュリティ侵害から企業を保護するため、AD FS に「スマート」エクストラネットのロックアウトや IP アドレス ベースのブロックなどの機能が導入されました。  

ただし、これらの軽減策は、事後対応型です。  AD FS では、これらの攻撃の重大度を減らす、プロアクティブな手段を提供するには、パスワードを収集する前にパスワード以外の要因を要求する機能があります。  

たとえば、最初の要素として、Authenticator アプリからの OTP コードを使用することができるように、AD FS 2016 では、プライマリ認証として Azure MFA を導入してされました。
AD FS 2019、このビルドのプライマリ認証要素として外部認証プロバイダーを構成できます。

これにより、2 つの主要シナリオがあります。

## <a name="scenario-1-protect-the-password"></a>シナリオ 1: パスワードを保護します。
最初に、追加の外部の要素を要求することで、ブルート フォース攻撃やロックアウトからパスワード ベースのログインを保護します。  外部の認証が正常に完了する場合にのみが、ユーザーを参照してくださいパスワードの入力。  これにより、攻撃者は侵害またはアカウントを無効にする試行したが、便利な方法がなくなります。

このシナリオでは、2 つのコンポーネントで構成されます。
- プライマリ認証と Azure MFA または外部の認証要素の入力を求める
- ユーザー名とパスワードとして AD FS で追加の認証

## <a name="scenario-2-password-free"></a>シナリオ 2: パスワードを使用しません。
パスワードを完全に排除が完了すると、強力な多要素認証がまったくないパスワードを使用してベースの AD FS でのメソッド
- Authenticator アプリを使用した azure MFA
- Windows 10 のこんにちは for Business
- 証明書の認証
- 外部認証プロバイダー

## <a name="concepts"></a>概念
どのような**プライマリ認証**本当に意味は、その他の要素の前に、最初のユーザーに求めるメソッドであります。  以前の AD FS で使用可能なプライマリのみメソッド用にビルドしたメソッドで Active Directory または Azure MFA、またはその他の LDAP 認証ストア。  外部メソッドは、プライマリ認証が正常に完了した後に行われる、「追加」の認証として構成できます。

AD FS 2019、主要な機能として外部認証意味 (Register-adfsauthenticationprovider を使用)、AD FS ファームに登録されているすべての外部認証プロバイダーがプライマリ認証だけでなく"additional"の利用になること認証します。 イントラネットやエクストラネットで使う証明書の認証、フォーム認証などの組み込みのプロバイダーと同じ方法が有効にすることができます。

![認証 (authentication)](media/Additional-Authentication-Methods-AD-FS/auth1.png)

エクストラネット、イントラネットの外部プロバイダーが有効にすると、またはその両方を使用するユーザーの使用可能になります。  複数の方法を有効にすると、ユーザーは選択したページを参照してくださいし、追加の認証の場合と同様、主要な方法を選択できます。

## <a name="pre-requisites"></a>前提条件
プライマリとして外部認証プロバイダーを構成する前に、次の前提条件であることを確認します
- '4' (この値は、AD FS 2019 に変換されます) を AD FS ファーム動作レベル (FBL) が発生しました
    - これは、新しい AD FS 2019 ファームの既定の FBL 値
    - AD FS ファームを Windows Server 2012 R2 または 2016 に基づいて、Invoke AdfsFarmBehaviorLevelRaise PowerShell コマンドレットを使用して、FBL を表示できます。  AD FS ファームをアップグレードする方法の詳細については、ファームのアップグレード SQL ファームや WID ファームの記事を参照してください。 
    - Get AdfsFarmInformation コマンドレットを使用して FBL 値をチェックすることができます。
- ページに接続する新しい 2019年 '改ページ調整された' ユーザーを使用する AD FS 2019 ファームが構成されています。
    - これは、新しい AD FS 2019 ファームの既定の動作
    - Windows Server 2012 R2 または 2016 からアップグレードされた AD FS ファーム、改ページ調整されたフローが自動的に有効に以下に示すプライマリとして、外部の認証が可能 (機能は、このドキュメントで説明)。

## <a name="enable-external-authentication-methods-as-primary"></a>プライマリとして、外部の認証方法を有効にします。
前提条件を確認した後は、プライマリとして AD FS の追加の認証プロバイダーを構成する 2 つの方法があります。

### <a name="using-powershell"></a>PowerShell を使用する


```powershell
PS C:\> Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true
``` 


AD FS サービスを有効にするか、プライマリと追加の認証を無効にすると再起動する必要があります。

### <a name="using-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用します。
AD FS 管理コンソールで [**サービス** -> **認証方法** **プライマリ認証方法**編集] をクリックして

チェック ボックスをクリックします。**プライマリと追加の認証プロバイダーを許可する**します。

AD FS サービスを有効にするか、プライマリと追加の認証を無効にすると再起動する必要があります。

## <a name="enable-username-and-password-as-additional-authentication"></a>追加の認証としてユーザー名とパスワードを有効にします。
「パスワードを保護する」シナリオを完了するには、PowerShell または AD FS 管理コンソールを使用して追加の認証とユーザー名とパスワードを有効にします。
### <a name="using-powershell"></a>PowerShell を使用する



```powershell
PS C:\> $providers = (Get-AdfsGlobalAuthenticationPolicy).AdditionalAuthenticationProvider

PS C:\>$providers = $providers + "FormsAuthentication"

PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider $providers
``` 

### <a name="using-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用します。
AD FS 管理コンソールで **サービス** -> **認証方法****追加の認証方法**、 をクリックして**編集します。**

チェック ボックスをクリックします。**フォーム認証**ユーザー名とパスワードとして追加の認証を有効にします。
