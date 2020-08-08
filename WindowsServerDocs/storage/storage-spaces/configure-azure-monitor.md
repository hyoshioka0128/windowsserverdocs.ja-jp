---
title: Azure Monitor の理解と構成
description: Azure Monitor とは何か、および Windows Server 2016 および2019で記憶域スペースダイレクトクラスターの電子メールと sms アラートを構成する方法に関する詳細な設定情報。
ms.author: adagashe
ms.topic: article
author: adagashe
ms.date: 01/10/2020
ms.openlocfilehash: 40ee23fa8c1fa88c54e5c8ee1e2c3ebd3453bfff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961136"
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Azure Monitor を使用してヘルス サービスのエラーの電子メールを送信する

>適用先:Windows Server 2019、Windows Server 2016

Azure Monitor は、クラウドおよびオンプレミス環境の利用統計情報を収集、分析し、それに対応する包括的なソリューションを提供することにより、アプリケーションの可用性とパフォーマンスを最大化します。 このツールは、ご利用のアプリケーションがどのように実行されているかを把握するのに役立ちます。さらに、このツールにより、そのアプリケーションに影響している問題点およびアプリケーションが依存しているリソースを事前に明らかにしておくことができます。

これは、オンプレミスのハイパー収束クラスターに特に役立ちます。 Azure Monitor 統合されたを使用すると、クラスターに何らかの問題が発生した場合 (または収集されたデータに基づいて他のアクティビティにフラグを設定する場合) に、電子メール、テキスト (SMS)、およびその他のアラートを構成して、ping を実行できるようになります。 次に、Azure Monitor の動作、Azure Monitor のインストール方法、通知を送信するように構成する方法について簡単に説明します。

