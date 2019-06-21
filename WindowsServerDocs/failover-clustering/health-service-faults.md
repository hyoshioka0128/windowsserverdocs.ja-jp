---
title: ヘルス サービスの障害
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 72b1593503db75aa275b9eb45c8342cee6724001
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280398"
---
# <a name="health-service-faults"></a>ヘルス サービスの障害
> 適用対象:Windows Server 2019、Windows Server 2016

## <a name="what-are-faults"></a>エラーとは

ヘルス サービスは、常に問題を検出し、「エラー」を生成するように記憶域スペース ダイレクト クラスターを監視します。 1 つの新しいコマンドレットは、すべてのエンティティを参照せず、展開の正常性を確認または機能を順番を簡単にすることができます、現在の障害を表示します。 障害は正確で理解しやすく、意思決定に役立つように設計されています。  

各エラーには、5 つの重要なフィールドが含まれています。  

-   重大度
-   問題の説明
-   問題への対処に推奨される次のステップ
-   障害が発生したエンティティの識別情報
-   物理的な場所 (該当する場合)

たとえば、一般的な障害は次のとおりです。  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > 物理的な場所は、障害ドメインの構成から取得されます。 障害ドメインの詳細については、次を参照してください。 [Windows Server 2016 での障害ドメイン](fault-domains.md)します。 こうした情報を指定していない場合、スロット番号しか表示されないなどのように、場所フィールドがあまり役に立ちません。  

## <a name="root-cause-analysis"></a>根本原因分析

ヘルス サービスは、エラーを特定して、同じ基になる問題の結果である障害を組み合わせるエンティティ間の潜在的な因果関係を評価できます。 影響の連鎖を認識することにより、レポートに記載される分量が絞られます。 たとえば、サーバーがダウンしている場合は、サーバー内の任意のドライブにも接続を使用しないなりますよりも想定されます。 そのため、根本原因 - この場合、サーバーの 1 つだけのエラーが生成されます。  

## <a name="usage-in-powershell"></a>PowerShell での使用法

PowerShell での現在の障害を表示するには、このコマンドレットを実行します。

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

これにより、記憶域スペース ダイレクト クラスター全体に影響する障害が返されます。 ほとんどの場合、このようなエラーは、ハードウェアまたは構成に関連します。 エラーがない場合、このコマンドレットは何も返しませんされます。  

>[!NOTE]
> 非運用環境では、ご自身の責任で、自分でエラーをトリガーすることによって - たとえば、1 つの物理ディスクを削除するか、1 つのノードをシャット ダウンしてこの機能で実験できます。 エラーが表示されているとは、物理ディスクまたはノードと、障害は再び表示されなく再起動を再び挿入します。

特定のボリュームまたはファイル共有と、次のコマンドレットのみに影響を与えるエラーを表示することもできます。  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

特定のボリュームまたはファイル共有のみに影響を与えるすべてのエラーが返されます。 ほとんどの場合、このようなエラーは、容量計画、データの回復性、または記憶域サービスの品質や記憶域レプリカなどの機能に関連します。 

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

### <a name="query-faults"></a>クエリ エラー

呼び出す**診断**スコープ ターゲットに現在の障害を取得する**CimInstance**、クラスターまたは任意のボリュームがあります。

Windows Server 2016 の各スコープで使用可能なエラーの完全な一覧は、以下に記載されています。

```       
public void GetFaults(CimSession Session, CimInstance Target)
{
    // Set Parameters (None)
    CimMethodParametersCollection FaultsParams = new CimMethodParametersCollection();
    // Invoke API
    CimMethodResult Result = Session.InvokeMethod(Target, "Diagnose", FaultsParams);
    IEnumerable<CimInstance> DiagnoseResults = (IEnumerable<CimInstance>)Result.OutParameters["DiagnoseResults"].Value;
    // Unpack
    if (DiagnoseResults != null)
    {
        foreach (CimInstance DiagnoseResult in DiagnoseResults)
        {
            // TODO: Whatever you want!
        }
    }
}
```

