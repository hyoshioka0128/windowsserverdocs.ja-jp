---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d50d26c5c654e5c91b82f6f209e21f257221c12d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843583"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

この Active Directory フェデレーション サービス\(AD FS\)目標に基づいて、展開の目的[提供、Active Directory ユーザーへのアクセス、クレーム対応アプリケーションとサービス](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)します。  
  
アカウント パートナー組織の管理者が、別の組織のホストされているリソースへのフェデレーション アクセスを従業員に提供することを展開の目的とする場合、次のようになります。  
  
-   企業ネットワーク内の Active Directory ドメインにログオンしている従業員は 1 つ使用して\-サインオン\-で\(SSO\)複数の Web にアクセスする機能\-ベースのアプリケーションまたはサービスをアプリケーションやサービスが別の組織で AD FS によって保護されます。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。  
  
-   AD FS で保護された Web にフェデレーション アクセスのために、組織内のフェデレーション サーバーから AD FS トークンを取得できますが、Active Directory ドメインにログオンしたリモート従業員は\-ベースのアプリケーションまたは別のホストされるサービス組織。  
  
    たとえば、Fabrikam には、そのリモートの社員へのフェデレーションは、Fabrikam 企業ネットワーク上にある fabrikam 社の従業員を必要とせず、Contoso, でホストされる AD FS で保護されたサービスへのアクセスができます。  
  
「 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) 」で説明されていて、次の図で影の付いている基本コンポーネントに加えて、この展開の目的には次のコンポーネントが必要です。  
  
-   **アカウント パートナー フェデレーション サーバー プロキシ:** フェデレーション サービスまたはアプリケーションをインターネットからアクセスする従業員は、この AD FS のコンポーネントを使用して、認証を実行します。 既定では、このコンポーネントはフォーム認証を実行しますが、基本認証も実行できます。 また、Secure Sockets Layer を実行するには、このコンポーネントを構成することもできます。 \(SSL\) 、組織の従業員を表示する証明書がある場合、クライアント認証です。 詳細については、次を参照してください。 [フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
-   **境界 DNS:** ドメイン ネーム システムのこの実装\(DNS\)境界ネットワークのホスト名を指定します。 フェデレーション サーバー プロキシの境界の DNS を構成する方法の詳細については、次を参照してください。 [フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
-   **リモート従業員:** リモートの社員が Web にアクセスする\-ベースのアプリケーション\(サポートされている Web ブラウザーを介して\)または Web\-ベースのサービス\(アプリケーションを通じて\)から有効な資格情報を使用します。企業ネットワークには、インターネットを使用してオフサイトにします。 リモートの場所に、従業員のクライアント コンピューターは、トークンを生成して、アプリケーションまたはサービスに対する認証をフェデレーション サーバー プロキシと直接通信します。  
  
リンク先のトピックの情報を確認した後には、次の手順に従って、この目標の展開を開始できます[チェックリスト。フェデレーション Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。  
  
![アプリへのアクセスします。](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
