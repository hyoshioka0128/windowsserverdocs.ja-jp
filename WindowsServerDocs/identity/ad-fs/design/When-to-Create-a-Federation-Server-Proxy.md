---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: フェデレーション サーバー プロキシを作成する状況
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 963070a15b075275cd5680fa3a39044abbb6b3ad
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972039"
---
# <a name="when-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシを作成する状況

組織でフェデレーションサーバープロキシを作成すると、Active Directory フェデレーションサービス (AD FS) AD FS の展開にセキュリティ層が追加さ \( \) れます。 次のような場合に、組織の境界ネットワークにフェデレーションサーバープロキシを展開することを検討してください。

-   外部クライアントコンピューターがフェデレーションサーバーに直接アクセスできないようにします。 境界ネットワークにフェデレーションサーバープロキシを展開することで、フェデレーションサーバーを効果的に分離して、外部クライアントコンピューターの代理として機能するフェデレーションサーバープロキシ経由で企業ネットワークにログインしているクライアントコンピューターからのみアクセスできるようにします。 フェデレーション サーバー プロキシは、トークンの生成に使用される秘密キーにアクセスしません。 詳細については、「[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)」を参照してください。

-   \-Windows 統合認証を使用して企業ネットワークからアクセスするユーザーではなく、インターネットからアクセスするユーザーのサインインエクスペリエンスを区別する便利な方法を提供します。 フェデレーションサーバープロキシは、 \( \) フェデレーションサーバープロキシに格納されているログオン、ログアウト、および id プロバイダーの検出ページを使用して、インターネットクライアントコンピューターから資格情報またはホーム領域の詳細を収集します。

    これに対して、企業ネットワークからのクライアントコンピューターでは、フェデレーションサーバーの構成に基づいて異なるエクスペリエンスが発生します。 企業ネットワークのフェデレーションサーバーは、多くの場合、企業ネットワーク上のユーザーにシームレスなサインインエクスペリエンスを提供する Windows 統合認証用に構成されてい \- ます。

フェデレーションサーバープロキシが組織内で果たす役割は、フェデレーションサーバープロキシをアカウントパートナー組織に配置するか、リソースパートナー組織に配置するかによって異なります。 たとえば、アカウントパートナーの境界ネットワークにフェデレーションサーバープロキシを配置する場合、その役割は、ブラウザークライアントからユーザー資格情報を収集することです。 フェデレーションサーバープロキシは、リソースパートナーの境界ネットワークに配置されると、セキュリティトークン要求をリソースフェデレーションサーバーにリレーし、そのアカウントパートナーによって提供されるセキュリティトークンに応答して組織のセキュリティトークンを生成します。

詳細については、「 [Review the Role of the Federation Server Proxy in the Account Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md) 」と「 [Review the Role of the Federation Server Proxy in the Resource Partner](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)」を参照してください。

## <a name="how-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの作成方法
フェデレーションサーバープロキシを作成するには、AD FS フェデレーションサーバープロキシ構成ウィザードまたは Fsconfig.exe コマンドラインツールを使用し \- ます。 これを行う方法については、「 [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)」を参照してください。

フェデレーション サーバー プロキシの展開に必要なすべての前提条件を設定する方法の詳細については、「 [Checklist: Setting Up a Federation Server Proxy](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)」を参照してください。

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
