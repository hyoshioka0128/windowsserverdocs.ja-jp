---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: "SQL Server を使用してフェデレーション サーバー ファーム"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2333f79c733415833b1d54afc8c385700ac5581e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用してフェデレーション サーバー ファーム

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) このトポロジは、ファーム内の各フェデレーション サーバーにデータをレプリケートしませんが、Windows Internal Database \(WID\) 展開トポロジを使用してフェデレーション サーバー ファームとは異なります。 代わりに、すべてのフェデレーション サーバー ファームの読み書きできるデータを企業ネットワークに配置されている Microsoft SQL Server を実行しているサーバーに格納されている一般的なデータベースにします。  
  
> [!IMPORTANT]  
> AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、および SQL Server 2014 を含む、新しいバージョンを使用することができます。  
  
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
Windows Server 2012 R2 の AD FS では、次の SQL server のバージョンがサポートされています。  
  
-   SQL Server 2008 \/R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
1 つのクラスター ドメイン ネーム システム \(DNS\) 名を使うように構成のすべてのフェデレーション サーバー ファーム内のフェデレーション サーバー ファームと WID トポロジと同様に、\ (フェデレーション サービスの名前 \/を表す) と、ネットワーク負荷分散 \(NLB\) クラスター構成の一部として 1 つのクラスター IP アドレスです。 これにより、クライアントの要求を個々 のフェデレーション サーバーを割り当てる NLB ホストできます。 プロキシのクライアント要求をフェデレーション サーバー ファームにフェデレーション サーバー プロキシを使用できます。  
  
次の図は、架空の Contoso Pharmaceuticals 会社が、企業ネットワーク内の SQL Server トポロジでそのフェデレーション サーバー ファームを展開する方法を示します。 DNS サーバーを同じクラスター DNS 名 \(fs.contoso.com\)、企業ネットワークの NLB クラスタで使用されているを使用して追加の NLB ホストへのアクセスと 2 つの Web アプリケーション プロキシに、その会社が境界ネットワークを構成する方法も示します \(wap1 and wap2\) します。  
  
![SQL を使用して、サーバー ファーム](media/SQLFarmADFSBlue.gif)  
  
