---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: "要求対応のアプリケーションとサービスをユーザーに他の組織がアクセスを提供します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4ec08182e2523b0fcb16088ec9c1d094a5923fe
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>要求対応のアプリケーションとサービスをユーザーに他の組織がアクセスを提供します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でリソース パートナー組織の管理者は、別の組織でユーザーにフェデレーション アクセスを提供する展開の目的をいる \ (アカウント パートナー organization\) claims\ 対応アプリケーションや組織に配置されている Web ベース サービスに \ (リソース パートナー organization\)。  
  
-   ユーザーが組織にとって信頼と、フェデレーションが構成されている組織で、組織内の両方をフェデレーション \ (アカウント パートナー organizations\) AD FS の保護されたアプリケーションや、組織でホストされているサービスにアクセスできます。 詳細については、次を参照してください。[Federated Web SSO Design](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのアクセスがフェデレーション、企業ネットワークの従業員にします。  
  
-   信頼済みの組織に直接関連付けを持たないユーザーをフェデレーション \ (など、個々 の customers\ の) ログオンしている属性ストア、境界ネットワークでホストされている場合は、インターネット上に配置されているクライアント コンピューターから 1 回ログオンしても、境界ネットワークでホストされている複数の AD FS\ で保護されたアプリケーションにアクセスできることにします。 つまりを境界ネットワークでアプリケーションまたはサービスへのアクセスを有効にする顧客のアカウントをホストしている場合の属性ストアにホストするお客様にアクセスできますアプリケーションまたはサービスを境界ネットワーク内の 1 つまたは複数 1 回ログオンするだけで。 詳細については、次を参照してください。[Web SSO 設計](Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam は、顧客にシングル sign\-で \(SSO\) へのアクセスを複数のアプリケーションまたは自社の境界ネットワークでホストされているサービス提供を必要があります。  
  
次のコンポーネントは、この展開の目的必要があります。  
  
-   **Active Directory Domain Services \(AD DS\):**リソース パートナーのフェデレーション サーバーは、Active Directory ドメインに参加する必要があります。  
  
-   **境界 DNS:**ドメイン ネーム システム \(DNS\) はクライアント コンピューターは、リソース パートナーのフェデレーション サーバーと Web サーバーを見つけられるように、単純なホスト \(A\) リソース レコードを含める必要があります。 DNS サーバーには、境界ネットワークにも必要なその他の DNS レコードがホストされます。 詳細については、次を参照してください。[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)します。  
  
-   **リソース パートナーのフェデレーション サーバー:**リソース パートナーのフェデレーション サーバーは、アカウント パートナーに送信される AD FS トークンを検証します。 アカウント パートナーの検出は、このフェデレーション サーバーによって行われます。 詳細については、次を参照してください。[リソース パートナーのフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。  
  
-   **Web サーバー:** Web サーバーは、Web アプリケーションまたは Web サービスのいずれかをホストできます。 Web サーバーは、受信した有効な AD FS トークン フェデレーション ユーザーから保護された Web アプリケーションまたは Web サービスへのアクセスを許可する前に確認します。  
  
    Windows Identity Foundation \(WIF\) を使用すると、ユーザー名とパスワードなどの任意の標準のログオン メソッドを使用して作成されるフェデレーション ユーザー ログオン要求を受け入れることができるように、Web アプリケーションまたはサービスを開発できます。  
  
後のリンク先のトピックの情報を確認するには、次の手順に従って、この目標のデプロイを開始できます[チェックリスト: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)と[チェックリスト: Web SSO 設計の実装](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開目標に必要なコンポーネントの各を示します。  
  
![要求へのアクセスします。](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
