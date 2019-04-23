---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: ホーム領域検出のカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1198d8b76f2ecdad728e2de6ce7a5c0d053f779f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868933"
---
# <a name="home-realm-discovery-customization"></a>ホーム領域検出のカスタマイズ

>適用先:Windows Server 2016、Windows Server 2012 R2

AD FS クライアントは、まず、リソースを要求する場合、リソース フェデレーション サーバーには、クライアントの領域に関する情報がありません。 リソースのフェデレーション サーバーが AD FS のクライアントには、 **クライアント領域の検出**  ページで、一覧から、ユーザーが、ホーム領域を選択します。 この一覧の値は、要求プロバイダー信頼の表示名プロパティから取得されます。 次の Windows PowerShell コマンドレットを使用して、変更および AD FS ホーム領域検出エクスペリエンスをカスタマイズします。  
  
![ホーム領域](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> ローカルの Active Directory に表示される要求プロバイダー名はフェデレーション サービスの表示名であることに注意してください。  
  



## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>特定の電子メール サフィックスを使用するための ID プロバイダーの構成  
組織は複数の要求プロバイダーとフェデレーションを確立できます。 では、AD FS で\-管理者は、サフィックスの一覧を表示するための機能をボックス@us.contoso.com、 @eu.contoso.com、つまり要求プロバイダーでサポートされているし、サフィックスを有効にする\-による検出します。 この構成では、エンドユーザーが自分の組織のアカウントに入力でき、AD FS が自動的に対応する要求プロバイダーを選択します。  
  
Id プロバイダーを構成する \(IDP\), など `fabrikam`, を特定の電子メール サフィックスを使用して、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
>[!NOTE]
> 2 つの AD FS サーバー間のフェデレーション時に、ForwardPromptAndHintsOverWsFederation する要求プロバイダー信頼 PromptLoginFederation プロパティを設定します。  これは、AD FS IDP へ login_hint とプロンプトのパラメーターの転送ができるようにします。  これは、次の PowerShell コマンドレットを実行して実行できます。
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>証明書利用者ごとの ID プロバイダーの一覧の構成  
組織によっては、エンド ユーザーがアプリケーションに固有の要求プロバイダーのみを参照できるように、ホーム領域検出ページに一部の要求プロバイダーのみを表示することが必要な場合があります。  
  
証明書利用者ごとに IDP の一覧を構成するパーティ \(RP\), 、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>イントラネットのホーム領域検出のバイパス  
ほとんどの組織では、ファイアウォールの内部からアクセスするユーザーに対してローカルの Active Directory のみをサポートしています。 このような場合は、管理者が、イントラネットのホーム領域検出をバイパスする AD FS を構成できます。  
  
イントラネットに HRD をバイパスするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> 証明書利用者の id プロバイダーの一覧が構成されている場合も、前の設定が有効であるに注意してくださいと、ユーザーにアクセスするイントラネット、AD FS であっても、ホーム領域検出 \(HRD\) ページです。 この場合に HRD をバイパスするには、この証明書利用者の IDP 一覧に "Active Directory" も追加する必要があります。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
