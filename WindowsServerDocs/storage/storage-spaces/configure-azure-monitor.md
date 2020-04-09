---
title: Azure Monitor の理解と構成
description: Azure Monitor とは何か、および Windows Server 2016 および2019で記憶域スペースダイレクトクラスターの電子メールと sms アラートを構成する方法に関する詳細な設定情報。
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/10/2020
ms.openlocfilehash: fa4d8793c07cabd39ee6cc0d54b5cddc84eac202
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859045"
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Azure Monitor を使用してヘルスサービスエラーのメールを送信する

>適用対象: Windows Server 2019、Windows Server 2016

Azure Monitor は、クラウドおよびオンプレミス環境の利用統計情報を収集、分析し、それに対応する包括的なソリューションを提供することにより、アプリケーションの可用性とパフォーマンスを最大化します。 また、ご利用のアプリケーションがどのように実行されているかを把握するのに役立ちます。さらに、そのアプリケーションに影響している問題点およびアプリケーションが依存しているリソースを事前に特定することができます。

これは、オンプレミスのハイパー収束クラスターに特に役立ちます。 Azure Monitor 統合されたを使用すると、クラスターに何らかの問題が発生した場合 (または収集されたデータに基づいて他のアクティビティにフラグを設定する場合) に、電子メール、テキスト (SMS)、およびその他のアラートを構成して、ping を実行できるようになります。 次に、Azure Monitor の動作、Azure Monitor のインストール方法、通知を送信するように構成する方法について簡単に説明します。

