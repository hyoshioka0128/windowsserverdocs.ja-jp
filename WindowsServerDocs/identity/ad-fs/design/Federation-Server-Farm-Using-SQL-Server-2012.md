---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: SQL Server を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 358199fd37cdbb320bc8f3e3e5b2900d261986f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359154"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS\)のこのトポロジは、データをレプリケートしないという点\(で\) 、Windows Internal Database WID 展開トポロジを使用するフェデレーションサーバーファームとは異なります。ファーム内の各フェデレーションサーバー。 代わりに、ファーム内のすべてのフェデレーションサーバーは、企業ネットワーク内に配置されている Microsoft SQL Server を実行しているサーバーに格納されている共通のデータベースにデータの読み取りと書き込みを行うことができます。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100以上の信頼関係を持つ大規模な組織では、内部ユーザーと外部ユーザーの両方に\-シングル\(サイン\)オン SSO アクセスを提供する必要があります。フェデレーションアプリケーションまたはサービスにアクセスします。  
  
-   既に SQL Server を使用し、既存のツールと専門知識を活用する組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   100を超える信頼関係\(を多数サポート\)  
  
-   \(トークンリプレイ検出のサポート Security Assertion Markup Language \(\) \(SAML\) 2.0 プロトコルのセキュリティ機能とアーティファクト解決の部分\)  
  
-   データベースミラーリング、フェールオーバークラスタリング、レポート、管理ツールなどの SQL Server の利点のすべてのサポート  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   このトポロジでは、データベースの冗長性は既定では提供されません。 WID トポロジを持つフェデレーションサーバーファームは、ファーム内の各フェデレーションサーバーで WID データベースを自動的にレプリケートしますが、SQL Server トポロジを持つフェデレーションサーバーファームには、データベースのコピーが1つだけ含まれます。  
  
> [!NOTE]  
> SQL Server は、フェールオーバークラスタリング、データベースミラーリング、およびさまざまな種類の SQL Server レプリケーションなど、さまざまなデータおよびアプリケーション冗長オプションをサポートしています。  
  
Microsoft \(の it 部門は\) 、安全性の高い\-同期\)モードとフェール\(オーバークラスタリングを使用して高い\-安全性を実現するために、SQL Server データベースミラーリングを使用しています。SQL Server インスタンスの可用性サポート。 SQL Server の\(トランザクション\-ピアツー\)ピアとマージレプリケーションは、Microsoft の AD FS 製品チームによってテストされていません。\- SQL Server の詳細については、「[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)」または[適切な種類のレプリケーションの選択](https://go.microsoft.com/fwlink/?LinkId=214648)に関するトピックを参照してください。  
  
### <a name="supported-sql-server-versions"></a>サポートされている SQL Server バージョン  
Windows Server 2012 と共にインストールされた AD FS では、次のバージョンの SQL server がサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
WID トポロジを持つフェデレーションサーバーファームと同様に、ファーム内のすべてのフェデレーションサーバーは、フェデレーションサービス名\(\) \(\)を表す1つのクラスタードメインネームシステムDNS名を使用するように構成されます。ネットワーク負荷分散\(NLB\)クラスター構成の一部として1つのクラスター IP アドレスを設定します。 これにより、NLB ホストは個々のフェデレーションサーバーにクライアント要求を割り当てることができます。 フェデレーションサーバープロキシは、フェデレーションサーバーファームにクライアント要求をプロキシするために使用できます。  
  
次の図は、架空の Contoso 薬品企業が企業ネットワークに SQL Server トポロジを使用してフェデレーションサーバーファームを展開した方法を示しています。 また、企業が DNS サーバーへのアクセスを使用して境界ネットワークを構成した方法や、同じクラスター DNS @no__t 名を使用する追加の NLB ホスト (企業ネットワーク NLB クラスターで使用されている contoso. com @ no__t) と、2台のフェデレーションサーバーがあることを示しています。プロキシ \(fsp1 と fsp2 @ no__t-3。  
  
![SQL を使用したサーバーファーム](media/FarmSQLProxies.gif)  
  
フェデレーションサーバーまたはフェデレーションサーバープロキシで使用するためのネットワーク環境を構成する方法の詳細については、「フェデレーション[サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」または「[フェデレーションの名前解決の要件」を参照してください。サーバープロキシ](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
