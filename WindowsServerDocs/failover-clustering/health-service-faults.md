---
title: "ヘルス サービス障害"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: c9e1fb4568ee93739c49ccc1a13106b09161c5f3
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-faults"></a>ヘルス サービス障害
> Windows Server 2016 に適用されます。

## <a name="what-are-faults"></a>障害は何ですか。

ヘルス サービスは、常に、問題を検出して「障害」を生成する、記憶域スペース ダイレクト クラスターを監視します。 1 つの新しいコマンドレットでは、すべてのエンティティを見ず、展開の状態を確認します。または、機能を順番に簡単にすることが、現在の障害が表示されます。 障害は正確な理解しやすく、および実践的な設計されています。  

それぞれの障害には、5 つの重要なフィールドが含まれています。  

-   重要度
-   問題の説明
-   問題に対処する推奨される次のステップ
-   障害が発生したエンティティの識別情報
-   物理的な場所 (該当する場合)

たとえば、一般的な障害を次に示します。  

```
Severity: MINOR                                         
Reason: Connectivity has been lost to the physical disk.                           
Recommendation: Check that the physical disk is working and properly connected.    
Part: Manufacturer Contoso, Model XYZ9000, Serial 123456789                        
Location: Seattle DC, Rack B07, Node 4, Slot 11
```

 >[!NOTE]
 > 物理的な場所は、障害ドメインの構成から取得されます。 障害ドメインの詳細については、次を参照してください。 [Windows Server 2016 での障害ドメイン](fault-domains.md)します。 この情報を提供していない場合、場所フィールドはあまり役に立ちませんになります - など、可能性がありますのみを表示スロットの数。  

## <a name="root-cause-analysis"></a>根本原因の分析

ヘルス サービスは、障害が発生して、特定して組み合わせるフォールト同じ基になる問題の結果であるエンティティの間での潜在的な原因を評価できます。 影響の連鎖を認識することでこれにより、分量レポートが少なくなります。 たとえば、サーバーがダウンしている場合、サーバー内の任意のドライブに接続せずなりますよりも予定です。 そのため、根本原因 - ここでは、サーバーの 1 つだけの障害が生成されます。  

## <a name="usage-in-powershell"></a>PowerShell の使用率

PowerShell の現在の障害を表示するには、このコマンドレットを実行します。

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem  
```

これには、記憶域スペース ダイレクト クラスター全体に影響を与える障害が返されます。 ほとんどの場合、これらの障害は、ハードウェアまたは構成に関連します。 障害がない場合、このコマンドレットは何も返しません。  

>[!NOTE]
> 非運用環境では、各自の責任で、自分で障害をトリガーすることによって - たとえば、1 つの物理ディスクを削除するか、1 つのノードをシャット ダウンしてこの機能を試すことができます。 障害が表示された後、再挿入、物理ディスクまたは再起動ノードと、障害は再び表示されなくなります。

特定のボリュームまたはファイル共有と、次のコマンドレットのみに影響を与えている障害を表示することもできます。  

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume  

Get-FileShare -Name <Name> | Debug-FileShare  
```

これには、特定のボリュームまたはファイル共有のみに影響を与える障害が返されます。 ほとんどの場合、これらの障害は、容量計画、データの回復性、または記憶域サービスの品質や記憶域レプリカなどの機能に関連します。 

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

### <a name="query-faults"></a>クエリの障害

呼び出す**診断**を対象とするターゲットの現在の障害を取得する**CimInstance**、クラスター、または任意のボリュームがあります。

Windows Server 2016 では、各スコープで使用可能な障害の完全なリストは、以下に記載されています。

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

合理的を構築し、障害の独自の表現を保持するためです。 たとえば、この**MyFault**クラスを含む、フォールトのいくつかのキー プロパティを格納する、**FaultId**、使用できる後で更新プログラムを関連付けるか、通知を削除するか、同じフォールトは、重複を除去するには何らかの理由で、複数回検出されました。

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

それぞれの障害のプロパティの完全なリスト (**DiagnoseResult**) の下に記載されています。

### <a name="fault-events"></a>障害イベント

障害を作成、削除すると、または更新すると、ヘルス サービスは、WMI イベントを生成します。 これらは、頻繁にポーリングなしで同期、アプリケーションの状態を維持するために不可欠であり、たとえば、電子メール アラートを送信するタイミングを決定するような作業を行うことができます。 これらのイベントをサブスクライブするは、このサンプル コードは、デザイン パターンをもう一度使用します。

