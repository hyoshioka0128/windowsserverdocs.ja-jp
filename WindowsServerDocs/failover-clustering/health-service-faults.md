---
title: ヘルスサービスエラー
manager: eldenc
ms.author: cosdar
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 5f35c52e6b4aaf382c80507ca562b52ce27da953
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990790"
---
# <a name="health-service-faults"></a>ヘルスサービスエラー

> 適用先:Windows Server 2019、Windows Server 2016

## <a name="what-are-faults"></a>障害とは

ヘルスサービスは、記憶域スペースダイレクトクラスターを絶えず監視して問題を検出し、"障害" を生成します。 1つの新しいコマンドレットで現在のエラーが表示されるため、すべてのエンティティや機能を順番に確認することなく、デプロイの正常性を簡単に確認できます。 障害は正確で理解しやすく、意思決定に役立つように設計されています。

各エラーには、次の5つの重要なフィールドが含まれます。

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
 > 物理的な場所は、障害ドメインの構成から取得されます。 障害ドメインの詳細については、「 [Windows Server 2016 の障害ドメイン](fault-domains.md)」を参照してください。 こうした情報を指定していない場合、スロット番号しか表示されないなどのように、場所フィールドがあまり役に立ちません。

## <a name="root-cause-analysis"></a>根本原因分析

ヘルスサービスは、障害が発生しているエンティティ間で潜在的な因果関係を評価して、根本的に同じ問題が発生した場合に発生する障害を特定し、組み合わせることができます。 影響の連鎖を認識することにより、レポートに記載される分量が絞られます。 たとえば、サーバーがダウンしている場合は、サーバー内のどのドライブも接続できなくなることが予想されます。 そのため、根本原因 (この場合はサーバー) に対して1つの障害のみが発生します。

## <a name="usage-in-powershell"></a>PowerShell での使用法

PowerShell の現在のエラーを確認するには、次のコマンドレットを実行します。

```PowerShell
Get-StorageSubSystem Cluster* | Debug-StorageSubSystem
```

これにより、記憶域スペースダイレクトクラスター全体に影響を与える障害が返されます。 多くの場合、これらの障害はハードウェアまたは構成に関連しています。 エラーがない場合、このコマンドレットは何も返しません。

>[!NOTE]
> 運用環境以外の環境では、1つの物理ディスクを削除するか、1つのノードをシャットダウンするなどして、自分でエラーをトリガーすることで、この機能を試すことができます。 障害が発生すると、物理ディスクを再挿入するか、ノードを再起動すると、エラーが再び表示されなくなります。

次のコマンドレットを使用すると、特定のボリュームまたはファイル共有のみに影響を与えるエラーを表示することもできます。

```PowerShell
Get-Volume -FileSystemLabel <Label> | Debug-Volume

Get-FileShare -Name <Name> | Debug-FileShare
```

これにより、特定のボリュームまたはファイル共有のみに影響するすべてのエラーが返されます。 多くの場合、これらの障害は容量計画、データの回復性、または記憶域のサービス品質や記憶域レプリカなどの機能に関連しています。

## <a name="usage-in-net-and-c"></a>.NET および C での使用#

### <a name="connect"></a>接続

ヘルスサービスを照会するには、クラスターで**CimSession**を確立する必要があります。 これを行うには、完全な .NET でしか使用できないものが必要になります。つまり、web アプリまたはモバイルアプリから直接この操作を行うことはできません。 これらのコードサンプルでは \# 、このデータアクセス層で最も単純な選択肢である C を使用します。

```
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

エラーまたはメトリックを取得するには、いくつかの関連オブジェクトのインスタンスを取得する必要があります。 最初に、クラスター上の記憶域スペースダイレクトを表す**MSFT \_ StorageSubSystem** 。 これを使用すると、クラスター内のすべての**msft \_ storagenode**情報と、すべての**msft \_ ボリューム**(データボリューム) を取得できます。 最後に、 **MSFT \_ storagehealth**、ヘルスサービス自体も必要になります。

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

「[ストレージ管理 API クラス](/previous-versions/windows/desktop/stormgmt/storage-management-api-classes)」で説明されているすべての同じプロパティにアクセスできます。

```
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

### <a name="query-faults"></a>クエリエラー

**診断**を呼び出して、ターゲット**CimInstance**(クラスターまたは任意のボリューム) にスコープが設定されている現在のエラーを取得します。

