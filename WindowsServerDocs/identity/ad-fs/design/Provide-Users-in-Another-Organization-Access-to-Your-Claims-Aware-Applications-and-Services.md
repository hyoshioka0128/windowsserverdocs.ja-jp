---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: 要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4a13332cd7cf6361824f05ead4568a45211cc70a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191017"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する


Active Directory フェデレーション サービスでリソース パートナー組織の管理者が\(AD FS\)別の組織のユーザーにフェデレーション アクセスを提供する展開の目的があり、 \(アカウント パートナー組織\)を要求する\-対応のアプリケーションまたは Web\-ベースのサービスは、組織にある\(リソース パートナー組織\):  
  
-   ユーザーの組織への信頼のフェデレーションが構成されていると、組織内の両方をフェデレーション\(アカウント パートナー組織\)によってホストされている AD FS で保護されたアプリケーションやサービスにアクセスできる、組織。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。  
  
-   信頼された組織との直接の関連付けを持たないユーザーをフェデレーション\(個人の顧客など\)、複数の AD FS にアクセスできる、境界ネットワークでホストされている属性ストアにログオンしたユーザーは\-セキュリティで保護されたアプリケーション、インターネットに配置されているクライアント コンピューターから 1 回ログオンすることで、境界ネットワークでホストされています。 つまり、あなたが顧客アカウントをホストして、境界ネットワークへのアクセスを有効にした場合、属性ストアでホストされた顧客は 1 回ログオンするだけで、境界ネットワーク内の 1 つ以上のアプリケーションやサービスにアクセスできるようになります。 詳細については、次を参照してください。 [Web SSO デザイン](Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam たいお客様は、1 つ\-記号\-に \(SSO\) 複数のアプリケーションまたはその境界ネットワークでホストされるサービスにアクセスします。  
  
このような展開目標を達成するには、次のコンポーネントが必要です。  
  
-   **Active Directory Domain Services \(AD DS\):** リソース パートナーのフェデレーション サーバーは、Active Directory ドメインに参加する必要があります。  
  
-   **境界 DNS:** ドメイン ネーム システム\(DNS\)単純なホストを含める必要があります\(A\)リソース レコードのクライアント コンピューターは、リソース パートナーのフェデレーション サーバーと Web サーバーを特定できるようにします。 DNS サーバーでは、境界ネットワークにも必要なその他の DNS レコードがホストされる場合があります。 詳細については、「[フェデレーション サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」をご覧ください。  
  
-   **リソース パートナーのフェデレーション サーバー:** リソース パートナーのフェデレーション サーバーは、アカウント パートナーが送信される AD FS トークンを検証します。 アカウント パートナーの検出は、このフェデレーション サーバーによって行われます。 詳細については、「 [Review the Role of the Federation Server in the Resource Partner](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)」を参照してください。  
  
-   **Web サーバー:** Web サーバーは、Web アプリケーションか Web サービスのいずれかをホストできます。 Web サーバーは、保護された Web アプリケーションや Web サービスへのアクセスを許可する前に、フェデレーション ユーザーから有効な AD FS トークンを受信したかどうかを確認します。  
  
    Windows Identity Foundation を使用して、 \(WIF\), Web アプリケーションを開発する、またはその it を受け入れるようにサービスがユーザー名とパスワードなどの任意の標準のログオン メソッドを使用して作成されるユーザー ログオン要求をフェデレーションします。  
  
リンク先のトピックの情報を確認した後には、次の手順に従って、この目標の展開を開始できます[チェックリスト。フェデレーション Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)と[チェックリスト。Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。  
  
![要求へのアクセスします。](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
