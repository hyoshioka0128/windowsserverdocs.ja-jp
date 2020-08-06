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
ms.openlocfilehash: 4527b6787531b3a349534092e3597a91dbebf78f
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864136"
---
# <a name="legacy-ad-fs-federation-server-farm-using-sql-server"></a>SQL Server を使用した従来の AD FS フェデレーションサーバーファーム

Active Directory フェデレーションサービス (AD FS) AD FS のこのトポロジは、 \( \) \( \) ファーム内の各フェデレーションサーバーにデータをレプリケートしないという点で、Windows Internal Database WID 展開トポロジを使用したフェデレーションサーバーファームとは異なります。 代わりに、ファーム内のすべてのフェデレーションサーバーは、企業ネットワーク内に配置されている Microsoft SQL Server を実行しているサーバーに格納されている共通のデータベースにデータの読み取りと書き込みを行うことができます。

> [!IMPORTANT]
> AD FS ファームを作成し SQL Server を使用して構成データを格納する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012、SQL Server 2014) を使用できます。

## <a name="deployment-considerations"></a>デプロイに関する考慮事項
このセクションでは、この展開トポロジに関連する対象ユーザー、利点、および制限事項に関するさまざまな考慮事項について説明します。

### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。

- 100以上の信頼関係を持つ大規模な組織では、内部ユーザーと外部ユーザーの両方にシングルサインオン SSO アクセスを提供する必要があります。 \- \( \) フェデレーションアプリケーションまたはサービスにアクセスします。

- 既に SQL Server を使用し、既存のツールと専門知識を活用する組織

### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは

- 100を超える信頼関係を多数サポート \(\)

- トークンリプレイ検出のサポート \( \) \( Security Assertion Markup Language \( SAML \) 2.0 プロトコルのセキュリティ機能とアーティファクト解決の部分\)

- データベースミラーリング、フェールオーバークラスタリング、レポート、管理ツールなどの SQL Server の利点のすべてのサポート

### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。

- このトポロジでは、データベースの冗長性は既定では提供されません。 WID トポロジを持つフェデレーションサーバーファームは、ファーム内の各フェデレーションサーバーで WID データベースを自動的にレプリケートしますが、SQL Server トポロジを持つフェデレーションサーバーファームには、データベースのコピーが1つだけ含まれます。

    > [!NOTE]
    > SQL Server は、フェールオーバークラスタリング、データベースミラーリング、およびさまざまな種類の SQL Server レプリケーションなど、さまざまなデータおよびアプリケーション冗長オプションをサポートしています。

Microsoft の \( it 部門は、 \) 安全性の高い同期モードおよびフェールオーバークラスタリングで SQL Server データベースミラーリングを使用して、 \- \( \) \- SQL Server インスタンスの高可用性をサポートしています。 SQL Server \( のトランザクションピアツー \- \- ピア \) とマージレプリケーションは、Microsoft の AD FS 製品チームによってテストされていません。 SQL Server の詳細については、「[高可用性ソリューションの概要](https://go.microsoft.com/fwlink/?LinkId=179853)」または[適切な種類のレプリケーションの選択](https://go.microsoft.com/fwlink/?LinkId=214648)に関するトピックを参照してください。

### <a name="supported-sql-server-versions"></a>サポートされている SQL Server バージョン
次のバージョンの SQL server は、Windows Server 2012 R2 の AD FS でサポートされています。

- SQL Server 2008 \/ R2

- SQL Server 2012

- SQL Server 2014

## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項
WID トポロジを持つフェデレーションサーバーファームと同様に、ファーム内のすべてのフェデレーションサーバーは、 \( \) \( \) ネットワーク負荷分散 NLB クラスター構成の一部として、フェデレーションサービス名と1つのクラスター IP アドレスを表す1つのクラスタードメインネームシステム DNS 名を使用するように構成され \( \) ます。 これにより、NLB ホストは個々のフェデレーションサーバーにクライアント要求を割り当てることができます。 フェデレーションサーバープロキシは、フェデレーションサーバーファームにクライアント要求をプロキシするために使用できます。

次の図は、架空の Contoso 薬品企業が企業ネットワークに SQL Server トポロジを使用してフェデレーションサーバーファームを展開した方法を示しています。 また、企業が DNS サーバーへのアクセスを使用して境界ネットワークを構成した方法、企業ネットワーク NLB クラスターで使用されているのと同じクラスター DNS 名 fs.contoso.com を使用する追加の NLB ホスト、 \( \) および2つの web アプリケーションプロキシ \( wap1 と wap2 を使用していることもわかり \) ます。

![SQL を使用したサーバーファーム](media/SQLFarmADFSBlue.gif)

フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照して、 [Web アプリケーションプロキシインフラストラクチャ (WAP) を計画](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))してください。

## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server ファームの高可用性オプション
Windows Server 2012 R2 では、SQL Server を使用して AD FS ファームで高可用性をサポートするための2つの新しいオプションが AD FS ます。

- SQL Server AlwaysOn 可用性グループのサポート

- SQL Server マージレプリケーションを使用した地理的に分散した高可用性のサポート

ここでは、これらの各オプションについて、それぞれの問題の解決方法と、展開するオプションを決定するための重要な考慮事項について説明します。

> [!NOTE]
> Windows Internal Database WID を使用するファーム AD FS、 \( \) \/ プライマリフェデレーションサーバーノードでの読み取り/書き込みアクセスと、セカンダリノードでの読み取り専用アクセスを備えた基本的なデータ冗長性を提供し \- ます。これは、地理的にローカルまたは地理的に分散したトポロジで使用できます。
>
> WID を使用する場合は、次の制限事項に注意してください。
>
> - 100を超える証明書利用者信頼がある場合、WID ファームには、最大30個のフェデレーションサーバーがあります。
> - WID ファームは、 \( Security Assertion Markup Language SAML プロトコルのトークンリプレイ検出またはアーティファクト解決部分をサポートしていません \( \) \) 。

WID ファームの使用の概要を次の表に示します。

| 1-100 個の RP 信頼 | 100 個を超える RP 信頼 |
|--|--|
| **1-30 個の AD FS ノード:** WID サポート対象 | **1-30 個の AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 |
| **30 個を超える AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 | **30 個を超える AD FS ノード:** WID の使用はサポート対象外 - SQL が必要 |

### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ
**概要**

AlwaysOn 可用性グループは SQL Server 2012 で導入され、高可用性 SQL Server インスタンスを作成するための新しい方法を提供しています。AlwaysOn 可用性グループは、クラスターとデータベースミラーリングの要素を組み合わせて、SQL インスタンス層とデータベース層の両方で冗長性とフェールオーバーを実現します。以前の高可用性オプションとは異なり、AlwaysOn 可用性グループは、 \( データベース層で共通の記憶域またはストレージエリアネットワークを必要としません \) 。

可用性グループは、 \( 一連の読み取り \- 書き込みプライマリデータベース \) と、 \( 対応するセカンダリデータベースの 1 ~ 4 個の可用性レプリカセットで構成され \) ます。可用性グループは、 \- \( プライマリレプリカ \) と 1 ~ 4 個の読み取り専用可用性レプリカの1つの読み取り書き込みコピーをサポートし \- ます。各可用性レプリカは、1つの Windows Server フェールオーバークラスタリング WSFC クラスターの別のノードに存在する必要があり \( \) ます。AlwaysOn 可用性グループの詳細については、「 [AlwaysOn 可用性グループ \( SQL Server \) の概要](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15)」を参照してください。

AD FS SQL Server ファームのノードの観点からは、1つの SQL Server インスタンスがポリシーアーティファクトデータベースとして、AlwaysOn 可用性グループに置き換えられ \/ ます。可用性グループリスナーは、 \( AD FS Security Token Service が \) SQL への接続に使用するクライアントです。

次の図は、AlwaysOn 可用性グループを使用したファーム SQL Server AD FS を示しています。

![SQL を使用したサーバーファーム](media/alwaysonavailabilitygroups.jpg)

> [!NOTE]
> AlwaysOn 可用性グループでは、SQL Server インスタンスが Windows Server フェールオーバークラスタリング WSFC ノードに存在する必要があり \( \) ます。

> [!NOTE]
> 自動フェールオーバーターゲットとして機能できる可用性レプリカは1つだけで、他の3つは手動フェールオーバーに依存します。

**展開に関する主な考慮事項**

AlwaysOn 可用性グループを SQL Server マージレプリケーションと組み合わせて使用する場合は、以下の「SQL Server マージレプリケーションで AD FS を使用するための展開に関する主な考慮事項」で説明されている問題を確認してください。特に、レプリケーションサブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーションサブスクリプションが失敗します。 レプリケーションを再開するためには、レプリケーション管理者が手動でそのサブスクライバーを再構成する必要があります。レプリケーション[、Change Tracking、変更データ \( \) キャプチャ、AlwaysOn 可用性グループ](/sql/database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability?view=sql-server-ver15)SQL Server のレプリケーションオプションを使用して、レプリケーション[サブスクライバーと AlwaysOn 可用性グループ \( SQL Server \) ](/sql/database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server?view=sql-server-ver15)および AlwaysOn 可用性グループの全体的なサポートステートメントに関する特定の問題の SQL Server 説明を参照してください。