Windows Server 2016 の各スコープで使用できる障害の完全な一覧については、以下で説明します。

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

独自のエラー表現を構築して永続化することが適切な場合もあります。 たとえば、この**Myfault**クラスは、 **FaultId**を含む、エラーのいくつかの重要なプロパティを格納します。このプロパティは、後で更新または削除通知を関連付けたり、同じエラーが何度も検出された場合に重複除去するために使用できます。

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

各エラー (**DiagnoseResult**) のプロパティの完全な一覧については、次のドキュメントを参照してください。

### <a name="fault-events"></a>障害イベント

エラーを作成、削除、または更新すると、ヘルスサービスによって WMI イベントが生成されます。 これらは、頻繁にポーリングせずにアプリケーションの状態を同期させるために不可欠です。たとえば、電子メール通知を送信するタイミングを決定する場合などに役立ちます。 このサンプルコードでは、これらのイベントをサブスクライブするために、オブザーバーデザインパターンを再度使用します。

まず、 **MSFT \_ StorageFaultEvent**イベントをサブスクライブします。

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

次に、新しいイベントが生成されるたびに**Onnext ()** メソッドが呼び出されるオブザーバーを実装します。

各イベントには、エラーが作成、削除、または更新されているかどうかを示す**ChangeType**と、関連する**FaultId**が含まれます。

さらに、エラー自体のすべてのプロパティが含まれています。

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

### <a name="understand-fault-lifecycle"></a>障害のライフサイクルについて

エラーは、"検出" またはユーザーによって解決されることを意図したものではありません。 これらは、ヘルスサービスが問題を監視するときに作成され、ヘルスサービスによって問題が発生しなくなった場合にのみ、自動的に削除されます。 一般に、これは問題が修正されたことを反映しています。

ただし、場合によっては、ヘルスサービスによってエラーが検出されることがあります (たとえば、フェールオーバー後や、断続的な接続などが原因で)。 このため、独自のエラー表現を永続化することが理にかなっているので、簡単に重複除去ことができます。 これは、電子メールアラートまたは同等のアラートを送信する場合に特に重要です。

### <a name="properties-of-faults"></a>エラーのプロパティ

次の表は、fault オブジェクトのいくつかの重要なプロパティを示しています。 完全なスキーマでは、 *storagewmi .mof*の**MSFT \_ StorageDiagnoseResult**クラスを調べます。

| **Property**              | **例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft. 正常性の種類. Volume. 容量                      |
| 理由                    | "ボリュームの空き領域が不足しています。"                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット11                                        |
| RecommendedActions        | {"ボリュームを拡張する"。 "ワークロードを他のボリュームに移行する"}   |

**FaultId**1つのクラスターのスコープ内で一意です。

**PerceivedSeverity**PerceivedSeverity = {4, 5, 6} = {"情報"、"Warning"、および "Error"}、または青、黄、赤などの同等の色。

**FaultingObjectDescription**ハードウェアのパーツ情報 (通常はソフトウェアオブジェクトの場合は空白)。

**FaultingObjectLocation**ハードウェアの場所情報。通常、ソフトウェアオブジェクトの場合は空白になります。

**RecommendedActions**独立しており、特定の順序ではない、推奨されるアクションの一覧。 現在、このリストの長さは1です。

## <a name="properties-of-fault-events"></a>Fault イベントのプロパティ

次の表は、fault イベントのいくつかの重要なプロパティを示しています。 完全なスキーマでは、 *storagewmi .mof*の**MSFT \_ StorageFaultEvent**クラスを調べます。

**ChangeType**は、エラーが作成、削除、または更新されているかどうか、および**FaultId**を示すことに注意してください。 イベントには、影響を受けたエラーのすべてのプロパティも含まれます。

| **Property**              | **例**                                                     |
|---------------------------|-----------------------------------------------------------------|
| ChangeType                | 0                                                               |
| FaultId                   | {12345-12345-12345-12345-12345}                                 |
| FaultType                 | Microsoft. 正常性の種類. Volume. 容量                      |
| 理由                    | "ボリュームの空き領域が不足しています。"                 |
| PerceivedSeverity         | 5                                                               |
| FaultingObjectDescription | Contoso XYZ9000 S.N. 123456789                                  |
| FaultingObjectLocation    | ラック A06、RU 25、スロット11                                        |
| RecommendedActions        | {"ボリュームを拡張する"。 "ワークロードを他のボリュームに移行する"}   |

