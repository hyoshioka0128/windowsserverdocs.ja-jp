---
ms.assetid: e983d2ab-4153-41e7-b243-12cf7d71a552
title: SQL Server を使用するフェデレーション サーバー ファーム
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0ab150a5070f076db70941bb106b42c3fb15411e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408094"
---
# <a name="federation-server-farm-using-sql-server"></a>SQL Server を使用するフェデレーション サーバー ファーム

Active Directory フェデレーションサービス (AD FS) \(AD FS\)のこのトポロジは、データをレプリケートしないという点\(で\) 、Windows Internal Database WID 展開トポロジを使用するフェデレーションサーバーファームとは異なります。ファーム内の各フェデレーションサーバー。 代わりに、ファーム内のすべてのフェデレーションサーバーは、企業ネットワーク内に配置されている Microsoft SQL Server を実行しているサーバーに格納されている共通のデータベースにデータの読み取りと書き込みを行うことができます。  
  
> [!IMPORTANT]  
> AD FS ファームを作成し SQL Server を使用して構成データを格納する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012、SQL Server 2014) を使用できます。  
  
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
次のバージョンの SQL server は、Windows Server 2012 R2 の AD FS でサポートされています。  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
-   SQL Server 2014  
  
## <a name="server-placement-and-network-layout-recommendations"></a>サーバーの配置とネットワークレイアウトに関する推奨事項  
WID トポロジを持つフェデレーションサーバーファームと同様に、ファーム内のすべてのフェデレーションサーバーは、フェデレーションサービス名\(\) \(\)を表す1つのクラスタードメインネームシステムDNS名を使用するように構成されます。ネットワーク負荷分散\(NLB\)クラスター構成の一部として1つのクラスター IP アドレスを設定します。 これにより、NLB ホストは個々のフェデレーションサーバーにクライアント要求を割り当てることができます。 フェデレーションサーバープロキシは、フェデレーションサーバーファームにクライアント要求をプロキシするために使用できます。  
  
次の図は、架空の Contoso 薬品企業が企業ネットワークに SQL Server トポロジを使用してフェデレーションサーバーファームを展開した方法を示しています。 また、企業が DNS サーバーへのアクセスを使用して境界ネットワークを構成した方法、企業ネットワーク NLB クラスターで使用さ\(れ\)ているのと同じクラスター DNS 名 fs.contoso.com を使用する追加の nlb ホスト、および2つの webアプリケーションプロキシ\(wap1 と wap2\)。  
  
![SQL を使用したサーバーファーム](media/SQLFarmADFSBlue.gif)  
  
