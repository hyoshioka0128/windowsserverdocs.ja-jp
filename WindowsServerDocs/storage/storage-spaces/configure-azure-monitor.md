---
title: 理解し、Azure Monitor の構成
description: Azure Monitor の概要と Windows Server 2016 および 2019 で、記憶域スペース ダイレクト クラスター用の電子メールと sms アラートを構成する方法の詳細設定します。
keywords: 記憶域スペース ダイレクト、azure の監視、通知、電子メール、sms
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 908e4a7a75606905caebfa4b79168b3976982e6d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447595"
---
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Azure Monitor を使用して、ヘルス サービスの障害の電子メールを送信するには

>適用対象:Windows Server 2019、Windows Server 2016

Azure Monitor の収集、分析、クラウドからのテレメトリに作用する包括的なソリューションを提供することにより、可用性と、アプリケーションのパフォーマンスを最大化し、オンプレミス環境にします。 アプリケーションを実行する方法について説明し、しに依存しているリソースに影響する問題を事前に識別します。

これは、オンプレミス ハイパー コンバージド クラスター用に特に便利です。 統合された Azure monitor で、電子メール、テキスト (SMS)、およびクラスターで (または収集されたデータに基づくその他のいくつかのアクティビティにフラグを設定する場合) に問題がある場合に ping を実行するには、他のアラートを構成することになります。 次には Azure Monitor のしくみ、Azure Monitor をインストールする方法、および通知を送信するように構成する方法を簡単に説明しましたが。


## <a name="understanding-azure-monitor"></a>Azure Monitor を理解します。

Azure Monitor によって収集されたすべてのデータが 2 つの基本的な型のいずれかに適合: メトリックとログ。