**ChangeType**ChangeType = {0, 1, 2} = {"作成"、"削除"、"更新"}。

## <a name="coverage"></a>カバレッジ

Windows Server 2016 では、ヘルスサービスによって次のエラーカバレッジが提供されます。

### <a name="physicaldisk-8"></a>**PhysicalDisk (8)**

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedmedia"></a>FaultType: Microsoft. 正常性の種類. PhysicalDisk. このメディア
* 重要度: 警告
* 理由: *"物理ディスクに障害が発生しました。"*
* RecommendedAction: *"物理ディスクを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldisklostcommunication"></a>FaultType: Microsoft. Health. LostCommunication
* 重要度: 警告
* 理由: *"物理ディスクへの接続が切断されました。"*
* RecommendedAction: *"物理ディスクが動作し、適切に接続されていることを確認してください。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunresponsive"></a>FaultType: Microsoft. 状態. PhysicalDisk. 応答なし
* 重要度: 警告
* 理由: *"物理ディスクに定期的な無応答があります。"*
* RecommendedAction: *"物理ディスクを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskpredictivefailure"></a>FaultType: Microsoft. Health. PredictiveFailure
* 重要度: 警告
* 理由: *"物理ディスクの障害が間もなく発生することが予測されています。"*
* RecommendedAction: *"物理ディスクを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedhardware"></a>FaultType: Microsoft. 正常性の種類。
* 重要度: 警告
* 理由: *"物理ディスクは、ソリューションベンダーによってサポートされていないため、検疫されています。"*
* RecommendedAction: *"物理ディスクをサポートされているハードウェアに交換してください。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunsupportedfirmware"></a>FaultType: Microsoft. 正常性の種類。
* 重要度: 警告
* 理由: *"物理ディスクのファームウェアバージョンがソリューションのベンダによってサポートされていないため、検疫中です。"*
* RecommendedAction: *"物理ディスク上のファームウェアをターゲットバージョンに更新します。"*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskunrecognizedmetadata"></a>FaultType: Microsoft. 正常性の種類. PhysicalDisk-メタデータ
* 重要度: 警告
* 理由: *"物理ディスクは認識されていないメタデータを含んでいます。"*
* RecommendedAction: *"このディスクには、不明な記憶域プールのデータが含まれている可能性があります。まず、このディスクに有用なデータがないことを確認してから、ディスクをリセットしてください。 "*

#### <a name="faulttype-microsofthealthfaulttypephysicaldiskfailedfirmwareupdate"></a>FaultType: Microsoft. Health. FailedFirmwareUpdate
* 重要度: 警告
* 理由: *"物理ディスクのファームウェアを更新できませんでした。"*
* RecommendedAction: *"別のファームウェアバイナリを使用してみてください。"*

### <a name="virtual-disk-2"></a>**仮想ディスク (2)**

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksneedsrepair"></a>FaultType: Microsoft. 正常性の種類。仮想ディスクの修復
* 重大度 : 情報
* 理由: *"このボリュームの一部のデータは完全に回復できません。アクセス可能な状態のままです。 "*
* RecommendedAction: *"データの回復性を復元しています。"*

#### <a name="faulttype-microsofthealthfaulttypevirtualdisksdetached"></a>FaultType: Microsoft. 状態. VirtualDisks. デタッチ済み
* 重大度: Critical
* 理由: *"ボリュームにアクセスできません。一部のデータが失われる可能性があります。 "*
* RecommendedAction: *"すべての記憶装置の物理的な接続またはネットワーク接続を確認します。バックアップからの復元が必要になる場合があります。 "*

### <a name="pool-capacity-1"></a>**プール容量 (1)**

#### <a name="faulttype-microsofthealthfaulttypestoragepoolinsufficientreservecapacityfault"></a>FaultType: InsufficientReserveCapacityFault を実行します。
* 重要度: 警告
* 理由: *"記憶域プールには、推奨される最小予約容量がありません。これにより、ドライブで障害が発生した場合にデータの回復性を復元する機能が制限される可能性があります。 "*
* RecommendedAction: *"記憶域プールに容量を追加するか、容量を解放します。推奨される最小予約は、デプロイによって異なりますが、約2ドライブの容量に相当します。 "*

