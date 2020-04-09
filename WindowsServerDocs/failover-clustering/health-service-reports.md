---
title: レポートのヘルスサービス
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 3b47e1abf3805b7e6e3dc180d5d937ddb2723fa4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827545"
---
# <a name="health-service-reports"></a>レポートのヘルスサービス
> 適用対象: Windows Server 2019、Windows Server 2016

## <a name="what-are-reports"></a>レポートとは  

ヘルスサービスにより、記憶域スペースダイレクトクラスターからパフォーマンスと容量に関するライブ情報を取得するために必要な作業が減少します。 1つの新しいコマンドレットには、クラスターメンバーシップを検出するための組み込みロジックを使用して、効率的に収集され、ノード間で動的に集計される、重要なメトリックの curated リストが用意されています。 値はすべて、リアルタイムかつ特定の時点のみのものです。  

## <a name="usage-in-powershell"></a>PowerShell での使用法

このコマンドレットを使用して、記憶域スペースダイレクトクラスター全体のメトリックを取得します。

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

省略可能な**Count**パラメーターは、1秒間隔で返される値のセット数を示します。  

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>  
```

また、1つの特定のボリュームまたはサーバーのメトリックを取得することもできます。  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>  

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>.NET およびでの使用C#

### <a name="connect"></a>接続

ヘルスサービスを照会するには、クラスターで**CimSession**を確立する必要があります。 これを行うには、完全な .NET でしか使用できないものが必要になります。つまり、web アプリまたはモバイルアプリから直接この操作を行うことはできません。 これらのコードサンプルでは、このデータアクセス層で最も単純な選択である C\#を使用します。

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

指定されたユーザー名は、対象のコンピューターのローカル管理者である必要があります。

パスワード**SecureString**をユーザー入力から直接作成することをお勧めします。そのため、パスワードはクリアテキストでメモリに格納されることはありません。 これは、さまざまなセキュリティの問題を軽減するのに役立ちます。 しかし実際には、プロトタイプ作成は、プロトタイプ作成の目的では一般的です。

### <a name="discover-objects"></a>オブジェクトを検出します

**CimSession**を確立したら、クラスターで WINDOWS MANAGEMENT INSTRUMENTATION (WMI) を照会できます。

エラーまたはメトリックを取得するには、いくつかの関連オブジェクトのインスタンスを取得する必要があります。 まず、 **MSFT\_StorageSubSystem**がクラスター上の記憶域スペースダイレクトを表します。 これを使用すると、クラスター内のすべての**msft\_storagenode**およびすべての**msft\_ボリューム**(データボリューム) を取得できます。 最後に、 **MSFT\_StorageHealth**、ヘルスサービス自体も必要になります。

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

これらは、 **StorageSubSystem**、 **get-storagenode**ようなコマンドレットを使用して PowerShell で**取得した**ものと同じオブジェクトです。

「[ストレージ管理 API クラス](https://msdn.microsoft.com/library/windows/desktop/hh830612(v=vs.85).aspx)」で説明されているすべての同じプロパティにアクセスできます。

```
...
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

**Getreport**を呼び出して、重要なメトリックの curated リストのストリーミングサンプルを開始します。これは、クラスターメンバーシップを検出するための組み込みロジックを使用して、効率的に収集され、ノード間で動的に集計されます。 サンプルは、その後、1秒ごとに到着します。 値はすべて、リアルタイムかつ特定の時点のみのものです。

メトリックは、クラスター、任意のノード、任意のボリュームの3つのスコープに対してストリーミングできます。

Windows Server 2016 の各スコープで利用可能なメトリックの完全な一覧については、次のドキュメントを参照してください。

### <a name="iobserveronnext"></a>IObserver. OnNext ()

このサンプルコードでは、[オブザーバーデザインパターン](https://msdn.microsoft.com/library/ee850490(v=vs.110).aspx)を使用して、新しいメトリックの各サンプルが到着したときに**onnext ()** メソッドが呼び出されるオブザーバーを実装します。 **Oncompleted ()** メソッドは、streaming が終了した場合に呼び出されます。 たとえば、ストリーミングを再開に使用して、無期限に続行することができます。

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

### <a name="begin-streaming"></a>ストリーミングの開始

オブザーバーを定義したら、ストリーミングを開始できます。

メトリックの対象となるターゲット**CimInstance**を指定します。 クラスター、任意のノード、任意のボリュームを指定できます。

Count パラメーターは、ストリーミングが終了する前のサンプルの数です。

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

言うまでもなく、これらのメトリックは視覚化したり、データベースに格納したり、最適な方法で使用したりすることができます。

### <a name="properties-of-reports"></a>レポートのプロパティ

メトリックのすべてのサンプルは、個々のメトリックに対応する多くの "レコード" を含む "レポート" です。

完全なスキーマの場合は、 **msft\_StorageHealthReport**と**msft\_HealthRecord** *クラスを調べます。*

各メトリックには、このテーブルにつき3つのプロパティしかありません。

| **"** | **例**       |
| -------------|-------------------|
| Name         | IOLatencyAverage  |
| 値        | 0.00021           |
| 単位        | 3                 |

Units = {0, 1, 2, 3, 4}、0 = "Bytes"、1 = "BytesPerSecond"、2 = "CountPerSecond"、3 = "Seconds"、または 4 = "パーセント"。

## <a name="coverage"></a>カバレッジ

Windows Server 2016 の各スコープで使用可能なメトリックを以下に示します。

### <a name="msft_storagesubsystem"></a>MSFT_StorageSubSystem

| **名前**                        | **部署** |
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
| Ioread Putread                | 1         |
| Ioby Puttotal               | 1         |
| IOThroughputWrite               | 1         |
| MemoryAvailable                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msft_storagenode"></a>MSFT_StorageNode

| **名前**            | **部署** |
|---------------------|-----------|
| CPUUsage            | 4         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| Ioread Putread    | 1         |
| Ioby Puttotal   | 1         |
| IOThroughputWrite   | 1         |
| MemoryAvailable     | 0         |
| MemoryTotal         | 0         |

### <a name="msft_volume"></a>MSFT_Volume

| **名前**            | **部署** |
|---------------------|-----------|
| CapacityAvailable   | 0         |
| CapacityTotal       | 0         |
| IOLatencyAverage    | 3         |
| IOLatencyRead       | 3         |
| IOLatencyWrite      | 3         |
| IOPSRead            | 2         |
| IOPSTotal           | 2         |
| IOPSWrite           | 2         |
| Ioread Putread    | 1         |
| Ioby Puttotal   | 1         |
| IOThroughputWrite   | 1         |

## <a name="see-also"></a>参照

- [Windows Server 2016 のヘルスサービス](health-service-overview.md)
