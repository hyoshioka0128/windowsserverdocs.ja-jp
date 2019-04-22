---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: SQL Server を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e26b7cac971f472bc8b5e48e3dc8cd2592dc22ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814783"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用するフェデレーション サーバー ファーム

>適用先:Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービスのこのトポロジ\(AD FS\) Windows Internal Database を使用してフェデレーション サーバー ファームとは異なります\(WID\)展開トポロジでデータを複製されません。ファームの各フェデレーション サーバー。 代わりに、ファーム内のすべてのフェデレーション サーバーは、読み取りし、は、企業ネットワークにある Microsoft SQL Server を実行しているサーバーに格納されている一般的なデータベースにデータを書き込みます。  
  
> [!IMPORTANT]  
> AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、および SQL Server 2014 を含む、新しいバージョンを使用することができます。  
  
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
Windows Server 2012 R2 で AD FS では、次の SQL server のバージョンがサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワーク レイアウトの推奨事項  
WID トポロジを使用したフェデレーション サーバー ファームと同様に、すべてのファームにフェデレーション サーバーが構成されて 1 つのクラスターのドメイン ネーム システムを使用して\(DNS\)名前\(フェデレーションサービス名を表す\)とネットワーク負荷分散の一部として 1 つのクラスター IP アドレス\(NLB\)クラスターの構成。 これにより、個々 のフェデレーション サーバーにクライアント要求の割り当ての NLB ホストできます。 クライアント要求のプロキシ、フェデレーション サーバー ファームにフェデレーション サーバー プロキシを使用できます。  
  
次の図は、架空の Contoso Pharmaceuticals 会社が企業ネットワーク内の SQL Server トポロジでそのフェデレーション サーバー ファームを展開する方法を示します。 その会社が DNS サーバー、同じクラスター DNS 名を使用する追加の NLB ホストにアクセスできる境界ネットワークを構成する方法も示します\(fs.contoso.com\)企業ネットワークの NLB クラスターで 2 つの web を使用して使用します。アプリケーション プロキシ\(wap1 と wap2\)します。  
  
![SQL を使用してサーバー ファーム](media/SQLFarmADFSBlue.gif)  
  