最初にサブスクライブ**MSFT\_StorageFaultEvent**イベントです。

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

次に、オブザーバーの実装が**OnNext()**メソッドが、新しいイベントが生成されるたびに呼び出されます。

各イベントに含まれる**ChangeType**かどうか、フォールト作成、削除、または更新された、および関連することを示す**FaultId**します。

さらに、障害自体のすべてのプロパティが含まれます。

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

「表示」またはユーザーによって解決済みとしてマークする障害を使用することはありません。 ヘルス サービス監視の問題と、自動的に削除されると、ヘルス サービスでは、問題を確認できます不要になった場合にのみ作成されます。 一般に、問題が修正されたことが反映されます。

ただし、場合によっては、障害が発生可能性がありますを再検出するヘルス サービス (例: フェールオーバー後に、または断続的な接続などのため)。します。 このため、可能性がありますに意味が重複を除去することができます簡単にするために、フォールトの独自の表現を保持します。 これは、電子メール アラートまたはそれと同等に送信する場合に特に重要です。

### <a name="properties-of-faults"></a>障害のプロパティ

次の表は、フォールト オブジェクトのいくつかのキー プロパティを表示します。 フル スキーマ、検査、**MSFT\_StorageDiagnoseResult**クラスの*storagewmi.mof*します。

| **プロパティ**              | **使用例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| 理由                    | 「ボリューム領域が不足して利用可能です。」                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット 11                                        |
| RecommendedActions        | {「展開ボリューム。」、「ワークロードは他のボリュームに移行します」}   |

**FaultId** 1 つのクラスターのスコープ内で一意です。

**PerceivedSeverity** PerceivedSeverity = {4、5、6} = {「情報」、"Warning"と"Error"} または同等の色を青、黄、red などです。

**FaultingObjectDescription**ハードウェア、ソフトウェアのオブジェクトの通常、空白の情報の一部です。

**FaultingObjectLocation**ハードウェアは、位置情報は、ソフトウェアのオブジェクトの通常空白です。

**RecommendedActions**の一覧に独立した推奨される操作、および特定の順序でします。 今日では、この一覧は、長さが 1 の多くの場合です。

## <a name="properties-of-fault-events"></a>フォールト イベントのプロパティ

次の表は、フォールト イベントのいくつかのキー プロパティを表示します。 フル スキーマ、検査、**MSFT\_StorageFaultEvent**クラスの*storagewmi.mof*します。

注:、**ChangeType**、かどうか、フォールト作成、削除、または、更新されたことを示しますが、**FaultId**します。 イベントには、影響を受けるフォールトのすべてのプロパティも含まれます。

| **プロパティ**              | **使用例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft.Health.FaultType.Volume.Capacity                      |
| 理由                    | 「ボリューム領域が不足して利用可能です。」                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット 11                                        |
| RecommendedActions        | {「展開ボリューム。」、「ワークロードは他のボリュームに移行します」}   |

**ChangeType** ChangeType = {0, 1, 2} = {「作成」、「削除」、"Update"}。

## <a name="coverage"></a>カバレッジ

Windows Server 2016 では、ヘルス サービスは、次のフォールト カバレッジを提供します。  

### **<a name="physicaldisk-8"></a>PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedMedia
* 重要度: 警告
* 理由: *「物理ディスクに失敗しました」。*
* RecommendedAction: *「物理ディスクを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.LostCommunication
* 重要度: 警告
* 理由: *「接続が失われました、物理ディスクに」。*
* RecommendedAction: *「物理ディスクが動作していて正しく接続されていることを確認」します。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.Unresponsive
* 重要度: 警告
* 理由: *「物理ディスクが発生している定期的な応答がない」。*
* RecommendedAction: *「物理ディスクを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.PredictiveFailure
* 重要度: 警告
* 理由: *「物理ディスクの障害はすぐに発生すると予測」。*
* RecommendedAction: *「物理ディスクを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedHardware
* 重要度: 警告
* 理由: *「物理ディスクが検疫、ソリューション ベンダーによってサポートされていないためです」。*
* RecommendedAction: *「物理ディスクはサポートされているハードウェアで置き換えます」。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnsupportedFirmware
* 重要度: 警告
* 理由: *「物理ディスクは検疫に、ソリューション ベンダーが、ファームウェアのバージョンがサポートされていないためです」。*
* RecommendedAction: *「ターゲット バージョンへの物理ディスク上のファームウェアを更新」します。*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.UnrecognizedMetadata
* 重要度: 警告
* 理由: *「物理ディスクが認識できないメタデータ」。*
* RecommendedAction: *"このディスクは、不明な記憶域プールからのデータを格納できます。まず、このディスクに有用なデータがないことを確認し、ディスクをリセットします。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft.Health.FaultType.PhysicalDisk.FailedFirmwareUpdate
* 重要度: 警告
* 理由: *「Failed しようと物理ディスクのファームウェアを更新します」。*
* RecommendedAction: *「バイナリの別のファームウェアを使用してを実行してください」。*

