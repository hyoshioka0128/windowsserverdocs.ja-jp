---
ms.assetid: f775cbda-a75d-439d-9aa7-82f3bc8dc932
title: WID を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b0a84940018a0e71aaa1b47c7af3aba5966fe0ae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408052"
---
# <a name="federation-server-farm-using-wid"></a>WID を使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t の既定のトポロジは、Windows Internal Database \(WID @ no__t を使用したフェデレーションサーバーファームです。 このトポロジでは、AD FS は、そのファームに参加しているすべてのフェデレーションサーバーの AD FS 構成データベースのストアとして WID を使用します。 ファームでは、構成データベースのフェデレーション サービス データがファーム内の各サーバー間で複製されて管理されます。 Windows Server 2012 R2 の AD FS では、100またはそれよりも小さい証明書利用者信頼を持つ組織は、最大30台のサーバーで WID を使用してフェデレーションサーバーファームを構成できます。  
  
ファームに最初のフェデレーション サーバーが作成されると、新しいフェデレーション サービスも作成されます。 AD FS 構成データベースに WID を使用する場合、ファームで作成する最初のフェデレーションサーバーは*プライマリフェデレーションサーバー*と呼ばれます。 つまり、このコンピューターは AD FS 構成データベースの読み取り\//書き込みコピーを使用して構成されます。  
  
このファーム用に構成した他のすべてのフェデレーションサーバーは AD FS、プライマリフェデレーションサーバーで行われたすべての変更をの読み取り\-専用コピーにレプリケートする必要があるため、*セカンダリフェデレーション*サーバーと呼ばれます。ローカルに格納する構成データベース。  
  
> [!IMPORTANT]  
> 負荷\-分散構成では、少なくとも2つのフェデレーションサーバーを使用することをお勧めします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100以下の信頼関係がある組織。シングルサイン\(\-オン\) \(を使用して企業ネットワークに物理的に接続されているコンピューターにログオンしている社内ユーザーを提供する必要があります。フェデレーション\)アプリケーションまたはサービスへの SSO アクセス  
  
-   社内ユーザーに Microsoft Online Services または Microsoft Office 365 への SSO アクセスを提供する必要がある組織  
  
-   冗長でスケーラブルなサービスを必要とする小規模の組織  
  
> [!NOTE]  
> 大規模なデータベースを使用する組織では、SQL Server 展開トポロジ[を使用したフェデレーションサーバーファーム](Federation-Server-Farm-Using-SQL-Server.md)の使用を検討する必要があります。 ネットワークの外部からログインするユーザーを持つ組織は、 [SQL Server トポロジを使用し](Federation-Server-Farm-Using-SQL-Server.md)て、 [WID とプロキシトポロジを使用するフェデレーションサーバーファーム](Federation-Server-Farm-Using-WID-and-Proxies.md)またはフェデレーションサーバーファームを使用することを検討する必要があります。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   内部ユーザーへの SSO アクセスを提供します。  
  
-   データとフェデレーションサービスの\(冗長性各フェデレーションサーバーは、同じファーム内の他のフェデレーションサーバーに変更をレプリケートします。\)  
  
-   WID は Windows に含まれています。そのため、SQL Server を購入する必要はありません  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   100を超える証明書利用者信頼がある場合、WID ファームには、最大30個のフェデレーションサーバーがあります。  
  
-   WID \(ファームは、Security Assertion Markup Language \(SAML\)プロトコル\)のトークンリプレイ検出またはアーティファクト解決部分をサポートしていません。  
  
WID ファームを使用する場合の概要を次の表に示します。  実装を計画するときに使用します。  
  
|| 1 \- 100 RP 信頼 | 100を超える RP 信頼 |
| --- | --- | --- |
|1 \-個の AD FS ノード|WID がサポートされる|WID を使用する場合はサポートされません-SQL が必要 
|30を超える AD FS ノード|WID を使用する場合はサポートされません-SQL が必要|WID を使用する場合はサポートされません-SQL が必要  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
ネットワークにこのトポロジを展開する準備ができたら、企業ネットワーク内のすべてのフェデレーションサーバーを、nlb クラスター用に構成できるネットワーク負荷分散\(nlb\)ホストの背後に配置するように計画する必要があります。専用のクラスタードメインネームシステム\(の DNS\)名とクラスター IP アドレスを使用します。  
  
> [!NOTE]  
> このクラスター DNS 名はフェデレーションサービス名と一致する必要があります (たとえば、fs.fabrikam.com)。  
  
NLB ホストは、この NLB クラスターで定義されている設定を使用して、クライアントの要求を個々のフェデレーションサーバーに割り当てることができます。 次の図は、架空の Fabrikam, inc. の企業が、2台\-のコンピューターのフェデレーションサーバーファーム\(fs1 と fs2\)を使用してデプロイの最初のフェーズを設定し、DNS サーバーの配置を設定する方法を示しています。また、企業ネットワークに接続されている単一の NLB ホストがあります。  
  
![WID を使用するサーバーファーム](media/FarmWID.gif)  
  
> [!NOTE]  
> この単一の NLB ホストで障害が発生した場合、ユーザーはフェデレーションアプリケーションまたはサービスにアクセスできなくなります。 ビジネス要件でこのような単一障害点を容認できない場合は、別の NLB ホストを追加します。  
  
フェデレーションサーバーで使用するネットワーク環境を構成する方法の詳細については、「 [AD FS の要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照してください。  
  
## <a name="see-also"></a>関連項目  
[AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

