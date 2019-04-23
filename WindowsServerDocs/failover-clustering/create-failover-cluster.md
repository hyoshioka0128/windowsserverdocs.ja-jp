---
title: フェールオーバー クラスターを作成する
description: Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 フェールオーバー クラスターを作成する方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f919e69488c4f2272ddd07e535ba4e2248ddf79c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843293"
---
# <a name="create-a-failover-cluster"></a>フェールオーバー クラスターを作成する

>適用対象:Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

このトピックでは、フェールオーバー クラスター マネージャー スナップインまたは Windows PowerShell を使用してフェールオーバー クラスターを作成する方法について説明します。 このトピックは、Active Directory ドメイン サービス (AD DS) でクラスターおよび関連するクラスター化された役割のコンピューター オブジェクトを作成する一般的な展開を対象としています。 記憶域スペース ダイレクト クラスターをデプロイする場合が代わりに参照してください[記憶域スペース ダイレクトの展開](../storage/storage-spaces/deploy-storage-spaces-direct.md)します。

Active Directory からデタッチされたクラスターをデプロイすることもできます。 この展開方法を使用すると、AD DS でコンピューター オブジェクトを作成するための権限を要求したり、AD DS でコンピューター オブジェクトがプレステージされるように要求したりしなくても、フェールオーバー クラスターを作成できます。 この方法は Windows PowerShell のみで使用でき、特定のシナリオのみに対して推奨されます。 詳細については、「 [Deploy an Active Directory-Detached Cluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))」を参照してください。

#### <a name="checklist-create-a-failover-cluster"></a>チェックリスト:フェールオーバー クラスターを作成する