フェデレーション サーバーまたは web アプリケーション プロキシを使用するため、ネットワーク環境を構成する方法の詳細については、「名前解決の要件」を参照してください。 セクション[AD FS の要件](AD-FS-Requirements.md)と[Web の計画アプリケーション プロキシ インフラストラクチャ (WAP)](https://technet.microsoft.com/library/dn383648.aspx)します。  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server ファームの高可用性オプション  
Windows Server 2012 R2、SQL Server を使用して AD FS ファームの高可用性をサポートするために 2 つのオプションは AD FS があります。  
  
-   SQL Server AlwaysOn 可用性グループのサポート  
  
-   SQL Server マージ レプリケーションを使用して高可用性を地理的に分散のサポート  
  
このセクションでは、これらのオプションのそれぞれについて説明します、解決それぞれどのような問題およびデプロイするためには、どのオプションを決定するための主な考慮事項。  
  
> [!NOTE]  
> Windows Internal Database を使用する AD FS ファーム\(WID\)基本的なデータの冗長性を備えた読み取り\/プライマリ フェデレーション サーバーのノードに書き込みアクセスと読み取り\-セカンダリ ノードでのみアクセスします。  これは、地理的にローカルまたは地理的に分散トポロジで使用できます。  
>   
> WID を使用するときは、次の制限事項に注意してください。  
>   
> -   WID ファームでは、100 以下の証明書利用者のパーティ信頼がある場合、30 台のフェデレーション サーバーの制限があります。  
> -   WID ファームは、トークン再生検出または成果物の解決をサポートしていません\(、Security Assertion Markup Language の一部\(SAML\)プロトコル\)します。  
  
次の表は、WID ファームの使用に関する概要を示します。  
  
||||  
|-|-|-|  
||1 \- 100 の RP 信頼|100 を超える RP 信頼|  
|1 \- 30年の AD FS ノード|WID のサポート|WID を使用してサポートされていません\-のために必要な SQL|  
|複数の 30年の AD FS ノード|WID を使用してサポートされていません\-のために必要な SQL|WID を使用してサポートされていません\-のために必要な SQL|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ  
**概要**  
  
AlwaysOn 可用性グループは、SQL Server 2012 で導入された、高可用性 SQL Server インスタンスを作成する新しい方法を提供します。  AlwaysOn 可用性グループは、クラスタ リングとデータベース ミラーリングの冗長性とフェールオーバーは、SQL インスタンスの層とデータベース層の両方での要素を結合します。  前の高可用性オプションとは異なり AlwaysOn 可用性グループ必要としない共通の記憶域\(やストレージ エリア ネットワーク\)データベース層。  
  
可用性グループがプライマリ レプリカから成る\(一連の読み取り\-プライマリ データベース書き込み\)と 1 ~ 4 の可用性レプリカ\(対応するセカンダリ データベースの設定\)します。  可用性グループが 1 つの読み取りをサポートしている\-コピーを作成\(、プライマリ レプリカ\)と 1 ~ 4 の読み取り\-可用性レプリカだけです。  各可用性レプリカが別のノードを 1 つ Windows Server フェールオーバー クラスタ リングの上に存在する必要があります\(WSFC\)クラスター。  詳細については、AlwaysOn 可用性グループを参照してください[AlwaysOn 可用性グループの概要\(SQL Server\)](https://technet.microsoft.com/library/ff877884.aspx)します。  
  
AD FS の SQL Server ファームのノードの観点から、AlwaysOn 可用性グループにポリシーとして 1 つの SQL Server インスタンスが置き換えられます\/成果物のデータベース。  可用性グループ リスナーはどのようなクライアント\(AD FS セキュリティ トークン サービス\)使用して SQL に接続します。  
  
次の図は、AlwaysOn 可用性グループに AD FS の SQL Server のファームを示します。  
  
![SQL を使用してサーバー ファーム](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 可用性グループでは、Windows Server フェールオーバー クラスタ リングに SQL Server インスタンスが存在する必要があります\(WSFC\)ノード。  
  
> [!NOTE]  
> 1 つだけ可用性レプリカは、3 つの他、自動フェールオーバー ターゲットは手動フェールオーバーに依存してために機能します。  
  
**キーの展開に関する考慮事項**  
  
AlwaysOn 可用性グループを SQL Server マージ レプリケーションと組み合わせて使用する場合は、以下の「キーのデプロイは SQL Server マージ レプリケーションで AD FS の使用に関する考慮事項」で説明する問題のをメモしてをおきますしてください。  具体的には、データベース レプリケーションのサブスクライバーを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するには、レプリケーション管理者は、サブスクライバーを手動で再構成する必要があります。  特定の問題の SQL Server の説明を参照して[レプリケーション サブスクライバーと AlwaysOn 可用性グループ\(SQL Server\) ](https://technet.microsoft.com/library/hh882436.aspx)での AlwaysOn 可用性グループの全体的なステートメントをサポートレプリケーションのオプションで[レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
**AlwaysOn 可用性グループを使用する AD FS を構成します。**  
  
AlwaysOn 可用性グループで、AD FS ファームを構成するには、AD FS の展開手順を少し変更する必要があります。  
  
1.  AlwaysOn 可用性グループを構成する前に、バックアップするデータベースを作成する必要があります。  AD FS には、セットアップと新しい AD FS の SQL Server ファームの最初のフェデレーション サービス ノードの初期構成の一部としてそのデータベースが作成されます。  AD FS 構成の一環として、SQL インスタンスに直接接続する最初の AD FS ファームのノードを構成する必要がありますので、SQL 接続文字列を指定する必要があります\(これは一時的なのみ\)します。   特定のガイダンスについては、SQL server 接続文字列で、AD FS ファームのノードの構成など、AD FS ファームを構成するのを参照してください。 [Configure a Federation Server](../../ad-fs/deployment/Configure-a-Federation-Server.md)します。  
  
2.  AD FS データベースが作成されたら、AlwaysOn 可用性グループに割り当てると SQL Server ツールを使用して一般的な TCPIP リスナーを作成および処理[の作成と構成の可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/ff878265.aspx).  
  
3.  最後に、PowerShell を使用して、AlwaysOn 可用性グループのリスナーの DNS アドレスを使用する SQL 接続文字列を更新する AD FS のプロパティを編集します。  
  
    PSH コマンドの例は、AD FS 構成データベースの SQL 接続文字列を更新する:  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  AD FS の成果物の解決サービス データベースの SQL 接続文字列を更新する PSH コマンドの例:  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>SQL Server マージ レプリケーション  
マージ レプリケーションは、次の特性を持つ AD FS ポリシー データの冗長性のためでも、SQL Server 2012 で導入されました。  
  
-   すべてのノードでの機能の読み書き\(だけでなく、プライマリ\)  
  
-   少量のデータの概要、システムの待機時間を回避するために非同期的にレプリケート  
  
次の図は、マージ レプリケーションでの geo 冗長の AD FS の SQL Server ファーム\(パブリッシャーが 1、2 つのサブスクライバー\):  
  
![SQL を使用してサーバー ファーム](media/ADFSSQLGeoRedundancy3.png)  
  
**SQL Server マージ レプリケーションで AD FS を使用するためキー展開に関する考慮事項\(上記の図の番号に注意してください\)**  
  
-   ディストリビューター データベースは、AlwaysOn 可用性グループまたはデータベース ミラーリングでの使用はサポートされていません。  SQL Server AlwaysOn 可用性グループで、レプリケーション オプションのステートメントのサポートを参照してください。[レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
-   データベース レプリケーションのサブスクライバーを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するには、レプリケーション管理者は、サブスクライバーを手動で再構成する必要があります。  特定の問題の SQL Server の説明を参照して[レプリケーション サブスクライバーと AlwaysOn 可用性グループ\(SQL Server\) ](https://technet.microsoft.com/library/hh882436.aspx)での AlwaysOn 可用性グループの全体的なステートメントをサポートレプリケーション オプション[レプリケーション、変更の追跡、変更データ キャプチャ、および AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)します。  
  
SQL Server マージ レプリケーションを使用する AD FS を構成する方法の詳細な手順は、「[地理的冗長化を SQL Server レプリケーション セットアップ](https://technet.microsoft.com/library/dn632406.aspx)します。  
  
## <a name="see-also"></a>関連項目  
[AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

