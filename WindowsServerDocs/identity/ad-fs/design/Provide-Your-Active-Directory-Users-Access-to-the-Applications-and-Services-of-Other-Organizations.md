---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: "アプリケーションや他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>アプリケーションや他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この Active Directory フェデレーション サービス \(AD FS\) 展開目的が基に目標に[提供 Your Active Directory Users Access to Your Claims-aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)します。  
  
管理者は、アカウント パートナー組織でとを従業員にフェデレーション アクセスを提供する展開の目的があるホストされているリソース別の組織で。  
  
-   企業ネットワーク内の Active Directory ドメインにログオンしている従業員は、複数の Web ベースのアプリケーションやサービスで、アプリケーションまたはサービスが別の組織にいる場合、AD FS によって保護されたアクセスするのに \(SSO\) 機能シングル sign\-でを使用できます。 詳細については、次を参照してください。[Federated Web SSO Design](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、企業ネットワークの社員へのフェデレーション Contoso でホストされている Web サービスへのアクセスをします。  
  
-   Active Directory ドメインにログオンしたリモート従業員は、AD FS で保護された Web ベース アプリケーションまたは別の組織でホストされているサービスにフェデレーション アクセスを組織内のフェデレーション サーバーから AD FS トークンを取得できます。  
  
    たとえば、Fabrikam が、そのリモートの社員へのフェデレーション Fabrikam 企業ネットワーク上にある fabrikam 社の従業員を必要とせず、Contoso でホストされている AD FS で保護されたサービスへのアクセスをします。  
  
基本コンポーネントに加えてに記載されている[提供 Your Active Directory Users Access to Your Claims-aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)とは、次の図で影の付いている、次のコンポーネントがこの展開の目的に必要です。  
  
-   **アカウント パートナーのフェデレーション サーバー プロキシ:**フェデレーション サービスまたはアプリケーションをインターネットからアクセスする従業員は、この AD FS のコンポーネントを使用して認証を実行することができます。 既定では、このコンポーネントは、フォーム認証を実行しますが、基本認証も実行できます。 また、組織で従業員が提示する証明書がある場合は、Secure Sockets Layer \(SSL\) クライアント認証を実行するには、このコンポーネントを構成することができます。 詳細については、次を参照してください。[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
-   **境界 DNS:**ドメイン ネーム システム \(DNS\) のこの実装は、境界ネットワークにホスト名を提供します。 フェデレーション サーバー プロキシの境界 DNS を構成する方法の詳細については、次を参照してください。[フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
-   **リモート従業員:**リモート従業員が Web ベース アプリケーションにアクセス \ (サポートされている Web browser\) 経由または Web ベース サービス \ (を通じて、できるアプリケーション) を使用して、企業ネットワークから有効な資格情報は、インターネットを使用してオフサイト中にします。 従業員のクライアント コンピューターは、リモートの場所には、トークンを生成して、アプリケーションまたはサービスに対する認証をフェデレーション サーバー プロキシと直接通信します。  
  
後のリンク先のトピックの情報を確認するには、次の手順に従って、この目標のデプロイを開始できます[チェックリスト: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開目標に必要なコンポーネントの各を示します。  
  
![アプリへのアクセスします。](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
