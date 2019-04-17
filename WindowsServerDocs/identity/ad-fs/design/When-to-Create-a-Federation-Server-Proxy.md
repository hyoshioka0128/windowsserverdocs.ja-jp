---
ms.assetid: aa20c8b3-7f01-4165-8b73-92642bff9676
title: "フェデレーション サーバー プロキシを作成する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1f0253dfb5a690371dae1a2bfcb6b7520077d473
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="when-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシを作成する場合

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

組織内のフェデレーション サーバー プロキシを作成すると、Active Directory フェデレーション サービス \(AD FS\) 展開に追加のセキュリティ層が追加されます。 組織の境界ネットワーク内のフェデレーション サーバー プロキシを展開するときに検討してください。  
  
-   外部のクライアント コンピューターが、フェデレーション サーバーに直接アクセスするを防止します。 境界ネットワーク内のフェデレーション サーバー プロキシを展開するには、効果的に分離する、フェデレーション サーバー、フェデレーション サーバー プロキシは、外部のクライアント コンピューターの代わりとして経由で企業ネットワークにログインしているクライアント コンピューターでのみアクセスできるようにします。 フェデレーション サーバー プロキシには、トークンの生成に使用される秘密キーへのアクセスはありません。 詳細については、次を参照してください。[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
-   Windows 統合認証を使用して、企業ネットワークからアクセスするユーザーではなく、インターネットからアクセスするユーザーのサインイン エクスペリエンスを区別するための便利な方法を提供します。 フェデレーション サーバー プロキシは資格情報またはホーム領域の詳細をログオン、ログアウト ページ、およびフェデレーション サーバー プロキシに保存されているの ID プロバイダー探索 \(homerealmdiscovery.aspx\) ページを使用してインターネット クライアント コンピューターから収集します。  
  
    これに対し、企業ネットワークが遭遇した、異なるエクスペリエンスから付属しているクライアント コンピューターは、フェデレーション サーバーの構成に基づいています。 企業ネットワークのフェデレーション サーバーは多くの場合 Windows 統合認証のため、企業ネットワーク上のユーザーのシームレスなサインイン エクスペリエンスを提供するように構成します。  
  
組織内のフェデレーション サーバー プロキシを再生する役割は、アカウント パートナー組織内、またはリソース パートナー組織のフェデレーション サーバー プロキシを配置するかどうかによって異なります。 たとえば、フェデレーション サーバー プロキシが、アカウント パートナーの境界ネットワークに配置されると、その役割は、ブラウザー クライアントからユーザーの資格情報を収集するはします。 フェデレーション サーバー プロキシがリソース パートナーの境界ネットワークに配置されると、リソース フェデレーション サーバーにセキュリティ トークン要求をリレーし、そのアカウント パートナーによって提供されるセキュリティ トークンへの応答で組織のセキュリティ トークンを生成します。  
  
詳細については、次を参照してください[アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認する](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)と[リソース パートナー内のフェデレーション サーバー プロキシの役割を確認する。](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)  
  
## <a name="how-to-create-a-federation-server-proxy"></a>フェデレーション サーバー プロキシを作成する方法  
AD FS フェデレーション サーバー プロキシ構成ウィザードまたは Fsconfig.exe コマンド ライン ツールを使用してフェデレーション サーバー プロキシを作成することができます。 これを行う方法に関する手順については、次を参照してください。[for Federation Server Proxy Role Configure a Computer](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。  
  
フェデレーション サーバー プロキシの展開に必要なすべての前提条件を設定する方法の概要については、次を参照してください。[チェックリスト: 設定をフェデレーション サーバー プロキシの](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
