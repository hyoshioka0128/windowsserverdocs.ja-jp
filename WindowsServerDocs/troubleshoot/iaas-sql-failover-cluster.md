---
title: フェールオーバー ベースライン ネットワークのしきい値の調整
description: この記事では、フェールオーバークラスターネットワークのしきい値を調整するためのソリューションについて説明します。
ms.prod: windows-server
ms.technology: server-general
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 86a7023f6480e68f917cb8cdd9d0c69c417d3145
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409793"
---
# <a name="iaas-with-sql-alwayson---tuning-failover-cluster-network-thresholds"></a>IaaS と SQL AlwaysOn - フェールオーバー クラスター ネットワークのしきい値の調整

この記事では、フェールオーバークラスターネットワークのしきい値を調整するためのソリューションについて説明します。

## <a name="symptom"></a>症状

SQL Server AlwaysOn を使用して IaaS で Windows フェールオーバークラスターノードを実行する場合は、クラスター設定をより緩やかな監視状態に変更することをお勧めします。 クラスター設定は制限がなく、不要な障害が発生する可能性があります。 既定の設定は、オンプレミスのネットワークを十分にチューニングするように設計されており、Windows Azure (IaaS) などのマルチテナント環境によって発生する待機時間を考慮しません。

Windows Server フェールオーバークラスタリングは、Windows クラスター内のノードのネットワーク接続と正常性を絶えず監視します。  ネットワーク経由でノードに到着できない場合、クラスターの別のノードで、アプリケーションやサービスを復元し、オンラインに戻す回復措置が取られます。 クラスターノード間の通信で待機時間が発生すると、次のエラーが発生する可能性があります。

> エラー 1135 (システムイベントログ)

クラスターノード**Node1**が、アクティブなフェールオーバークラスターのメンバーシップから削除されました。 このノードのクラスターサービスが停止している可能性があります。 これは、ノードがフェールオーバークラスター内の他のアクティブなノードと通信を失ったことが原因である可能性もあります。 構成の検証ウィザードを実行して、ネットワークの構成を確認します。 条件が引き続き発生する場合は、このノードのネットワークアダプターに関連するハードウェアまたはソフトウェアのエラーを確認します。 また、ノードが接続されている他のネットワークコンポーネント (ハブ、スイッチ、ブリッジなど) のエラーを確認します。

Cluster .log の例:

```console
0000ab34.00004e64::2014/06/10-07:54:34.099 DBG   [NETFTAPI] Signaled NetftRemoteUnreachable event, local address 10.xx.x.xxx:3343 remote address 10.x.xx.xx:3343
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] got event: Remote endpoint 10.xx.xx.xxx:~3343~ unreachable from 10.xx.x.xx:~3343~
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Marking Route from 10.xxx.xxx.xxxx:~3343~ to 10.xxx.xx.xxxx:~3343~ as down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] Checking to see if all routes for route (virtual) local fexx::xxx:5dxx:xxxx:3xxx:~0~ to remote xxx::cxxx:xxxd:xxx:dxxx:~0~ are down
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [NDP] All routes for route (virtual) local fxxx::xxxx:5xxx:xxxx:3xxx:~0~ to remote fexx::xxxx:xxxx:xxxx:xxxx:~0~ are down
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [CORE] Node 8: executing node 12 failed handlers on a dedicated thread
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: Cleaning up connections for n12.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [Nodename] Clearing 0 unsent and 15 unacknowledged messages.
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: n12 node object is closing its connections
0000ab34.00008b68::2014/06/10-07:54:34.099 INFO  [DCM] HandleNetftRemoteRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 1: Old: 05.936, Message: Response, Route sequence: 150415, Received sequence: 150415, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:28.000, Ticks since last sending: 4
0000ab34.00007328::2014/06/10-07:54:34.099 INFO  [NODE] Node 8: closing n12 node object channels
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 2: Old: 06.434, Message: Request, Route sequence: 150414, Received sequence: 150402, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.665, Ticks since last sending: 36
0000ab34.0000a8ac::2014/06/10-07:54:34.099 INFO  [DCM] HandleRequest: dcm/netftRouteChange
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 3: Old: 06.934, Message: Response, Route sequence: 150414, Received sequence: 150414, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:27.165, Ticks since last sending: 4
0000ab34.00004b38::2014/06/10-07:54:34.099 INFO  [IM] Route history 4: Old: 07.434, Message: Request, Route sequence: 150413, Received sequence: 150401, Heartbeats counter/threshold: 5/5, Error: Success, NtStatus: 0 Timestamp: 2014/06/10-07:54:26.664, Ticks since last sending: 36
```

```console
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realLocal>10.xxx.xx.xxx:~3343~</realLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <realRemote>10.xxx.xx.xxx:~3343~</realRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualLocal>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualLocal>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <virtualRemote>fexx::xxxx:xxxx:xxxx:xxxx:~0~</virtualRemote>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Delay>1000</Delay>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Threshold>5</Threshold>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Priority>140481</Priority>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO    <Attributes>2147483649</Attributes>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO  </struct mscs::FaultTolerantRoute>
0000ab34.00007328::2014/06/10-07:54:34.100 INFO   removed
```