1. [メトリック](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collection#metrics)は時間で特定の時点のシステムの一部の側面を表す数値。 軽量でリアルタイムに近いシナリオをサポートします。 Azure Monitor 右側で、Azure portal の [概要] ページで収集されたデータが表示されます。

![メトリックス エクスプ ローラーでのメトリックの取り込みの画像](media/configure-azure-monitor/metrics.png)

2. [ログ](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collection#logs)さまざまな種類の異なる種類ごとにプロパティのセットを持つレコードに編成されたデータを含めることができます。 イベントやトレースなどのテレメトリとして格納されますログさらにパフォーマンス データをすべて組み合わせることができます分析できるようにします。 Azure Monitor によって収集されたログ データを使用して分析することができます[クエリ](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview)すばやく取得し、統合、および、収集されたデータを分析します。 作成してテストを使用してクエリ[Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/portals) 、Azure portal といずれかから直接これらのツールを使用してデータを分析またはで使用するためのクエリを保存[視覚化](https://docs.microsoft.com/en-us/azure/azure-monitor/visualizations)または[アラートルール](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-overview)します。

![ログの log analytics での取り込みの画像](media/configure-azure-monitor/logs.png)

これらのアラートを構成する方法の詳細については以下が。

## <a name="configuring-health-service"></a>ヘルス サービスの構成

行う必要がある最初の処理は、クラスターの構成です。 、ご想像どおり、[ヘルス サービス](../../failover-clustering/health-service-overview.md)日常的な監視と記憶域スペース ダイレクトを実行するクラスターの運用エクスペリエンスが向上します。 

上記のとおり、Azure Monitor は、クラスター内で実行されている各ノードからログを収集します。 そのため、ヘルス サービスがイベント チャネルへの書き込みを構成しなければなりません。

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

ヘルス サービスを構成するには、次の操作を実行します。

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

書き込まれるを開始するイベントが発生する正常性の設定を設定する上記のコマンドレットを実行すると、 *Microsoft-Windows-正常性/運用*イベント チャネル。

## <a name="configuring-log-analytics"></a>Log Analytics を構成します。

セットアップ、クラスターで適切なログ記録、次の手順がある log analytics を適切に構成します。

概要、 [Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/agent-windows)詳細な分析と相関のための 1 つのリポジトリにデータ センターまたは他のクラウド環境で物理または仮想 Windows コンピューターから直接データを収集できます。

サポートされる構成については、確認[サポートされている Windows オペレーティング システム](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)と[ネットワーク ファイアウォール構成](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)します。

Azure サブスクリプションを持っていない場合は、作成、[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)開始する前にします。

### <a name="login-in-to-azure-portal"></a>Azure Portal にログイン

Azure portal にログイン[ https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)します。

### <a name="create-a-workspace"></a>ワークスペースを作成します。

以下の手順について詳しくは、次を参照してください。、 [Azure Monitor のドキュメント](https://docs.microsoft.com/en-us/azure/azure-monitor/learn/quick-collect-windows-computer)します。

1. Azure portal のをクリックして**すべてのサービス**します。 リソースの一覧で、入力**Log Analytics**します。 一覧がフィルター処理は、入力に基づくように入力を開始します。 選択**Log Analytics**します。<br><br> 

   ![Azure portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. をクリックして**作成**、次の項目の選択肢を選択します。

   * 新しい名前を付けます**Log Analytics ワークスペース**など*DefaultLAWorkspace*します。 
   * 選択、**サブスクリプション**既定の選択が適切でない場合は、ドロップダウン リストから選択してリンクします。
   * **リソース グループ**、1 つまたは複数の Azure 仮想マシンを含む既存のリソース グループを選択します。 <br><br>

      ![Log Analytics リソース ブレードを作成します。](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. 必要な情報を入力したら、 **Log Analytics ワークスペース**ウィンドウで、をクリックして**OK**します。  

情報の検証であり、ワークスペースを作成、進行状況を追跡できます**通知** メニューから。 

### <a name="obtain-workspace-id-and-key"></a>ワークスペース ID とキーを取得します。
ワークスペース ID とキーが必要、Microsoft 監視エージェントの Windows をインストールする前に、Log Analytics ワークスペース。  この情報は、適切にエージェントを構成し、Log Analytics と正常に通信できることを確認するには、セットアップ ウィザードで必要です。  

1. Azure portal のをクリックして**すべてのサービス**左上隅にあります。 リソースの一覧で、入力**Log Analytics**します。 一覧がフィルター処理は、入力に基づくように入力を開始します。 選択**Log Analytics**します。
2. Log Analytics ワークスペースの一覧、選択*DefaultLAWorkspace*以前に作成します。
3. 選択**詳細設定**します。<br><br> ![Log Analytics の詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. 選択**接続されたソース**、し、 **Windows サーバー**します。   
5. 値の右側に**ワークスペース ID**と**主キー**します。 両方を一時的に保存 - コピーして、両方の好みのエディターに貼り付けます。   

## <a name="installing-the-agent-on-windows"></a>Windows にエージェントをインストールします。
次の手順では、インストールし、Microsoft Monitoring Agent を構成します。 **クラスター内の各サーバーにこのエージェントをインストールし、エージェントを Windows の起動時に実行することを指定してください。**

1. **Windows サーバー**  ページで、適切な選択**Windows エージェントのダウンロード**バージョンによっては、Windows オペレーティング システムのプロセッサ アーキテクチャをダウンロードします。
2. コンピューターにエージェントをインストールするセットアップを実行します。
2. **ウェルカム** ページで、 **[次へ]** をクリックします。
3. **ライセンス条項**ページ、ライセンスを読んで、 をクリックし、**同意**します。
4. **先フォルダー**ページ、変更または既定のインストール フォルダーを保持し、クリックして **[次へ]** します。
5. **エージェントのセットアップ オプション**ページで、Azure Log Analytics にエージェントを接続し、クリックして選択**次**します。   
6. **Azure Log Analytics**ページで、次を実行します。
   1. 貼り付け、**ワークスペース ID**と**ワークスペース キー (主キー)** 先ほどコピーしました。    
    a. Log Analytics サービスにプロキシ サーバーを介して通信するために、コンピューターに必要な場合にクリックします**詳細**URL を指定し、プロキシ サーバーのポート番号。  プロキシ サーバーで認証が必要な場合は、ユーザー名とパスワードがプロキシ サーバーで認証し、順にクリックしますを入力**次**します。  
7. クリックして**次**必要な構成設定を提供することが完了したら。<br><br> ![ワークスペース ID と主キーを貼り付けます](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. **インストールの準備完了** ページで選択内容を確認してクリックして**インストール**します。
9. **構成が正常に完了**] ページで [**完了**します。

完了すると、 **Microsoft Monitoring Agent**に表示されます**コントロール パネルの** します。 構成を確認し、エージェントが Log Analytics に接続されていることを確認できます。 接続しているときに、 **Azure Log Analytics**  タブで、エージェントのことを示すメッセージが表示されます。**Microsoft Monitoring Agent は、Microsoft Log Analytics サービスに正常に接続します。** 

![Log Analytics への MMA 接続の状態](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

サポートされる構成については、確認[サポートされている Windows オペレーティング システム](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)と[ネットワーク ファイアウォール構成](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)します。

## <a name="collecting-event-and-performance-data"></a>イベントとパフォーマンス データの収集

Log Analytics では、長期分析およびレポート作成用に指定されたパフォーマンス カウンターと Windows イベント ログからイベントを収集でき、特定の条件が検出されたときにアクションを実行することができます。  最初に、Windows イベント ログ、およびいくつかの一般的なパフォーマンス カウンターからのイベントのコレクションを構成するこれらの手順に従います。  

1. Azure portal のをクリックして**その他のサービス**左下隅で確認します。 リソースの一覧で、入力**Log Analytics**します。 一覧がフィルター処理は、入力に基づくように入力を開始します。 選択**Log Analytics**します。
2. 選択**詳細設定**します。<br><br> ![Log Analytics の詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. 選択**データ**、し、 **Windows イベント ログ**します。  
4. ここでは、ヘルス サービス イベントのチャネルを追加し、次の名前、プラス記号を入力して **+** します。  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. 表に、重大度レベルを確認**エラー**と**警告**します。   
6. クリックして**保存**構成を保存するには、ページの上部にあります。
7. 選択**Windows パフォーマンス カウンター** Windows コンピューターのパフォーマンス カウンターの収集を有効にします。 
8. 新しい Log Analytics ワークスペースの Windows パフォーマンス カウンターを初めて構成する場合は、いくつかの一般的なカウンターをすばやく作成するオプションが表示されます。 それぞれの横にあるチェック ボックスが表示されます。<br> ![既定の Windows パフォーマンス カウンターが選択されています。](media/configure-azure-monitor/windows-perfcounters-default.png)<br> クリックして**選択したパフォーマンス カウンターを追加する**します。  追加され、10 秒間の収集サンプル間隔でプリセットされます。  
9. クリックして**保存**構成を保存するには、ページの上部にあります。

## <a name="creating-alerts-based-on-log-data"></a>ログ データに基づくアラートを作成します。

行った場合、この Log Analytics へと、までは、クラスターをログおよびパフォーマンス カウンターは、送信する必要があります。 次の手順では、一定の間隔でログ検索を自動的に実行するアラート ルールを作成します。 ログ検索の結果は、電子メールやテキスト通知を送信すると警告が発生し、特定の条件と一致します。 場合、 これを調べてみましょう以下。

### <a name="create-a-query"></a>クエリを作成します。

まず、ログ検索ポータルを開きます。   

1. Azure portal のをクリックして**すべてのサービス**します。 リソースの一覧で、入力**モニター**します。 一覧がフィルター処理は、入力に基づくように入力を開始します。 選択**モニター**します。
2. モニターのナビゲーション メニューで、次のように選択します。 **Log Analytics**し、ワークスペースを選択します。

使用するいくつかのデータを取得する最も簡単な方法は、簡単なクエリをテーブル内のすべてのレコードを返します。 検索ボックスに、次のクエリを入力し、検索ボタンをクリックします。  

```
Event
```

既定のリスト ビューでデータが返され、返された数の合計レコードを参照してください。

![単純なクエリ](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

画面の左側にあるフィルター ペインに直接変更することがなく、クエリにフィルター処理を追加することができます。  いくつかのレコードのプロパティがそのレコードの種類の表示され、検索結果を絞り込むことの 1 つまたは複数のプロパティ値を選択できます。

横にチェック ボックスをオン**エラー**  **EVENTLEVELNAME**か、結果のエラー イベントに制限するには、次を入力します。

```
Event | where (EventLevelName == "Error")
```

![フィルター](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

関心のあるイベントに対して行われた適切クエリした後は、次の手順で保存します。

### <a name="create-alerts"></a>アラートを作成します。
ここで、アラートを作成する例を見てみましょう。

1. Azure portal のをクリックして**すべてのサービス**します。 リソースの一覧で、入力**Log Analytics**します。 一覧がフィルター処理は、入力に基づくように入力を開始します。 選択**Log Analytics**します。
2. 左側のウィンドウで次のように選択します。**アラート** をクリックし、**アラート ルールの新しい**新しいアラートを作成するページの上部から。<br><br> ![新しいアラート ルールを作成します。](media/configure-azure-monitor/alert-rule-02.png)<br>
3. 最初の手順では、下、**アラートの作成** セクションで、ログ ベースのアラート シグナルは、このため、リソースとして、Log Analytics ワークスペースを選択することができます。  特定の選択によって、結果をフィルター**サブスクリプション**1 つ以上、先ほど作成した Log Analytics ワークスペースを含む必要がある場合は、ドロップダウン リストから。  フィルター、**リソースの種類**を選択して**Log Analytics**ドロップダウン リストから。  最後に、選択、**リソース** **DefaultLAWorkspace**  をクリックし、**完了**します。<br><br> ![アラートの手順 1 のタスクを作成します。](media/configure-azure-monitor/alert-rule-03.png)<br>
4. セクションの下**アラート条件**、 をクリックして**条件の追加**保存されたクエリを選択し、アラート ルールに依存するロジックを指定します。
5. 次の情報でアラートを構成します。  
   a. **に基づいて**ドロップダウン リストで、**メトリック測定**します。  メトリック測定は、クエリを指定したしきい値を超える値でオブジェクトごとにアラートを作成します。  
   b. **条件**を選択します**より大きい**thershold を指定します。  
   c. アラートをトリガーするタイミングを定義します。 たとえばを選択できます**連続する違反**と選択 ドロップダウン リストから**より大きい**3 の値。  
   d. 下のセクションに基づく評価、変更、**期間**値を**30**分と**頻度**5 にします。 このルールは 5 分ごとに実行し、現在の時刻から過去 30 分以内に作成されたレコードが返されます。  多くのウィンドウに期間を設定して、アカウントのデータ待機時間の潜在的なにより、クエリは、警告が決して発生という偽陰性を回避するためにデータを返します。  
6. クリックして**完了**アラート ルールを完成させます。<br><br> ![アラートの信号を設定します。](media/configure-azure-monitor/alert-signal-logic-02.png)<br> 
7. ご利用のアラートの名前を指定する 2 番目の手順では、上に移動、**アラート ルール名**フィールドに、**に関するすべてのエラー イベント アラート**します。  指定、**説明**、アラートの詳細と、選択**重大 (重大度 0)** の**重大度**提供されるオプションからの値。
8. 作成時にアラート ルールをすぐにアクティブ化するには、既定値を受け入れる**有効にするルールの作成時**します。
9. 3 番目と最後の手順では、指定した、**アクション グループ**、これにより、同じ操作のたびにアラートがトリガーされ、各ルールを定義するのに使用できますが実行されます。 次の情報で新しいアクション グループを構成します。  
   a. 選択**新しいアクション グループ**と**アクション グループの追加**ウィンドウが表示されます。  
   b. **アクション グループ名**、名前を指定します**IT 操作 - 通知**と**短い名前**など**itops n**します。  
   c. 既定値を確認して**サブスクリプション**と**リソース グループ**が正しい。 それ以外の場合は、ドロップダウン リストから正しいサブスクリプションを選択します。   
   d. アクション セクションになど、アクションの名前を指定**電子メールの送信** **アクションの種類**選択**電子メール/SMS/プッシュ/音声**ドロップダウン リストから。 **電子メール/SMS/プッシュ/音声**追加情報を提供するために右にプロパティ ペインが開きます。  
   e. **電子メール/SMS/プッシュ/音声**ウィンドウを選択し、基本設定をセットアップします。 などを有効にする**電子メール**SMTP アドレスにメッセージを配信する有効な電子メール アドレスを提供します。  
   f. **[OK]** をクリックして変更を保存します。<br><br> 

    ![新しいアクション グループを作成します。](media/configure-azure-monitor/action-group-properties-01.png)

10. をクリックして**OK**アクション グループを完了します。 
11. クリックして**アラート ルールの作成**アラート ルールを完成させます。 すぐに実行を開始します。<br><br> ![新しいアラート ルールの作成を完了します。](media/configure-azure-monitor/alert-rule-01.png)<br> 

### <a name="test-alerts"></a>テスト アラート

リファレンスについては、アラートの例がどのようにこれは。

![アラートの電子メールの例](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- 詳細については、読み取り、 [Azure Monitor のドキュメント](https://docs.microsoft.com/en-us/azure/azure-monitor/learn/tutorial-viewdata)します。
