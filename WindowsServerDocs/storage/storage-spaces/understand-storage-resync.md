---
title: 理解し、記憶域の再同期を参照してください。
description: 記憶域の再同期が行われるタイミング、および Windows Server 2019 で表示する方法の詳細情報。
keywords: 記憶域スペース ダイレクト、記憶域の再同期は、ストレージ、S2D を再同期
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813463"
---
# <a name="understand-and-monitor-storage-resync"></a>記憶域の再同期を理解して管理する

>適用対象:Windows Server 2019

記憶域の再同期のアラートは、の新しい機能[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)記憶域が再同期しているときに、エラーをスローするヘルス サービスを許可する Windows Server 2019 でします。 アラートはときに通知する再同期が行われている場合より多くのサーバーを誤って実行しないようにするのに便利です (これは、考えられる原因が影響する複数の障害ドメインで、クラスターがダウン) ダウンします。 

このトピックでは、背景と手順を理解して、記憶域スペース ダイレクトと Windows Server フェールオーバー クラスターで記憶域の再同期を提供します。

## <a name="understanding-resync"></a>再同期の理解

記憶域を同期取得する方法を理解する簡単な例から始めましょう。注意してくださいシェアード ナッシング (ローカル ドライブのみ) 分散ストレージ ソリューションは、この動作を示します。 1 つのサーバー ノードがダウンした場合、そのドライブは、オンラインに復帰するまで更新されませんし、以下を確認するためこれは、ハイパー コンバージドの両方のアーキテクチャの場合は true。 

文字列"HELLO"を格納する必要があるとします。 

![文字列「こんにちは」の ASCII](media/understand-storage-resync/hello.png)

Asssuming 3 方向ミラー回復性があること、この文字列の 3 つのコピーがあります。 ここで、一時的に (メンテナンス) のサーバーと 1 を実行した場合は、1 のコピーをアクセスできません。

![1 のコピーにアクセスできません。](media/understand-storage-resync/copy1.png)

たとえば、"HELP!"を"HELLO"から文字列を更新しました この時点。

![文字列"help!"の ASCII](media/understand-storage-resync/help.png)

文字列を更新すると 2 および 3 のコピーが正常に更新になります。 ただし、コピー 1 もアクセスできません (メンテナンス) を一時的に、サーバー 1 がダウンするため。 

![#2 と 2 のコピーへの書き込みの Gif"](media/understand-storage-resync/write.gif)

ここで、同期されていません。 データのコピー 1 があります。オペレーティング システムでは、詳細なダーティ領域が同期されていないビットを追跡する追跡を使用します。これにより、サーバー 1 がオンラインに戻ったときに、2 または 3 のコピーからデータを読み取り、コピーが 1 でデータを上書きする、変更を同期しましたできます。 このアプローチの利点は、サーバー 2 または 3 のサーバーからデータをすべて再同期しているのではなく、古いデータをコピーするだけ必要があります。

![1 のコピーを上書きする Gif"](media/understand-storage-resync/overwrite.gif)

そのため、これはデータを同期取得する方法について説明します。しかし、どのように高レベルのでしょうか。 この例では、3 つのサーバーのハイパー コンバージド クラスターがあると仮定します。 サーバー 1 がメンテナンス中の場合は、ダウン中として表示されます。 バックアップ サーバー #1 を表示するとすべて (上述) ダーティ領域の詳細な追跡を使用してその記憶域の再同期が開始されます。 すべてのサーバーが表示されます、データがすべての同期と。

![再同期の管理ビューの Gif"](media/understand-storage-resync/admin.gif)

## <a name="how-to-monitor-storage-resync-in-windows-server-2019"></a>Windows Server 2019 で記憶域の再同期を監視する方法

記憶域の再同期のしくみを理解したところでは、Windows Server 2019 に現れるこの方法を見てみましょう。 新しいエラーを追加しました、[ヘルス サービス](../../failover-clustering/health-service-overview.md)記憶域が再同期しているときに表示するされます。

PowerShell でこのエラーを表示するには、次のコマンドを実行します。

``` PowerShell
Get-HealthFault
```

これは Windows Server 2019 で新しい障害であるため、PowerShell、およびその他の場所、クラスター検証レポートで正常性の障害のビルドに表示されます。 

詳細なビューを取得するには、次のように PowerShell でタイム シリーズ データベースを照会できます。

```PowerShell
Get-ClusterNode | Get-ClusterPerf -ClusterNodeSeriesName ClusterNode.Storage.Degraded
```
次に出力の例を示します。

```
Object Description: ClusterNode Server1

Series                       Time                Value Unit
------                       ----                ----- ----
ClusterNode.Storage.Degraded 01/11/2019 16:26:48     214 GB
```

特に、Windows Admin Center では、状態とクラスター ノードの色を設定するのに正常性エラーを使用します。 そのため、この新しい障害では、HCI のダッシュ ボードの赤から黄色 (再同期している) を緑 (上)、緑、赤から直接移動せずに (ダウン) 移行するクラスター ノードが発生します。

![再同期の 2016 vs 2019 ビューの画像"](media/understand-storage-resync/compare.png)

全体的な記憶域再同期の進行状況を表示するには、同期されていません。 データの量と、システムは進行を行っているかどうかを正確に知ることができます。 Windows Admin Center を開くし、に移動するときに、*ダッシュ ボード*、新しいアラートを次のように表示されます。

![Windows Admin Center でアラートの画像"](media/understand-storage-resync/alert.png)

アラートはときに通知する再同期が行われている場合より多くのサーバーを誤って実行しないようにするのに便利です (これは、考えられる原因が影響する複数の障害ドメインで、クラスターがダウン) ダウンします。 

移動する場合、*サーバー* Windows Admin Center でのページで、をクリックして*インベントリ*、特定のサーバーを選択し、サーバーごとにこの記憶域の再同期のしくみの詳細なビューを取得できます。 場合は、サーバーに移動し、見て、*ストレージ*グラフで修復する必要があるデータの量が表示されます、*紫*正確な数の行のすぐ上。 この量は、サーバーの詳細データ必要があります (再同期化されます)、停止時に向上し、徐々 に減らしてサーバーがオンラインに戻ったときに (データが同期されているが)。 場合は 0 です。 修復する必要があるデータの量、ストレージが再同期の実行は今すぐを自由にする必要がある場合は、サーバーを停止します。 Windows Admin Center では、このエクスペリエンスのスクリーン ショットは、以下に示します。

![Windows Admin Center でのサーバーのビューの画像"](media/understand-storage-resync/server.png)

## <a name="how-to-see-storage-resync-in-windows-server-2016"></a>Windows Server 2016 で記憶域の再同期を確認する方法

ご覧のように、このアラートは、ストレージ層で何が起こっているかの全体像を取得する場合に特に役立ちます。 実質的に、記憶域スペースでの修復操作などの実行時間の長い Storage モジュール ジョブに関する情報を返す Get-storagejob コマンドレットから取得できる情報をまとめたものです。 例は、以下に示します。

```PowerShell
Get-StorageJob
```

次の出力例に示します。

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

ボリュームごとの記憶域ジョブを一覧表示されます、実行されているジョブの一覧を表示できます、およびその個々 の進行状況を追跡するため、このビューははるかに細分化されました。 このコマンドレットは、Windows Server 2016 と 2019 の両方で機能します。

## <a name="see-also"></a>関連項目

- [メンテナンスのサーバーをオフラインにすること](maintain-servers.md)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)