```console
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: Lost quorum (3 4 5 6 7 8)
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   [QUORUM] Node 8: goingAway: 0, core.IsServiceShutdown: 0
0000ab34.0000a7c0::2014/06/10-07:54:38.433 ERR   lost quorum (status = 5925)
```

## <a name="cause"></a>原因

クラスターの接続の正常性を構成するために使用される設定は2つあります。

[**遅延**] –クラスターのハートビートがノード間で送信される頻度を定義します。  Delay は、次のハートビートが送信されるまでの秒数です。  同じクラスター内では、同じサブネット上のノードと、異なるサブネット上にあるノード間の遅延が異なる場合があります。

**しきい値**–ハートビートの数を定義します。これは、クラスターが回復操作を実行する前に失われます。  しきい値は、ハートビートの数です。  同じクラスター内では、同じサブネット上のノードと異なるサブネット上のノードの間に異なるしきい値が存在する可能性があります。

既定では、Windows Server 2016 は**SameSubnetThreshold**を10に、 **SameSubnetDelay**を1000ミリ秒に設定します。 たとえば、接続の監視が10秒間失敗した場合、フェールオーバーのしきい値に達すると、そのノードがクラスターメンバーシップから削除されます。 その結果、リソースがクラスター上の使用可能な別のノードに移動されます。 クラスターエラー 1135 (上の図を含む) が報告されます。

## <a name="resolution"></a>解決方法

IaaS 環境では、クラスターのネットワーク構成設定を緩和します。

### <a name="steps-to-verify-current-configuration"></a>現在の構成を確認する手順

現在のクラスターネットワーク構成設定を確認するには、次のコマンドを使用します。

```powershell
C:\Windows\system32> get-cluster | fl *subnet*
```

各サポート OS の既定値、最小値、最大値、推奨値

| 説明 | OS | Min | Max | Default | 推奨 |
|--|--|--|--|--|--|
| CrossSubnetThreshold | 2008 R2 | 3 | 20 | 5 | 20 |
| クロスサブネットのしきい値 | 2012 | 3 | 120 | 5 | 20 |
| クロスサブネットのしきい値 | 2012 R2 | 3 | 120 | 5 | 20 |
| クロスサブネットのしきい値 | 2016 | 3 | 120 | 20 | 20 |
| SameSubnet しきい値 | 2008 R2 | 3 | 10 | 5 | 10 |
| SameSubnet しきい値 | 2012 | 3 | 120 | 5 | 10 |
| SameSubnet しきい値 | 2012 R2 | 3 | 120 | 5 | 10 |
| SameSubnetThreshold | 2016 | 3 | 120 | 10 | 10 |

しきい値の値は、次の記事で説明されているように、デプロイのスコープに関する現在の推奨事項を反映しています。

[Windows Server 2012 R2 でのフェールオーバークラスターのネットワークしきい値の微調整](https://support.microsoft.com/en-us/help/3153887/fine-tuning-failover-cluster-network-thresholds-in-windows-server-2012)

**しきい値**は、クラスターが回復操作を実行する前に失われたハートビートの数を定義します。  しきい値は、ハートビートの数です。  同じクラスター内では、同じサブネット上のノードと、異なるサブネット上のノードの間に異なるしきい値が存在する可能性があります。

## <a name="recommendations-for-changing-to-more-relaxed-settings-for-multi-tenant-environments-like-azure-iaas"></a>Azure (IaaS) などのマルチテナント環境向けに、より緩やかな設定に変更するための推奨事項

> [!NOTE]
> クラスターネットワークの構成設定を調整して、クラスター環境の回復性を高めると、ダウンタイムが増加する可能性があります。 詳細については、「[フェールオーバークラスターのネットワークしきい値の調整](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834)」を参照してください。

1. より緩やかな設定に変更します:

    > [!NOTE]
    > クラスターのしきい値を変更するとすぐに有効になり、クラスターやリソースを再起動する必要はありません。

    次の設定は、AlwaysOn 可用性グループの同じサブネットまたはリージョン間のデプロイに推奨されます。

    ```powershell
    C:\Windows\system32> (get-cluster).SameSubnetThreshold = 20
    ```

    ```powershell
    C:\Windows\system32> (get-cluster).CrossSubnetThreshold = 20
    ```

2. 次の変更を確認します。

    ```powershell
    C:\Windows\system32> get-cluster | fl *subnet*
    ```

    :::image type="content" source="media/iaas-sql-failover-cluster/cmd.png" alt-text="cmd" border="false":::

## <a name="references"></a>参考資料

Windows クラスターのネットワーク構成設定の調整の詳細については、「[フェールオーバークラスターのネットワークしきい値の調整](https://techcommunity.microsoft.com/t5/failover-clustering/tuning-failover-cluster-network-thresholds/ba-p/371834)」を参照してください。

cluster.exe を使用して Windows クラスターのネットワーク構成設定を調整する方法については、「[フェールオーバークラスターのクラスターネットワークを構成する方法](/previous-versions/office/exchange-server-2007/bb690953(v=exchg.80)?redirectedfrom=MSDN)」を参照してください。