フェデレーション サーバーまたは Web アプリケーション プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、「名前解決の要件」を参照してください。セクション[AD FS の要件](AD-FS-Requirements.md)と[Web アプリケーション プロキシ インフラストラクチャ (WAP) を計画](https://technet.microsoft.com/library/dn383648.aspx)します。  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server ファームの高可用性オプション  
Windows Server 2012 R2 では、SQL Server を使用して AD FS ファームで高可用性をサポートするために 2 つのオプションは AD FS があります。  
  
-   SQL Server AlwaysOn 可用性グループのサポート  
  
-   SQL Server のマージ レプリケーションを使用して高可用性を地理的に分散のサポート  
  
この説明ではこれらの各オプション、どのような問題が解決されるそれぞれおよび展開するオプションを決定するための主な考慮事項です。  
  
> [!NOTE]  
> Windows Internal Database \(WID\) を使用している AD FS ファームでは、セカンダリ ノードで、プライマリ フェデレーション サーバーのノードで読み取り \/書き込みのアクセスと読み取り専用アクセスの基本的なデータの冗長性を提供します。  これは、地理的にローカルまたは地理的に分散トポロジで使用できます。  
>   
> WID を使用する場合は、次の制限事項に注意してください。  
>   
> -   WID ファームは 30 台のフェデレーション サーバーの制限が 100 台以下証明書利用者信頼がある場合。  
> -   WID ファームはトークン リプレイ検出またはアーティファクトの解像度をサポートしていない \ (Security Assertion Markup Language \(SAML\) protocol\ の一部)。  
  
次の表に、WID ファームの概要について説明します。  
  
||||  
|-|-|-|  
||1 \-100 RP 信頼|100 を超える RP 信頼|  
|1 \-30 AD FS ノード|WID のサポート|WID を使用してサポートされていません \-必要な SQL|  
|複数の 30 AD FS ノード|WID を使用してサポートされていません \-必要な SQL|WID を使用してサポートされていません \-必要な SQL|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ  
**概要**  
  
AlwaysOn 可用性グループは、SQL Server 2012 で導入されたし、高可用性 SQL Server インスタンスを作成する新しい方法を指定します。  AlwaysOn 可用性グループは、データベースのミラーリング冗長性と SQL インスタンス レイヤーとデータベース層の両方でフェールオーバー クラスタ リング ボリュームとの要素を結合します。  以前の高可用性オプションとは異なり AlwaysOn 可用性グループを必要としない一般的な記憶域 \ (または記憶域エリア ネットワーク) データベース層でします。  
  
可用性グループがプライマリ レプリカの構成 \ (する読み取り \/書き込みプライマリ databases\ のセット) と 1 ~ 4 可用性レプリカ \ (対応するセカンダリ databases\ のセット)。  可用性グループは、単一の読み取り/書き込みコピーをサポートしている \ (プライマリ replica\) と 1 ~ 4 読み取り専用の可用性レプリカします。  可用性の各レプリカは、1 つの Windows Server フェールオーバー クラスタ リング \(WSFC\) クラスターの別のノード上に存在する必要があります。  詳細については、AlwaysOn 可用性グループを参照してください[AlwaysOn 可用性グループの概要 \(SQL Server\)](https://technet.microsoft.com/library/ff877884.aspx)します。  
  
AlwaysOn 可用性グループは、AD FS の SQL Server ファームの各ノードの観点からポリシーとして 1 つの SQL Server インスタンスを置き換えます \/アーティファクト データベース。  可用性グループ リスナーはどのようなクライアント \ (、AD FS のセキュリティ トークン service \current) を使用して SQL に接続します。  
  
次の図は、AlwaysOn 可用性グループと AD FS SQL Server ファームを示します。  
  
![SQL を使用して、サーバー ファーム](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 可用性グループは、Windows Server フェールオーバー クラスタ リング \(WSFC\) ノードに、SQL Server インスタンスが存在する必要があります。  
  
> [!NOTE]  
> 1 つだけの可用性レプリカは、他の 3 つ、自動フェールオーバー ターゲットは、手動によるフェールオーバーに依存するように機能します。  
  
**キーの展開に関する考慮事項**  
  
SQL Server のマージ レプリケーションとの組み合わせで AlwaysOn 可用性グループを使用する場合は、注意しておいてください"キー展開に関する考慮事項の SQL Server のマージ レプリケーションで AD FS を使用して"」の説明を次の問題。  具体的には、経由でレプリケーション サブスクライバは、データベースを含む AlwaysOn 可用性グループが失敗した場合、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するには、レプリケーション管理者はサブスクライバを手動で再構成する必要があります。  SQL Server で特定の問題の説明を参照して[AlwaysOn 可用性グループのレプリケーションの被発行者と \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx)で、レプリケーション オプション AlwaysOn 可用性グループの全体的なサポートの説明と[レプリケーション、変更の追跡、データのキャプチャの変更、および AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
**AlwaysOn 可用性グループを使用する AD FS を構成します。**  
  
AlwaysOn 可用性グループを使用して、AD FS ファームを構成するには、AD FS の展開の手順を少し変更が必要です。  
  
1.  AlwaysOn 可用性グループを構成する前に、バックアップを作成するデータベースを作成する必要があります。  AD FS では、セットアップと新しい AD FS の SQL Server ファームの最初のフェデレーション サービス ノードの初期構成の一部としてそのデータベースを作成します。  AD FS の構成の一環として、ため、SQL インスタンスに直接接続する最初の AD FS ファーム ノードを構成する必要が、SQL 接続文字列の場合を指定する必要があります \ (これは唯一 temporary\ です)。   SQL server の接続文字列で AD FS ファーム ノードの構成など、AD FS ファームの構成に関する詳しいガイダンスを参照してください。[フェデレーション サーバーを構成する](../../ad-fs/deployment/Configure-a-Federation-Server.md)します。  
  
2.  AD FS データベースが作成されたら、AlwaysOn 可用性グループに割り当てると SQL Server のツールを使用して一般的な TCPIP リスナーを作成および処理[の作成と構成の可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/ff878265.aspx)します。  
  
3.  最後に、PowerShell を使用して、AlwaysOn 可用性グループ リスナーの DNS アドレスを使用する SQL 接続文字列を更新する AD FS のプロパティを編集します。  
  
    AD FS ポリシー データベースの SQL 接続文字列を更新する PSH コマンドの例:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  AD FS ポリシー データベースの SQL 接続文字列を更新する PSH コマンドの例:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server のマージ レプリケーション  
また、SQL Server 2012 で導入された、マージ レプリケーションでは、次の特性を持つ AD FS ポリシー データの冗長性。  
  
-   すべてのノードで機能を読み書き \ (だけでなく primary\)  
  
-   システムの待機時間を防ぐに非同期的にレプリケートされるデータ量  
  
次の図は、マージ レプリケーションの冗長な地理的に AD FS の SQL Server ファーム \ (発行元の 1、2 subscribers\)。  
  
![SQL を使用して、サーバー ファーム](media/ADFSSQLGeoRedundancy3.png)  
  
**キーの SQL Server のマージ レプリケーションで AD FS を使用するための展開に関する考慮事項 \ (図 above\ の数値に注意してください)**  
  
-   AlwaysOn 可用性グループまたはデータベース ミラーリングのどちらで使用するため、ディストリビュータ データベースはサポートされていません。  SQL Server AlwaysOn 可用性グループで、レプリケーション オプションのサポートの説明を参照して[レプリケーション、変更の追跡、データのキャプチャの変更、および AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
-   経由でレプリケーション サブスクライバは、データベースを含む AlwaysOn 可用性グループが失敗した場合、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するには、レプリケーション管理者はサブスクライバを手動で再構成する必要があります。  SQL Server で特定の問題の説明を参照して[AlwaysOn 可用性グループのレプリケーションの被発行者と \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx)レプリケーション オプションを使用して AlwaysOn 可用性グループの全体的なサポートの説明と[レプリケーション、変更の追跡、データのキャプチャの変更、および AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
SQL Server のマージ レプリケーションを使用するより詳細な手順を AD FS を構成する方法については、次を参照してください。[セットアップの地理的な冗長性を SQL Server レプリケーション](https://technet.microsoft.com/en-us/library/dn632406.aspx)します。  
  
## <a name="see-also"></a>参照してください。  
[AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