フェデレーションサーバーまたは web アプリケーションプロキシで使用するためのネットワーク環境を構成する方法の詳細については、「AD FS の[要件](AD-FS-Requirements.md)」の「名前解決の要件」セクションを参照してください。 [(WAP)](https://technet.microsoft.com/library/dn383648.aspx)。  
  
## <a name="high-availability-options-for-sql-server-farms"></a>SQL Server ファームの高可用性オプション  
Windows Server 2012 R2 では、SQL Server を使用して AD FS ファームで高可用性をサポートするための2つの新しいオプションが AD FS ます。  
  
-   SQL Server AlwaysOn 可用性グループのサポート  
  
-   SQL Server マージレプリケーションを使用した地理的に分散した高可用性のサポート  
  
ここでは、これらの各オプションについて、それぞれの問題の解決方法と、展開するオプションを決定するための重要な考慮事項について説明します。  
  
> [!NOTE]  
> Windows Internal Database \(WID\)を使用するファーム AD FS、プライマリフェデレーションサーバーノード\/での読み取り/書き込みアクセスと、セカンダリノード\-での読み取り専用アクセスを備えた基本的なデータ冗長性を提供します。  これは、地理的にローカルまたは地理的に分散したトポロジで使用できます。  
>   
> WID を使用する場合は、次の制限事項に注意してください。  
>   
> -   100を超える証明書利用者信頼がある場合、WID ファームには、最大30個のフェデレーションサーバーがあります。  
> -   WID \(ファームは、Security Assertion Markup Language \(SAML\)プロトコル\)のトークンリプレイ検出またはアーティファクト解決部分をサポートしていません。  
  
WID ファームを使用する場合の概要を次の表に示します。  
  
||||  
|-|-|-|  
||1 \- 100 RP 信頼|100を超える RP 信頼|  
|1 \-個の AD FS ノード|WID がサポートされる|WID \- SQL が必要な場合はサポートされません|  
|30を超える AD FS ノード|WID \- SQL が必要な場合はサポートされません|WID \- SQL が必要な場合はサポートされません|  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性グループ  
**概要**  
  
AlwaysOn 可用性グループは SQL Server 2012 で導入され、高可用性 SQL Server インスタンスを作成するための新しい方法を提供しています。  AlwaysOn 可用性グループは、クラスターとデータベースミラーリングの要素を組み合わせて、SQL インスタンス層とデータベース層の両方で冗長性とフェールオーバーを実現します。  以前の高可用性オプションとは異なり、AlwaysOn 可用性グループは、データベース\(層で共通の\)記憶域またはストレージエリアネットワークを必要としません。  
  
可用性グループは、一連\(の読み取り\-書き込みプライマリデータベース\)と、対応するセカンダリデータベース\)の 1 ~ 4 個の\(可用性レプリカセットで構成されます。  可用性グループは、\-プライマリレプリカ\)と 1 ~ \(4 個の読み取り\-専用可用性レプリカの1つの読み取り書き込みコピーをサポートします。  各可用性レプリカは、1つの Windows Server フェールオーバークラスタリング\(WSFC\)クラスターの別のノードに存在する必要があります。  AlwaysOn 可用性グループの詳細については、「 [ \(AlwaysOn 可用性グループ\)SQL Server の概要](https://technet.microsoft.com/library/ff877884.aspx)」を参照してください。  
  
AD FS SQL Server ファームのノードの観点からは、1つの SQL Server インスタンスがポリシー \/アーティファクトデータベースとして、AlwaysOn 可用性グループに置き換えられます。  可用性グループリスナーは、AD FS Security Token Service \(\)が SQL への接続に使用するクライアントです。  
  
次の図は、AlwaysOn 可用性グループを使用したファーム SQL Server AD FS を示しています。  
  
![SQL を使用したサーバーファーム](media/alwaysonavailabilitygroups.jpg)  
  
> [!NOTE]  
> AlwaysOn 可用性グループでは、SQL Server インスタンスが Windows Server フェールオーバークラスタリング\(WSFC\)ノードに存在する必要があります。  
  
> [!NOTE]  
> 自動フェールオーバーターゲットとして機能できる可用性レプリカは1つだけで、他の3つは手動フェールオーバーに依存します。  
  
**展開に関する主な考慮事項**  
  
AlwaysOn 可用性グループを SQL Server マージレプリケーションと組み合わせて使用する場合は、以下の「SQL Server マージレプリケーションで AD FS を使用するための展開に関する主な考慮事項」で説明されている問題を確認してください。  特に、レプリケーションサブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーションサブスクリプションが失敗します。 レプリケーションを再開するには、レプリケーション管理者が手動でサブスクライバーを再構成する必要があります。  レプリケーション[サブスクライバーと AlwaysOn 可用性グループ\(\) SQL Server](https://technet.microsoft.com/library/hh882436.aspx) 、およびレプリケーションオプション[を使用した AlwaysOn 可用性グループのすべてのサポートステートメントについては、「SQL Server」で特定の問題の説明を参照してください。レプリケーション、Change Tracking、変更データキャプチャ、AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)。  
  
**AlwaysOn 可用性グループを使用するように AD FS を構成する**  
  
AlwaysOn 可用性グループを使用して AD FS ファームを構成するには、AD FS の展開手順を少し変更する必要があります。  
  
1.  バックアップするデータベースは、AlwaysOn 可用性グループを構成する前に作成しておく必要があります。  AD FS は、新しい AD FS SQL Server ファームの最初のフェデレーションサービスノードのセットアップと初期構成の一部としてデータベースを作成します。  AD FS 構成の一部として、sql 接続文字列を指定する必要があります。そのため、最初の AD FS ファームノードが sql インスタンスに直接\(接続するように構成する必要があります。これは一時的\)なものです。   SQL server 接続文字列を使用した AD FS ファームノードの構成など、AD FS ファームの構成に関する具体的なガイダンスについては、「 [Configure a Federation server](../../ad-fs/deployment/Configure-a-Federation-Server.md)」を参照してください。  
  
2.  AD FS データベースを作成したら、それらのデータベースを AlwaysOn 可用性グループに割り当てて、SQL Server ツールとプロセスを使用して[可用性グループ\(の作成と構成を\)行うことによって、共通の TCPIP リスナーを作成 SQL Server](https://technet.microsoft.com/library/ff878265.aspx).  
  
3.  最後に、PowerShell を使用して AD FS のプロパティを編集し、AlwaysOn 可用性グループのリスナーの DNS アドレスを使用するように SQL 接続文字列を更新します。  
  
    AD FS 構成データベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。  
  
    ```  
    PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService  
    PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”  
    PS:\>$temp.put()  
  
    ```  
  
4.  AD FS アーティファクト解決サービスデータベースの SQL 接続文字列を更新するための PSH コマンドの例を次に示します。  
  
    ```  
    PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”  
    ```  
  
### <a name="sql-server-merge-replication"></a>マージレプリケーションの SQL Server  
また、SQL Server 2012 で導入されたマージレプリケーションでは、次の特性を持つ AD FS ポリシーデータの冗長性を実現できます。  
  
-   プライマリだけでなくすべてのノード\(での読み取りおよび書き込み機能\)  
  
-   システムへの待機時間の導入を避けるため、非同期的にレプリケートされるデータの量が少ない  
  
次の図は、マージレプリケーション\(1 パブリッシャー、2つのサブスクライバー\)を含む AD FS SQL Server の地理的冗長なファームを示しています。  
  
![SQL を使用したサーバーファーム](media/ADFSSQLGeoRedundancy3.png)  
  
**SQL Server マージレプリケーション\(での AD FS の使用に関する主な考慮事項については、上の図のメモ番号を確認してください。\)**  
  
-   AlwaysOn 可用性グループまたはデータベースミラーリングでのディストリビューターデータベースの使用はサポートされていません。  レプリケーション[、Change Tracking、変更データキャプチャ、および AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)でのレプリケーションオプションを使用した AlwaysOn 可用性グループのサポートステートメントについては、「SQL Server」を参照してください。  
  
-   レプリケーションサブスクライバーであるデータベースを含む AlwaysOn 可用性グループがフェールオーバーすると、レプリケーションサブスクリプションが失敗します。 レプリケーションを再開するには、レプリケーション管理者が手動でサブスクライバーを再構成する必要があります。  レプリケーションの[サブスクライバーと AlwaysOn 可用性グループ\(\) SQL Server](https://technet.microsoft.com/library/hh882436.aspx)およびレプリケーションオプション[を使用した AlwaysOn 可用性グループの全体的なサポートステートメントについては、SQL Server の特定の問題の説明を参照してください。レプリケーション、Change Tracking、変更データキャプチャ、AlwaysOn 可用性グループ\(SQL Server\)](https://technet.microsoft.com/library/hh403414.aspx)。  
  
SQL Server マージレプリケーションを使用するように AD FS を構成する方法の詳細については、「 [SQL Server レプリケーションを使用した地理的冗長性のセットアップ](https://technet.microsoft.com/library/dn632406.aspx)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
[AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)  
[Windows Server 2012 R2 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)  
  

