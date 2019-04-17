---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: "ホーム領域検出のカスタマイズ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 328c313b2d5bf174f6e6af20cd91ac9620edac82
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="home-realm-discovery-customization"></a>ホーム領域検出のカスタマイズ

>適用対象: Windows Server 2016、Windows Server 2012 R2

AD FS のクライアントはまず、リソースを要求時に、リソース フェデレーション サーバーには、クライアントの領域に関する情報がありません。 AD FS のクライアントに応答する、リソース フェデレーション サーバー、**クライアント領域の検出**] ページで、ユーザーが、一覧からホーム領域を選択します。 要求プロバイダー信頼の表示名のプロパティからは、この一覧の値が設定されます。 次の Windows PowerShell コマンドレットを使用して、変更および AD FS ホーム領域検出エクスペリエンスをカスタマイズします。  
  
![ホーム領域](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> ローカルの Active Directory に対して表示される要求プロバイダー名がフェデレーション サービスの表示名であるに注意してください。  
  
## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>特定の電子メール サフィックスを使用する Id プロバイダーを構成します。  
組織は、複数の要求プロバイダーとフェデレーションことができます。 AD FS、サフィックスの一覧を表示する管理者の詳細なボックス機能を提供できるようになりました@us.contoso.com、@eu.contoso.comされる要求プロバイダーでサポートされているし、suffix\ ベースの検出を有効にします。 この構成では、エンドユーザーが自身の組織アカウントを入力し、AD FS が自動的に対応する要求プロバイダーを選択します。  
  
Id プロバイダーを構成する \(IDP\)、よう`fabrikam`するために、特定の電子メール サフィックスを使用し、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
  
## <a name="configure-an-identity-provider-list-per-relying-party"></a>証明書利用者ごとの id プロバイダーの一覧を構成するパーティ  
組織によっていくつかのシナリオについては、エンドユーザーが要求プロバイダーのサブセットのみがホーム領域検出ページに表示されるように、アプリケーションに固有の要求プロバイダーのみが表示できる可能性があります。  
  
証明書利用者ごとに IDP の一覧を構成する \(RP\) をパーティーは、次の Windows PowerShell コマンドレットと構文を使用します。  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>イントラネットのホーム領域検出をバイパスします。  
ほとんどの組織は、そのファイアウォールの内側からアクセスするユーザーのローカルの Active Directory をサポートするだけです。 このような場合は、管理者は、イントラネットのホーム領域検出をバイパスする AD FS を構成できます。  
  
イントラネットに HRD をバイパスするには、次の Windows PowerShell コマンドレットと構文を使用します。  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> ください注場合は、証明書利用者に対する id プロバイダーの一覧パーティーが構成されている、以前の設定を有効にした場合でも、イントラネットからユーザーのアクセス、AD FS は依然ホーム領域検出 \(HRD\) ページに表示されます。 ここで HRD をバイパスするには、"Active Directory"がこの証明書利用者の IDP 一覧にも追加されないようにする必要があります。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