### **<a name="virtual-disk-2"></a>仮想ディスク (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.NeedsRepair
* 重要度: 情報
* 理由: *"このボリューム上でいくつかのデータは回復力のある完全ではありません。アクセシビリティ対応のままです。"*
* RecommendedAction: *「復元中の回復性のデータ」。*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft.Health.FaultType.VirtualDisks.Detached
* 重要度: 重大
* 理由: *"ボリュームにアクセスできません。一部のデータが失われます。"*
* RecommendedAction: *"物理の確認やネットワークのすべての記憶装置の接続します。必要がありますバックアップから復元する。"*

### **<a name="pool-capacity-1"></a>プール容量 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: Microsoft.Health.FaultType.StoragePool.InsufficientReserveCapacityFault
* 重要度: 警告
* 理由: *"記憶域プールには、推奨される最小の予約容量がありません。これは、機能を制限をドライブの障害が発生した場合、データの回復性を復元します。"*
* RecommendedAction: *"、記憶域プールに追加の容量を追加または容量を解放します。最小推奨予約は、展開によって異なりますが、ドライブの約 2 分の容量の。"*

### <a name="volume-capacity-2sup1sup"></a>**ボリューム容量 (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 重要度: 警告
* 理由: *「ボリューム領域が不足して利用可能な」。*
* RecommendedAction: *「ボリュームを拡大または他のボリュームにワークロードを移行します」。*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft.Health.FaultType.Volume.Capacity
* 重要度: 重大
* 理由: *「ボリューム領域が不足して利用可能な」。*
* RecommendedAction: *「ボリュームを拡大または他のボリュームにワークロードを移行します」。*

