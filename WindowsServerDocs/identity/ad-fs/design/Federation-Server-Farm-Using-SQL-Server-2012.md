---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: "SQL Server を使用してフェデレーション サーバー ファーム"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a0fff975b9cb278e59686323d2bd72e641597573
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用してフェデレーション サーバー ファーム

>適用対象: Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) このトポロジは、ファーム内の各フェデレーション サーバーにデータをレプリケートしませんが、Windows Internal Database \(WID\) 展開トポロジを使用してフェデレーション サーバー ファームとは異なります。 代わりに、すべてのフェデレーション サーバー ファームの読み書きできるデータを企業ネットワークに配置されている Microsoft SQL Server を実行しているサーバーに格納されている一般的なデータベースにします。  
  
## <a name="deployment-considerations"></a>展開に関する考慮事項  
このセクションでは、対象となるユーザー、利点、およびこの展開トポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用している必要がありますか。  
  
-   単一 sign\ で \(SSO\) アクセス権を持つフェデレーション アプリケーションまたはサービスに内部ユーザーと外部ユーザーの両方を提供する必要は 100 を超えるの信頼関係を持つ大規模な組織  
  
-   組織を既に SQL Server を使用して、既存のツールと専門知識を活用します。  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点は何ですか。  
  
-   多数の信頼関係のサポート \(more than 100\)  
  
-   トークン リプレイ検出のサポート \(a security feature\) アーティファクト解決および \ (Security Assertion Markup Language \(SAML\) 2.0 の一部 protocol\)  
  
-   データベース ミラーリングは、フェールオーバー クラスタ リング、レポート、および管理ツールなど、SQL Server のすべてのメリットのサポート  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項とは何ですか。  
  
-   このトポロジは、既定でデータベース冗長化を提供しません。 SQL Server トポロジとフェデレーション サーバー ファームにはデータベースのコピー 1 つだけにはが含まれていますが、フェデレーション サーバー ファームと WID トポロジは、自動的に、ファーム内の各フェデレーション サーバー上の WID データベースを複製します。  
  
> [!NOTE]  
> SQL Server では、多くのさまざまなデータとフェールオーバー クラスタ リング、データベース ミラーリングは、さまざまな種類の SQL Server レプリケーションなどのアプリケーションの冗長性オプションをサポートします。  
  
Microsoft の情報技術 \(IT\) 部門では、高セーフティ \(synchronous\) モードとフェールオーバー クラスタ リングの SQL Server インスタンスの高可用性をサポートする SQL Server データベース ミラーリングを使用します。 Microsoft での AD FS 製品チームによって SQL Server トランザクション \(peer\-to\-peer\) とマージ レプリケーションがテストされていません。 SQL Server の詳細については、次を参照してください。[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)または[適切なレプリケーションの種類を選択すると](https://go.microsoft.com/fwlink/?LinkId=214648)します。  
  
### <a name="supported-sql-server-versions"></a>サポートされている SQL Server のバージョン  
Windows Server 2012 にインストールされている AD FS では、次の SQL server のバージョンがサポートされています。  
  
-   SQL Server 2008 \/R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
1 つのクラスター ドメイン ネーム システム \(DNS\) 名を使うように構成のすべてのフェデレーション サーバー ファーム内のフェデレーション サーバー ファームと WID トポロジと同様に、\ (フェデレーション サービスの名前 \/を表す) と、ネットワーク負荷分散 \(NLB\) クラスター構成の一部として 1 つのクラスター IP アドレスです。 これにより、クライアントの要求を個々 のフェデレーション サーバーを割り当てる NLB ホストできます。 プロキシのクライアント要求をフェデレーション サーバー ファームにフェデレーション サーバー プロキシを使用できます。  
  
次の図は、架空の Contoso Pharmaceuticals 会社が、企業ネットワーク内の SQL Server トポロジでそのフェデレーション サーバー ファームを展開する方法を示します。 DNS サーバーを同じクラスター DNS 名 \(fs.contoso.com\)、企業ネットワークの NLB クラスタで使用されているを使用して追加の NLB ホストへのアクセスと 2 台のフェデレーション サーバー プロキシに、その会社が境界ネットワークを構成する方法も示します \(fsp1 and fsp2\) します。  
  
![SQL を使用して、サーバー ファーム](media/FarmSQLProxies.gif)  
  
フェデレーション サーバーまたはフェデレーション サーバー プロキシで使用するため、ネットワーク環境を構成する方法の詳細については、いずれかを参照して[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)または[フェデレーション サーバー プロキシの名前解決要件](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
