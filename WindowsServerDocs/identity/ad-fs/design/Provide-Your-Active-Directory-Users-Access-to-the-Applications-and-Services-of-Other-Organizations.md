---
ms.assetid: 2d62386c-b466-4a54-b6fa-5d16cda120d8
title: Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bcf9b9ec91c1757ad060747a6aa1589012c1ec14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359033"
---
# <a name="provide-your-active-directory-users-access-to-the-applications-and-services-of-other-organizations"></a>Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する

この Active Directory フェデレーションサービス (AD FS) は、 [Active Directory ユーザーが要求に対応するアプリケーションとサービスにアクセスできるようにする](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)ことの目標に基づいて、\) のデプロイ目標を AD FS \(ます。  
  
アカウント パートナー組織の管理者が、別の組織のホストされているリソースへのフェデレーション アクセスを従業員に提供することを展開の目的とする場合、次のようになります。  
  
-   企業ネットワーク内の Active Directory ドメインにログオンしている従業員は \(SSO\) 機能でシングル\-署名\-を使用して、アプリケーションまたはサービスが別の組織にある場合に\-によって保護されている複数の Web AD FS ベースのアプリケーションまたはサービスにアクセスできます。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。  
  
-   Active Directory ドメインにログオンしたリモート従業員は、組織内のフェデレーションサーバーから AD FS トークンを取得して、AD FS で保護された Web\-ベースのアプリケーションや、別の組織でホストされているサービスへのフェデレーションアクセスを取得できます。  
  
    たとえば、Fabrikam には、そのリモートの社員へのフェデレーションは、Fabrikam 企業ネットワーク上にある fabrikam 社の従業員を必要とせず、Contoso, でホストされる AD FS で保護されたサービスへのアクセスができます。  
  
「 [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md) 」で説明されていて、次の図で影の付いている基本コンポーネントに加えて、この展開の目的には次のコンポーネントが必要です。  
  
-   **アカウント パートナー フェデレーション サーバー プロキシ:** フェデレーション サービスまたはアプリケーションがインターネットからアクセスする従業員は、この AD FS のコンポーネントを使用して認証を実行します。 既定では、このコンポーネントはフォーム認証を実行しますが、基本認証も実行できます。 また、Secure Sockets Layer を実行するには、このコンポーネントを構成することもできます。 \(SSL\) 、組織の従業員を表示する証明書がある場合、クライアント認証です。 詳細については、次を参照してください。 [フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
-   **境界の DNS:** ドメイン ネーム システムのこの実装 \(DNS\) 、境界ネットワークのホスト名を提供します。 フェデレーション サーバー プロキシの境界の DNS を構成する方法の詳細については、次を参照してください。 [フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
-   **リモートの社員:** リモートの社員が Web にアクセスする\-ベースのアプリケーション \(サポートされている Web ブラウザーを介して\) または Web\-ベースのサービス \(アプリケーションを通じて\), 、従業員は、インターネットを使用して、企業ネットワークから有効な資格情報を使用しています。 リモートの場所に、従業員のクライアント コンピューターは、トークンを生成して、アプリケーションまたはサービスに対する認証をフェデレーション サーバー プロキシと直接通信します。  
  
リンク先のトピックの情報を確認した後は、「 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)」の手順に従って、この目標のデプロイを開始できます。  
  
次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。  
  
![アプリへのアクセスします。](media/50af4837-31e0-451f-a942-e705c2300065.gif)  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
