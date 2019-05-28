---
title: Azure での RDS データ センターの地理冗長
description: 複数のデータ センターを使用して、さまざまな場所で高可用性を提供する RDS デプロイを作成する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61c36528-cf47-4af0-83c1-a883f79a73a5
author: haley-rowland
ms.author: elizapo
ms.date: 06/14/2017
manager: dongill
ms.openlocfilehash: 2d12062f302c28a8124e0aa49af7f441e77ffe33
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222791"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>Geo 冗長、複数のデータ センターのディザスター リカバリーの RDS のデプロイの作成します。

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Azure での複数のデータ センターを活用することにより、リモート デスクトップ サービス展開のディザスター リカバリーを有効にできます。 高可用性 RDS の標準デプロイとは異なり (」の説明に従って、[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md))、単一の Azure リージョン (西ヨーロッパなど) でのデータ センターを使用する、複数データ センター デプロイ データの使用展開 - 1 つの Azure データ センターの可用性を高める、複数の地理的な場所でセンターを使用できない可能性がありますが、複数のリージョンが同時にダウンは可能性はほとんどありません。 Geo 冗長 RDS アーキテクチャをデプロイすることで、リージョン全体の重大なエラーの場合のフェールオーバーを有効にできます。

以下の手順を使用してを通じて複数のテナントに Microsoft Azure インフラストラクチャ サービスと geo 冗長のデスクトップ ホスティング サービスおよびサブスクライバー アクセス ライセンス (Sal) を提供する RDS を利用することができます、 [Microsoft サービス プロバイダーライセンス契約 (SPLA) プログラム](https://www.microsoft.com/hosting/licensing/splabenefits.aspx)します。 使用して、独自の従業員の geo 冗長のホスティング サービスを作成する次の手順を使用することもできます。[拡張権利のソフトウェア アシュアランスによる RDS ユーザー Cal](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)します。

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>高可用性 - 1 つの論理アーキテクチャと複数のリージョン
次の図は、単一の Azure リージョンで高可用性展開のアーキテクチャを示しています。

![単一の Azure リージョンでの高可用性の展開](media/rds-ha-single-region.png)

展開は、3 つの層で構成されます。

- Azure サービスでは、Azure ポータルと Api では、DNS とパブリック IP アドレスの指定などのパブリック ネットワーク サービスなど、Azure 管理インターフェイス。
- デスクトップ ホスティング サービスに仮想マシン、ネットワーク、ストレージ、Azure サービス、および Windows サーバーの役割サービス
- Azure ファブリックに HYPER-V ロールを実行して、Windows Server オペレーティング システムの物理サーバー、記憶域ユニット、ネットワーク スイッチ、およびルーターを仮想化するために使用します。 Azure Fabric を使用して、Vm、ネットワーク、ストレージ、およびアプリケーションを基になるハードウェアから独立して作成できます。


比較では、複数の Azure データ センターを使用する展開のアーキテクチャを示します。

![複数の Azure リージョンを使用している RDS のデプロイ](media/rds-ha-multi-region.png)

RDS デプロイ全体は、geo 冗長の展開を作成する 2 つ目の Azure リージョンにレプリケートされます。 このアーキテクチャでは、一度に 1 つだけの RDS のデプロイが実行されている、アクティブ/パッシブ モデルを使用します。 VNet 対 VNet 接続は、互いに通信する 2 つの環境を使用できます。 RDS のデプロイは、単一の Active Directory フォレスト/ドメイン、に基づいて、AD サーバーは、2 つのデプロイ間でレプリケート、意味のユーザーと同じ資格情報を使用してデプロイをいずれかにサインインできます。 ユーザー設定とユーザー プロファイル ディスク (UPD) に格納されているデータは、2 ノード クラスターの記憶域スペース ダイレクト スケール アウト ファイル サーバー (SOFS) に格納されます。 2 番目と同じ記憶域スペース ダイレクト クラスターが 2 つ目の (パッシブ) リージョンにデプロイし、記憶域レプリカはアクティブからパッシブ デプロイにユーザー プロファイルを複製するために使用します。 Azure Traffic Manager を使用して終了する地域のどちらの展開にエンドユーザーが現在アクティブで、エンドユーザーの観点から、1 つの URL を使用して、展開にアクセスしてに対応していないに自動的に出力するために使用されます。


*でした*、各リージョンで非高可用性 RDS デプロイを作成しますが、フェールオーバーが発生すると、1 つのリージョンで 1 つの VM が再起動された場合、フェールオーバーで発生しているが増加する可能性に関連付け、パフォーマンスに影響します。

## <a name="deployment-steps"></a>展開の手順
複数のデータ センターの地理冗長 RDS 展開を作成する Azure で、次のリソースを作成します。

1. 2 つのリソース グループに 2 つの Azure リージョンで区切ります。 たとえば、(RG、アクティブなデプロイは [リソース グループ]) RG A と RG B (パッシブ配置) など。
2. RG A. で Active Directory の高可用性展開使用することができます、 [AD で新しいドメインを 2 つのドメイン コント ローラー テンプレート](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/)展開を作成します。
3. RG A. 使用中の高可用性 RDS デプロイ、 [RDS ファームの既存の active directory を使用してデプロイを](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)、基本的な RDS 展開を作成し、次の情報は、テンプレート[リモート デスクトップ サービス - 高可用性](rds-plan-high-availability.md)高可用性のため、他の RDS のコンポーネントを構成します。
4. RG A の展開を重複しないアドレス空間を使用するように RG b - VNet
5. A [VNet 対 VNet 接続](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)2 つのリソース グループ間で。
6. 2 つの AD 仮想マシンの可用性セット RG B - VM の名前が RG A. デプロイで 1 つの可用性の 2 つの Windows Server 2016 Vm の設定、Active Directory Domain Services の役割をインストール、およびドメインの続きを昇格させることで AD Vm から異なるを確認します。手順 1 で作成したドメインでローラー。
7. RG B の 2 番目の高可用性 RDS デプロイ 
   1. 使用して、 [RDS ファームの既存の active directory を使用してデプロイを](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)テンプレートをもう一度、今度は、次の変更を行います。 (テンプレートをカスタマイズするには、ギャラリーから選択します をクリックして**Deploy to Azure**し**テンプレートの編集**)。
      1. RG B の VNet に対応する DNS サーバーのプライベート IP のアドレス空間を調整します。 
      
         変数に"dnsServerPrivateIp"を検索します。 RG B の VNet で定義したアドレス空間に対応する既定の IP (10.0.0.4) の編集します。
   
      2. RG A の展開とは競合が発生しないように、コンピューター名を編集します。
      
         内の Vm を検索、**リソース**テンプレートのセクション。 変更、 **computerName**フィールド**osProfile**します。 たとえば、「ゲートウェイ」になれる"ゲートウェイ **-b**";"[concat ('rdsh-'、copyIndex())]""[concat ('rdsh-b-'、copyIndex())]"になるし、「ブローカー」になることがあります"ブローカー **-b**"。
      
         (ことも、Vm の名前手動で変更するテンプレートを実行した後です。)
   2. 上の 3 つの手順のように、情報を使用して、[リモート デスクトップ サービスの高可用性](rds-plan-high-availability.md)高可用性のため、他の RDS のコンポーネントを構成します。
8. 記憶域スペース ダイレクト スケール アウト ファイル サーバー記憶域レプリカで複数の 2 つのデプロイ。 使用して、 [PowerShell スクリプト](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts)を展開する、[テンプレート](https://github.com/robotechredmond/301-s2d-sr-dr-md)すべてのリソース グループ。

   > [!NOTE]
   > 手動ではなく、PowerShell スクリプトとテンプレートを使用して) ストレージをプロビジョニングできます。 
   >1. デプロイを[2 つのノードの記憶域スペース ダイレクト SOFS](rds-storage-spaces-direct-deployment.md) RG a のユーザー プロファイル ディスク (Upd) を格納します。
   >2. 2 つ目と同等の記憶域スペース ダイレクト SOFS RG B でを展開する-各クラスター内の同じ量の記憶域を使用してください。
   >3. 設定する[非同期レプリケーションでの記憶域レプリカ](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)2 つの間。

### <a name="enable-upds"></a>Upd を有効にします。
記憶域レプリカは、レプリケーション先のボリューム (セカンダリ/パッシブ デプロイに関連付けられている) にソース ボリューム (プライマリ/アクティブ デプロイに関連付けられている) からデータをレプリケートします。 仕様では、移行先クラスターとして表示されます。**オンライン (アクセスなし)** -記憶域レプリカが、移行先ボリュームとそのドライブ文字またはマウント ポイントをマウント解除します。 つまり、ボリュームがマウントされていないため、ファイル共有のパスを提供することで、セカンダリ デプロイの Upd を有効にするが失敗します。 

レプリケーションの管理についての詳細をしますか。 チェック アウト[クラスター記憶域のレプリケーションを](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)します。

両方のデプロイに Upd を有効にするには、次の操作を行います。

1. 実行、[セット RDSessionCollectionConfiguration コマンドレット](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdsessioncollectionconfiguration)プライマリ (アクティブ) デプロイのユーザー プロファイル ディスクを有効にするには、(手順 7 で作成するには、展開の手順で) がソース ボリュームのファイル共有へのパスを提供します。
2. (このボリュームをマウントおよびセカンダリの展開でアクセスできるように) ソース ボリュームが回復先ボリュームになるように記憶域レプリカの方向を反転します。 実行することができます**Set-srpartnership**これを行うコマンドレット。 例:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. セカンダリ (パッシブ) デプロイでのユーザー プロファイル ディスクを有効にします。 手順 1 で、プライマリ展開の場合と同じ手順を使用します。
4. 方向を反転する記憶域レプリカもう一度、元のソース ボリュームが記憶域レプリカのパートナーシップで、ソース ボリュームで、もう一度と、プライマリ展開は、ファイル共有にアクセスできるようにします。 例:

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager 

作成、 [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview)プロファイル、および選択することを確認、**優先度**ルーティング方法。 2 つのエンドポイントを各展開のパブリック IP アドレスに設定します。 **構成**、(HTTP) ではなく HTTPS ポート (80) ではなく 443 にプロトコルを変更します。 メモ、 **DNS の time to live**、し、フェールオーバーが必要なの適切に設定します。 

Traffic Manager がエンドポイントを「正常」としてマークするために GET 要求に応答-OK 200 を返す必要があります。 RDS テンプレートから作成されたパブリック Ip オブジェクトは、機能しますが、パスの補遺を追加しないでください。 代わりに、ユーザーに提供するエンドで Traffic Manager URL"/RDWeb"など、追加されます。 ```http://deployment.trafficmanager.net/RDWeb```

優先順位によるルーティング方法で Azure Traffic Manager を展開することでは、パッシブ配置へのアクセスのアクティブな展開は機能をエンドユーザーを防止します。 エンドユーザーがパッシブのデプロイメントにアクセスすると、フェールオーバーの記憶域レプリカの方向を切り替えられましたが、ユーザー サインインがハングする、配置しようとパッシブ記憶域スペース ダイレクト クラスターのデプロイでは最終的に上のファイル共有のアクセスに失敗すると諦め、一時的なプロファイルをユーザーに与えます。  

### <a name="deallocate-vms-to-save-resources"></a>リソースを保存する Vm の割り当てを解除します。 
両方のデプロイを構成した後必要に応じてシャット ダウンし、セカンダリの RDS インフラストラクチャとこれらの Vm でのコストを節約する RDSH 仮想マシンの割り当てを解除することができます。 記憶域スペース ダイレクト SOFS と AD サーバー Vm では、ユーザー アカウントとプロファイルの同期を有効にするセカンダリ/パッシブ配置で実行されている必要があります常います。  

フェールオーバーが発生したときに、割り当てが解除された Vm を起動する必要があります。 この配置構成では、フェールオーバー時点で譲歩のコストが小さいという利点があります。 致命的な障害は、アクティブなデプロイで発生する場合は、パッシブの展開を手動で開始する必要があります。 または自動化スクリプトをエラーを検出し、パッシブ配置を自動的に開始する必要があります。 いずれの場合もかかる場合があります実行され、ユーザーがサインインできる、パッシブ配置を取得するのに数分によってサービスのダウンタイムが発生します。 このようなダウンタイムに依存の時間に RDS インフラストラクチャと RDSH 仮想マシン (通常 2 ~ 4 分を並列ではなく連続的には、Vm が起動している場合)、(クラスターのサイズに依存するパッシブ クラスターをオンラインに時間を開始するまで、通常は 2 ノード クラスターのノードごとの 2 つのディスクで 2 ~ 4 分)。 

### <a name="active-directory"></a>Active Directory 
各デプロイ内の Active Directory サーバーは、同じフォレストまたはドメイン内のレプリカです。 Active Directory では、4 つのドメイン コント ローラーの同期を維持する組み込みの同期プロトコルがあります。ただし、1 つの AD サーバーに新しいユーザーを追加する場合は、2 つのデプロイ内のすべての AD サーバー間でレプリケートするまでに時間がかかる場合がありますように、若干の差する可能性があります。 その結果、いないドメインに追加された後すぐにサインインしようとするユーザーに警告することを確認します。 

### <a name="rd-license-server"></a>RD ライセンス サーバー 
提供、[ユーザーごとの RD CAL](rds-client-access-license.md) geo 冗長のデプロイメントにアクセスする権限を持つ名前付きユーザーごとにします。 配布、ユーザーのアクティブなデプロイでは、2 つの RD ライセンス サーバーの間で均等に Cal ごと。 次に、パッシブの展開では、2 つの RD ライセンス サーバーにこれらの Cal が重複しています。 接続するユーザーをアクティブにできる 1 つのみの展開の特定の時点で、アクティブとパッシブの展開の間、Cal が重複しているため、それ以外の場合、使用許諾契約に違反しています。  

### <a name="image-management"></a>イメージの管理 
ソフトウェアの更新プログラムや新しいアプリケーションを提供する、RDSH イメージを更新するときは、両方のデプロイ全体で一般的なユーザー エクスペリエンスを維持するには、各デプロイに RDSH コレクションを個別に更新する必要があります。 使用することができます、 [Update RDSH コレクション テンプレート](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/)テンプレートを実行するパッシブ配置の RDS インフラストラクチャと RDSH 仮想マシンを実行する必要があることに注意してください。 

## <a name="failover"></a>フェールオーバー

場合は、アクティブ/パッシブ配置フェールオーバーはセカンダリ配置の Vm を起動する必要があります。 これは、手動またはオートメーション スクリプトを使用して行うことができます。 記憶域スペース ダイレクト SOFS に壊滅的なフェールオーバーの場合に、ソース ボリュームが回復先ボリュームになるように、記憶域レプリカのパートナーシップの方向を変更します。 次に、例を示します。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

詳細については、[クラスター記憶域のレプリケーションを](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)します。

Azure Traffic Manager は、プライマリ展開が失敗したことと、セカンダリ配置が正常な状態に自動的に認識されます (RD ゲートウェイの Vm 内で開始されている RG B) とセカンダリのデプロイにユーザー トラフィックを転送します。 ユーザーは、同じ Traffic Manager の URL を使用して、一貫したエクスペリエンスを享受、リモートのリソースの操作を続行します。 クライアント DNS キャッシュは Azure Traffic Manager の構成で設定された TTL の間のレコードを更新しないことに注意してください。

### <a name="test-failover"></a>テスト フェールオーバー
記憶域レプリカのパートナーシップで 1 つのボリューム (ソース) を有効にする時間。 つまりを記憶域レプリカのパートナーシップの方向を切り替えた場合にプライマリ展開 (RG A) で、ボリュームは、レプリケーションの対象になります、非表示には、そのため。 したがって、RG A に接続するすべてのユーザーは、RG A. で SOFS 上に格納された Upd へのアクセス 

ログインを続行できるようにしながら、フェールオーバーをテストします。
1. RG B の RDSH 仮想マシンとインフラストラクチャの Vm を開始します。
2. 記憶域レプリカのパートナーシップの方向を切り替える (クラスター b s2d c では、ソース ボリュームになります)。
3. [エンドポイントを無効にする](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint)RG RG B. またはへのトラフィックをダイレクトに ATM を強制するには、Azure Traffic Manager プロファイルに A の PowerShell スクリプトを使用します。

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

RG B がプライマリのアクティブなデプロイではようになりました。 プライマリ展開として RG A に切り替えるには

1. 記憶域レプリカのパートナーシップの方向を切り替える (クラスター、s2d c では、ソース ボリュームになります)。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Azure Traffic Manager プロファイルで RG A のエンドポイントを再度有効にするには。

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA 
   ```

## <a name="considerations-for-on-premises-deployments"></a>オンプレミスの配置に関する考慮事項

オンプレミス デプロイでは、この記事で参照されている Azure クイック スタート テンプレートを使用できませんでした、インフラストラクチャのすべてのロールを手動で実装することができます。 場所コストは、Azure の消費量によって決まりますがない、オンプレミスのデプロイでは、アクティブ/アクティブ モデルを使用して、高速フェールオーバーを検討してください。

Azure Traffic Manager を使用するには、オンプレミスのエンドポイントを持つ Azure サブスクリプションが必要があります。 また、エンドユーザーに提供される dns から付与単にユーザーをプライマリ展開をリダイレクトする CNAME レコードをします。 フェールオーバーの場合は、セカンダリのデプロイにリダイレクトする DNS CNAME レコードを変更します。 この方法で、エンドユーザーと同じように Azure Traffic Manager で、適切な展開をユーザーに指示するに 1 つの URL を使用します。 

オンプレミス-に-Azure のサイトでモデルを作成する場合は、使用を検討[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)します。