### <a name="optional-myfault-class"></a>省略可能: MyFault クラス

構築し、エラーの独自の表現を保持するが合理的可能性があります。 たとえば、この**MyFault**クラスなど、エラーのいくつかのキー プロパティを格納する、 **FaultId**、更新プログラムを関連付けるか、通知を削除または重複除去を後でを使用できますイベントで何らかの理由から、複数回、同じエラーが検出されました。

```       
public class MyFault {
    public String FaultId { get; set; }
    public String Reason { get; set; }
    public String Severity { get; set; }
    public String Description { get; set; }
    public String Location { get; set; }

    // Constructor
    public MyFault(CimInstance DiagnoseResult)
    {
        CimKeyedCollection<CimProperty> Properties = DiagnoseResult.CimInstanceProperties;
        FaultId     = Properties["FaultId"                  ].Value.ToString();
        Reason      = Properties["Reason"                   ].Value.ToString();
        Severity    = Properties["PerceivedSeverity"        ].Value.ToString();
        Description = Properties["FaultingObjectDescription"].Value.ToString();
        Location    = Properties["FaultingObjectLocation"   ].Value.ToString();
    }
}
```

```
List<MyFault> Faults = new List<MyFault>;

foreach (CimInstance DiagnoseResult in DiagnoseResults)
{
    Faults.Add(new Fault(DiagnoseResult));
}
```

各エラー プロパティの完全な一覧 (**DiagnoseResult**) 以下で説明します。

### <a name="fault-events"></a>エラー イベント

エラーは、作成、削除、または更新は、ヘルス サービスでは WMI イベントが生成されます。 これらは、頻繁にポーリングなしで同期、アプリケーションの状態を維持するために不可欠であり、たとえば電子メール通知を送信するタイミングの決定などに役立ちます。 これらのイベントをサブスクライブするには、は、このサンプル コードは、オブザーバー デザイン パターンをもう一度使用します。

まず、購読**MSFT\_StorageFaultEvent**イベント。

```      
public void ListenForFaultEvents()
{
    IObservable<CimSubscriptionResult> Events = Session.SubscribeAsync(
        @"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageFaultEvent");
    // Subscribe the Observer
    FaultsObserver<CimSubscriptionResult> Observer = new FaultsObserver<CimSubscriptionResult>(this);
    IDisposable Disposeable = Events.Subscribe(Observer);
}   
```

次に、オブザーバーを実装が**OnNext()** メソッドが新しいイベントが生成されるたびに呼び出されます。

各イベントが含まれる**ChangeType**かどうか、エラー作成、削除、または更新、および関連することを示す**FaultId**します。

さらに、違反自体のすべてのプロパティが含まれます。

```
class FaultsObserver : IObserver
{
    public void OnNext(T Event)
    {
        // Cast
        CimSubscriptionResult SubscriptionResult = Event as CimSubscriptionResult;

        if (SubscriptionResult != null)
        {
            // Unpack            
            CimKeyedCollection<CimProperty> Properties = SubscriptionResult.Instance.CimInstanceProperties;
            String ChangeType = Properties["ChangeType"].Value.ToString();
            String FaultId = Properties["FaultId"].Value.ToString();

            // Create
            if (ChangeType == "0")
            {
                Fault MyNewFault = new MyFault(SubscriptionResult.Instance);
                // TODO: Whatever you want!
            }
            // Remove
            if (ChangeType == "1")
            {
                // TODO: Use FaultId to find and delete whatever representation you have...
            }
            // Update
            if (ChangeType == "2")
            {
                // TODO: Use FaultId to find and modify whatever representation you have...
            }
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Nothing
    }
}
```

### <a name="understand-fault-lifecycle"></a>障害のライフ サイクルを理解します。

エラーは、「表示」またはユーザーによって解決済みとしてマークする意図されていません。 ヘルス サービスでは、問題を確認できます不要になった場合にのみ、ヘルス サービスは、問題を監視し、自動的に削除されるときに作成されます。 一般に、これは、問題が解決されることが反映されます。

