---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: "フェデレーション サーバーを作成する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8013764b88a1061cfcaa3a507466c111bfd59aad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server"></a>フェデレーション サーバーを作成する場合

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フェデレーションした serverin の Active Directory フェデレーション サービス \(AD FS\) を作成するときに、これによって、組織ことができます手段を提供します。  
  
-   Web シングル-sign\-上に協力して \ (SSO\) – ベースで別の組織との通信 \ (もある少なくとも 1 つのフェデレーション サーバー \) と、必要に応じて、自分の組織内の従業員と \ (した必要なアクセスとは限らない経由で)。  
  
-   Id 委任を使用して、インフラストラクチャ サービスにユーザーを偽装するフロント エンド サービスを有効にします。 詳細については、次を参照してください。[When to Use Identity Delegation](When-to-Use-Identity-Delegation.md)します。  
  
次のセクションでは、1 つまたは複数のフェデレーション サーバーを作成するタイミングと場所を判断するための重要な決定事項について説明します。  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>組織のフェデレーション サーバーの役割を決定します。  
新しいフェデレーション サーバーを作成するタイミングに関する情報に基づいて判断するためは、まず、サーバーが存在する組織を決定する必要があります。 フェデレーション サーバーは、組織で果たす役割は、アカウント パートナー組織内、またはリソース パートナー組織のフェデレーション サーバーを配置するかどうかによって異なります。  
  
アカウント パートナーの企業ネットワークにフェデレーション サーバーが配置されると、その役割は、ブラウザー、Web サービス、または ID セレクター クライアントのユーザーの資格情報を認証し、セキュリティ トークンをクライアントに送信するのには。 詳細については、次を参照してください。[アカウント パートナーのフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)します。  
  
リソース パートナーの企業ネットワークにフェデレーション サーバーが配置されると、その役割は、リソース パートナー組織内のフェデレーション サーバーによって発行されるセキュリティ トークンに基づいて、ユーザーの認証には、その役割は、クライアントが属するアカウント パートナー組織に構成されている Web アプリケーションや Web サービスからのトークン要求をリダイレクトするのには 詳細については、次を参照してください。[リソース パートナーのフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>展開する AD FS 設計を決定します。  
次の AD FS 設計のいずれかを展開するときに、組織内のフェデレーション サーバーを作成します。  
  
-   [Web SSO 設計](Web-SSO-Design.md)  
  
-   [フェデレーション Web SSO 設計](Federated-Web-SSO-Design.md)  
  
必要に応じて、フェデレーション Web SSO 設計を展開する組織は、アカウント パートナー ロールとリソース パートナーの役割で動作できるように、1 つのフェデレーション サーバーを構成できます。 この場合は、フェデレーション サーバーは自身の組織でのユーザー アカウントに基づいて、Security Assertion Markup Language \(SAML\) トークンを生成可能性があります。またはユーザーのアカウントの存在に基づいて、組織に再ルーティング トークンを要求します。  
  
> [!NOTE]  
> フェデレーション Web SSO 設計で、アカウント パートナー内の少なくとも 1 つのフェデレーション サーバーと、リソース パートナーに少なくとも 1 つのフェデレーション サーバーに必要があります。  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>フェデレーション サーバーとフェデレーション サーバー プロキシの違い  
フェデレーション サーバーは、フェデレーション サーバー プロキシを実行するのと同じ方法でサインイン、ポリシー、認証、および検出用 Web ページを使用できます。 フェデレーション サーバーとフェデレーション サーバー プロキシの主な違いが、どのような操作をフェデレーション サーバーがフェデレーション サーバー プロキシを実行できないことを実行することができます。  
  
フェデレーション サーバーのみを実行できる操作を次に示します。  
  
-   フェデレーション サーバーは、トークンを生成する暗号操作を実行します。 ただし、フェデレーション サーバー プロキシは、トークンを生成できないは、ルーティングまたはクライアントや、フェデレーション サーバーに、必要な場合に、トークンのリダイレクトを使用できます。 詳細については、フェデレーション サーバーを使用して、次を参照してください。[When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md)します。  
  
-   フェデレーション サーバーが企業ネットワーク上のクライアントに対して Windows 統合認証の使用をサポートします。フェデレーション サーバー プロキシは必要ありません。 詳細については、フェデレーション サーバーとの統合 Windows 認証を使用して、次を参照してください。[When to Create a Federation Server Farm](When-to-Create-a-Federation-Server-Farm.md)します。  
  
> [!CAUTION]  
> フェデレーション サーバーと SQL Server 構成データベース、SQL Server 属性ストア、ドメイン コントローラー、および AD LDS インスタンスの間の通信は、整合性や機密性が既定では保護できません。 この問題を軽減するには、IPSEC を使用して、またはこれらのサーバーのすべての間で物理的にセキュリティで保護された接続を使用してこれらのサーバー間の通信チャネルを保護する検討してください。 フェデレーション サーバーと SQL server 間の通信、接続文字列に SSL 保護の使用を検討してください。 フェデレーション サーバーとドメイン コントローラー間の接続、Kerberos による署名と暗号化をオンにするを検討してください。 Ldap、LDAP\/秒に用 AD LDS\/AD DS はサポートされません。  
  
## <a name="how-to-create-a-federation-server"></a>フェデレーション サーバーを作成する方法  
AD FS フェデレーション サーバー構成ウィザードまたは Fsconfig.exe コマンド ライン ツールを使用してフェデレーション サーバーを作成することができます。 これらのツールのいずれかを使用する場合は、フェデレーション サーバーを作成するには、次のオプションのいずれかを選択できます。  
  
-   スタンドアロンのフェデレーション サーバーを作成します。  
  
    スタンドアロンのフェデレーション サーバーを設定する方法の詳細については、次を参照してください。[スタンドアロン フェデレーション サーバーを作成](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)します。  
  
-   フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します。  
  
    最初のフェデレーション サーバーを設定またはファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成する](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)します。  
  
-   フェデレーション サーバー ファームにフェデレーション サーバーを追加します。  
  
    ファームにフェデレーション サーバーを追加する方法の詳細については、次を参照してください。[フェデレーション サーバー ファームにフェデレーション サーバーを追加](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md)します。  
  
作業をどのようにこれらの各オプションに関する情報の詳細を参照してください。[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)します。  
  
フェデレーション サーバーを展開するために必要なすべての前提条件を設定する方法の詳細については、次を参照してください。[チェックリスト: フェデレーション サーバーの設定](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

