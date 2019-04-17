---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: "フェデレーション サーバーを配置する場所"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 376cec7f3a4fb1f988ac5d458b05220c7b9de970
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="where-to-place-a-federation-server"></a>フェデレーション サーバーを配置する場所

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

セキュリティのベスト プラクティス、ファイアウォールの前に、Active Directory フェデレーション サービス \(AD FS\) フェデレーション サーバーを配置およびをインターネットからの不正アクセスを防ぐために、企業ネットワークに接続します。 これは、機能は、フェデレーション サーバーがあるフル承認をセキュリティ トークンを付与するために重要です。 そのため、ドメイン コントローラーと同様に保護があります。 フェデレーション サーバーが侵害された場合、悪意のあるユーザーは、すべての Web アプリケーションをすべてのリソース パートナー組織内の Active Directory フェデレーション サービス \(AD FS\) で保護されているフェデレーション サーバーを完全なアクセス トークンを発行する権限を持ちます。  
  
> [!NOTE]  
> セキュリティ ベスト プラクティスとして、インターネット上で、フェデレーション サーバーを直接アクセスを必要があります。 テスト ラボ環境をまたは、組織が境界ネットワークにないときに設定している場合にのみ、フェデレーション サーバーにインターネットに直接アクセスを与えることを検討してください。  
  
典型的な企業ネットワークでは、企業ネットワークと、境界ネットワークの間、intranet\ 接続されたファイアウォールが確立されているしとは限らない接続されたファイアウォールを境界ネットワークとインターネットの間に設けます。 このような状況では、フェデレーション サーバーは、企業ネットワーク内に配置しはインターネット クライアントから直接アクセスします。  
  
> [!NOTE]  
> 企業ネットワークに接続されているクライアント コンピューターは、Windows 統合認証を通じて、フェデレーション サーバーと直接通信できます。  
  
フェデレーション サーバー プロキシは、AD FS と共に使用するためのファイアウォール サーバーを構成する前に、境界ネットワークに配置する必要があります。 詳細については、次を参照してください。[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>フェデレーション サーバーのファイアウォール サーバーの構成  
フェデレーション サーバーは、フェデレーション サーバー プロキシと直接通信できる、ように、フェデレーション サーバーにフェデレーション サーバー プロキシから Secure Hypertext Transfer Protocol \(HTTPS\) トラフィックを許可するイントラネット ファイアウォール サーバーを構成する必要があります。 これは、イントラネット ファイアウォール サーバーは、境界ネットワーク内のフェデレーション サーバー プロキシには、フェデレーション サーバーがアクセスできるように、ポート 443 を使用してフェデレーション サーバーを公開する必要があるためにの要件です。  
  
さらに、Internet Security and Acceleration を実行するサーバーなどのサーバーのファイアウォール intranet\ に接続している \(ISA\) サーバー、サーバー公開と呼ばれるプロセスを使用して適切な企業のフェデレーション サーバーをインターネット クライアント要求を分散します。 つまり、クラスター化されたフェデレーション サーバーの URL、たとえば、http:///\/fs.fabrikam.com を公開する ISA Server を実行しているイントラネット サーバーでサーバーの公開規則を手動で作成する必要があります。  
  
境界ネットワーク内のサーバー公開を構成する方法の詳細については、次を参照してください。[フェデレーション サーバー プロキシを配置する場所](Where-to-Place-a-Federation-Server-Proxy.md)します。 サーバーを公開する ISA Server を構成する方法については、次を参照してください。[セキュリティで保護された Web 公開規則を作成する](https://go.microsoft.com/fwlink/?LinkId=75182)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