ただし、場合によっては、エラー可能性がありますを再検出するヘルス サービス (例: フェールオーバー後、または断続的な接続などが原因)。 します。 このためが理にかなって簡単に除去することができますので、フォールトの独自の表現を保持します。 これは、電子メール アラートまたはそれと同等に送信する場合に特に重要です。

### <a name="properties-of-faults"></a>エラーのプロパティ

このテーブルは、エラー オブジェクトのいくつかのキー プロパティを表示します。 完全なスキーマでは、検査、 **MSFT\_StorageDiagnoseResult**クラス*storagewmi.mof*します。

| **プロパティ**              | **例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Reason                    | 「ボリューム領域が不足して利用可能です。」                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット 11                                        |
| RecommendedActions        | {「展開ボリューム。」,「ワークロードは他のボリュームに移行します」}   |

**FaultId** 1 つのクラスターのスコープ内で一意です。

**PerceivedSeverity** PerceivedSeverity = {4, 5, 6} {"Informational"、"Warning"、「エラー」} を = または同等の色を青、黄、赤など。

**FaultingObjectDescription**ハードウェア、ソフトウェア オブジェクトの通常空白の情報をパートします。

**FaultingObjectLocation**ソフトウェア オブジェクトの通常空白のハードウェアには、位置情報。

**RecommendedActions**に独立している、推奨される操作の任意の順序で一覧します。 現在、この一覧は、長さ 1 の多くの場合は。

## <a name="properties-of-fault-events"></a>エラー イベントのプロパティ

このテーブルは、障害イベントのいくつかのキー プロパティを表示します。 完全なスキーマでは、検査、 **MSFT\_StorageFaultEvent**クラス*storagewmi.mof*します。

注、 **ChangeType**、かどうか、フォールト作成、削除、または、更新されたことを示しますが、 **FaultId**します。 イベントには、影響を受けたフォールトのすべてのプロパティも含まれています。

| **プロパティ**              | **例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| Reason                    | 「ボリューム領域が不足して利用可能です。」                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット 11                                        |
| RecommendedActions        | {「展開ボリューム。」,「ワークロードは他のボリュームに移行します」}   |

**ChangeType** ChangeType = { 0, 1, 2 } = { "Create", "Remove", "Update" }.

## <a name="coverage"></a>対象範囲

Windows Server 2016 では、ヘルス サービスは、次のエラーのカバレッジを提供します。  

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* ［重要度］:警告
* 理由: *「物理ディスクが失敗しました。」*
* RecommendedAction: *「物理ディスクを交換します。」*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* ［重要度］:警告
* 理由: *「接続が失われた物理ディスクにします。」*
* RecommendedAction: *「物理ディスクは、機能し、正しく接続されていることを確認」します。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* ［重要度］:警告
* 理由: *「物理ディスクが発生している定期的な無応答。」*
* RecommendedAction: *「物理ディスクを交換します。」*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* ［重要度］:警告
* 理由: *「物理ディスクの障害は間もなく発生を予測します。」*
* RecommendedAction: *「物理ディスクを交換します。」*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* ［重要度］:警告
* 理由: *「物理ディスクが、ソリューションのベンダーでサポートされていないため、検疫された」。*
* RecommendedAction: *「物理ディスクはサポートされているハードウェアで置き換えます。」*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* ［重要度］:警告
* 理由: *「物理ディスクが検疫にそのファームウェアのバージョンが、ソリューションのベンダーでサポートされていません。」*
* RecommendedAction: *「対象のバージョンへの物理ディスクのファームウェアを更新」します。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* ［重要度］:警告
* 理由: *「物理ディスクが認識できないメタデータです」。*
* RecommendedAction: *"このディスクは、不明な記憶域プールからのデータを含めることができます。まず、このディスクに有用なデータがないことを確認し、ディスクをリセットします。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType:Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* ［重要度］:警告
* 理由: *「物理ディスクのファームウェアの更新が失敗した試行です。」*
* RecommendedAction: *「バイナリの別のファームウェアを使用してを実行してください。」*

