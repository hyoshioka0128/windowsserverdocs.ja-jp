---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: フェデレーション サーバー プロキシを作成する状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b41c2194940c85e39e5a3724f747dd12c2544259
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190637"
---
# <a name="when-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシを作成する状況

Active Directory フェデレーション サービスに追加のセキュリティ レイヤーを追加、組織のフェデレーション サーバー プロキシを作成する\(AD FS\)展開します。 組織の境界ネットワーク内のフェデレーション サーバー プロキシを展開するときに検討してください。  
  
-   外部のクライアント コンピューターが、フェデレーション サーバーに直接アクセスするを防止します。 境界ネットワーク内のフェデレーション サーバー プロキシを展開することで効果的に分離、フェデレーション サーバーの代わりに操作を実行するフェデレーション サーバー プロキシ経由で企業ネットワークにログオンしているクライアント コンピューターでのみアクセスできるように外部のクライアント コンピューター。 フェデレーション サーバー プロキシは、トークンの生成に使用される秘密キーにアクセスしません。 詳細については、次を参照してください。 [フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
-   サインインを区別するために便利な手段\-Windows 統合認証を使用して、企業ネットワークからアクセスするユーザーではなく、インターネットからアクセスするユーザーのエクスペリエンス。 フェデレーション サーバー プロキシの資格情報またはホーム領域の詳細はコンピューターから収集インターネット クライアント ログオン、ログアウト、および id プロバイダーの検出を使用して\(homerealmdiscovery.aspx\)フェデレーションに格納されているページサーバー プロキシ。  
  
    これに対し、企業ネットワークが検出、異なるエクスペリエンスから取得したクライアント コンピューターは、フェデレーション サーバーの構成に基づいています。 シームレスなサインインを提供する Windows 統合認証を企業ネットワークのフェデレーション サーバーが構成されている多くの場合、\-企業ネットワーク上のユーザーのエクスペリエンス。  
  
組織でフェデレーション サーバー プロキシが果たす役割は、アカウント パートナー組織内、またはリソース パートナー組織のフェデレーション サーバー プロキシを配置するかどうかによって異なります。 たとえば、フェデレーション サーバー プロキシがアカウント パートナーの境界ネットワークに配置されると、その役割は、ブラウザー クライアントからユーザーの資格情報を収集するは。 セキュリティ トークンの要求をリソースのフェデレーション サーバーとによって提供されるセキュリティ トークンへの応答で組織のセキュリティ トークンを生成するリレー リソース パートナーの境界ネットワークにフェデレーション サーバー プロキシが配置されると、そのアカウント パートナーです。  
  
詳細については、「 [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) 」と「 [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)」を参照してください。  
  
## <a name="how-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの作成方法  
AD FS フェデレーション サーバー プロキシ構成ウィザードまたは Fsconfig.exe コマンドを使用してフェデレーション サーバー プロキシを作成する\-ライン ツール。 これを行う方法については、「 [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)」を参照してください。  
  
フェデレーション サーバー プロキシの展開に必要なすべての前提条件を設定する方法についての概要については、次を参照してください。[チェックリスト。フェデレーション サーバー プロキシを設定する](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
