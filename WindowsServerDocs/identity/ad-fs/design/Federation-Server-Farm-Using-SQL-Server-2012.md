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

この Active Directory フェデレーションサービス (AD FS) \(\) AD FS のトポロジは、ファーム内の各フェデレーションサーバーにデータをレプリケートしないという点で、Windows Internal Database \(WID\) 展開トポロジを使用したフェデレーションサーバーファームとは異なります。 代わりに、ファーム内のすべてのフェデレーションサーバーは、企業ネットワーク内に配置されている Microsoft SQL Server を実行しているサーバーに格納されている共通のデータベースにデータの読み取りと書き込みを行うことができます。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   100を超える信頼関係を持つ大規模な組織は、\(SSO\) フェデレーションアプリケーションまたはサービスへのアクセスに対して、内部ユーザーと外部ユーザーの両方にシングルサイン\-を提供する必要があります。  
  
-   既に SQL Server を使用し、既存のツールと専門知識を活用する組織  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   100を超える \(の信頼関係のサポート\)  
  
-   トークンリプレイ検出のサポートは、セキュリティ機能\) とアーティファクト解決 \(Security Assertion Markup Language \(SAML\) 2.0 プロトコルの一部 \(\)  
  
-   データベースミラーリング、フェールオーバークラスタリング、レポート、管理ツールなどの SQL Server の利点のすべてのサポート  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   このトポロジでは、データベースの冗長性は既定では提供されません。 WID トポロジを持つフェデレーションサーバーファームは、ファーム内の各フェデレーションサーバーで WID データベースを自動的にレプリケートしますが、SQL Server トポロジを持つフェデレーションサーバーファームには、データベースのコピーが1つだけ含まれます。  
  
> [!NOTE]  
> SQL Server は、フェールオーバークラスタリング、データベースミラーリング、およびさまざまな種類の SQL Server レプリケーションなど、さまざまなデータおよびアプリケーション冗長オプションをサポートしています。  
  
IT\) 部門の \(Microsoft の情報技術では、SQL Server データベースミラーリングを高\-安全性で使用し、同期 \(モードとフェールオーバークラスタリングを使用して\) インスタンスの高\-可用性をサポートしています。 トランザクション \(ピア\-を\-ピア\) に SQL Server、マージレプリケーションは、Microsoft の AD FS 製品チームによってテストされていません。 SQL Server の詳細については、「[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)」または[適切な種類のレプリケーションの選択](https://go.microsoft.com/fwlink/?LinkId=214648)に関するトピックを参照してください。  
  
### <a name="supported-sql-server-versions"></a>サポートされている SQL Server バージョン  
Windows Server 2012 と共にインストールされた AD FS では、次のバージョンの SQL server がサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
WID トポロジを持つフェデレーションサーバーファームと同様に、ファーム内のすべてのフェデレーションサーバーは、1つのクラスタードメインネームシステム \(DNS\) 名 \(を使用するように構成されています。これは、フェデレーションサービス名\) と、NLB \(クラスター構成\) ネットワーク負荷分散の一部として1つのクラスター IP アドレスを使用します。 これにより、NLB ホストは個々のフェデレーションサーバーにクライアント要求を割り当てることができます。 フェデレーションサーバープロキシは、フェデレーションサーバーファームにクライアント要求をプロキシするために使用できます。  
  
次の図は、架空の Contoso 薬品企業が企業ネットワークに SQL Server トポロジを使用してフェデレーションサーバーファームを展開した方法を示しています。 また、企業が DNS サーバーへのアクセスを使用して境界ネットワークを構成した方法、企業ネットワーク NLB クラスターで使用されている同じクラスター DNS 名 \(fs.contoso.com\) を使用する追加の NLB ホスト、および2つのフェデレーションサーバープロキシ \(fsp1 と fsp2\)を使用していることも示します。  
  
![SQL を使用したサーバーファーム](media/FarmSQLProxies.gif)  
  
フェデレーションサーバーまたはフェデレーションサーバープロキシで使用するネットワーク環境を構成する方法の詳細については、「フェデレーションサーバー[の名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」または「[フェデレーションサーバープロキシの名前解決の要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