### <a name="volume-capacity-2sup1sup"></a>**ボリューム容量 (2)**<sup>1</sup>

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft. 正常性の種類。容量
* 重要度: 警告
* 理由: *"ボリュームの空き領域が不足しています。"*
* RecommendedAction: *"ボリュームを拡張するか、ワークロードを他のボリュームに移行します。"*

#### <a name="faulttype-microsofthealthfaulttypevolumecapacity"></a>FaultType: Microsoft. 正常性の種類。容量
* 重大度: Critical
* 理由: *"ボリュームの空き領域が不足しています。"*
* RecommendedAction: *"ボリュームを拡張するか、ワークロードを他のボリュームに移行します。"*

### <a name="server-3"></a>**サーバー (3)**

#### <a name="faulttype-microsofthealthfaulttypeserverdown"></a>FaultType: Microsoft. Health. Server. Down
* 重大度: Critical
* 理由: *"サーバーに到達できません。"*
* RecommendedAction: *"Start or replace server."*

#### <a name="faulttype-microsofthealthfaulttypeserverisolated"></a>FaultType: Microsoft. Health. サーバー分離
* 重大度: Critical
* 理由:*接続の問題により、サーバーがクラスターから分離されています。*
* RecommendedAction: *"分離が維持されている場合は、ネットワークを確認するか、ワークロードを他のノードに移行します。"*

#### <a name="faulttype-microsofthealthfaulttypeserverquarantined"></a>FaultType: Microsoft. Health. サーバー. 検疫済み
* 重大度: Critical
* 理由: *"繰り返し発生するエラーが発生したため、サーバーはクラスターによって検疫されています。"*
* RecommendedAction: *"サーバーを交換するか、ネットワークを修正します。"*

### <a name="cluster-1"></a>**クラスター (1)**

#### <a name="faulttype-microsofthealthfaulttypeclusterquorumwitnesserror"></a>FaultType: ClusterQuorumWitness を入力します。
* 重大度: Critical
* 理由: *"クラスターは、1台のサーバーで障害が発生しています。"*
* RecommendedAction: *"監視リソースを確認し、必要に応じて再起動します。失敗したサーバーを開始または置換します。 "*

### <a name="network-adapterinterface-4"></a>**ネットワークアダプター/インターフェイス (4)**

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisconnected"></a>FaultType: ネットワークアダプター (接続解除)
* 重要度: 警告
* 理由: *"ネットワークインターフェイスが切断されました。"*
* RecommendedAction: *"ネットワークケーブルを再接続します。"*

#### <a name="faulttype-microsofthealthfaulttypenetworkinterfacemissing"></a>FaultType: NetworkInterface。存在しません。
* 重要度: 警告
* 理由: *"サーバー {server} には、クラスターネットワーク {cluster network} に接続されているネットワークアダプターがありません。"*
* RecommendedAction: *"サーバーを見つからないクラスターネットワークに接続します。"*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterhardware"></a>FaultType: ネットワークアダプター (正常性)
* 重要度: 警告
* 理由: *"ネットワークインターフェイスにハードウェア障害が発生しました。"*
* RecommendedAction: *"ネットワークインターフェイスアダプターを置き換えます。"*

#### <a name="faulttype-microsofthealthfaulttypenetworkadapterdisabled"></a>FaultType: ネットワークアダプターは無効です。
* 重要度: 警告
* 理由: *"ネットワークインターフェイス {network interface} が有効になっ*ておらず、使用されていません。"
* RecommendedAction: *"ネットワークインターフェイスを有効にする"*

### <a name="enclosure-6"></a>**エンクロージャ (6)**

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurelostcommunication"></a>FaultType: LostCommunication を実行します。
* 重要度: 警告
* 理由: *"ストレージエンクロージャへの通信が切断されました。"*
* RecommendedAction: *"ストレージエンクロージャを起動または交換します。"*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurefanerror"></a>FaultType: FanError を実行します。
* 重要度: 警告
* 理由: *"記憶域エンクロージャの位置 {位置} にあるファンが失敗しました。"*
* RecommendedAction: *"記憶域エンクロージャのファンを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurecurrentsensorerror"></a>FaultType: Microsoft. 正常性の種類。 StorageEnclosure。 CurrentSensorError
* 重要度: 警告
* 理由: *"記憶域エンクロージャの位置 {位置} にある現在のセンサーが失敗しました。"*
* RecommendedAction: *"記憶域エンクロージャの現在のセンサーを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosurevoltagesensorerror"></a>FaultType: VoltageSensorError を実行します。
* 重要度: 警告
* 理由: *"ストレージエンクロージャの位置 {位置} の電圧センサーが失敗しました。"*
* RecommendedAction: *"記憶域エンクロージャの電圧センサーを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosureiocontrollererror"></a>FaultType: Microsoft. 正常性の種類. StorageEnclosure ジャエラー
* 重要度: 警告
* 理由: *"記憶域エンクロージャの位置 {位置} にある IO コントローラーが失敗しました。"*
* RecommendedAction: *"記憶域エンクロージャの IO コントローラーを交換します。"*

