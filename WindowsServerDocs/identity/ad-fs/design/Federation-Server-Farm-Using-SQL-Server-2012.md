---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: SQL Server を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 66c8bae2fbccca2bf618e46ffd3ccc05cb52f911
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191499"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用するフェデレーション サーバー ファーム

Active Directory フェデレーション サービスのこのトポロジ\(AD FS\) Windows Internal Database を使用してフェデレーション サーバー ファームとは異なります\(WID\)展開トポロジでデータを複製されません。ファームの各フェデレーション サーバー。 代わりに、ファーム内のすべてのフェデレーション サーバーは、読み取りし、は、企業ネットワークにある Microsoft SQL Server を実行しているサーバーに格納されている一般的なデータベースにデータを書き込みます。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの配置トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   1 つの記号の内部ユーザーと外部ユーザーの両方を指定する必要が 100 以上の信頼関係を持つ大規模な組織\-で\(SSO\)フェデレーション アプリケーションまたはサービスへのアクセス  
  
-   組織が既に SQL Server を使用して、およびその既存のツールと専門知識を活用します。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   信頼関係の数が大きくサポート\(100 を超える\)  
  
-   トークン リプレイ検出のサポート\(セキュリティ機能\)とアーティファクト解決\(、Security Assertion Markup Language の一部\(SAML\) 2.0 プロトコル\)  
  
-   データベース ミラーリング、フェールオーバー クラスタ リング、レポート、および管理ツールなど、SQL Server のすべてのメリットのサポート  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   このトポロジでは、既定ではデータベースの冗長性は提供されません。 SQL Server のトポロジを使用したフェデレーション サーバー ファームには、データベースのコピー 1 つだけにはが含まれていますが、WID トポロジを使用したフェデレーション サーバー ファームでは、ファーム内の各フェデレーション サーバー上の WID データベースが自動的にレプリケートします、  
  
> [!NOTE]  
> SQL Server には、多くのさまざまなデータやフェールオーバー クラスタ リング、データベース ミラーリングは、さまざまな種類の SQL Server レプリケーションなど、アプリケーションの冗長性オプションがサポートしています。  
  
Microsoft の Information Technology \(IT\)部門が高で SQL Server データベースのミラーリングを使用して\-安全\(同期\)モードとフェールオーバー クラスターを高\-SQL Server インスタンスの可用性のサポート。 SQL Server トランザクション\(ピア\-に\-ピア\)とマージ レプリケーションは Microsoft の AD FS 製品チームがテストされていません。 SQL Server の詳細については、次を参照してください。[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)または[適切なレプリケーションの種類を選択すると](https://go.microsoft.com/fwlink/?LinkId=214648)します。  
  
### <a name="supported-sql-server-versions"></a>サポートされている SQL Server のバージョン  
Windows Server 2012 と共にインストールされる AD FS では、次の SQL server のバージョンがサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
WID トポロジを使用したフェデレーション サーバー ファームと同様に、すべてのファームにフェデレーション サーバーが構成されて 1 つのクラスターのドメイン ネーム システムを使用して\(DNS\)名前\(フェデレーションサービス名を表す\)とネットワーク負荷分散の一部として 1 つのクラスター IP アドレス\(NLB\)クラスターの構成。 これにより、個々 のフェデレーション サーバーにクライアント要求の割り当ての NLB ホストできます。 クライアント要求のプロキシ、フェデレーション サーバー ファームにフェデレーション サーバー プロキシを使用できます。  
  
次の図は、架空の Contoso Pharmaceuticals 会社が企業ネットワーク内の SQL Server トポロジでそのフェデレーション サーバー ファームを展開する方法を示します。 その会社が DNS サーバー、同じクラスター DNS 名を使用する追加の NLB ホストにアクセスできる境界ネットワークを構成する方法も示します\(fs.contoso.com\)企業ネットワークの NLB クラスターで 2 つを使用して使用します。フェデレーション サーバー プロキシ\(fsp1 および fsp2\)します。  
  
![SQL を使用してサーバー ファーム](media/FarmSQLProxies.gif)  
  
フェデレーション サーバーまたはフェデレーション サーバー プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、のいずれかの操作を参照して[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)または[名フェデレーション サーバー プロキシの解決の要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
