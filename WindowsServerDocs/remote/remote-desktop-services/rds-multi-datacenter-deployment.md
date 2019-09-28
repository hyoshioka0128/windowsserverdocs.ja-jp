---
title: Azure の地理冗長型 RDS データ センター
description: 地理的に離れた複数の場所にわたって高可用性を実現するために、複数のデータ センターを使用した RDS 展開を作成する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 55b96c112dd7f7294ff674ee4675501af4287da4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403960"
---
# <a name="create-a-geo-redundant-multi-data-center-rds-deployment-for-disaster-recovery"></a>ディザスター リカバリー用の地理冗長型複数データ センター RDS 展開の作成

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Azure で複数のデータ センターを活用することにより、リモート デスクトップ サービス展開のディザスター リカバリーを行えるようになります。 1 つの Azure リージョン (西ヨーロッパなど) のデータ センターを使用する標準の高可用性 RDS 展開 (「[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md)」で概説) とは異なり、複数データ センター展開は、地理的に離れた複数の場所にあるデータ センターを使用して、展開の可用性を高めます。1 つの Azure データ センターが使用できなくても、複数のリージョンが同時にダウンする可能性はほとんどありません。 地理冗長型 RDS アーキテクチャを展開することで、リージョン全体に壊滅的な障害が発生した場合に、フェールオーバーを有効にすることができます。