System Center を使用している場合は、Windows Server 2019 と Windows Server 2016 記憶域スペースダイレクトクラスターの両方を監視する[記憶域スペースダイレクト管理パック](https://www.microsoft.com/download/details.aspx?id=100782)を確認してください。

この管理パックには次の機能が含まれています。

* 物理ディスクのヘルスとパフォーマンスの監視
* 記憶域ノードの正常性とパフォーマンスの監視
* 記憶域プールの正常性とパフォーマンスの監視
* ボリュームの回復性の種類と重複除去の状態

## <a name="understanding-azure-monitor"></a>Azure Monitor について

Azure Monitor によって収集されたすべてのデータは、2 つの基本的な種類であるメトリックとログのどちらかに該当します。

1. [メトリック](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#metrics)は、特定の時点におけるシステムのいくつかの側面を表す数値です。 メトリックは軽量であり、リアルタイムに近いシナリオをサポートできます。 Azure portal の [概要] ページに Azure Monitor によって収集されたデータが表示されます。

![メトリックスエクスプローラーのメトリック取り込みの画像](media/configure-azure-monitor/metrics.png)

2. [ログ](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)には、種類ごとに異なるプロパティセットを持つレコードに整理されたさまざまな種類のデータが含まれます。 イベントやトレースなどの利用統計情報は、組み合わせて分析できるように、パフォーマンス データとともにログとして格納されます。 Azure Monitor によって収集されたログデータを[クエリ](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview)で分析し、収集したデータを迅速に取得、統合、および分析することができます。 Azure portal で[Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/portals)を使用してクエリを作成およびテストした後、これらのツールを使用してデータを直接分析するか、[視覚エフェクト](https://docs.microsoft.com/azure/azure-monitor/visualizations)や[アラートルール](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview)で使用するクエリを保存することができます。

![log analytics のログ取り込みの画像](media/configure-azure-monitor/logs.png)

これらのアラートを構成する方法の詳細については、以下を参照してください。

## <a name="onboarding-your-cluster-using-windows-admin-center"></a>Windows 管理センターを使用してクラスターをオンボードする

Windows 管理センターを使用して、クラスターを Azure Monitor にオンボードすることができます。

![Azure Monitor するクラスターをオンボードするための Gif](media/configure-azure-monitor/onboarding.gif)

このオンボードフローでは、次の手順が内部で発生しています。 クラスターを手動で設定する場合に備えて、詳細な構成方法について詳しく説明します。 

### <a name="configuring-health-service"></a>ヘルスサービスの構成

まず、クラスターを構成する必要があります。 ご存知のように、[ヘルスサービス](../../failover-clustering/health-service-overview.md)によって、記憶域スペースダイレクトを実行しているクラスターの日常的な監視と操作エクスペリエンスが向上します。 

既に説明したように、Azure Monitor は、クラスター内で実行されている各ノードからログを収集します。 そのため、イベントチャネルに書き込むようにヘルスサービスを構成する必要があります。これは次のようになります。

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

ヘルスサービスを構成するには、次のように実行します。

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

上のコマンドレットを実行して正常性の設定を設定すると、イベントが生成されて、 *Microsoft-Windows-Health/Operational*イベントチャネルへの書き込みが開始されます。

### <a name="configuring-log-analytics"></a>Log Analytics の構成

クラスターに適切なログ記録を設定したので、次の手順では log analytics を適切に構成します。

概要を説明するために、 [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows)では、データセンターまたは他のクラウド環境内の物理または仮想 Windows コンピューターからデータを直接収集して、詳細な分析と相関化を行うことができます。

サポートされている構成を理解するには、[サポートされている Windows オペレーティングシステム](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)と[ネットワークファイアウォールの構成](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)を確認してください。

Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成してください。

#### <a name="login-in-to-azure-portal"></a>Azure ポータルにログインする

[https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)で Azure portal にログインします。

#### <a name="create-a-workspace"></a>ワークスペースの作成

以下に示す手順の詳細については、 [Azure Monitor のドキュメント](https://docs.microsoft.com/azure/azure-monitor/learn/quick-collect-windows-computer)を参照してください。

1. Azure portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で、「 **Log Analytics**」と入力します。 入力していくと、入力に基づいて一覧がフィルター処理されます。 **[Log Analytics]** を選択します。<br><br> 

   ![Azure ポータル](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. **[作成]** をクリックし、次の項目の選択肢を選択します。

   * 新しい**Log Analytics ワークスペース**の名前 ( *defaultlaworkspace*など) を指定します。 
   * 既定の選択が適切でない場合は、ドロップダウンリストから選択して、リンク先の**サブスクリプション**を選択します。
   * **[リソースグループ]** で、1つまたは複数の Azure 仮想マシンを含む既存のリソースグループを選択します。 <br><br>

      ![Log Analytics リソース ブレードの作成](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. **[Log Analytics ワークスペース]** ウィンドウで必要な情報を指定したら、[ **OK]** をクリックします。  

情報が検証され、ワークスペースが作成されている間、メニューの **[通知]** で進行状況を追跡できます。 

#### <a name="obtain-workspace-id-and-key"></a>ワークスペース ID とキーを取得する
Microsoft Monitoring Agent for Windows をインストールする前に、Log Analytics ワークスペースのワークスペース ID とキーが必要です。  この情報は、設定ウィザードがエージェントを適切に構成し、そのエージェントを Log Analytics と正常に通信できるようにするために必要です。  

1. Azure portal で、左上隅にある **[すべてのサービス]** をクリックします。 リソースの一覧で、「 **Log Analytics**」と入力します。 入力していくと、入力に基づいて一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. Log Analytics ワークスペースの一覧で、前の手順で作成した*Defaultlaworkspace*を選択します。
3. **[詳細設定]** を選択します。<br><br> ![Log Analytics 詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. **[接続されたソース]** を選択し、 **[Windows サーバー]** を選択します。   
5. **[ワークスペース ID]** と **[主キー]** の右側の値。 一時的に両方を保存しておきます。しばらくの間、お気に入りのエディターに両方をコピーして貼り付けます。   

### <a name="installing-the-agent-on-windows"></a>Windows へのエージェントのインストール
次の手順では、Microsoft Monitoring Agent をインストールして構成します。 **クラスター内の各サーバーにこのエージェントをインストールし、エージェントを Windows の起動時に実行するように指定してください。**

1. **[Windows サーバー]** ページで、windows オペレーティングシステムのプロセッサアーキテクチャに応じて、ダウンロードする**windows エージェント**の適切なバージョンを選択します。
2. セットアップを実行して、コンピューターにエージェントをインストールします。
2. **[ようこそ]** ページで **[次へ]** をクリックします。
3. **[ライセンス条項]** ページで、ライセンスを読み、 **[同意]** する をクリックします。
4. インストール **[先のフォルダー]** ページで、既定のインストールフォルダーを変更するか、そのままにして、 **[次へ]** をクリックします。
5. **[エージェントのセットアップオプション]** ページで、エージェントを Azure Log Analytics に接続することを選択し、 **[次へ]** をクリックします。   
6. **[Azure Log Analytics]** ページで、次の手順を実行します。
   1. 前の手順でコピーした**ワークスペース ID**と**ワークスペースキー (主キー)** を貼り付けます。    
    a. コンピューターがプロキシサーバーを介して Log Analytics サービスに通信する必要がある場合は、 **[詳細設定]** をクリックし、プロキシサーバーの URL とポート番号を指定します。  プロキシサーバーで認証が必要な場合は、プロキシサーバーで認証するためのユーザー名とパスワードを入力し、 **[次へ]** をクリックします。  
7. 必要な構成設定の指定が完了したら、 **[次へ]** をクリックします。<br><br> ワークスペース ID と主キー](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png) を貼り付け ![<br><br>
8. **[インストールの準備完了]** ページで、選択内容を確認し、 **[インストール]** をクリックします。
9. **[構成が正常に完了]** しました ページで、 **[完了]** をクリックします。

完了すると、[**コントロールパネル]** に**Microsoft Monitoring Agent**が表示されます。 構成を検証して、エージェントが Log Analytics に接続されていることを確認できます。 接続されている場合、 **[Azure Log Analytics]** タブのエージェントには、 **Microsoft Monitoring Agent が Microsoft Log Analytics サービスに正常に接続さ**れたことを示すメッセージが表示されます。 

![Log Analytics への MMA 接続の状態](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

サポートされている構成を理解するには、[サポートされている Windows オペレーティングシステム](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)と[ネットワークファイアウォールの構成](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)を確認してください。

## <a name="setting-up-alerts-using-windows-admin-center"></a>Windows 管理センターを使用したアラートの設定

Windows 管理センターでは、Log Analytics ワークスペースのすべてのサーバーに適用される既定のアラートを構成できます。 

![アラートの設定の Gif "](media/configure-azure-monitor/setup1.gif)

選択できるアラートとその既定の状態を次に示します。

| アラート名                | 既定の条件                                  |
|---------------------------|----------------------------------------------------|
| CPU 使用率           | 10分間で85% 以上                            |
| ディスク容量使用率 | 10分間で85% 以上                            |
| メモリ使用率        | 10分間で 100 MB 未満の使用可能なメモリ   |
| ハートビート                 | 5分間の拍が2未満                   |
| システム重大エラー     | クラスタシステムのイベントログに記録されている重大なアラート |
| ヘルスサービスのアラート      | クラスター上のヘルスサービスのエラー            |

Windows 管理センターでアラートを構成すると、Azure の log analytics ワークスペースにアラートが表示されます。

![アラートの設定の Gif "](media/configure-azure-monitor/setup2.gif)

このオンボードフローでは、次の手順が内部で発生しています。 クラスターを手動で設定する場合に備えて、詳細な構成方法について詳しく説明します。 

### <a name="collecting-event-and-performance-data"></a>イベントとパフォーマンスデータの収集

Log Analytics は、イベントを Windows イベント ログから収集でき、長期分析およびレポートのために指定されたパフォーマンス カウンターからも収集できます。また、特定の条件が検出された場合はアクションを実行できます。  以下の手順に従って、Windows イベント ログと、手始めとしていくつかの一般的なパフォーマンス カウンターからのイベントの収集を構成します。  

1. Azure portal で、左下隅にある **[その他のサービス]** をクリックします。 リソースの一覧で、「 **Log Analytics**」と入力します。 入力していくと、入力に基づいて一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. **[詳細設定]** を選択します。<br><br> ![Log Analytics 詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. **[データ]** を選択し、 **[Windows イベントログ]** を選択します。  
4. ここで、以下の名前を入力してヘルスサービスイベントチャネルを追加し、プラス記号 **+** をクリックします。  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. テーブルで、重大度の**エラー**と**警告**を確認します。   
6. ページの上部にある **[保存]** をクリックして構成を保存します。
7. Windows**パフォーマンスカウンター**を選択して、windows コンピューターでのパフォーマンスカウンターの収集を有効にします。 
8. 新しい Log Analytics ワークスペースの Windows パフォーマンス カウンターを初めて構成する場合は、いくつかの一般的なカウンターをすばやく作成するためのオプションが表示されます。 それぞれのオプションの横には、チェック ボックスが表示されます。<br> 既定の Windows パフォーマンスカウンターが選択された ![](media/configure-azure-monitor/windows-perfcounters-default.png)<br> [**選択したパフォーマンスカウンターを追加する] を**クリックします。  カウンターが追加され、10 秒間の収集サンプル間隔でプリセットされます。  
9. ページの上部にある **[保存]** をクリックして構成を保存します。

## <a name="creating-alerts-based-on-log-data"></a>ログデータに基づく警告の作成

これまでに実行したことがある場合、クラスターはログとパフォーマンスカウンターを Log Analytics に送信する必要があります。 次の手順では、定期的にログ検索を自動的に実行するアラートルールを作成します。 ログ検索の結果が特定の条件に一致する場合は、電子メールまたはテキスト通知を送信するアラートが発生します。 次に、これについて説明します。

### <a name="create-a-query"></a>クエリの作成

最初に、ログ検索ポータルを開きます。   

1. Azure portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で、「 **Monitor**」と入力します。 入力していくと、入力に基づいて一覧がフィルター処理されます。 **[モニター]** を選択します。
2. モニター ナビゲーションメニューで、 **Log Analytics** を選択し、ワークスペースを選択します。

テーブルのすべてのレコードを返すシンプルなクエリを使用すると、作業データを最も簡単に取得できます。 検索ボックスに次のクエリを入力し、[検索] ボタンをクリックします。  

```
Event
```

データは既定のリスト ビューに返されます。ここで、返されたレコードの合計数を確認できます。

![単純なクエリ](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

画面の左側はフィルター ウィンドウです。ここでは、クエリを直接変更せずに、フィルターを追加することができます。  そのレコードの種類について、レコードのプロパティがいくつか表示されます。1 つまたは複数のプロパティ値を選択して検索結果を絞り込むことができます。

**[Eventlevelname]** の **[エラー]** の横にあるチェックボックスをオンにするか、次のように入力して、結果をエラーイベントに限定します。

```
Event | where (EventLevelName == "Error")
```

![フィルター](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

注意が必要なイベントに対して approriate クエリを作成したら、次の手順のために保存します。

### <a name="create-alerts"></a>アラートの作成
ここで、アラートを作成する例を見てみましょう。

1. Azure portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で、「 **Log Analytics**」と入力します。 入力していくと、入力に基づいて一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. 左側のウィンドウで、 **[アラート]** を選択し、ページの上部にある **[新しいアラートルール]** をクリックして新しいアラートを作成します。<br><br> 新しいアラートルールを作成 ![](media/configure-azure-monitor/alert-rule-02.png)<br>
3. 最初の手順では、**アラートの作成** セクションで、Log Analytics ワークスペースをリソースとして選択します。これは、ログベースのアラートシグナルであるためです。  前の手順で作成した Log Analytics ワークスペースが含まれている場合は、ドロップダウンリストから特定の**サブスクリプション**を選択して結果をフィルター処理します。  ドロップダウンリストから **[Log Analytics]** を選択して、**リソースの種類**をフィルター処理します。  最後に、[**リソース** **defaultlaworkspace** ] を選択し、 **[完了]** をクリックします。<br><br> 警告ステップ1タスク](media/configure-azure-monitor/alert-rule-03.png) の作成 ![<br>
4. アラートの **[条件]** セクションで、 **[条件の追加]** をクリックして保存したクエリを選択し、アラートルールが従うロジックを指定します。
5. 次の情報を指定して、アラートを構成します。  
   a. **[ベース]** ドロップダウンリストから **[メトリック測定]** を選択します。  メトリック測定では、クエリの対象となったオブジェクトのうち、値が指定されたしきい値を上回っているオブジェクトについて、それぞれ別個にアラートが生成されます。  
   b. **条件**として **より大きい** を選択し、値 を指定します。  
   c. 次に、アラートをトリガーするタイミングを定義します。 たとえば、[連続した**侵害**] を選択し、ドロップダウンリストから [値 3**より大きい**] を選択できます。  
   d. [評価基準] セクションで、**期間**の値を**30**分に、 **Frequency**を5に変更します。 ルールは 5 分ごとに実行され、現在の時刻から直近の 30 分以内に作成されたレコードが返されます。  この期間をより広い時間枠に設定すると、潜在的なデータの待機時間の原因となるため、クエリでは、アラートが決して発生しない検知漏れを回避するために確実にデータが返されるようにします。  
6. **[完了]** をクリックして、アラートルールを完了します。<br><br> アラートシグナル](media/configure-azure-monitor/alert-signal-logic-02.png) を構成 ![には<br> 
7. 次に、2番目の手順に進み、[アラート**ルール名**] フィールドにアラートの名前を指定します ( **[すべてのエラーイベントにアラートを記録**する] など)。  アラートの詳細情報の**説明**を指定し、提供されているオプションから重要**度**の値として [**重大] (重大度 0)** を選択します。
8. 作成時にアラートルールをすぐにアクティブにするには、[**作成時にルールを有効**にする] の既定値をそのまま使用します。
9. 3番目と最後の手順では、**アクショングループ**を指定します。これにより、アラートがトリガーされるたびに同じアクションが実行され、定義した各ルールに使用できるようになります。 次の情報を指定して、新しいアクション グループを構成します。  
   a. **[新しいアクショングループ]** を選択すると、 **[アクショングループの追加]** ウィンドウが表示されます。  
   b. **[アクショングループ名]** に、「**操作-通知**」や「 **itops-n**」などの**短い名前**を指定します。  
   c. **サブスクリプション**と**リソースグループ**の既定値が正しいことを確認します。 正しくない場合は、ドロップダウン リストから正しいものを 1 つ選択します。   
   d. アクション セクションで、アクションの名前を指定します。たとえば、**電子メールの送信**、**アクションの種類** の順に選択し、ドロップダウンリストから **電子メール/SMS/プッシュ/音声** を選択します。 追加情報を提供するために、[**電子メール/SMS/プッシュ/音声**のプロパティ] ウィンドウが右側に表示されます。  
   e. **[電子メール/SMS/プッシュ/音声]** ウィンドウで、設定を選択して設定します。 たとえば、**電子メール**を有効にし、メッセージの配信先となる有効な電子メール SMTP アドレスを指定します。  
   f. **[OK]** をクリックし、変更を保存します。<br><br> 

    ![新しいアクション グループの作成](media/configure-azure-monitor/action-group-properties-01.png)

10. **[OK]** をクリックして、アクショングループを完成させます。 
11. アラートルールを完了するには、 **[アラートルールの作成]** をクリックします。 すぐに実行が開始されます。<br><br> 新しいアラートルールの作成を完了 ![](media/configure-azure-monitor/alert-rule-01.png)<br> 

### <a name="example-alert"></a>アラートの例

参考までに、Azure でのアラートの例を次に示します。

![Azure でのアラートの Gif](media/configure-azure-monitor/alert.gif)

Azure Monitor によって送信される電子メールの例を次に示します。

![アラートの電子メールの例](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- 詳細については、 [Azure Monitor のドキュメント](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-viewdata)を参照してください。
- [他の Azure ハイブリッドサービスに接続](../../manage/windows-admin-center/azure/index.md)する方法の概要については、こちらをご覧ください。
