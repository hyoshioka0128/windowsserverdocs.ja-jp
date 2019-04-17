---
title: "ヘルス サービスをレポートします。"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: bc21b9fdec5700fec23dc6af7ca15873ded34bea
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-reports"></a>ヘルス サービスをレポートします。
> Windows Server 2016 に適用されます。

## <a name="what-are-reports"></a>レポートとは何ですか。  

ヘルス サービスでは、記憶域スペース ダイレクト クラスターから現在のパフォーマンスおよび容量の情報を取得するために必要な作業が軽減されます。 1 つの新しいコマンドレットは、効率的に収集され、クラスター メンバーシップを検出する組み込みロジックを使用してノード全体で動的に集計する重要なメトリックの整理された一覧を提供します。 すべての値は、リアルタイムの時点のみです。  

## <a name="usage-in-powershell"></a>PowerShell の使用率

記憶域スペース ダイレクト クラスター全体のメトリックを取得するのにには、このコマンドレットを使用します。

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

省略可能な**カウント**パラメーターは、戻るには、1 秒間隔で値の数に設定を示します。  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

1 つの特定のボリュームまたはサーバーのメトリックを取得することもできます。  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET および c# での使用率

### <a name="connect"></a>接続

ヘルス サービスを照会するために確立する必要があります、**CimSession**クラスターとします。 を行うには、フル .NET でのみ使用されるものが必要になりますので、意味することはできませんしやすくなりましたから直接実行 Web またはモバイル アプリ。 これらのコード サンプルは C \#、このデータ アクセス層の最も単純な選択肢で使用されます。

``` 
...
using System.Security;
using Microsoft.Management.Infrastructure;

public CimSession Connect(string Domain = "...", string Computer = "...", string Username = "...", string Password = "...")
{
    SecureString PasswordSecureString = new SecureString();
    foreach (char c in Password)
    {
        PasswordSecureString.AppendChar(c);
    }

    CimCredential Credentials = new CimCredential(
        PasswordAuthenticationMechanism.Default, Domain, Username, PasswordSecureString);
    WSManSessionOptions SessionOptions = new WSManSessionOptions();
    SessionOptions.AddDestinationCredentials(Credentials);
    Session = CimSession.Create(Computer, SessionOptions);
    return Session;
}
```

指定されたユーザー名は、ターゲット コンピューターのローカル管理者にする必要があります。

パスワードを作成することをお勧め**SecureString**直接でユーザー入力からリアルタイムでため、パスワードことはありませんメモリに格納クリア テキストでします。 これは、さまざまなセキュリティの問題を軽減できます。 実際には、上記とを構築するが一般的プロトタイプを作成します。

### <a name="discover-objects"></a>オブジェクトを検出します。

**CimSession**確立されると、クエリを実行できます Windows Management Instrumentation (WMI)、クラスターでします。

障害またはメトリックを取得することができます、いくつかの関連するオブジェクトのインスタンスを取得する必要があります。 まず、**MSFT\_StorageSubSystem**クラスターで記憶域スペース ダイレクトを表します。 使用すると、表示できるようにすべて**MSFT\_StorageNode**、クラスター内と各**MSFT\_Volume**、データ ボリューム。 最後に、必要があります、**MSFT\_StorageHealth**、ヘルス サービス自体、すぎます。

```
CimInstance Cluster;
List<CimInstance> Nodes;
List<CimInstance> Volumes;
CimInstance HealthService;

public void DiscoverObjects(CimSession Session)
{
    // Get MSFT_StorageSubSystem for Storage Spaces Direct
    Cluster = Session.QueryInstances(@"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageSubSystem")
        .First(Instance => (Instance.CimInstanceProperties["FriendlyName"].Value.ToString()).Contains("Cluster"));

    // Get MSFT_StorageNode for each cluster node
    Nodes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageNode", null, "StorageSubSystem", "StorageNode").ToList();

    // Get MSFT_Volumes for each data volume
    Volumes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToVolume", null, "StorageSubSystem", "Volume").ToList();

    // Get MSFT_StorageHealth itself
    HealthService = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageHealth", null, "StorageSubSystem", "StorageHealth").First();
}
```

これらは、同じオブジェクトと同様にコマンドレットを使用して PowerShell で取得した**Get-storagesubsystem**、**Get-storagenode**、および**Get-volume**します。

