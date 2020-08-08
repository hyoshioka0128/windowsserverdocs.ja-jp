---
title: ストレージの再同期について理解する
description: ストレージの再同期が行われるタイミングと、Windows Server 2019 でどのように表示されるかに関する詳細情報。
ms.author: adagashe
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2a8eb653de2d72177f3ce39f0b63fe53b50c0ae8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957329"
---
# <a name="understand-and-monitor-storage-resync"></a>記憶域の再同期を理解して管理する

>適用対象:Windows Server 2019

記憶域の再同期アラートは、Windows Server 2019 の[記憶域スペースダイレクト](storage-spaces-direct-overview.md)の新機能であり、記憶域が再同期されたときにヘルスサービスがエラーをスローできるようにします。 このアラートは、再同期が発生したときに通知するのに役立ちます。これにより、誤ってサーバーを増やしたりすることはありません (複数の障害ドメインが影響を受け、クラスターが停止する可能性があります)。

このトピックでは、記憶域スペースダイレクトを使用した Windows Server フェールオーバークラスターでの記憶域の再同期について説明します。

## <a name="understanding-resync"></a>再同期について

まず、ストレージがどのように同期されるかを理解するための簡単な例を見てみましょう。共有されていない (ローカルドライブのみ) 分散ストレージソリューションでは、この動作が行われることに注意してください。 次に示すように、1つのサーバーノードがダウンした場合、そのドライブはオンラインに戻るまで更新されません。これは、すべてのハイパー収束アーキテクチャに当てはまります。

文字列 "HELLO" を格納するとします。

![文字列 "hello" の ASCII](media/understand-storage-resync/hello.png)

3方向ミラーの回復性を備えているため、この文字列のコピーは3つあります。 ここで、サーバー #1 を一時的に停止した場合 (メンテナンスの場合)、copy #1 にアクセスできません。

![コピー #1 にアクセスできません](media/understand-storage-resync/copy1.png)

文字列を "HELLO" から "HELP!" に更新するとします。 この時点で。

![文字列 "help!" の ASCII](media/understand-storage-resync/help.png)

文字列を更新すると #2 がコピーされ、#3 が正常に更新されます。 ただし、サーバー #1 が一時的にダウンしている (メンテナンスの場合) ため、コピー #1 にまだアクセスできません。

![#2 と #2 をコピーするための書き込みの Gif](media/understand-storage-resync/write.gif)

ここでは、同期されていないデータを含む #1 をコピーします。オペレーティングシステムでは、詳細なダーティ領域追跡を使用して、同期されていないビットを追跡します。このようにして、サーバー #1 がオンラインに戻ったときに、コピー #2 または #3 からデータを読み取り、コピー #1 でデータを上書きすることによって、変更を同期できます。 この方法の利点は、サーバー #2 またはサーバー #3 からのすべてのデータを再同期するのではなく、古いデータをコピーすることだけです。

![コピー #1 "に上書きする Gif](media/understand-storage-resync/overwrite.gif)

ここでは、データが同期されないようにする方法について説明します。しかし、このようなことは大まかに見てみましょう。 この例では、3台のサーバーハイパー集約クラスターを使用しているとします。 サーバー #1 がメンテナンス中の場合は、停止していると表示されます。 サーバー #1 バックアップを作成すると、詳細なダーティリージョンの追跡 (上で説明した) を使用して、すべてのストレージの再同期が開始されます。 データがすべて同期されると、すべてのサーバーが表示されます。

![再同期の管理ビューの Gif](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Windows Server 2019 で記憶域の再同期を監視する方法

これで、記憶域の再同期のしくみを理解できたので、Windows Server 2019 でこれがどのように表示されるかを見てみましょう。 ストレージが再同期したときに表示される[ヘルスサービス](../../failover-clustering/health-service-overview.md)に新しいエラーが追加されました。

PowerShell でこのエラーを表示するには、次のように実行します。

``` PowerShell
Get-HealthFault
```

これは、Windows Server 2019 の新しいエラーであり、PowerShell、クラスター検証レポート、および正常性エラーに基づいて構築された他の任意の場所に表示されます。

より深いビューを取得するには、次のように PowerShell でタイムシリーズデータベースに対してクエリを実行します。

```PowerShell
Get-ClusterNode | Get-ClusterPerf -ClusterNodeSeriesName ClusterNode.Storage.Degraded
```
出力例を次に示します。

```
Object Description: ClusterNode Server1

Series                       Time                Value Unit
------                       ----                ----- ----
ClusterNode.Storage.Degraded 01/11/2019 16:26:48     214 GB
```

特に、Windows 管理センターでは、正常性エラーを使用して、クラスターノードの状態と色を設定します。 この新しいエラーが発生すると、クラスターノードが赤 (down) から黄色 (再同期) に、赤から緑に直接移動するのではなく、HCI ダッシュボードで緑 (上) に移行します。

![再同期の2016対2019ビューの画像](media/understand-storage-resync/compare.png)

全体的なストレージ再同期の進行状況を表示することにより、同期されていないデータの量と、システムが進行中であるかどうかを正確に把握できます。 Windows 管理センターを開き、*ダッシュボード*にアクセスすると、次のように新しいアラートが表示されます。

![Windows 管理センターのアラートの画像](media/understand-storage-resync/alert.png)

このアラートは、再同期が発生したときに通知するのに役立ちます。これにより、誤ってサーバーを増やしたりすることはありません (複数の障害ドメインが影響を受け、クラスターが停止する可能性があります)。

Windows 管理センターの [*サーバー* ] ページに移動し、[*インベントリ*] をクリックしてから特定のサーバーを選択すると、この記憶域の再同期がサーバーごとにどのように表示されるかを詳細に確認できます。 サーバーに移動して*ストレージ*グラフを確認すると、上記の完全な数字を含む*紫色*の線で修復が必要なデータの量が表示されます。 この量は、サーバーがダウンしたときに増加します (より多くのデータを resynced する必要があります)。また、サーバーがオンラインに戻ったとき (データは同期されています)、徐々に減少します。 修復する必要があるデータの量が0の場合、記憶域は再同期になります。必要に応じて、サーバーを解放しておくことができます。 Windows 管理センターでのこのエクスペリエンスのスクリーンショットを次に示します。

![Windows 管理センターのサーバービューの画像](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Windows Server 2016 で記憶域の再同期を確認する方法

ご覧のように、このアラートは、ストレージ層で起こっていることを総合的に把握するうえで特に役立ちます。 これは、記憶域スペースでの修復操作など、長時間実行される記憶域モジュールジョブに関する情報を返す、Get StorageJob コマンドレットから取得できる情報を効果的に要約します。 例を次に示します。

```PowerShell
Get-StorageJob
```

出力例を次に示します。

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

一覧表示されている記憶域ジョブはボリュームごとに表示されるため、このビューの方がはるかに細分化されています。実行中のジョブの一覧を確認したり、個々の進行状況を追跡したりすることができます。 このコマンドレットは、Windows Server 2016 と2019の両方で動作します。

## <a name="additional-references"></a>その他の参照情報

- [メンテナンスのためサーバーをオフラインにする](maintain-servers.md)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)