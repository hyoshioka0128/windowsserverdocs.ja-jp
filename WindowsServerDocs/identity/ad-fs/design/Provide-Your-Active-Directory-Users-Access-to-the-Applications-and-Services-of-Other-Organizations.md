---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 0d1bf60c276932a77573acff2e4e011831e65a05
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967569"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する

この Active Directory フェデレーション サービス \(AD FS\) 展開の目的で目標に基づき [提供、Active Directory ユーザーへのアクセス、クレーム対応アプリケーションとサービス](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)します。

アカウント パートナー組織の管理者が、別の組織のホストされているリソースへのフェデレーション アクセスを従業員に提供することを展開の目的とする場合、次のようになります。

-   企業ネットワーク内の Active Directory ドメインにログオンしている従業員が 1 つ使用して\-記号\-に \(SSO\) 複数の Web にアクセスする機能\-ベースのアプリケーションまたはサービスで、アプリケーションやサービスが別の組織で AD FS によって保護されました。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。

    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。

-   Active Directory ドメインにログオンしているリモートの社員は、AD FS で保護された Web にフェデレーション アクセスするために、組織内のフェデレーション サーバーから AD FS トークンを取得できます\-ベースのアプリケーションまたは別の組織でホストされるサービスです。

    たとえば、Fabrikam には、そのリモートの社員へのフェデレーションは、Fabrikam 企業ネットワーク上にある fabrikam 社の従業員を必要とせず、Contoso, でホストされる AD FS で保護されたサービスへのアクセスができます。

「 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) 」で説明されていて、次の図で影の付いている基本コンポーネントに加えて、この展開の目的には次のコンポーネントが必要です。

-   **アカウント パートナー フェデレーション サーバー プロキシ:** フェデレーション サービスまたはアプリケーションがインターネットからアクセスする従業員は、この AD FS のコンポーネントを使用して認証を実行します。 既定では、このコンポーネントはフォーム認証を実行しますが、基本認証も実行できます。 また、Secure Sockets Layer を実行するには、このコンポーネントを構成することもできます。 \(SSL\) 、組織の従業員を表示する証明書がある場合、クライアント認証です。 詳細については、「[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)」を参照してください。

-   **境界 DNS:** このドメインネームシステム DNS の \( 実装 \) により、境界ネットワークのホスト名が提供されます。 フェデレーション サーバー プロキシの境界の DNS を構成する方法の詳細については、次を参照してください。 [フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。

-   **リモート従業員:** リモート従業員は、 \- \( 企業ネットワークからの有効な資格情報を使用して、サポートされている web ブラウザーまたは web ベースのサービスを介して web ベースのアプリケーションにアクセスし \) \- \( \) ます。このとき、従業員はオフサイトでインターネットを使用しています。 リモートの場所に、従業員のクライアント コンピューターは、トークンを生成して、アプリケーションまたはサービスに対する認証をフェデレーション サーバー プロキシと直接通信します。

リンク先のトピックの情報を確認した後は、「 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)」の手順に従って、この目標のデプロイを開始できます。

次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。

![アプリへのアクセスします。](media/50af4837-31e0-451f-a942-e705c2300065.gif)

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