Microsoft Azure インフラストラクチャ サービスおよび RDS を活用して、[マイクロソフトのサービス プロバイダー ライセンス アグリーメント (SPLA) プログラム](https://www.microsoft.com/hosting/licensing/splabenefits.aspx)を通して、地理冗長型デスクトップ ホスティング サービスやサブスクライバー アクセス ライセンス (SAL) を複数のテナントに提供するには、以下の手順を使用します。 以下の手順を使用すると、[ソフトウェア アシュアランスによる RDS ユーザー CAL の拡張された権利](https://download.microsoft.com/download/6/B/A/6BA3215A-C8B5-4AD1-AA8E-6C93606A4CFB/Windows_Server_2012_R2_Remote_Desktop_Services_Licensing_Datasheet.pdf)を使用して、自社従業員向けの地理冗長型ホスティング サービスを作成することもできます。

## <a name="logical-architecture-for-high-availability---single-and-multiple-regions"></a>高可用性の論理アーキテクチャ - 1 つのリージョンと複数のリージョン
次の図は、1 つの Azure リージョンにおける高可用性の展開のアーキテクチャを示しています。

![1 つの Azure リージョンでの高可用性の展開](media/rds-ha-single-region.png)

展開は、3 つの層で構成されます。

- Azure サービス - Azure portal および API を含む Azure 管理インターフェイスと、DNS やパブリック IP アドレス指定などのパブリック ネットワーク サービス。
- デスクトップ ホスティング サービス - 仮想マシン、ネットワーク、記憶域、Azure サービス、および Windows Server の役割サービス
- Azure ファブリック - HYPER-V の役割を実行している Windows Server オペレーティング システム。物理サーバー、記憶域ユニット、ネットワーク スイッチ、およびルーターを仮想化するために使用されます。 Azure ファブリックを使用すると、基になるハードウェアから独立した VM、ネットワーク、記憶域、およびアプリケーションを作成できます。


対照的に、複数の Azure データ センターを使用する展開のアーキテクチャはこのようになります。

![複数の Azure リージョンを使用する RDS 展開](media/rds-ha-multi-region.png)

RDS 展開全体は、地理冗長型の展開を作成するために、2 つ目の Azure リージョンにレプリケートされます。 このアーキテクチャは、一度に 1 つの RDS 展開のみが実行されている、アクティブ/パッシブ モデルを使用しています。 VNet 間接続により、2 つの環境が相互に通信できるようになります。 RDS 展開は、1 つの Active Directory フォレスト/ドメインに基づき、AD サーバーは 2 つの展開全体でレプリケートされます。これは、ユーザーが同じ資格情報を使用してどちらの展開にもサインインできることを意味します。 ユーザー プロファイル ディスク (UPD) に格納されているユーザー設定およびデータは、2 ノード クラスター記憶域スペース ダイレクト スケールアウト ファイル サーバー (SOFS) に格納されます。 2 つ目の同じ記憶域スペース ダイレクト クラスターが 2 つ目の (パッシブ) リージョンに展開されます。記憶域レプリカが使用されて、アクティブからパッシブの展開にユーザー プロファイルがレプリケートされます。 Azure Traffic Manager は、現在アクティブであるいずれかの展開にエンドユーザーを自動的に誘導するために使用されます。エンドユーザーの視点からは、1 つの URL を使用して展開にアクセスしているので、どちらのリージョンを使用しているかはわかりません。


各リージョンに非高可用性 RDS 展開を作成することは "*可能です*" が、1 つのリージョンで 1 つの VM が再起動された場合でもフェールオーバーが発生し、関連するパフォーマンスの影響を伴うフェールオーバーが発生する可能性が高くなります。

## <a name="deployment-steps"></a>展開の手順
地理冗長型の複数データ センター RDS 展開を作成するには、Azure で次のリソースを作成します。

1. 2 つの別個の Azure リージョンにある 2 つのリソース グループ。 たとえば、RG A (アクティブな展開、RG は "リソース グループ" の略) と RG B (パッシブな展開) などです。
2. RG A にある高可用性の Active Directory 展開。[2 つのドメイン コント ローラーを含む新しい AD ドメインのテンプレート](https://azure.microsoft.com/resources/templates/active-directory-new-domain-ha-2-dc/)を使用して、展開を作成できます。
3. RG A にある高可用性 RDS 展開。[既存の Active Directory を使用した RDS ファーム展開](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)のテンプレートを使用して基本的な RDS 展開を作成します。次に、[リモート デスクトップ サービス - 高可用性](rds-plan-high-availability.md)に関する記事の情報に従って、高可用性のためにその他の RDS コンポーネントを構成します。
4. RG B 内の VNet - RG A にある展開と重複しないアドレス空間を使用するようにしてください。
5. 2 つのリソース グループ間の [VNet 間接続](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)。
6. RG B 内の可用性セットにある 2 つの AD 仮想マシン - それらの VM 名が RG A 内の AD VM と異なることを確認します。1 つの可用性セットに 2 つの Windows Server 2016 VM を展開し、Active Directory Domain Services の役割をインストールしてから、手順 1 で作成したドメインのドメイン コントローラーにそれらを昇格させます。
7. RG B 内の 2 つ目の高可用性 RDS 展開。 
   1. [既存の Active Directory を使用した RDS ファーム展開](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/)のテンプレートをもう一度使用しますが、今度は次の変更を行います (テンプレートをカスタマイズするには、ギャラリーでそれを選択し、 **[Azure に配置する]** をクリックしてから、 **[テンプレートの編集]** をクリックします)。
      1. RG B の VNet に対応する DNS サーバーのプライベート IP のアドレス空間を調整します。 
      
         変数内で "dnsServerPrivateIp" を検索します。 RG B の VNet に定義したアドレス空間に対応する既定の IP (10.0.0.4) を編集します。
   
      2. RG A の展開内の名前と競合しないように、コンピューター名を編集します。
      
         テンプレートの **[Resources]** セクションに VM を配置します。 **[osProfile]** の下の **[computerName]** フィールドを変更します。 たとえば、"gateway" は "gateway **-b**"、"[concat('rdsh-', copyIndex())]" は "[concat('rdsh-b-', copyIndex())]"、"broker" は "broker **-b**" にすることができます
      
         (テンプレートを実行した後に、VM の名前を手動で変更することもできます)。
   2. 上記の手順 3 のように、[リモート デスクトップ サービス - 高可用性](rds-plan-high-availability.md)に関する記事の情報を使用して、高可用性のためにその他の RDS のコンポーネントを構成します。
8. 2 つの展開の間で記憶域レプリカを使用する記憶域スペース ダイレクト スケールアウト ファイル サーバー。 [PowerShell スクリプト](https://github.com/robotechredmond/301-s2d-sr-dr-md/tree/master/scripts)を使用して、 リソース グループ全体に[テンプレート](https://github.com/robotechredmond/301-s2d-sr-dr-md)を展開します。

   > [!NOTE]
   > (PowerShell スクリプトとテンプレートを使用する代わりに) 記憶域を手動でプロビジョニングできます。 
   >1. RG A 内で [2 つのノード記憶域スペース ダイレクト SOFS](rds-storage-spaces-direct-deployment.md) を展開して、ユーザー プロファイル ディスク (UPD) を格納します。
   >2. RG B 内で 2 つ目の同じ記憶域スペース ダイレクト SOFS を展開します。各クラスターで同じ容量の記憶域を使用してください。
   >3. 2 つの間で[非同期レプリケーションを使用する記憶域レプリカ](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)を設定します。

### <a name="enable-upds"></a>UPD の有効化
記憶域レプリカは、(プライマリ/アクティブ展開に関連付けられている) ソース ボリュームから (セカンダリ/パッシブ展開に関連付けられている) 宛先ボリュームにデータをレプリケートします。 仕様では、宛先クラスターは **[Online (No Access)]/(オンライン (アクセスなし)/)** と表示されます。記憶域レプリカは、宛先ボリュームと、それらのドライブ文字またはマウント ポイントをマウント解除します。 つまり、そのボリュームがマウントされていないため、ファイル共有パスを指定してセカンダリ展開の UPD の有効化を行うと、失敗します。 

レプリケーションの管理について詳しくは、 「[クラスター間の記憶域のレプリケーション](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)」をご覧ください。

両方の展開で UPD を有効にするには、次の手順を実行します。

1. [Set-RDSessionCollectionConfiguration コマンドレット](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdsessioncollectionconfiguration)を実行して、プライマリ (アクティブ) 展開のユーザー プロファイル ディスクを有効にします。(「展開の手順」の手順 7 で作成した) ソース ボリューム上のファイル共有のパスを指定します。
2. 宛先ボリュームがソース ボリュームになるように、記憶域レプリカの方向を反転します (これにより、そのボリュームがマウントされ、セカンダリ展開がアクセスできるようになります) 。 これを行うには、**Set-SRPartnership** コマンドレットを実行します。 次に、例を示します。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```
3. セカンダリ (パッシブ) 展開のユーザー プロファイル ディスクを有効にします。 手順 1 でプライマリ展開に行った手順と同じ手順を使用します。
4. 記憶域レプリカの方向をもう一度反転します。それにより、元のソース ボリュームが再び SR パートナーシップのソース ボリュームになり、プライマリ展開がファイル共有にアクセスできるようになります。 次に、例を示します。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```


### <a name="azure-traffic-manager"></a>Azure Traffic Manager 

[Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview) プロファイルを作成し、 **[優先順位]** ルーティング方法を必ず選択します。 2 つのエンドポイントを各展開のパブリック IP アドレスに設定します。 **[構成]** で、プロトコルを (HTTP ではなく) HTTPS に変更し、ポートを (80 ではなく) 443 に変更します。 **[DNS time to live]** を確認して、フェールオーバーのニーズに合わせて適切に設定します。 

Traffic Manager では、"正常" としてマークされるためにエンドポイントが GET 要求に応答して 200 OK を返す必要があることに注意してください。 RDS テンプレートから作成された publicIP オブジェクトは機能しますが、パスの補足は追加しないでください。 代わりに、"/RDWeb" を付加した Traffic Manager URL をエンド ユーザーに提供できます。例: ```http://deployment.trafficmanager.net/RDWeb```

優先順位によるルーティング方法を指定した Azure Traffic Manager を展開することで、アクティブな展開が機能している間、エンドユーザーがパッシブ展開にアクセスしないようにします。 エンドユーザーがパッシブ展開にアクセスし、記憶域レプリカの方向がフェールオーバー用に切り替えられていない場合、展開でパッシブ記憶域スペース ダイレクト クラスターのファイル共有へのアクセスを試行して失敗するため、ユーザーのサインインがハングします。最終的にその展開は中断し、一時的なプロファイルをユーザーに提供します。  

### <a name="deallocate-vms-to-save-resources"></a>リソースを節約するために VM の割り当てを解除する 
両方の展開を構成した後、必要に応じてセカンダリ RDS インフラストラクチャと RDSH VM をシャット ダウンして、割り当てを解除し、これらの VM でのコストを節約することができます。 ユーザー アカウントとプロファイルの同期を有効にするには、記憶域スペース ダイレクト SOFS と AD サーバー VM がセカンダリ/パッシブ展開で常に実行されている必要があります。  

フェールオーバーが発生したとき、割り当てが解除された VM を起動する必要があります。 この展開構成には低コストという利点がありますが、フェールオーバーに時間がかかります。 アクティブな展開で破壊的な障害が発生した場合は、パッシブ展開を手動で開始するか、障害を検出してパッシブ展開を自動的に開始する自動化スクリプトが必要になります。 いずれの場合も、パッシブ展開を稼働させてユーザーがサインインできるようにするのに数分かかる可能性があり、サービスのダウンタイムが発生することになります。 このダウンタイムは、RDS インフラストラクチャと RDSH VM の起動にかかる時間 (VM が順次ではなく並列で起動された場合、通常は 2 分から 4 分) と、パッシブ クラスターをオンラインにするのにかかる時間 (クラスターのサイズによりますが、 ノードごとに 2 つのディスクがある 2 ノード クラスターの場合、通常、2 分から 4 分) によって異なります。 

### <a name="active-directory"></a>Active Directory 
各展開内の Active Directory サーバーは、同じフォレスト/ドメイン内のレプリカです。 Active Directory には、4 つのドメイン コント ローラーの同期を維持する組み込みの同期プロトコルがあります。ただし、多少遅延する場合があるので、新しいユーザーを 1 つの AD サーバーに追加すると、2 つの展開内のすべての AD サーバーにわたってレプリケートするのに多少時間がかかる可能性があります。 したがって、ドメインに追加された直後にサインインを試みないようにユーザーに警告してください。 

### <a name="rd-license-server"></a>RD ライセンス サーバー 
地理冗長型の展開にアクセスする権限を持つ名指定ユーザーに、[ユーザーごとの RD CAL](rds-client-access-license.md) を提供してください。 アクティブな展開内の 2 つの RD ライセンス サーバー間で、ユーザーごとの CAL を均等に配布します。 次に、パッシブ展開内の 2 つの RD ライセンス サーバーにこれらの CAL を複製します。 CAL はアクティブとパッシブの展開の間で複製されるため、ユーザーの接続でアクティブにできる展開は常に 1 つだけです。それ以外の場合は、使用許諾契約に違反します。  

### <a name="image-management"></a>イメージの管理 
ソフトウェアの更新プログラムや新しいアプリケーションを提供するために RDSH イメージを更新する場合は、両方の展開全体で共通のユーザー エクスペリエンスを維持するために、各展開で RDSH コレクションを個別に更新する必要があります。 [RDSH コレクションの更新のテンプレート](https://azure.microsoft.com/resources/templates/rds-update-rdsh-collection/)を使用できますが、テンプレートを実行するには、パッシブ展開の RDS インフラストラクチャと RDSH VM が実行されている必要があることに注意してください。 

## <a name="failover"></a>フェールオーバー

アクティブ/パッシブ展開の場合は、フェールオーバーでセカンダリ展開の VM を起動する必要があります。 これは、手動で行うことも、自動化スクリプトを使用して行うこともできます。 記憶域スペース ダイレクト SOFS の壊滅的なフェールオーバーの場合は、記憶域レプリカのパートナーシップの方向を変更して、宛先ボリュームがソース ボリュームになるようにします。 次に、例を示します。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-b-s2d-c" -SourceRGName "cluster-b-s2d-c" -DestinationComputerName "cluster-a-s2d-c" -DestinationRGName "cluster-a-s2d-c"
   ```

詳細については、「[クラスター間の記憶域のレプリケーション](../../storage/storage-replica/cluster-to-cluster-storage-replication.md)」をご覧ください。

Azure Traffic Manager は、プライマリ展開で障害が発生したことと、セカンダリ展開が正常である (RD ゲートウェイ内で VM が RG B で起動されている) ことを自動的に認識し、セカンダリ展開にユーザー トラフィックを誘導します。 ユーザーは、同じ Traffic Manager URL を使用して各自のリモート リソースの操作を続行でき、一貫したエクスペリエンスを利用できます。 Azure Traffic Manager の構成で設定された TTL の間はクライアント DNS キャッシュでレコードが更新されないことに留意してください。

### <a name="test-failover"></a>テスト フェールオーバー
記憶域レプリカのパートナーシップでは、一度に 1 つのボリューム (ソース) のみをアクティブにできます。 つまり、SR パートナーシップの方向を切り替えると、プライマリ展開 (RG A) 内のボリュームがレプリケーションの宛先になるため、非表示になります。 したがって、RG A に接続するすべてのユーザーは、RG A 内の SOFS 上に格納された UPD にアクセスできなくなります。 

ユーザーが引き続きログインできるようにしながらフェールオーバーをテストするには:
1. RG B 内のインフラストラクチャ VM と RDSH VM を起動します。
2. SR パートナーシップの方向を切り替えます (cluster-b-s2d-c がソース ボリュームになります)。
3. Azure Traffic Manager プロファイル内の RG A の[エンドポイントを無効にして](/azure/traffic-manager/traffic-manager-manage-endpoints#to-disable-an-endpoint)、RG B にトラフィックを誘導するように ATM を強制します。あるいは、PowerShell スクリプトを使用します。

   ```powershell
   Disable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA -Force
   ```

これで、RG B がアクティブなプライマリ展開になりました。 プライマリ展開として RG A にもう一度切り替えるには:

1. SR パートナーシップの方向を切り替えます (cluster-a-s2d-c がソース ボリュームになります)。

   ```powershell
   Set-SRPartnership -NewSourceComputerName "cluster-a-s2d-c" -SourceRGName "cluster-a-s2d-c" -DestinationComputerName "cluster-b-s2d-c" -DestinationRGName "cluster-b-s2d-c"
   ```
2. Azure Traffic Manager プロファイル内の RG A のエンドポイントを再度有効にするには:

   ```powershell
   Enable-AzureRmTrafficManagerEndpoint -Name publicIpA -Type AzureEndpoints -ProfileName MyTrafficManagerProfile -ResourceGroupName RGA 
   ```

## <a name="considerations-for-on-premises-deployments"></a>オンプレミス展開に関する考慮事項

オンプレミス展開では、この記事で参照されている Azure クイック スタート テンプレートを使用することはできませんが、すべてのインフラストラクチャ役割を手動で実装することはできます。 Azure の使用によってコストが左右されないオンプレミス展開では、フェールオーバーを高速化するためにアクティブ/アクティブ モデルの使用を検討してください。

オンプレミスのエンドポイントで Azure Traffic Manager を使用できますが、Azure サブスクリプションが必要です。 または、エンドユーザーに提供される DNS については、ユーザーを単純にプライマリ展開に誘導する CNAME レコードをエンドユーザーに提供します。 フェールオーバーの場合は、DNS CNAME レコードを変更して、セカンダリ展開にリダイレクトするようにしてください。 このようにして、エンドユーザーは、Azure Traffic Manager を使用するときと同じように、1 つの URL を使用してユーザーを適切な展開に誘導します。 

on-premises-to-Azure-site モデルの作成に関心がある場合は、[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) の使用を検討してください。