### **<a name="server-3"></a>サーバー (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft.Health.FaultType.Server.Down
* 重要度: 重大
* 理由: *"のサーバーに到達できません"。*
* RecommendedAction: *"を開始するか、サーバーを交換します"。*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft.Health.FaultType.Server.Isolated
* 重要度: 重大
* 理由: *「サーバーは、[接続の問題により、クラスターから切り離されて」です。*
* RecommendedAction: *「チェック、ネットワークの分離が引き続き発生する場合または他のノードにワークロードを移行します」。*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft.Health.FaultType.Server.Quarantined
* 重要度: 重大
* 理由: *「サーバーは定期的な障害によるクラスターによって検疫された」。*
* RecommendedAction: *「サーバーの交換またはネットワークを修正します」。*

### **<a name="cluster-1"></a>クラスター (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: Microsoft.Health.FaultType.ClusterQuorumWitness.Error
* 重要度: 重大
* 理由: *"、クラスターは、下方向にから 1 つのサーバーの障害を"。*
* RecommendedAction: *"、監視リソースを確認し、必要に応じて再起動します。開始または障害が発生したサーバーの交換します。"*

### **<a name="network-adapterinterface-4"></a>ネットワーク アダプター/インターフェイス (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disconnected
* 重要度: 警告
* 理由: *「ネットワーク インターフェイスになる切断されました」。*
* RecommendedAction: *「ネットワーク ケーブルを再接続します」。*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: Microsoft.Health.FaultType.NetworkInterface.Missing
* 重要度: 警告
* 理由: *「{サーバー} が、ネットワーク アダプターは {クラスター ネットワーク} のクラスタ ネットワークに接続されているが見つかりません」。*
* RecommendedAction: *「サーバーは、不足しているクラスター ネットワークに接続します」。*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Hardware
* 重要度: 警告
* 理由: *「ネットワーク インターフェイスでがハードウェア障害います」。*
* RecommendedAction: *「ネットワーク インターフェイス アダプターを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: Microsoft.Health.FaultType.NetworkAdapter.Disabled
* 重要度: 警告
* 理由: *「{ネットワーク インターフェイス} ネットワーク インターフェイスは無効になってし、が使用されていない」です。*
* RecommendedAction: *"を有効にする、ネットワーク インターフェイスです"。*

### **<a name="enclosure-6"></a>エンクロージャ (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.LostCommunication
* 重要度: 警告
* 理由: *「通信が失われました記憶域エンクロージャにします」。*
* RecommendedAction: *「スタートまたは記憶域エンクロージャを置換します」。*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.FanError
* 重要度: 警告
* 理由: *「記憶域エンクロージャの位置 {位置} ファンに失敗しました」。*
* RecommendedAction: *「ファン、記憶域エンクロージャに交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.CurrentSensorError
* 重要度: 警告
* 理由: *「記憶域エンクロージャの位置 {位置} に現在のセンサーに失敗しました」。*
* RecommendedAction: *「記憶域エンクロージャ内の現在のセンサーを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.VoltageSensorError
* 重要度: 警告
* 理由: *「記憶域エンクロージャの位置 {位置} 電圧センサーに失敗しました」。*
* RecommendedAction: *「記憶域エンクロージャで電圧センサーを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.IoControllerError
* 重要度: 警告
* 理由: *「記憶域エンクロージャの位置 {位置} IO コントローラーに失敗しました」。*
* RecommendedAction: *「記憶域エンクロージャで、IO コントローラーを交換してください」。*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: Microsoft.Health.FaultType.StorageEnclosure.TemperatureSensorError
* 重要度: 警告
* 理由: *「記憶域エンクロージャの位置 {位置} 温度センサーに失敗しました」。*
* RecommendedAction: *「記憶域エンクロージャの温度センサーを交換してください」。*

### **<a name="firmware-rollout-3"></a>ファームウェアのロールアウト (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FailedMaintenanceMode
* 重要度: 警告
* 理由: *"現在できませんファームウェアのロールアウトを実行するときに、進行状況を確認します"。*
* RecommendedAction: *「すべての記憶域スペースは、正常な状態およびフォールト ドメインがない現在をメンテナンス モードを確認します」。*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.FirmwareVerifyVersionFaile
* 重要度: 警告
* 理由: *「ファームウェアのロールアウトが取り消されたファームウェアの更新プログラムを適用した後、予期しない、または読み取り不可能なファームウェア バージョン情報が原因です」。*
* RecommendedAction: *「再起動ファームウェア ロールアウト ファームウェアの問題が解決したら」。*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: Microsoft.Health.FaultType.FaultDomain.TooManyFailedUpdates
* 重要度: 警告
* 理由: *「ファームウェアのロールアウトが取り消されたファームウェアの更新の試行が失敗している物理ディスクが多すぎるためです」。*
* RecommendedAction: *「再起動ファームウェア ロールアウト ファームウェアの問題が解決したら」。*

### <a name="storage-qos-3sup2sup"></a>**記憶域の QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: Microsoft.Health.FaultType.StorQos.InsufficientThroughput
* 重要度: 警告
* 理由: *「記憶域のスループットは予約を満たすために十分な無効」です。*
* RecommendedAction: *「記憶域 QoS ポリシーを再構成します」。*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: Microsoft.Health.FaultType.StorQos.LostCommunication
* 重要度: 警告
* 理由: *「記憶域 QoS ポリシー マネージャーが失われたボリュームとの通信します」。*
* RecommendedAction: *「{ノード} のノードを再起動してください」*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: Microsoft.Health.FaultType.StorQos.MisconfiguredFlow
* 重要度: 警告
* 理由: *「1 つまたは複数の記憶域のコンシューマー (通常は仮想マシン) を使用している、存在しないポリシー ID {id}」。*
* RecommendedAction: *「不足している記憶域の QoS ポリシーを再作成します」。*

<sup>1</sup> 80% に達した (重大度: マイナー) または 90% に達した (重大度: メジャー)、ボリュームに達したことを示します。  
<sup>2</sup>ボリュームの一部の .vhd に用の最小 IOPS が満たされていないことを示します上 10% (マイナー)、30% (メジャー)、または 50% (重大) の 24 時間の期間をロールバックします。  

>[!NOTE]
> ファン、電源、センサーなどのストレージ格納装置コンポーネントの正常性は、SCSI エンクロージャ サービス (SES) から派生します。 ベンダーがこの情報を提供していない場合、ヘルス サービスは表示されません。  

## <a name="see-also"></a>参照してください。

- [Windows Server 2016 のヘルス サービス](health-service-overview.md)