#### <a name="faulttype-microsofthealthfaulttypestorageenclosuretemperaturesensorerror"></a>FaultType: TemperatureSensorError を実行します。
* 重要度: 警告
* 理由: *"記憶域エンクロージャの位置 {位置} の温度センサーが失敗しました。"*
* RecommendedAction: *"ストレージエンクロージャの温度センサーを交換します。"*

### <a name="firmware-rollout-3"></a>**ファームウェアロールアウト (3)**

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfailedmaintenancemode"></a>FaultType: FailedMaintenanceMode を実行します。
* 重要度: 警告
* 理由: *"ファームウェアのロールアウトの実行中に進行を進めることができません。"*
* RecommendedAction: *"すべての記憶域スペースが正常であり、障害ドメインが現在メンテナンスモードになっていないことを確認します。"*

#### <a name="faulttype-microsofthealthfaulttypefaultdomainfirmwareverifyversionfaile"></a>FaultType: FirmwareVerifyVersionFaile を実行します。
* 重要度: 警告
* 理由: *"ファームウェアの更新プログラムを適用した後に、読み取り不能または予期しないファームウェアバージョン情報が発生したため、ファームウェアのロールアウトが取り消されました。"*
* RecommendedAction: *"ファームウェアの問題が解決されたら、ファームウェアのロールアウトを再開します。"*

#### <a name="faulttype-microsofthealthfaulttypefaultdomaintoomanyfailedupdates"></a>FaultType: TooManyFailedUpdates を実行します。
* 重要度: 警告
* 理由: *"ファームウェアの更新の試行に失敗した物理ディスクの数が多すぎるため、ファームウェアのロールアウトが取り消されました。"*
* RecommendedAction: *"ファームウェアの問題が解決されたら、ファームウェアのロールアウトを再開します。"*

### <a name="storage-qos-3sup2sup"></a>**記憶域 QoS (3)**<sup>2</sup>

#### <a name="faulttype-microsofthealthfaulttypestorqosinsufficientthroughput"></a>FaultType: InsufficientThroughput を実行します。
* 重要度: 警告
* 理由: *"予約を満たすには、ストレージのスループットが不十分です。"*
* RecommendedAction: *"記憶域 QoS ポリシーを再構成します。"*

#### <a name="faulttype-microsofthealthfaulttypestorqoslostcommunication"></a>FaultType: LostCommunication を実行します。
* 重要度: 警告
* 理由: *"記憶域 QoS ポリシーマネージャーがボリュームと通信できなくなりました。"*
* RecommendedAction: *"ノード {nodes} を再起動してください"*

#### <a name="faulttype-microsofthealthfaulttypestorqosmisconfiguredflow"></a>FaultType: MisconfiguredFlow を実行します。
* 重要度: 警告
* 理由: *"1 つ以上のストレージコンシューマー (通常は Virtual Machines) が、id {id} の存在しないポリシーを使用しています。"*
* RecommendedAction: *"不足している記憶域 QoS ポリシーを再作成します。"*

<sup>1</sup>ボリュームが 80% full (軽微な重大度) または 90% full (重要度) に達したことを示します。
<sup>2</sup>は、ボリューム上の一部の .vhd が、24時間枠のローリングで 10% (マイナー)、30% (メジャー)、または 50% (重大) の最小 IOPS を満たしていないことを示します。

>[!NOTE]
> ファン、電源、センサーなどのストレージ格納装置コンポーネントの正常性は、SCSI エンクロージャ サービス (SES) から取得されます。 この情報は、ベンダーから提供されていない場合はヘルス サービスで表示されません。

## <a name="additional-references"></a>その他の参照情報

- [Windows Server 2016 のヘルス サービス](health-service-overview.md)