|状況|タスク|リファレンス|
|:---:|---|---|
|☐|前提条件を検証する|[前提条件を確認します。](#verify-the-prerequisites)|
|☐|クラスター ノードとして追加する各サーバーにフェールオーバー クラスタリング機能をインストールする|[フェールオーバー クラスタ リング機能をインストールします。](#install-the-failover-clustering-feature)|
|☐|クラスター検証ウィザードを実行して構成を検証する|[構成を検証します。](#validate-the-configuration)|
|☐|クラスターの作成ウィザードを実行してフェールオーバー クラスターを作成する|[フェールオーバー クラスターを作成します。](#create-the-failover-cluster)|
|☐|クラスター化された役割を作成してクラスター ワークロードをホストする|[クラスター化された役割を作成します。](#create-clustered-roles)|

## <a name="verify-the-prerequisites"></a>前提条件を検証する

開始する前に、次の前提条件を検証します。

- クラスター ノードとして追加するすべてのサーバーで同じバージョンの Windows Server が実行されていることを確認します。
- ハードウェア要件を確認し、目的の構成がサポートされていることを確認します。 詳細については、「[フェールオーバー クラスタリングのハードウェア要件と記憶域オプション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj612869(v%3dws.11))」を参照してください。 記憶域スペース ダイレクト クラスターを作成する場合は、次を参照してください。[記憶域スペース ダイレクトのハードウェア要件](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)します。
- クラスターの作成中にクラスター化された記憶域を追加するには、すべてのサーバー、記憶域にアクセスできることを確認します。 (クラスターの作成後にクラスター化された記憶域を追加することもできます)。
- クラスター ノードとして追加するすべてのサーバーが同じ Active Directory ドメインに参加していることを確認します。
- (オプション) 組織単位 (OU) を作成し、クラスター ノードとして追加するサーバーのコンピューター アカウントを OU に移動します。 ベスト プラクティスとして、フェールオーバー クラスターを AD DS で専用の OU に配置することをお勧めします。 これにより、クラスター ノードに影響を及ぼすグループ ポリシー設定またはセキュリティ テンプレート設定をより細かく制御できるようになります。 また、クラスターを専用の OU に分離することによって、クラスターのコンピューター オブジェクトが誤って削除されるのを防ぐことができます。

さらに、次のアカウント要件を確認します。

- クラスターを作成するために使用するアカウントが、クラスター ノードとして追加するすべてのサーバーに対する管理者権限を持つドメイン ユーザーであることを確認します。
- 次のいずれかに該当することを確認します。
    - クラスターを作成するユーザーが、OU に対して、またはクラスターを形成するサーバーが存在するコンテナーに対して、**コンピューター オブジェクトを作成する**権限を持っている。
    - **コンピューター オブジェクトを作成する**権限を持っていない場合、クラスターのコンピューター オブジェクトをプレステージするようにドメイン管理者に依頼している。 詳細については、「[Active Directory ドメイン サービスでクラスター コンピューター オブジェクトをプレステージする](prestage-cluster-adds.md)」を参照してください。

>[!NOTE]
>この要件は、Windows Server 2012 R2 で Active Directory からデタッチされたクラスターを作成する場合に適用されません。 詳細については、「 [Deploy an Active Directory-Detached Cluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))」を参照してください。

## <a name="install-the-failover-clustering-feature"></a>フェールオーバー クラスター機能をインストールする

フェールオーバー クラスター ノードとして追加する各サーバーにフェールオーバー クラスタリング機能をインストールする必要があります。

### <a name="install-the-failover-clustering-feature"></a>フェールオーバー クラスター機能をインストールする

1. サーバー マネージャーを起動します。
2. **管理**メニューの **追加の役割と機能の**します。
3. **開始する前に**] ページで、[**次**します。
4. **インストールの種類を選択します。**  ページで **役割ベースまたは機能ベースのインストール**、し、 **次へ**。
5. **対象サーバーの選択**、機能をインストールし、選択するサーバーの選択 ページで、**次**します。
6. **サーバーの役割の選択**ページで、選択**次**します。
7. **[機能の選択]** ページで、**[フェールオーバー クラスタリング]** チェック ボックスをオンにします。
8. フェールオーバー クラスターの管理ツールをインストールするには、選択**機能の追加**、し、**次**します。
9. **インストール オプションの確認**] ページで、[**インストール**します。
<br>フェールオーバー クラスタリング機能の場合はサーバーの再起動は必要ありません。

10. インストールが完了したら、選択**閉じる**します。
11. フェールオーバー クラスター ノードとして追加する各サーバーに対してこの手順を繰り返します。

>[!NOTE]
>フェールオーバー クラスタリング機能をインストールしたら、Windows Update から最新の更新プログラムを適用することをお勧めします。 また、Windows Server 2012 ベースのフェールオーバー クラスターでは、次のように確認します。、[プログラムと Windows Server 2012 ベースのフェールオーバー クラスターの更新プログラムをお勧めします](https://support.microsoft.com/help/2784261/recommended-hotfixes-and-updates-for-windows-server-2012-based-failove)Microsoft サポート記事と、適用される更新プログラムをインストールします。

## <a name="validate-the-configuration"></a>構成を検証する

フェールオーバー クラスターを作成する前に、構成を検証して、ハードウェアおよびハードウェア設定がフェールオーバー クラスタリングに適していることを確認することを強くお勧めします。 Microsoft では、構成全体がすべての検証テストに合格し、すべてのハードウェアがクラスター ノードで実行されている Windows Server バージョン用として認定されている場合にのみ、クラスター ソリューションをサポートします。

>[!NOTE]
>すべてのテストを実行するには、少なくとも 2 つのノードが必要です。 ノードが 1 つしか存在しない場合、重要な記憶域テストの多くが実行されません。

### <a name="run-cluster-validation-tests"></a>クラスター検証テストを実行します。

1. リモート サーバー管理ツールからフェールオーバー クラスター管理ツールをインストールしたコンピューター、またはフェールオーバー クラスタリング機能をインストールしたサーバーで、フェールオーバー クラスター マネージャーを起動します。 サーバーにサーバー マネージャーを起動し、**ツール**メニューの **フェールオーバー クラスター マネージャー**します。
2. **フェールオーバー クラスター マネージャー**  ウィンドウで、**管理**を選択します**構成の検証**です。
3. **開始する前に**] ページで、[**次**します。
4. **またはクラスターのサーバーの選択**ページで、**名前の入力**ボックス、NetBIOS 名またはフェールオーバー クラスター ノードとして追加する予定のサーバーの完全修飾ドメイン名を入力し、 **追加**します。 追加するサーバーごとに、この手順を繰り返します。 一度に複数のサーバーを追加するには、名前をコンマまたはセミコロンで区切って入力します。 たとえば、 *server1.contoso.com, server2.contoso.com*という形式で入力します。 完了したら、選択**次**します。
5. **テスト オプション** ページで、 **(推奨) すべてのテストを実行**、し、**次**します。
6. **確認**] ページで、[**次**します。

    検証ページに、実行されているテストのステータスが表示されます。
7. **[概要]** ページで、次のいずれかの操作を実行します。
    
      - 結果を示すこと、テストが正常に完了し、構成がクラスタ リング、適してし、すぐに、クラスターを作成する場合、以下のことを確認、**今すぐ検証されたノードを使用してクラスターを作成する**チェックボックスがオンの場合、**完了**します。 次に、「 [フェールオーバー クラスターを作成する](#create-the-failover-cluster) 」の手順 4 に進みます。
      - 結果は、警告またはエラーがあることを示しの場合は、選択**レポートの表示**詳細を表示し、問題を修正する必要がありますを特定します。 特定の検証テストで警告が発生した場合、フェールオーバー クラスターのこの面はサポートされるものの、推奨されるベスト プラクティスを満たしていない可能性があります。
        
        >[!NOTE]
        >記憶域の永続的な予約の検証テストで警告が発生した場合は、ブログ記事「 [Windows フェールオーバー クラスター検証の警告でディスクが記憶域の永続的な予約をサポートしていないことが示された場合](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) 」を参照してください。

ハードウェア検証テストの詳細については、「[フェールオーバー クラスター用ハードウェアを検証する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)」を参照してください。

## <a name="create-the-failover-cluster"></a>フェールオーバー クラスターを作成する

この手順を完了するには、ログオンに使用するユーザー アカウントが、このトピックの「[前提条件を検証する](#verify-the-prerequisites)」セクションで説明した要件を満たしている必要があります。

1. サーバー マネージャーを起動します。
2. **ツール**メニューの **フェールオーバー クラスター マネージャー**します。
3. **フェールオーバー クラスター マネージャー**  ウィンドウで、**管理**を選択します**クラスターの作成**です。
    
    クラスターの作成ウィザードが表示されます。
4. **開始する前に**] ページで、[**次**します。
5. 場合、**サーバーの選択**でページが表示されます、**名前の入力**ボックス、NetBIOS 名またはフェールオーバー クラスター ノードとして追加する予定のサーバーの完全修飾ドメイン名を入力し、 **追加**します。 追加するサーバーごとに、この手順を繰り返します。 一度に複数のサーバーを追加するには、名前をコンマまたはセミコロンで区切って入力します。 たとえば、 *server1.contoso.com; server2.contoso.com*という形式で入力します。 完了したら、選択**次**します。
    
    >[!NOTE]
    >検証を実行した後にクラスターを作成した場合、[構成プロシージャの検証](#validate-the-configuration)は表示されません、**サーバーの選択**ページ。 検証済みのノードはクラスターの作成ウィザードに自動的に追加されるため、それらをもう一度入力する必要はありません。
6. 検証を省略した場合、**[検証の警告]** ページが表示されます。 クラスター検証を実行することを強くお勧めします。 Microsoft によってサポートされるのは、すべての検証テストに合格したクラスターのみです。 検証テストを実行する次のように選択します。**はい**、し、**次**。 」の説明に従って、構成の検証ウィザードを完了[構成を検証する](#validate-the-configuration)します。
7. **[クラスター管理用のアクセス ポイント]** ページで、次の手順に従います。
    
    1. **[クラスター名]** ボックスに、クラスターを管理するために使用する名前を入力します。 この操作の前に、次の情報を参照してください。
        
          - クラスターの作成中に、この名前はクラスター コンピューター オブジェクト ( *クラスター名オブジェクト* または *CNO*とも呼ぶ) として AD DS に登録されます。 クラスターの NetBIOS 名を指定した場合、CNO はクラスター ノードのコンピューター オブジェクトが存在する場所に作成されます。 これは既定のコンピューター コンテナーまたは OU です。
          - CNO 用として別の場所を指定するには、OU の識別名を **[クラスター名]** ボックスに入力します。 例:*CN=ClusterName, OU=Clusters, DC=Contoso, DC=com*.
          - ドメイン管理者が CNO をクラスター ノードが存在する場所とは異なる OU にプレステージした場合は、ドメイン管理者が指定する識別名を指定します。
    2. DHCP を使用するように構成されているネットワーク アダプターがサーバーに存在しない場合は、フェールオーバー クラスター用として 1 つ以上の静的 IP アドレスを構成する必要があります。 クラスター管理用に使用する各ネットワークの隣にあるチェック ボックスをオンにします。 選択、**アドレス**、選択したネットワークの横にあるフィールドし、クラスターに割り当てる IP アドレスを入力します。 この IP アドレス (1 つまたは複数) は、ドメイン ネーム システム (DNS) でクラスター名に関連付けられます。
    3. 完了したら、選択**次**します。
8. **[確認]** ページで、設定を確認します。 既定では、 **[使用可能な記憶域をすべてクラスターに追加する]** チェック ボックスがオンになっています。 次のいずれかの場合は、このチェック ボックスをオフにします。
    
      - 記憶域を後で構成する。
      - クラスター化された記憶域スペースをフェールオーバー クラスター マネージャーまたはフェールオーバー クラスタリング Windows PowerShell コマンドレットで作成する予定であり、ファイル サービスおよび記憶域サービスで記憶域スペースをまだ作成していない。 詳細については、「 [Deploy Clustered Storage Spaces](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)」を参照してください。
9. 選択**次**フェールオーバー クラスターを作成します。
10. **[概要]** ページで、フェールオーバー クラスターが正常に作成されたことを確認します。 警告またはエラーがあった、概要ページの出力や選択を表示**レポートの表示**完全なレポートを表示します。 **[完了]** を選択します。
11. クラスターが作成されたことを確認するには、クラスター名がナビゲーション ツリーの **[フェールオーバー クラスター マネージャー]** の下に表示されていることを確認します。 クラスター名を展開して、下にある項目を選択し、**ノード**、**ストレージ**または**ネットワーク**に関連付けられているリソースを表示します。
    
    DNS でクラスター名が正常にレプリケートされるまで若干の時間がかかる場合があります。 DNS の登録に成功したと選択した場合のレプリケーション後**すべてのサーバー**サーバー マネージャーで、クラスター名を持つサーバーとして表示されるはずの**管理の容易性**の状態**オンライン**.

クラスターが作成されたら、クラスター クォーラムの構成などの操作を実行し、必要に応じてクラスターの共有ボリューム (CSV) を作成できます。 詳細については、次を参照してください。[記憶域スペース ダイレクトでのクォーラムの理解](../storage/storage-spaces/understand-quorum.md)と[Use Cluster Shared Volumes フェールオーバー クラスターで](failover-cluster-csvs.md)します。

## <a name="create-clustered-roles"></a>クラスターの役割を作成する

フェールオーバー クラスターを作成したら、クラスター化された役割を作成してクラスター ワークロードをホストできます。

>[!NOTE]
>クラスター化された役割でクライアント アクセス ポイントが必要な場合は、仮想コンピューター オブジェクト (VCO) が AD DS で作成されます。 既定では、クラスターのすべての VCO は同じコンテナーまたは OU に CNO として作成されます。 クラスターの作成後に、CNO を任意の OU に移動できます。

クラスター化された役割を作成する方法を次に示します。

1. サーバー マネージャーまたは Windows PowerShell を使用して、クラスター化された役割に必要な役割または機能を各フェールオーバー クラスター ノードにインストールします。 たとえば、クラスター化されたファイル サーバーを作成する場合は、ファイル サーバーの役割をすべてのクラスター ノードにインストールします。
    
    次の表に、高可用性ウィザードで構成できるクラスター化された役割と、前提条件としてインストールする必要がある関連するサーバーの役割または機能を示します。
    
    <table>
    <thead>
    <tr class="header">
    <th>クラスター化された役割</th>
    <th>役割または機能の前提条件</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>DFS 名前空間サーバー</td>
    <td>DFS 名前空間 (ファイル サーバーの役割の一部)</td>
    </tr>
    <tr class="even">
    <td>DHCP サーバー</td>
    <td>DHCP サーバーの役割</td>
    </tr>
    <tr class="odd">
    <td>分散トランザクション コーディネーター (DTC)</td>
    <td>なし</td>
    </tr>
    <tr class="even">
    <td>ファイル サーバー</td>
    <td>ファイル サーバーの役割</td>
    </tr>
    <tr class="odd">
    <td>汎用アプリケーション</td>
    <td>該当なし</td>
    </tr>
    <tr class="even">
    <td>汎用スクリプト</td>
    <td>該当なし</td>
    </tr>
    <tr class="odd">
    <td>汎用サービス</td>
    <td>該当なし</td>
    </tr>
    <tr class="even">
    <td>Hyper-V レプリカ ブローカー</td>
    <td>Hyper-V の役割</td>
    </tr>
    <tr class="odd">
    <td>iSCSI ターゲット サーバー</td>
    <td>iSCSI ターゲット サーバー (ファイル サーバーの役割の一部)</td>
    </tr>
    <tr class="even">
    <td>iSNS サーバー</td>
    <td>iSNS サーバー サービスの機能</td>
    </tr>
    <tr class="odd">
    <td>メッセージ キューイング (Message Queuing)</td>
    <td>メッセージ キュー サービスの機能</td>
    </tr>
    <tr class="even">
    <td>他のサーバー</td>
    <td>なし</td>
    </tr>
    <tr class="odd">
    <td>仮想マシン</td>
    <td>Hyper-V の役割</td>
    </tr>
    <tr class="even">
    <td>WINS サーバー</td>
    <td>WINS サーバーの機能</td>
    </tr>
    </tbody>
    </table>
2. フェールオーバー クラスター マネージャーでクラスター名を展開し、右クリックして**ロール**、し、**役割の構成**します。
3. 高可用性ウィザードの手順に従って、クラスター化された役割を作成します。
4。 クラスター化された役割が作成されたことを検証するには、 **[役割]** ウィンドウで、役割の状態が **[実行中]** であることを確認します。 [役割] ウィンドウには、所有者ノードも表示されます。 フェールオーバーをテストするには、ロールを右クリックして**移動**、し、 **ノードの**します。 **クラスター化された役割の移動**ダイアログ ボックスで、目的のクラスター ノードを選択し、 **OK**します。 **[所有者ノード]** 列で、所有者ノードが変更されたことを確認します。

## <a name="create-a-failover-cluster-by-using-windows-powershell"></a>Windows PowerShell を使用してフェールオーバー クラスターをインストールする

次の Windows PowerShell コマンドレットは、このトピックで前の手順と同じ機能を実行します。 1 行ずつ各コマンドレットを入力します。書式上の制約から複数行に改行されて表示される場合もあります。

>[!NOTE]
>Windows PowerShell を使用して、Windows Server 2012 R2 で Active Directory からデタッチされたクラスターを作成する必要があります。 詳細については、「[Active Directory からデタッチされたクラスターを展開する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))」を参照してください。

次の例では、フェールオーバー クラスター機能をインストールします。

```PowerShell
Install-WindowsFeature –Name Failover-Clustering –IncludeManagementTools
```

次の例では、 *Server1* および *Server2*という名前のコンピューターですべてのクラスター検証テストを実行します。

```PowerShell
Test-Cluster –Node Server1, Server2
```

>[!NOTE]
>**Test-cluster**コマンドレットは、現在の作業ディレクトリ内のログ ファイルに結果を出力します。 例:C:\Users\<username > \AppData\Local\Temp します。

次の例では、 *Server1* および *Server2* というノードを持つ *MyCluster*という名前のフェールオーバー クラスターを作成し、静的 IP アドレス *192.168.1.12*を割り当て、使用可能な記憶域をすべてフェールオーバー クラスターに追加します。

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12
```

次の例では、前の例と同じフェールオーバー クラスターを作成しますが、使用可能な記憶域を追加しません。

```PowerShell
New-Cluster –Name MyCluster –Node Server1, Server2 –StaticAddress 192.168.1.12 -NoStorage
```

次の例では、 *MyCluster* という名前のクラスターをドメイン *Contoso.com* の *Cluster*OU に作成します。

```PowerShell
New-Cluster -Name CN=MyCluster,OU=Cluster,DC=Contoso,DC=com -Node Server1, Server2
```

クラスター化された役割を追加する方法の例については、「 [Add-ClusterFileServerRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clusterfileserverrole?view=win10-ps) 」や「 [Add-ClusterGenericApplicationRole](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergenericapplicationrole?view=win10-ps)」などのトピックを参照してください。

## <a name="more-information"></a>詳細情報

  - [フェールオーバー クラスタ リング](failover-clustering.md)
  - [HYPER-V クラスターをデプロイします。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj863389(v%3dws.11)>)
  - [アプリケーション データ用のスケール アウト ファイル サーバー](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831349(v%3dws.11)>)
  - [Active Directory からデタッチされたクラスターをデプロイします。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265970(v=ws.11))
  - [ゲスト クラスタ リングの高可用性を使用します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)
  - [クラスター対応更新](cluster-aware-updating.md)
  - [新しいクラスター](https://docs.microsoft.com/powershell/module/failoverclusters/new-cluster?view=win10-ps)
  - [テスト クラスター](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)
