---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: WID を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bb4e5f88f3d62511b185a2b4317416169717c860
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851403"
---
# <a name="federation-server-farm-using-wid"></a>WID を使用するフェデレーション サーバー ファーム

>適用先:Windows Server 2012

Active Directory フェデレーション サービスの既定のトポロジ\(AD FS\) Windows Internal Database を使用して、フェデレーション サーバー ファームは、 \(WID\)、最大 5 台のフェデレーション サーバーをホストしているので構成される、組織のフェデレーション サービス。 このトポロジでは、AD FS は、WID をファームに参加しているすべてのフェデレーション サーバーの AD FS 構成データベースのストアとして使用します。 ファームでは、構成データベースのフェデレーション サービス データがファーム内の各サーバー間で複製されて管理されます。  
  
ファームに最初のフェデレーション サーバーが作成されると、新しいフェデレーション サービスも作成されます。 AD FS 構成データベースの WID を使用すると、ファーム内に作成する最初のフェデレーション サーバーと呼びます、*プライマリ フェデレーション サーバー*します。 つまり、読み取りと、このコンピューターが構成されている\/AD FS 構成データベースのコピーを作成します。  
  
このファームを構成するその他のすべてのフェデレーション サーバーと呼びます*セカンダリ フェデレーション サーバー* 、読み取り専用にプライマリ フェデレーション サーバーに対して行われた変更をレプリケートする必要がありますので\-のみローカルに保存された AD FS 構成データベースのコピー。  
  
> [!NOTE]  
> 負荷の少なくとも 2 つのフェデレーション サーバーの使用はお勧め\-バランスの取れた構成です。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの配置トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   組織が内部ユーザーを指定する必要がある 100 以下の構成済みの信頼関係を持つ\(企業ネットワークに物理的に接続されているコンピューターにログオン\)1 つの記号\-で\(SSO\)フェデレーション アプリケーションまたはサービスへのアクセス  
  
-   Microsoft Online Services や Microsoft Office 365 に SSO アクセス権を持つ内部ユーザーを提供する必要があります。  
  
-   重複した、スケーラブルなサービスを必要とする小規模な組織  
  
> [!NOTE]  
> 大きなデータベースを持つ組織は、使用を検討する必要があります、[フェデレーション サーバー ファームを使用して SQL Server](Federation-Server-Farm-Using-SQL-Server.md)展開トポロジは、このセクションでは、後述します。 ネットワークの外からログインするユーザーと組織では、いずれかを使用して検討してください、[フェデレーション サーバー ファームを使用して WID とプロキシ](Federation-Server-Farm-Using-WID-and-Proxies.md)トポロジまたは[フェデレーション サーバー ファームを使用して SQL Server](Federation-Server-Farm-Using-SQL-Server.md)トポロジ。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   内部ユーザーに SSO アクセスを提供します。  
  
-   データとのフェデレーション サービスの冗長性\(の各フェデレーション サーバーの変更を同じファーム内の他のフェデレーション サーバーにレプリケートします\)  
  
-   ファームを最大 5 つのフェデレーション サーバーを追加してスケール アウトをできます。  
  
-   WID では Windows; に含まれていますSQL Server を購入する必要はそのため、ありません。  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   WID ファームでは、5 つのフェデレーション サーバーの制限があります。 詳細については、次を参照してください。 [AD FS 展開トポロジに関する考慮事項](AD-FS-Deployment-Topology-Considerations.md)します。  
  
-   WID ファームは、トークン再生検出または成果物の解決をサポートしていません\(、Security Assertion Markup Language の一部\(SAML\)プロトコル\)します。  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
ネットワーク負荷分散の背後にある、企業ネットワーク内のすべてのフェデレーション サーバーを配置するように計画する必要があります、ネットワーク内には、このトポロジのデプロイを開始する準備ができたら、 \(NLB\) NLB クラスタの構成可能なホストドメイン ネーム システム専用クラスターを使用\(DNS\)名とクラスターの IP アドレス。  
  
> [!NOTE]  
> このクラスター DNS 名は fs.fabrikam.com など、フェデレーション サービス名と一致する必要があります。  
  
NLB ホストには、個々 のフェデレーション サーバーにクライアント要求を割り当てるには、この NLB クラスターで定義されている設定を使用できます。 次の図は、Fabrikam, Inc. の架空の会社が、2 つを使用して、展開の最初のフェーズを設定する方法を示します\-コンピューター フェデレーション サーバー ファーム\(fs1 および fs2\) WID と DNS サーバーの配置企業ネットワークにワイヤード (有線) は、1 台の NLB ホストを選択します。  
  
![WID を使用して、サーバー ファーム](media/FarmWID.gif)  
  
> [!NOTE]  
> この 1 つの NLB ホストに障害がある場合は、ユーザーはフェデレーション アプリケーションまたはサービスにアクセスできません。 ビジネス要件でこのような単一障害点を容認できない場合は、別の NLB ホストを追加します。  
  
フェデレーション サーバーを使用するため、ネットワーク環境を構成する方法の詳細については、次を参照してください。[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)で、AD FS 設計ガイド。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
