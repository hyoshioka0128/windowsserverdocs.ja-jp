---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: フェデレーション サーバーを作成するのに適した状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e61c734780baa1482670af3f24697c10345b292
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190587"
---
# <a name="when-to-create-a-federation-server"></a>フェデレーション サーバーを作成するのに適した状況

フェデレーションした serverin Active Directory フェデレーション サービスを作成するときに\(AD FS\)、組織できます手段を提供します。  
  
-   Web の 1 つに参加\-サインオン\-で\(SSO\)– 別の組織との通信に基づく\(に少なくとも 1 つのフェデレーション サーバーを含む\)とで、必要な場合、お客様の組織内従業員\(、インターネット経由でアクセスを必要がある\)します。  
  
-   ID 委任を使用して、インフラストラクチャ サービスにユーザーを代理処理するためのフロント エンド サービスを有効化する。 詳細については、「 [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md)」を参照してください。  
  
次のセクションでは、1 つまたは複数のフェデレーション サーバーを作成するタイミングと場所を決定するための重要な決定事項について説明します。  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>フェデレーション サーバーの組織役割を確認する  
新しいフェデレーション サーバーを作成する場合に関する情報に基づいて判断を行うには、まず、サーバーが存在する組織でを確認する必要があります。 組織でフェデレーション サーバーが果たす役割は、アカウント パートナー組織内、またはリソース パートナー組織のフェデレーション サーバーを配置するかどうかによって異なります。  
  
アカウント パートナーの企業ネットワークにフェデレーション サーバーが配置されると、役割ブラウザー、Web サービス、または id セレクター クライアントのユーザーの資格情報の認証し、セキュリティ トークンをクライアントに送信することです。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)します。  
  
リソース パートナーの企業ネットワークにフェデレーション サーバーが配置されると、その役割は、リソース パートナー組織内のフェデレーション サーバーによって発行されるセキュリティ トークンに基づいてユーザーを認証する、または役割からのトークン要求をリダイレクトすることです。Web アプリケーションまたはクライアントが属しているアカウント パートナー組織の Web サービスを構成します。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>展開する AD FS 設計を決定する  
次の AD FS 設計のいずれかを展開するときに、組織内のフェデレーション サーバーを作成します。  
  
-   [Web SSO 設計](Web-SSO-Design.md)  
  
-   [フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)  
  
必要に応じて、フェデレーション Web SSO 設計を展開する組織は、アカウント パートナー ロールとリソース パートナーの役割で動作できるように、1 つのフェデレーション サーバーを構成できます。 ここでは、フェデレーション サーバーが生じる場合 Security Assertion Markup Language \(SAML\)独自の組織、または、組織に再接続トークン要求内のユーザー アカウントに基づいて、トークンがユーザーのアカウントが置かれている場所に基づいて.  
  
> [!NOTE]  
> フェデレーション Web SSO 設計に、アカウント パートナー内の少なくとも 1 つのフェデレーション サーバーとリソース パートナー内の少なくとも 1 つのフェデレーション サーバーが必要があります。  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>フェデレーション サーバーとフェデレーション サーバー プロキシの違い  
フェデレーション サーバーを Web ページを使用できる符号\-で、ポリシー、認証、およびフェデレーション サーバー プロキシは同じ方法で検出します。 フェデレーション サーバーとフェデレーション サーバー プロキシの主な違い行う必要がある操作で、フェデレーション サーバーがフェデレーション サーバー プロキシを実行できませんを実行することができます。  
  
フェデレーション サーバーのみを実行できる操作を次に示します。  
  
-   フェデレーション サーバーは、トークンを生成する暗号操作を実行します。 フェデレーション サーバー プロキシは、トークンを生成できないは、ルーティングまたはクライアントと、フェデレーション サーバーに、必要な場合、トークンのリダイレクトを使用できます。 詳細については、フェデレーション サーバーを使用して、次を参照してください。[フェデレーション サーバー プロキシを作成するときに](When-to-Create-a-Federation-Server-Proxy.md)します。  
  
-   フェデレーション サーバーが企業ネットワーク上のクライアントに対して Windows 統合認証の使用をサポートします。フェデレーション サーバー プロキシは必要ありません。 フェデレーション サーバーで Windows 統合認証の使用に関する詳細については、次を参照してください。 [When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md)します。  
  
> [!CAUTION]  
> フェデレーション サーバーと、SQL Server 構成データベース、SQL Server 属性ストア、ドメイン コント ローラー、および AD LDS インスタンスの間の通信は、整合性や機密性が既定では保護されません。 この状況を回避するには、IPSEC を使用するか、これらすべてのサーバー間の接続を物理的にセキュリティ保護して、これらのサーバー間の通信チャネルを保護することを検討してください。 フェデレーション サーバーと SQL server の間の通信については、接続文字列に SSL 保護を使用することを検討してください。 フェデレーション サーバーとドメイン コント ローラーの間の接続については、Kerberos による署名と暗号化を有効にすることを検討してください。 LDAP、LDAP の\/AD LDS の S がサポートされていません\/AD DS です。  
  
## <a name="how-to-create-a-federation-server"></a>フェデレーション サーバーの作成方法  
AD FS フェデレーション サーバー構成ウィザードまたは Fsconfig.exe コマンドを使用してフェデレーション サーバーを作成する\-ライン ツール。 これらのツールを使用する場合、フェデレーション サーバーを作成するために次のいずれかのオプションを選択できます。  
  
-   作成、スタンド\-だけでフェデレーション サーバー  
  
    スタンドを設定する方法について\-単独でフェデレーション サーバーを参照してください[Create a Stand-Alone Federation Server](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)。  
  
-   フェデレーション サーバー ファーム内に最初のフェデレーション サーバーを作成する  
  
    最初のフェデレーション サーバーを設定またはファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファーム内の最初のフェデレーション サーバーの作成](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)です。  
  
-   フェデレーション サーバー ファームにフェデレーション サーバーを追加する  
  
    ファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファームにフェデレーション サーバーを追加](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)します。  
  
これらの各オプションの作業についての詳細を参照してください。 [、AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)します。  
  
フェデレーション サーバーを展開するために必要なすべての前提条件を設定する方法の詳細については、次を参照してください。[チェックリスト。フェデレーション サーバーを設定する](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

