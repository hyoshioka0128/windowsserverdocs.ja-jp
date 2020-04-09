---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: SQL Server を使用するフェデレーション サーバー ファーム
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fd82edbcd2403416a08a4d707e5271ab2ced4b22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853125"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用するフェデレーション サーバー ファーム

この Active Directory フェデレーションサービス (AD FS) \(\) AD FS のトポロジは、ファーム内の各フェデレーションサーバーにデータをレプリケートしないという点で、Windows Internal Database \(WID\) 展開トポロジを使用したフェデレーションサーバーファームとは異なります。 代わりに、ファーム内のすべてのフェデレーションサーバーは、企業ネットワーク内に配置されている Microsoft SQL Server を実行しているサーバーに格納されている共通のデータベースにデータの読み取りと書き込みを行うことができます。  
  
> [!IMPORTANT]  
> AD FS ファームを作成し SQL Server を使用して構成データを格納する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012、SQL Server 2014) を使用できます。  
  
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
次のバージョンの SQL server は、Windows Server 2012 R2 の AD FS でサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
WID トポロジを持つフェデレーションサーバーファームと同様に、ファーム内のすべてのフェデレーションサーバーは、1つのクラスタードメインネームシステム \(DNS\) 名 \(を使用するように構成されています。これは、フェデレーションサービス名\) と、NLB \(クラスター構成\) ネットワーク負荷分散の一部として1つのクラスター IP アドレスを使用します。 これにより、NLB ホストは個々のフェデレーションサーバーにクライアント要求を割り当てることができます。 フェデレーションサーバープロキシは、フェデレーションサーバーファームにクライアント要求をプロキシするために使用できます。  
  
次の図は、架空の Contoso 薬品企業が企業ネットワークに SQL Server トポロジを使用してフェデレーションサーバーファームを展開した方法を示しています。 また、企業が DNS サーバーへのアクセスを使用して境界ネットワークを構成した方法、企業ネットワーク NLB クラスターで使用されているのと同じクラスター DNS 名 \(fs.contoso.com\) を使用する追加の NLB ホスト、および2つの web アプリケーションプロキシ \(wap1 と wap2\)を使用していることも示しています。  
  
![SQL を使用したサーバーファーム](media/SQLFarmADFSBlue.gif)  
  
フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照して、 [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画](https://technet.microsoft.com/library/dn383648.aspx)してください。  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server ファームの高可用性オプション  
Windows Server 2012 R2 では、SQL Server を使用して AD FS ファームで高可用性をサポートするための2つの新しいオプションが AD FS ます。  
  
-   SQL Server AlwaysOn 可用性グループのサポート  
  
-   SQL Server マージレプリケーションを使用した地理的に分散した高可用性のサポート  
  
ここでは、これらの各オプションについて、それぞれの問題の解決方法と、展開するオプションを決定するための重要な考慮事項について説明します。  
  
> [!NOTE]  
> Windows Internal Database \(WID\) 使用するファーム AD FS、プライマリフェデレーションサーバーノードで読み取り\/書き込みアクセス権を持つ基本的なデータの冗長性を提供し、セカンダリノードでの読み取り\-アクセスのみを行います。  これは、地理的にローカルまたは地理的に分散したトポロジで使用できます。  
>   
> WID を使用する場合は、次の制限事項に注意してください。  
>   
> -   100を超える証明書利用者信頼がある場合、WID ファームには、最大30個のフェデレーションサーバーがあります。  
> -   WID ファームでは、トークンリプレイ検出またはアーティファクト解決をサポートしていません。 Security Assertion Markup Language \(SAML\) プロトコル\)の一部 \(ます。  
  
WID ファームを使用する場合の概要を次の表に示します。  
  
||||  
|-|-|-|  
||1 \- 100 RP 信頼|100を超える RP 信頼|  
|1 \- 30 AD FS ノード|WID でサポートされる|WID を使用してサポートされていません \- SQL が必要です|  
|30を超える AD FS ノード|WID を使用してサポートされていません \- SQL が必要です|WID を使用してサポートされていません \- SQL が必要です|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ  
**概要**  
  
AlwaysOn 可用性グループは SQL Server 2012 で導入され、高可用性 SQL Server インスタンスを作成するための新しい方法を提供しています。  AlwaysOn 可用性グループは、クラスターとデータベースミラーリングの要素を組み合わせて、SQL インスタンス層とデータベース層の両方で冗長性とフェールオーバーを実現します。  以前の高可用性オプションとは異なり、AlwaysOn 可用性グループは、データベース層で共通の記憶域 \(や記憶域ネットワーク\) を必要としません。  
  
可用性グループは、プライマリデータベース\) の一連の読み取り\-書き込み、1 ~ 4 個の可用性レプリカ \(対応するセカンダリ\)データベースのセット \(、プライマリレプリカから構成されます。  可用性グループは、プライマリレプリカ\)\(読み取り\-書き込みコピーを1つだけサポートし、1 ~ 4 個の読み取り\-可用性レプリカのみを読み取ります。  各可用性レプリカは、1つの Windows Server フェールオーバークラスタリング \(WSFC\) クラスターの別のノードに存在する必要があります。  AlwaysOn 可用性グループの詳細については、「 [AlwaysOn 可用性グループ \(SQL Server\)の概要](https://technet.microsoft.com/library/ff877884.aspx)」を参照してください。  
  
AD FS SQL Server ファームのノードの観点からは、1つの SQL Server インスタンスをポリシー \/ アーティファクトデータベースに置き換える AlwaysOn 可用性グループ。  可用性グループリスナーは、クライアントが SQL に接続するために使用\) Security Token Service AD FS \(します。  
  
次の図は、AlwaysOn 可用性グループを使用したファーム SQL Server AD FS を示しています。  
  
![SQL を使用したサーバーファーム](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 可用性グループでは、SQL Server インスタンスが Windows Server フェールオーバークラスタリング \(WSFC\) ノードに存在する必要があります。  
  
> [!NOTE]  
> 自動フェールオーバーターゲットとして機能できる可用性レプリカは1つだけで、他の3つは手動フェールオーバーに依存します。  
  
**展開に関する主な考慮事項**  
  
AlwaysOn 可用性グループを SQL Server マージレプリケーションと組み合わせて使用する場合は、以下の「SQL Server マージレプリケーションで AD FS を使用するための展開に関する主な考慮事項」で説明されている問題を確認してください。  特に、レプリケーションサブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーションサブスクリプションが失敗します。 レプリケーションを再開するためには、レプリケーション管理者が手動でそのサブスクライバーを再構成する必要があります。  レプリケーション[、\)、変更データキャプチャ、Change Tracking ](https://technet.microsoft.com/library/hh403414.aspx)AlwaysOn 可用性グループ \(SQL Server のレプリケーションオプションを使用して、レプリケーション[サブスクライバーと AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx)および AlwaysOn 可用性グループの全体的なサポートステートメントについては、SQL Server の特定の問題についての説明を参照してください。  
  
**AlwaysOn 可用性グループを使用するように AD FS を構成する**  
  
AlwaysOn 可用性グループを使用して AD FS ファームを構成するには、AD FS の展開手順を少し変更する必要があります。  
  
1.  バックアップするデータベースは、AlwaysOn 可用性グループを構成する前に作成しておく必要があります。  AD FS は、新しい AD FS SQL Server ファームの最初のフェデレーションサービスノードのセットアップと初期構成の一部としてデータベースを作成します。  AD FS 構成の一部として、SQL 接続文字列を指定する必要があります。そのため、最初の AD FS ファームノードが SQL インスタンスに \(直接接続するように構成する必要があります。これは一時的な\)にすぎません。   SQL server 接続文字列を使用した AD FS ファームノードの構成など、AD FS ファームの構成に関する具体的なガイダンスについては、「 [Configure a Federation server](../../ad-fs/deployment/Configure-a-Federation-Server.md)」を参照してください。  
  
2.  AD FS データベースを作成したら、それらのデータベースを AlwaysOn 可用性グループに割り当て、SQL Server ツールとプロセスを使用して、 [SQL Server\)\(可用性グループの作成と構成](https://technet.microsoft.com/library/ff878265.aspx)を行い、共通の TCPIP リスナーを作成します。  
  
3.  最後に、PowerShell を使用して AD FS のプロパティを編集し、AlwaysOn 可用性グループのリスナーの DNS アドレスを使用するように SQL 接続文字列を更新します。  
  
    AD FS 構成データベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring="data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true"  
    PS:\>$temp.put()  
  
    ```  
  
4.  AD FS アーティファクト解決サービスデータベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection "Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True"  
    ```  
  
### <a name="sql-server-merge-replication"></a>マージレプリケーションの SQL Server  
また、SQL Server 2012 で導入されたマージレプリケーションでは、次の特性を持つ AD FS ポリシーデータの冗長性を実現できます。  
  
-   プライマリ\) だけでなく \(すべてのノードの読み取りおよび書き込み機能  
  
-   システムへの待機時間の導入を避けるため、非同期的にレプリケートされるデータの量が少ない  
  
次の図は、マージレプリケーション \(1 パブリッシャー、2サブスクライバー\)で、地理的に冗長な AD FS SQL Server ファームを示しています。  
  
![SQL を使用したサーバーファーム](media/ADFSSQLGeoRedundancy3.png)  
  
**SQL Server マージレプリケーションで AD FS を使用する場合の主な展開に関する考慮事項 \(上の図のメモ番号\)**  
  
-   AlwaysOn 可用性グループまたはデータベースミラーリングでのディストリビューターデータベースの使用はサポートされていません。  レプリケーション[、Change Tracking、変更データキャプチャ、AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)のレプリケーションオプションを使用して、AlwaysOn 可用性グループの SQL Server サポートステートメントを参照してください。  
  
-   レプリケーション サブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するためには、レプリケーション管理者が手動でそのサブスクライバーを再構成する必要があります。  レプリケーションの[サブスクライバーと AlwaysOn 可用性グループ \(SQL Server\)](https://technet.microsoft.com/library/hh882436.aspx)と、レプリケーションオプションの[レプリケーション、Change Tracking、変更データキャプチャ、および](https://technet.microsoft.com/library/hh403414.aspx)AlwaysOn 可用性グループ \(SQL Server\)を使用した AlwaysOn 可用性グループの全体的なサポートステートメントについては、SQL Server の特定の問題の説明を参照してください。  
  
SQL Server マージレプリケーションを使用するように AD FS を構成する方法の詳細については、「 [SQL Server レプリケーションを使用した地理的冗長性のセットアップ](https://technet.microsoft.com/library/dn632406.aspx)」を参照してください。  
  
## <a name="see-also"></a>参照  
[AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