**AlwaysOn 可用性グループを使用するように AD FS を構成する**

AlwaysOn 可用性グループを使用して AD FS ファームを構成するには、AD FS の展開手順を少し変更する必要があります。

1. バックアップするデータベースは、AlwaysOn 可用性グループを構成する前に作成しておく必要があります。AD FS は、新しい AD FS SQL Server ファームの最初のフェデレーションサービスノードのセットアップと初期構成の一部としてデータベースを作成します。AD FS 構成の一部として、SQL 接続文字列を指定する必要があります。そのため、最初の AD FS ファームノードが SQL インスタンスに直接接続するように構成する必要があり \( ます。これは一時的なものです \) 。 SQL server 接続文字列を使用した AD FS ファームノードの構成など、AD FS ファームの構成に関する具体的なガイダンスについては、「 [Configure a Federation server](../../ad-fs/deployment/Configure-a-Federation-Server.md)」を参照してください。

2. AD FS データベースを作成したら、そのデータベースを AlwaysOn 可用性グループに割り当てて、SQL Server ツールとプロセスを使用して、 [ \( \) SQL Server の可用性グループの作成と構成](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15)を行い、共通の TCPIP リスナーを作成します。

3. 最後に、PowerShell を使用して AD FS のプロパティを編集し、AlwaysOn 可用性グループのリスナーの DNS アドレスを使用するように SQL 接続文字列を更新します。

    AD FS 構成データベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。

    ```
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService
    PS:\>$temp.ConfigurationdatabaseConnectionstring="data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true"
    PS:\>$temp.put()

    ```

4. AD FS アーティファクト解決サービスデータベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。

    ```
    PS:\> Set-AdfsProperties –artifactdbconnection "Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True"
    ```

### <a name="sql-server-merge-replication"></a>マージレプリケーションの SQL Server
また、SQL Server 2012 で導入されたマージレプリケーションでは、次の特性を持つ AD FS ポリシーデータの冗長性を実現できます。

- プライマリだけでなくすべてのノードでの読み取りおよび書き込み機能 \(\)

- システムへの待機時間の導入を避けるため、非同期的にレプリケートされるデータの量が少ない

次の図は、マージレプリケーション \( 1 パブリッシャー、2つのサブスクライバーを含む AD FS SQL Server の地理的冗長なファームを示してい \) ます。

![SQL を使用したサーバーファーム](media/ADFSSQLGeoRedundancy3.png)

**SQL Server マージレプリケーションでの AD FS の使用に関する主な考慮事項について \( は、上の図のメモ番号を確認してください。\)**

- AlwaysOn 可用性グループまたはデータベースミラーリングでのディストリビューターデータベースの使用はサポートされていません。レプリケーション[、Change Tracking、変更データキャプチャ、および AlwaysOn 可用性グループ \( SQL Server \) ](/sql/database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability?view=sql-server-ver15)でのレプリケーションオプションを使用した AlwaysOn 可用性グループのサポートステートメントについては、「SQL Server」を参照してください。

- レプリケーション サブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーション サブスクリプションは失敗します。 レプリケーションを再開するためには、レプリケーション管理者が手動でそのサブスクライバーを再構成する必要があります。レプリケーション[、Change Tracking、変更データキャプチャ \( \) 、および AlwaysOn 可用性グループ](/sql/database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability?view=sql-server-ver15)SQL Server を使用して、レプリケーション[サブスクライバーと AlwaysOn 可用性グループ \( SQL Server \) ](/sql/database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server?view=sql-server-ver15)および AlwaysOn 可用性グループの全体的なサポートステートメントに関する特定の問題の SQL Server 説明を参照してください。

SQL Server マージレプリケーションを使用するように AD FS を構成する方法の詳細については、「 [SQL Server レプリケーションを使用した地理的冗長性のセットアップ](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn632406(v=ws.11))」を参照してください。

## <a name="see-also"></a>参照
[AD FS の展開トポロジ](Plan-Your-AD-FS-Deployment-Topology.md) 
 を計画する[Windows Server 2012 R2 の AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)