### <a name="virtual-disk-2"></a>**仮想ディスク (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType:Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* ［重要度］:情報
* 理由: *"このボリュームのいくつかのデータは完全には回復できません。アクセス可能のままです。"*
* RecommendedAction: *「データの回復性を復元します。」*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType:Microsoft.Health.FaultType.VirtualDisks.Detached
* ［重要度］:重大
* 理由: *"ボリュームにアクセスできません。一部のデータが失われます。"*
* RecommendedAction: *"物理の確認やネットワークのすべての記憶装置の接続。必要がありますバックアップから復元する。"*

### <a name="pool-capacity-1"></a>**プールの容量 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType:Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* ［重要度］:警告
* 理由: *"記憶域プールには、推奨される最小の予約容量がありません。これは、機能を制限するドライブのエラーが発生した場合、データの回復性を復元します。"*
* RecommendedAction: *"記憶域プールに追加の容量を追加または容量を解放します。最小推奨予約は、展開によって異なりますが、容量の約 2 のドライブの価値が。"*

### <a name="volume-capacity-2sup1sup"></a>**ボリュームの容量 (2)** <sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType:Microsoft.Health.FaultType.Volume.Capacity
* ［重要度］:警告
* 理由: *「ボリューム領域が不足して利用可能です。」*
* RecommendedAction: *「ボリュームを拡張またはその他のボリュームにワークロードを移行します。」*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType:Microsoft.Health.FaultType.Volume.Capacity
* ［重要度］:重大
* 理由: *「ボリューム領域が不足して利用可能です。」*
* RecommendedAction: *「ボリュームを拡張またはその他のボリュームにワークロードを移行します。」*

### <a name="server-3"></a>**サーバー (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType:Microsoft.Health.FaultType.Server.Down
* ［重要度］:重大
* 理由: *「サーバーは到達できません。」*
* RecommendedAction: *「開始またはサーバーを交換します。」*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType:Microsoft.Health.FaultType.Server.Isolated
* ［重要度］:重大
* 理由: *「サーバーは、接続の問題によってクラスターから分離されます」。*
* RecommendedAction: *「確認して、ネットワーク分離が解決しない場合または他のノードにワークロードを移行します。」*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType:Microsoft.Health.FaultType.Server.Quarantined
* ［重要度］:重大
* 理由: *「サーバーは、定期的な障害によるクラスターによって検疫されたは、」。*
* RecommendedAction: *「サーバーの交換またはネットワークを修正します。」*

### <a name="cluster-1"></a>**クラスター (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType:Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* ［重要度］:重大
* 理由: *「クラスターがダウンしてから離れた場所の 1 つのサーバー エラー。」*
* RecommendedAction: *"、監視リソースを確認し、必要に応じて再起動します。開始するか失敗したサーバーを置き換えてください。"*

### <a name="network-adapterinterface-4"></a>**ネットワーク アダプターまたはインターフェイス (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType:Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* ［重要度］:警告
* 理由: *「ネットワーク インターフェイスになる切断されました。」*
* RecommendedAction: *「ネットワーク ケーブルを再接続します。」*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType:Microsoft.Health.FaultType.NetworkInterface.Missing
* ［重要度］:警告
* 理由: *「{サーバー} が {クラスター ネットワーク} のクラスター ネットワークに接続されているアダプターのネットワークがありません。」*
* RecommendedAction: *「サーバーは、不足しているクラスター ネットワークに接続します。」*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType:Microsoft.Health.FaultType.NetworkAdapter.Hardware
* ［重要度］:警告
* 理由: *"ネットワーク インターフェイス ハードウェア障害をしました。"*
* RecommendedAction: *「ネットワーク インターフェイス アダプターを交換します。」*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType:Microsoft.Health.FaultType.NetworkAdapter.Disabled
* ［重要度］:警告
* 理由: *「ネットワーク インターフェイス {0} ネットワーク インターフェイス} は無効になっておりが使用されていない」。*
* RecommendedAction: *「ネットワーク インターフェイスを有効にします。」*