System Center を使用している場合は、Windows Server 2019 と Windows Server 2016 記憶域スペースダイレクトクラスターの両方を監視する[記憶域スペースダイレクト管理パック](https://www.microsoft.com/download/details.aspx?id=100782)を確認してください。

この管理パックには次の機能が含まれています。

* 物理ディスクのヘルスとパフォーマンスの監視
* 記憶域ノードの正常性とパフォーマンスの監視
* 記憶域プールの正常性とパフォーマンスの監視
* ボリュームの回復性の種類と重複除去の状態

## <a name="understanding-azure-monitor"></a>Azure Monitor について

Azure Monitor によって収集されたすべてのデータは、2 つの基本的な種類であるメトリックとログのどちらかに該当します。

1. [メトリック](/azure/azure-monitor/platform/data-collection#metrics)は、特定の時点におけるシステムの何らかの側面を表す数値です。 メトリックは軽量であり、リアルタイムに近いシナリオをサポートできます。 Azure portal の [概要] ページに Azure Monitor によって収集されたデータが表示されます。

![メトリックス エクスプローラーへのメトリックの取り込みの画像](media/configure-azure-monitor/metrics.png)

2. [ログ](/azure/azure-monitor/platform/data-collection#logs)には、種類ごとに異なるプロパティ セットを持つレコードに編成されたさまざまな種類のデータが含まれます。 イベントやトレースなどの利用統計情報は、組み合わせて分析できるように、パフォーマンス データとともにログとして格納されます。 Azure Monitor が収集したログ データは、収集されたデータをすばやく検索、統合、分析する[クエリ](/azure/azure-monitor/log-query/log-query-overview)を使用して分析できます。 Azure portal で [Log Analytics](/azure/azure-monitor/log-query/portals) を使用してクエリを作成およびテストした後、これらのツールを使用してデータを直接分析できるほか、クエリを保存して[視覚化](/azure/azure-monitor/visualizations)または[アラート ルール](/azure/azure-monitor/platform/alerts-overview)に利用することができます。

![Log Analytics へのログの取り込みの画像](media/configure-azure-monitor/logs.png)

これらのアラートを構成する方法の詳細については、以下を参照してください。

## <a name="onboarding-your-cluster-using-windows-admin-center"></a>Windows 管理センターを使用してクラスターをオンボードする

Windows 管理センターを使用して、クラスターを Azure Monitor にオンボードすることができます。

![Azure Monitor するクラスターをオンボードするための Gif](media/configure-azure-monitor/onboarding.gif)

このオンボードフローでは、次の手順が内部で発生しています。 クラスターを手動で設定する場合に備えて、詳細な構成方法について詳しく説明します。

### <a name="configuring-health-service"></a>ヘルスサービスの構成

まず、クラスターを構成する必要があります。 ご存じのように、[ヘルス サービス](../../failover-clustering/health-service-overview.md)によって、記憶域スペース ダイレクトが実行されているクラスターでの日常的な監視と操作エクスペリエンスが向上します。

上記で説明したように、Azure Monitor では、クラスター内で実行されている各ノードからログが収集されます。 そのため、イベント チャネルに書き込まむようにヘルス サービスを構成する必要があります。イベント チャネルは以下であるとします。

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

ヘルス サービスを構成するには、以下を実行します。

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

上のコマンドレットを実行して正常性の設定を設定すると、イベントが生成されて、 *Microsoft-Windows-Health/Operational*イベントチャネルへの書き込みが開始されます。

### <a name="configuring-log-analytics"></a>Log Analytics の構成

クラスターに適切なログ記録を設定したので、次の手順では log analytics を適切に構成します。

概要を説明するために、 [Azure Log Analytics](/azure/azure-monitor/platform/agent-windows)では、データセンターまたは他のクラウド環境内の物理または仮想 Windows コンピューターからデータを直接収集して、詳細な分析と相関化を行うことができます。

サポートされている構成を確認するには、「[サポートされている Windows オペレーティング システム](/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)」と「[ネットワーク ファイアウォールの構成](/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)」をご覧ください。

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) を作成してください。

#### <a name="login-in-to-azure-portal"></a>Azure Portal へのログイン

Azure Portal ([https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)) にログインします。

#### <a name="create-a-workspace"></a>ワークスペースの作成

以下に示す手順の詳細については、[Azure Monitor のドキュメント](/azure/azure-monitor/learn/quick-collect-windows-computer)を参照してください。

1. Azure Portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で、「**Log Analytics**」と入力します。 入力を始めると、入力内容に基づいて、一覧がフィルター処理されます。 **[Log Analytics]** を選択します。<br><br>

   ![Azure portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. **[作成]** をクリックし、次の項目について選択します。

   * 新しい **Log Analytics ワークスペース**の名前 (*DefaultLAWorkspace* など) を指定します。
   * 関連付ける**サブスクリプション**をドロップダウン リストから選択します (既定値が適切でない場合)。
   * **[リソース グループ]** では、1 つ以上の Azure Virtual Machines を含む既存のリソース グループを選択します。 <br><br>

      ![Log Analytics リソース ブレードの作成](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>

3. **[Log Analytics ワークスペース]** ウィンドウで必要な情報を入力したら、 **[OK]** をクリックします。

情報が検証され、ワークスペースが作成されている間、メニューの **[通知]** でその進行状況を追跡することができます。

#### <a name="obtain-workspace-id-and-key"></a>ワークスペース ID とキーを取得する
Microsoft Monitoring Agent for Windows をインストールする前に、Log Analytics ワークスペースのワークスペース ID とキーが必要です。  この情報は、設定ウィザードがエージェントを適切に構成し、そのエージェントを Log Analytics と正常に通信できるようにするために必要です。

1. Azure Portal の左上隅にある **[すべてのサービス]** をクリックします。 リソースの一覧で、「**Log Analytics**」と入力します。 入力を始めると、入力内容に基づいて、一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. Log Analytics ワークスペースの一覧で、前の手順で作成した *DefaultLAWorkspace* を選択します。
3. **[詳細設定]** を選択します。<br><br> ![Log Analytics の詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>
4. **[接続されたソース]** 、 **[Windows サーバー]** の順に選択します。
5. **[ワークスペース ID]** と **[主キー]** の右側に値が表示されます。 一時的に両方を保存しておきます。ここでは、任意のエディターに両方をコピーして貼り付けます。

### <a name="installing-the-agent-on-windows"></a>Windows へのエージェントのインストール
次の手順では、Microsoft Monitoring Agent をインストールして構成します。 **クラスター内の各サーバーにこのエージェントをインストールし、エージェントを Windows の起動時に実行するように指定してください。**

1. **[Windows サーバー]** ページの **[Windows エージェントのダウンロード]** で、Windows オペレーティング システムのプロセッサ アーキテクチャに応じた適切なバージョンを選択します。
2. セットアップを実行して、コンピューターにエージェントをインストールします。
2. **[ようこそ]** ページで **[次へ]** をクリックします。
3. **[ライセンス条項]** ページの記述内容を確認し、 **[同意する]** をクリックします。
4. **[インストール先フォルダー]** ページで、既定のインストール フォルダーを変更するか、変更せずに **[次へ]** をクリックします。
5. **[エージェントのセットアップ オプション]** ページで、エージェントを接続する Azure Log Analytics をクリックし、 **[次へ]** をクリックします。
6. **[Azure Log Analytics]** ページで、次の手順を実行します。
   1. **[ワークスペース ID]** と **[ワークスペース キー (主キー)]** に、先ほどコピーした値を貼り付けます。
    a. コンピューターがプロキシ サーバーを介して Log Analytics サービスと通信する必要がある場合は、 **[詳細]** をクリックし、プロキシ サーバーの URL とポート番号を指定します。  プロキシ サーバーで認証が必要な場合には、プロキシ サーバーにアクセスするためのユーザー名とパスワードを入力し、 **[次へ]** をクリックします。
7. 必要な構成設定をしたら、 **[次へ]** をクリックします。<br><br> ![ワークスペース ID と主キーの貼り付け](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. **[インストールの準備完了]** ページで、設定内容を確認し、 **[インストール]** をクリックします。
9. **[構成は正常に終了しました]** ページで **[完了]** をクリックします。

完了すると、**コントロール パネル**に **Microsoft Monitoring Agent** が表示されます。 構成を検証して、エージェントが Log Analytics に接続されていることを確認できます。 接続時に、 **[Azure ログ分析]** タブで、エージェントに以下を示すメッセージが表示されます。**Microsoft Monitoring Agent は、Microsoft ログ分析サービスに正常に接続されています。**

![Log Analytics への MMA 接続の状態](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

サポートされている構成を確認するには、「[サポートされている Windows オペレーティング システム](/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems)」と「[ネットワーク ファイアウォールの構成](/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)」をご覧ください。

## <a name="setting-up-alerts-using-windows-admin-center"></a>Windows Admin Center を使用してアラートを設定する

Windows 管理センターでは、Log Analytics ワークスペースのすべてのサーバーに適用される既定のアラートを構成できます。

![アラートの設定の Gif "](media/configure-azure-monitor/setup1.gif)

選択できるアラートとその既定の条件を次に示します。

| アラート名                | 既定の条件                                  |
|---------------------------|----------------------------------------------------|
| CPU 使用率           | 10 分の間 85% を超えている                            |
| ディスク容量使用率 | 10 分の間 85% を超えている                            |
| メモリ使用率        | 使用可能なメモリが 10 分の間 100 MB 未満である   |
| Heartbeat                 | 5 分間のビート数が 2 未満である                   |
| システムの重大なエラー     | クラスター システムのイベント ログ内に重大なアラートがある |
| ヘルス サービスのアラート      | クラスター上にヘルス サービスのエラーがある            |

Windows 管理センターでアラートを構成すると、Azure の log analytics ワークスペースにアラートが表示されます。

![アラートの設定の Gif "](media/configure-azure-monitor/setup2.gif)

このオンボードフローでは、次の手順が内部で発生しています。 クラスターを手動で設定する場合に備えて、詳細な構成方法について詳しく説明します。

### <a name="collecting-event-and-performance-data"></a>イベントとパフォーマンス データを収集する

Log Analytics は、イベントを Windows イベント ログから収集でき、長期分析およびレポートのために指定されたパフォーマンス カウンターからも収集できます。また、特定の条件が検出された場合はアクションを実行できます。  以下の手順に従って、Windows イベント ログと、手始めとしていくつかの一般的なパフォーマンス カウンターからのイベントの収集を構成します。

1. Azure ポータルで、左下隅にある **[その他のサービス]** をクリックします。 リソースの一覧で、「**Log Analytics**」と入力します。 入力を始めると、入力内容に基づいて、一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. **[詳細設定]** を選択します。<br><br> ![Log Analytics の詳細設定](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>
3. **[データ]** を選択してから、 **[Windows イベント ログ]** を選択します。
4. ここで、次の名前を入力してヘルス サービス イベント チャネルを追加し、プラス記号 **+** をクリックします。
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. テーブルで、重大度の **[エラー]** と **[警告]** のチェック ボックスをオンにします。
6. ページの上部にある **[保存]** をクリックして構成を保存します。
7. **[Windows パフォーマンス カウンター]** を選択して、Windows コンピューターでのパフォーマンス カウンターの収集を有効にします。
8. 新しい Log Analytics ワークスペースの Windows パフォーマンス カウンターを初めて構成する場合は、いくつかの一般的なカウンターをすばやく作成するためのオプションが表示されます。 それぞれのオプションの横には、チェック ボックスが表示されます。<br> ![既定の Windows パフォーマンス カウンターが選択されている状態](media/configure-azure-monitor/windows-perfcounters-default.png)<br> **[選択したパフォーマンス カウンターを追加する]** をクリックします。  カウンターが追加され、10 秒間の収集サンプル間隔でプリセットされます。
9. ページの上部にある **[保存]** をクリックして構成を保存します。

## <a name="creating-alerts-based-on-log-data"></a>ログデータに基づく警告の作成

ここまで進むと、クラスターから Log Analytics にログとパフォーマンス カウンターが送信されるようになります。 次の手順では、ログ検索を一定の間隔で自動的に実行するアラート ルールを作成します。 ログ検索の結果が特定の条件に一致した場合、電子メールまたはテキスト通知を送信するアラートが発生します。 以下で、これについて説明します。

### <a name="create-a-query"></a>クエリを作成する

最初に、ログ検索ポータルを開きます。

1. Azure Portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で「**Monitor**」と入力します。 入力を始めると、入力内容に基づいて、一覧がフィルター処理されます。 **[モニター]** を選択します。
2. [モニター] ナビゲーション メニューで **[Log Analytics]** を選択し、ワークスペースを選択します。

テーブルのすべてのレコードを返すシンプルなクエリを使用すると、作業データを最も簡単に取得できます。 検索ボックスに次のクエリを入力し、検索ボタンをクリックします。

```
Event
```

データは既定のリスト ビューに返されます。ここで、返されたレコードの合計数を確認できます。

![単純なクエリ](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

画面の左側はフィルター ウィンドウです。ここでは、クエリを直接変更せずに、フィルターを追加することができます。  そのレコードの種類について、レコードのプロパティがいくつか表示されます。1 つまたは複数のプロパティ値を選択して検索結果を絞り込むことができます。

**[EVENTLEVELNAME]** の下にある **[エラー]** の横のチェックボックスをオンにするか、次のように入力して結果をエラー イベントに限定します。

```
Event | where (EventLevelName == "Error")
```

![Assert](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

注意が必要なイベントに対して approriate クエリを作成したら、次の手順のために保存します。

### <a name="create-alerts"></a>アラートを作成する
ここで、アラートの作成例を見ていきましょう。

1. Azure Portal で、 **[すべてのサービス]** をクリックします。 リソースの一覧で、「**Log Analytics**」と入力します。 入力を始めると、入力内容に基づいて、一覧がフィルター処理されます。 **[Log Analytics]** を選択します。
2. 左側のウィンドウで、 **[アラート]** を選択し、ページの上部の **[新しいアラート ルール]** をクリックして新しいアラートを作成します。<br><br> ![新しいアラート ルールの作成](media/configure-azure-monitor/alert-rule-02.png)<br>
3. 最初の手順では、**[アラートの作成]** セクションで、リソースとして Log Analytics ワークスペースを選択します。これがログ ベースのアラート シグナルであるためです。  複数のサブスクリプションがある場合は、ドロップダウン リストから、先ほど作成した Log Analytics ワークスペースが含まれている特定の**サブスクリプション**を選択して結果をフィルターします。  ドロップダウン リストから **[Log Analytics]** を選択して **[リソースの種類]** をフィルターします。  最後に、 **[リソース**  **DefaultLAWorkspace]** を選択し、 **[完了]** をクリックします。<br><br> ![アラートの作成手順 1 のタスク](media/configure-azure-monitor/alert-rule-03.png)<br>
4. **[アラートの条件]** セクションで、 **[条件の追加]** をクリックして保存済みのクエリを選択し、アラート ルールが従うロジックを指定します。
5. 次の情報を指定して、アラートを構成します。a. **[基準]** ドロップダウン リストで **[メトリック測定]** を選択します。  メトリック測定では、クエリの対象となったオブジェクトのうち、値が指定されたしきい値を上回っているオブジェクトについて、それぞれ別個にアラートが生成されます。
   b. **条件**として [**より大きい**] を選択し、[値] を指定します。
   c. 次に、アラートをトリガーするタイミングを定義します。 たとえば、 **[連続する違反]** を選択し、ドロップダウン リストから **[より大きい]** を選択し、値「3」を入力します。
   d. [評価基準] セクションで、 **[期間]** の値を **30** 分に変更し、 **[頻度]** を 5 に変更します。 ルールは 5 分ごとに実行され、現在の時刻から直近の 30 分以内に作成されたレコードが返されます。  この期間をより広い時間枠に設定すると、潜在的なデータの待機時間の原因となるため、クエリでは、アラートが決して発生しない検知漏れを回避するために確実にデータが返されるようにします。
6. **[完了]** をクリックして、アラート ルールを完成させます。<br><br> ![アラート シグナルの構成](media/configure-azure-monitor/alert-signal-logic-02.png)<br>
7. 2 番目の手順に進み、 **[アラート ルール名]** フィールドに「**すべてのエラー イベントでのアラート**」のようなアラートの名前を入力します。  アラートの詳細を説明する **[説明]** を指定し、表示されたオプションから **[重大度]** 値として **[重大 (重大度 0)]** を選択します。
8. 作成時にアラート ルールをすぐにアクティブ化するには、 **[ルールの作成時に有効にする]** の既定値を受け入れます。
9. 3 番目および最後の手順では、 **[アクション グループ]** を指定します。これにより、アラートがトリガーされるたびに同じアクションが実行され、定義する各ルールに同じアクションを使用できます。 次の情報を指定して、新しいアクション グループを構成します。a. **[新しいアクション グループ]** を選択すると、 **[アクション グループの追加]** ウィンドウが表示されます。
   b. **[アクション グループ名]** で、「**IT 操作 - 通知**」のような名前と **itops-n** などの **[短い名前]** を指定します。
   c. **[サブスクリプション]** と **[リソース グループ]** の既定値が正しいことを確認します。 正しくない場合は、ドロップダウン リストから正しいものを 1 つ選択します。
   d. [アクション] セクションで、「**電子メールの送信**」などのアクション名を指定し、 **[アクションの種類]** でドロップダウン リストから **[電子メール/SMS/プッシュ/音声]** を選択します。 追加情報を指定するために **[電子メール/SMS/プッシュ/音声]** プロパティ ウィンドウが右側に開きます。
   e. **[電子メール/SMS/プッシュ/音声]** ウィンドウで、任意のものを選択して設定します。 たとえば、 **[電子メール]** を有効にし、メッセージの配信先の有効な電子メール SMTP アドレスを指定します。
   f. **[OK]** をクリックして変更を保存します。<br><br>

    ![新しいアクション グループの作成](media/configure-azure-monitor/action-group-properties-01.png)

10. **[OK]** をクリックしてアクション グループを完成させます。
11. **[アラート ルールの作成]** をクリックしてアラート ルールを完成させます。 すぐに実行が開始されます。<br><br> ![新しいアラート ルールの作成の完了](media/configure-azure-monitor/alert-rule-01.png)<br>

### <a name="example-alert"></a>アラートの例

参考のため、Azure でのアラートの例を次に示します。

![Azure でのアラートの Gif](media/configure-azure-monitor/alert.gif)

Azure Monitor によって送信される電子メールの例を次に示します。

![アラートの電子メールの例](media/configure-azure-monitor/warning.png)

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- 詳細については、 [Azure Monitor のドキュメント](/azure/azure-monitor/learn/tutorial-viewdata)を参照してください。
- [他の Azure ハイブリッドサービスに接続](../../manage/windows-admin-center/azure/index.md)する方法の概要については、こちらをご覧ください。
