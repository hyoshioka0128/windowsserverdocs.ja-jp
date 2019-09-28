---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: フェデレーション サーバーを作成するのに適した状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 91c260dad1bd260a7dad7320fecd15e6472c50a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407884"
---
# <a name="when-to-create-a-federation-server"></a>フェデレーション サーバーを作成するのに適した状況

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 でフェデレーションサーバーを作成するときに、組織が次のことを行うことができる手段を提供します。  
  
-   1つ以上のフェデレーションサーバー @ no__t があり、必要に応じて、自分の組織の従業員が必要とする場合は、@no__t 組織内の従業員が必要な場合は、no__t を使用して、Web 単一の @ no__t-0sign @-1on on SSO @ no__t に @no__t 接続します。インターネット経由でのアクセス @ no__t。  
  
-   ID 委任を使用して、インフラストラクチャ サービスにユーザーを代理処理するためのフロント エンド サービスを有効化する。 詳細については、「 [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md)」を参照してください。  
  
以下のセクションでは、1つまたは複数のフェデレーションサーバーをいつどのように作成するかを決定する際に重要な決定事項について説明します。  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>フェデレーション サーバーの組織役割を確認する  
新しいフェデレーションサーバーを作成するタイミングについての情報に基づいた決定を行うには、まず、サーバーがどの組織に存在するかを判断する必要があります。 フェデレーションサーバーが組織内で果たす役割は、フェデレーションサーバーをアカウントパートナー組織に配置するか、リソースパートナー組織に配置するかによって異なります。  
  
フェデレーションサーバーがアカウントパートナーの企業ネットワークに配置されている場合、その役割は、ブラウザー、Web サービス、または id セレクタークライアントのユーザー資格情報を認証し、クライアントにセキュリティトークンを送信することになります。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)します。  
  
フェデレーションサーバーがリソースパートナーの企業ネットワークに配置されている場合、その役割は、リソースパートナー組織のフェデレーションサーバーによって発行されたセキュリティトークンに基づいてユーザーを認証するか、またはそのロールがトークン要求をリダイレクトすることになります。クライアントが属しているアカウントパートナー組織に対して構成された Web アプリケーションまたは Web サービス。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>展開する AD FS 設計を決定する  
次の AD FS の設計のいずれかを展開する場合は常に、組織内にフェデレーションサーバーを作成します。  
  
-   [Web SSO 設計](Web-SSO-Design.md)  
  
-   [フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)  
  
必要に応じて、フェデレーション Web SSO 設計を展開する組織は、1つのフェデレーションサーバーを構成して、アカウントパートナーロールとリソースパートナーロールの両方で動作するようにすることができます。 この場合、フェデレーションサーバーは、自身の組織内のユーザーアカウントに基づいて Security Assertion Markup Language @no__t 0SAML @ no__t トークンを生成するか、ユーザーのアカウントが存在する場所に基づいて、トークン要求を組織に再ルーティングすることができます。  
  
> [!NOTE]  
> フェデレーション Web SSO 設計では、アカウントパートナーに少なくとも1つのフェデレーションサーバーがあり、リソースパートナーに少なくとも1つのフェデレーションサーバーがあることが必要です。  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>フェデレーション サーバーとフェデレーション サーバー プロキシの違い  
フェデレーションサーバーは、フェデレーションサーバープロキシと同じ方法で、@ no__t-0in、ポリシー、認証、および検出のための Web ページを提供できます。 フェデレーションサーバーとフェデレーションサーバープロキシの主な違いは、フェデレーションサーバープロキシが実行できない操作をフェデレーションサーバーが実行できる操作です。  
  
フェデレーションサーバーのみが実行できる操作は次のとおりです。  
  
-   フェデレーションサーバーは、トークンを生成する暗号化操作を実行します。 フェデレーションサーバープロキシは、トークンを生成することはできませんが、トークンをクライアントにルーティングまたはリダイレクトしたり、必要に応じてフェデレーションサーバーに戻したりするために使用できます。 フェデレーションサーバーの使用方法の詳細については、「 [When To Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md)」を参照してください。  
  
-   フェデレーションサーバーは、企業ネットワーク上のクライアントに対して Windows 統合認証を使用することをサポートしています。フェデレーションサーバープロキシでは実行されません。 フェデレーションサーバーで Windows 統合認証を使用する方法の詳細については、「 [When To Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md)」を参照してください。  
  
> [!CAUTION]  
> フェデレーション サーバーと、SQL Server 構成データベース、SQL Server 属性ストア、ドメイン コント ローラー、および AD LDS インスタンスの間の通信は、整合性や機密性が既定では保護されません。 この状況を回避するには、IPSEC を使用するか、これらすべてのサーバー間の接続を物理的にセキュリティ保護して、これらのサーバー間の通信チャネルを保護することを検討してください。 フェデレーション サーバーと SQL server の間の通信については、接続文字列に SSL 保護を使用することを検討してください。 フェデレーション サーバーとドメイン コント ローラーの間の接続については、Kerberos による署名と暗号化を有効にすることを検討してください。 LDAP の場合、AD LDS @ no__t-1 AD DS では LDAP @ no__t はサポートされていません。  
  
## <a name="how-to-create-a-federation-server"></a>フェデレーション サーバーの作成方法  
フェデレーションサーバーを作成するには、AD FS フェデレーションサーバー構成ウィザードまたは Fsconfig .exe コマンド @ no__t-0line ツールを使用します。 これらのツールを使用する場合、フェデレーション サーバーを作成するために次のいずれかのオプションを選択できます。  
  
-   作成、スタンド\-だけでフェデレーション サーバー  
  
    スタンドアロンフェデレーションサーバーをセットアップする方法の詳細については、「[スタンドアロンフェデレーションサーバーを作成](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)する」を参照してください。  
  
-   フェデレーション サーバー ファーム内に最初のフェデレーション サーバーを作成する  
  
    最初のフェデレーション サーバーを設定またはファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファーム内の最初のフェデレーション サーバーの作成](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)です。  
  
-   フェデレーション サーバー ファームにフェデレーション サーバーを追加する  
  
    ファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファームにフェデレーション サーバーを追加](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)します。  
  
これらの各オプションの作業についての詳細を参照してください。 [、AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)します。  
  
フェデレーションサーバーを展開するために必要なすべての前提条件を設定する方法の詳細については、「@no__t」チェックリストを参照してください。フェデレーションサーバー @ no__t をセットアップしています。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