プロパティにアクセスできますすべて同じに記載されている[記憶域管理 API クラス](https://msdn.microsoft.com/en-us/library/windows/desktop/hh830612(v=vs.85).aspx)します。

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

呼び出す**GetReport**エキスパート選曲の一覧を効率的に収集され、クラスター メンバーシップを検出する組み込みロジックを使用してノード全体で動的に集計する、重要なメトリックのサンプルをストリームを開始します。 サンプルには、その後、毎秒、到着します。 すべての値は、リアルタイムの時点のみです。

次の 3 つのスコープに対してメトリックをストリーミングすることができます: クラスター、任意のノード、または任意のボリューム。

Windows Server 2016 では、各スコープで使用可能なメトリックの完全なリストは、以下に記載されています。

### <a name="iobserveronnext"></a>IObserver.OnNext()

このサンプル コードを使用して、[デザイン パターン](https://msdn.microsoft.com/en-us/library/ee850490(v=vs.110).aspx)オブザーバーを実装するが**OnNext()**到着するとメトリックの新しい各サンプル メソッドが呼び出されます。 その**OnCompleted()**メソッドが呼び出される場合は/終了をストリーミングする場合。 たとえば、可能性がありますを使用ストリーミング、再開するのにため、無期限に続行します。

```
class MetricsObserver<T> : IObserver<T>
{
    public void OnNext(T Result)
    {
        // Cast
        CimMethodStreamedResult StreamedResult = Result as CimMethodStreamedResult;

        if (StreamedResult != null)
        {
            // For illustration, you could store the metrics in this dictionary
            Dictionary<string, string> Metrics = new Dictionary<string, string>();

            // Unpack
            CimInstance Report = (CimInstance)StreamedResult.ItemValue;
            IEnumerable<CimInstance> Records = (IEnumerable<CimInstance>)Report.CimInstanceProperties["Records"].Value;
            foreach (CimInstance Record in Records)
            {
                /// Each Record has "Name", "Value", and "Units"
                Metrics.Add(
                    Record.CimInstanceProperties["Name"].Value.ToString(),
                    Record.CimInstanceProperties["Value"].Value.ToString()
                    );
            }

            // TODO: Whatever you want!
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Reinvoke BeginStreamingMetrics(), defined in the next section
    }
}
```

### <a name="begin-streaming"></a>ストリームを開始します。

定義されているオブザーバー、ストリーミングを開始できます。

ターゲット指定**CimInstance**メトリックを対象とするとします。 クラスター、任意のノード、またはボリュームを指定できます。

Count パラメーターの値は、サンプルの数をストリーミングが終了する前にです。

```
CimInstance Target = Cluster; // From among the objects discovered in DiscoverObjects()

public void BeginStreamingMetrics(CimSession Session, CimInstance HealthService, CimInstance Target)
{
    // Set Parameters
    CimMethodParametersCollection MetricsParams = new CimMethodParametersCollection();
    MetricsParams.Add(CimMethodParameter.Create("TargetObject", Target, CimType.Instance, CimFlags.In));
    MetricsParams.Add(CimMethodParameter.Create("Count", 999, CimType.UInt32, CimFlags.In));
    // Enable WMI Streaming
    CimOperationOptions Options = new CimOperationOptions();
    Options.EnableMethodResultStreaming = true;
    // Invoke API
    CimAsyncMultipleResults<CimMethodResultBase> InvokeHandler;
    InvokeHandler = Session.InvokeMethodAsync(
        HealthService.CimSystemProperties.Namespace, HealthService, "GetReport", MetricsParams, Options
        );
    // Subscribe the Observer
    MetricsObserver<CimMethodResultBase> Observer = new MetricsObserver<CimMethodResultBase>(this);
    IDisposable Disposeable = InvokeHandler.Subscribe(Observer);
}
```

言うまでも、これらのメトリックを視覚化する、データベースに格納されている、または適切にどのような方法で使用します。

### <a name="properties-of-reports"></a>レポートのプロパティ

メトリックのすべてのサンプルは、1 つ「レポート」個々 の測定基準に対応する"多く"レコードが含まれています。

フル スキーマ、検査、**MSFT\_StorageHealthReport**と**MSFT\_HealthRecord**クラス*storagewmi.mof*します。

各メトリックには、下の表に従って、3 つのプロパティがあります。

| **プロパティ** | **使用例**       |
| -------------|-------------------|
| 名         | IOLatencyAverage  |
| 値        | 0.00021           |
| 単位        | 3                 |

ユニット = {0, 1、2、3, 4}、0 =""(バイト単位) 1 ="BytesPerSecond"、2 = 3"CountPerSecond"="Seconds"、または 4 =「%」です。

## <a name="coverage"></a>カバレッジ

Windows Server 2016 では、各スコープに対して利用可能なメトリックを次に示します。

### <a name="msftstoragesubsystem"></a>MSFT_StorageSubSystem

| **名**                        | **単位** |
|---------------------------------|-----------|
| 稼働                        | 4         |
| CapacityPhysicalPooledAvailable | 0         |
| CapacityPhysicalPooledTotal     | 0         |
| CapacityPhysicalTotal           | 0         |
| CapacityPhysicalUnpooled        | 0         |
| CapacityVolumesAvailable        | 0         |
| CapacityVolumesTotal            | 0         |
| IOLatencyAverage                | 3         |
| IOLatencyRead                   | 3         |
| IOLatencyWrite                  | 3         |
| IOPSRead                        | 2         |
| IOPSTotal                       | 2         |
| IOPSWrite                       | 2         |
| IOThroughputRead                | 1         |
| IOThroughputTotal               | 1         |
| IOThroughputWrite               | 1         |
| MemoryAvailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msftstoragenode"></a>MSFT_StorageNode

| **名**            | **単位** |
|---------------------|-----------|
| 稼働            | 4         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |
| MemoryAvailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msftvolume"></a>MSFT_Volume

| **名**            | **単位** |
|---------------------|-----------|
| CapacityAvailable   | 0         |
| CapacityTotal       | 0         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| IOThroughputRead    | 1         |
| IOThroughputTotal   | 1         |
| IOThroughputWrite   | 1         |

## <a name="see-also"></a>参照してください。

- [Windows Server 2016 のヘルス サービス](health-service-overview.md)
