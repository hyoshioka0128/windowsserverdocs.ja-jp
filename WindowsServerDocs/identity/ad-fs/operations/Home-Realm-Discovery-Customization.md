---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: ホーム領域検出のカスタマイズ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1667199e99545d3b29ba31512bd0c25718b93c4b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816325"
---
# <a name="home-realm-discovery-customization"></a>ホーム領域検出のカスタマイズ


AD FS クライアントは、まず、リソースを要求する場合、リソース フェデレーション サーバーには、クライアントの領域に関する情報がありません。 リソースのフェデレーション サーバーが AD FS のクライアントには、 **クライアント領域の検出**  ページで、一覧から、ユーザーが、ホーム領域を選択します。 この一覧の値は、要求プロバイダー信頼の表示名プロパティから取得されます。 次の Windows PowerShell コマンドレットを使用して、変更および AD FS ホーム領域検出エクスペリエンスをカスタマイズします。  
  
![ホーム領域](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> ローカルの Active Directory に表示される要求プロバイダー名はフェデレーション サービスの表示名であることに注意してください。  
  



## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>特定の電子メール サフィックスを使用するための ID プロバイダーの構成  
組織は複数の要求プロバイダーとフェデレーションを確立できます。 AD FS では、管理者が\-box の機能を使用して、要求プロバイダーでサポートされているサフィックス (@us.contoso.com、@eu.contoso.comなど) を一覧表示し、サフィックス\-ベースの検出に対して有効にすることができるようになりました。 この構成では、エンドユーザーが自分の組織のアカウントに入力でき、AD FS が自動的に対応する要求プロバイダーを選択します。  
  
Id プロバイダーを構成する \(IDP\), など `fabrikam`, を特定の電子メール サフィックスを使用して、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
>[!NOTE]
> 2つの AD FS サーバー間でフェデレーションを行う場合は、要求プロバイダー信頼の PromptLoginFederation プロパティを ForwardPromptAndHintsOverWsFederation に設定します。  これは、AD FS が login_hint とプロンプトを IDP に転送するためです。  これを行うには、次の PowerShell コマンドレットを実行します。
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
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