### <a name="enclosure-6"></a>**エンクロージャ (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* ［重要度］:警告
* 理由: *「通信が失われました記憶域エンクロージャを。」*
* RecommendedAction: *「開始または記憶域エンクロージャを置き換えます。」*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.FanError
* ［重要度］:警告
* 理由: *「記憶域エンクロージャの位置 {0} 位置} のファンが失敗しました。」*
* RecommendedAction: *「ファン、記憶域エンクロージャに交換してください。」*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* ［重要度］:警告
* 理由: *「記憶域エンクロージャの位置 {0} 位置} にある現在のセンサーが失敗しました。」*
* RecommendedAction: *「記憶域エンクロージャ内の現在のセンサーを置換します。」*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* ［重要度］:警告
* 理由: *「記憶域エンクロージャの位置 {0} 位置} 電圧センサーが失敗しました。」*
* RecommendedAction: *「記憶域エンクロージャの電圧センサーを置換します。」*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* ［重要度］:警告
* 理由: *「IO コント ローラー、記憶域エンクロージャの位置 {0} 位置} で失敗しました。」*
* RecommendedAction: *「記憶域エンクロージャで IO がコント ローラーを交換してください。」*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType:Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* ［重要度］:警告
* 理由: *「記憶域エンクロージャの位置 {0} 位置} で、温度センサーが失敗しました。」*
* RecommendedAction: *「記憶域エンクロージャ内の温度センサーを置換します。」*

### <a name="firmware-rollout-3"></a>**ファームウェアのロールアウト (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType:Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* ［重要度］:警告
* 理由: *「現在できません。 ファームウェアのロールアウトを実行するときに、進行状況を確認します。」*
* RecommendedAction: *「すべての記憶域スペースは正常であり、および障害ドメインがない現在メンテナンス モードでを確認します。」*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType:Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* ［重要度］:警告
* 理由: *「ファームウェアのロールアウトは、ファームウェアの更新プログラムを適用した後に読み取り不可能なまたは予期しないファームウェアのバージョン情報のためにキャンセルされました」。*
* RecommendedAction: *「再起動ファームウェアのロールアウト ファームウェアの問題が解決されたとします。」*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType:Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* ［重要度］:警告
* 理由: *「ファームウェアのロールアウトはファームウェアの更新の試行が失敗している物理ディスクが多すぎるため取り消されました。」*
* RecommendedAction: *「再起動ファームウェアのロールアウト ファームウェアの問題が解決されたとします。」*

### <a name="storage-qos-3sup2sup"></a>**記憶域の QoS (3)** <sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType:Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* ［重要度］:警告
* 理由: *「記憶域のスループットは予約を満たすのに十分です。」*
* RecommendedAction: *「記憶域の QoS ポリシーを再構成します。」*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType:Microsoft.Health.FaultType.StorQos.LostCommunication
* ［重要度］:警告
* 理由: *「記憶域の QoS ポリシー マネージャーが、ボリュームとの通信を失いました。 が」*
* RecommendedAction: *「{のノード} のノードを再起動してください」*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType:Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* ［重要度］:警告
* 理由: *「1 つまたは複数の記憶域コンシューマー (通常は仮想マシン) を使用している、存在しないポリシー id {id}。」*
* RecommendedAction: *「すべての不足している記憶域の QoS ポリシーを再作成します。」*

<sup>1</sup>ボリュームは 80% に達した (重要度のマイナー) または 90% に達した (重大度: メジャー) に達したことを示します。  
<sup>2</sup>一部 .vhd(s) ボリューム上の最小 IOPS を満たしていないことを示します経由の 10% (マイナー)、30% (メジャー)、または 50% の 24 時間の期間 (重大)。  

>[!NOTE]
> ファン、電源、センサーなどのストレージ格納装置コンポーネントの正常性は、SCSI エンクロージャ サービス (SES) から取得されます。 この情報は、ベンダーから提供されていない場合はヘルス サービスで表示されません。  

## <a name="see-also"></a>関連項目

- [Windows Server 2016 でヘルス サービス](health-service-overview.md)
