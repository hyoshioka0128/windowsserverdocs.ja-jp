---
title: ヘルス サービスをレポートします。
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: e018c0270a0bf410dada9c05d2c25e51fdfac1d8
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280161"
---
# <a name="health-service-reports"></a>ヘルス サービスをレポートします。
> 適用対象:Windows Server 2019、Windows Server 2016

## <a name="what-are-reports"></a>レポートとは  

ヘルス サービスでは、記憶域スペース ダイレクト クラスターから現在のパフォーマンスと容量の情報を取得するために必要な作業が減少します。 1 つの新しいコマンドレットは、効率的に収集され、クラスター メンバーシップを検出するロジックを組み込むと、ノード間で動的に集計された重要なメトリックを精選した一覧を提供します。 値はすべて、リアルタイムかつ特定の時点のみのものです。  

## <a name="usage-in-powershell"></a>PowerShell での使用法

記憶域スペース ダイレクト クラスター全体のメトリックを取得するのにには、このコマンドレットを使用します。

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

省略可能な**カウント**パラメーターは、1 秒間隔で、返される値の数に設定を示します。  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

1 つの特定のボリュームまたはサーバーのメトリックを取得することもできます。  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET での使用状況とC#

### <a name="connect"></a>接続

ヘルス サービスのクエリを実行するために確立する必要があります、 **CimSession**クラスター。 完全な .NET で使用できるだけのものが必要になりますのでには、つまり簡単にできない web またはモバイル アプリから直接。 次のコード サンプルは C# を使用して\#最も簡単ですこのデータ アクセス層を選択します。

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

指定されたユーザー名には、ターゲット コンピューターのローカル管理者をする必要があります。

パスワードを構築することをお勧め**SecureString**直接におけるユーザー入力からリアルタイムでため自分のパスワードは決してメモリに格納クリア テキストでします。 これは、さまざまなセキュリティ上の問題を軽減できます。 実際には、上記の構築が一般的でプロトタイプを作成します。

### <a name="discover-objects"></a>オブジェクトを検出します。

**CimSession**確立されると、クエリ可能な Windows Management Instrumentation (WMI) クラスター。

障害またはメトリックを取得する前に、いくつかの関連するオブジェクトのインスタンスを取得する必要があります。 最初に、 **MSFT\_StorageSubSystem**クラスターで記憶域スペース ダイレクトを表します。 取得できますを使用して、すべて**MSFT\_StorageNode** 、クラスターで、毎回**MSFT\_ボリューム**、データ ボリューム。 最後に、する必要があります、 **MSFT\_StorageHealth**、正常性サービス自体、すぎます。

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

これらは、同じオブジェクトのようなコマンドレットを使用して PowerShell で取得した**Get-storagesubsystem**、 **Get-storagenode**、および**Get-volume**します。

記載されているプロパティをすべて同じアクセスできる[記憶域管理 API クラス](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx)します。

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

呼び出す**GetReport**エキスパート curated が効率的に収集され、クラスター メンバーシップを検出するロジックを組み込むと、ノード間で動的に集計されますが、重要なメトリックのリストのサンプルのストリーミングを開始します。 サンプルには、その後、毎秒、到着します。 値はすべて、リアルタイムかつ特定の時点のみのものです。

メトリックは、次の 3 つのスコープにストリーミングできます。 クラスター、任意のノード、または任意のボリューム。

Windows Server 2016 の各スコープで使用可能なメトリックの完全な一覧は、以下に記載されています。

### <a name="iobserveronnext"></a>IObserver.OnNext()

このサンプル コードを使用して、[オブザーバー デザイン パターン](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx)オブザーバーを実装するために持つ**OnNext()** メトリックの新しい各サンプルが到着すると、メソッドが呼び出されます。 その**OnCompleted()** メソッドが呼び出される場合、/終了をストリーミングする場合。 たとえば、可能性があります使用する、ストリーミングを再開するのにため、無期限に続行します。

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

### <a name="begin-streaming"></a>ストリーミングを開始します。

オブザーバーが定義されている、ストリーミングを開始できます。

ターゲット指定**CimInstance**スコープ メトリックをします。 クラスター、任意のノード、または任意のボリュームを指定できます。

カウント パラメーターは、ストリーミングが終了する前にサンプルの数。

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

もちろん、これらのメトリックを視覚化する、データベースに格納されているまたは自由な方法で使用されます。

### <a name="properties-of-reports"></a>レポートのプロパティ

メトリックの各サンプルは 1 つ「レポート」メトリックを個別に対応する"多数"レコードを含むです。

完全なスキーマでは、検査、 **MSFT\_StorageHealthReport**と**MSFT\_HealthRecord**クラス*storagewmi.mof*します。

各メトリックには、このテーブルごとの 3 つのプロパティがあります。

| **プロパティ** | **例**       |
| -------------|-------------------|
| 名前         | IOLatencyAverage  |
| Value        | 0.00021           |
| 単位        | 3                 |

単位 = {0, 1、2、3, 4}、0 = 1 ("Bytes"、"BytesPerSecond"、2 = ="CountPerSecond"、3 ="Seconds"、または 4「割合」を =。

## <a name="coverage"></a>対象範囲

Windows Server 2016 では、各スコープの使用可能なメトリックを次に示します。

### <a name="msftstoragesubsystem"></a>MSFT_StorageSubSystem

| **名前**                        | **ユニット** |
|---------------------------------|-----------|
| CPUUsage                        | 4         |
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

| **名前**            | **ユニット** |
|---------------------|-----------|
| CPUUsage            | 4         |
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

| **名前**            | **ユニット** |
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

## <a name="see-also"></a>関連項目

- [Windows Server 2016 でヘルス サービス](health-service-overview.md)
