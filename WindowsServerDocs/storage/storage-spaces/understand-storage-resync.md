---
title: 理解し、記憶域の再同期を参照してください。
description: 記憶域の再同期が発生したとき、および Windows Server 2019 で表示する方法の詳細情報。
keywords: 記憶域スペース ダイレクト、記憶域の再同期、再同期、記憶域、S2D
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 81b1136a4b6a5cf8423a99e898b482a9b2849b5f
ms.sourcegitcommit: 748eccd10fc0c3c962d6e64ff6ead08017ac1947
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2019
ms.locfileid: "9009669"
---
# 理解し、記憶域の再同期の監視

>適用対象: Windows Server 2019

記憶域の再同期アラートは、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)記憶域が再同期したときにエラーをスローする正常性サービスできる Windows Server 2019 の新機能です。 アラート、ときに通知する再同期が発生していて、サーバーを誤って実行しないようにに便利です (を引き起こします、影響を受けるに複数の障害ドメイン下方向に、クラスター内の結果) ダウンします。 

このトピックでは、バック グラウンドと理解して、記憶域スペース ダイレクトを使用した Windows Server フェールオーバー クラスターで記憶域の再同期のための手順を提供します。

## 再同期の理解

記憶域を同期しなく取得する方法を理解する単純な例を見てみましょう。注意してください間で共有できない (ローカル ドライブのみ) 用に配布された記憶域ソリューションが動作します。 ように、1 つのサーバー ノードがダウンした後に再びオンラインになるまで、そのドライブを更新しない場合は、これは、ハイパーコンバージド アーキテクチャ当てはまります。 

"HELLO"という文字列を格納することがあるとします。 

![文字列「こんにちは」の ASCII](media/understand-storage-resync/hello.png)

この文字列の 3 つのコピーが存在します Asssuming 3 方向ミラー回復性があること、します。 これで、一時的に (メンテナンス) のサーバー 1 を実施する場合は、コピー 1 をアクセスすることはできません。

![コピー 1 にアクセスできません。](media/understand-storage-resync/copy1.png)

たとえば、「ヘルプ!」を"HELLO"から文字列を更新します この時点でします。

![文字列「ヘルプ!」の ASCII](media/understand-storage-resync/help.png)

文字列を更新します 2 と 3 のコピーが正常に更新できます。 ただし、コピー 1 もアクセスできません (メンテナンス) を一時的に、サーバー 1 がダウンします。 

![2 と 2 コピーへの書き込みの Gif"](media/understand-storage-resync/write.gif)

これで、同期されているデータがコピー 1 があります。オペレーティング システムでは、同期するビットを追跡する追跡ダーティ領域を細かくを使用します。これにより、サーバー 1 がオンラインに戻るとき、コピー 2 または 3 からデータを読み取り、コピー 1 でデータを上書きする変更を同期することができます。 この方法の利点は、のみ必要とすることをすべてのサーバー 2 またはサーバー 3 からデータを再同期するのではなく、古い、データをコピーします。

![1 のコピーを上書きする Gif"](media/understand-storage-resync/overwrite.gif)

そのため、これはデータを同期しなく取得する方法について説明します。しかし、内容は、この見える大まかに言うでしょうか。 この例では、3 つのサーバーのハイパーコンバージド クラスターがあると仮定します。 メンテナンスがサーバー 1 には、下として表示されます。 バックアップ サーバー 1 を表示すると、すべて (上で説明した) 細かくダーティ領域の追跡を使用して、記憶域の再同期中に開始されます。 すべてのサーバーが示されるデータがすべて同期と、最大とします。

![再同期の管理者のビューの Gif"](media/understand-storage-resync/admin.gif)

## Windows Server 2019 でストレージの再同期を監視する方法

記憶域の再同期のしくみを理解したら、次の Windows Server 2019 に現れるこの方法を見てみましょう。 記憶域が再同期するときに表示されます[ヘルス サービス](../../failover-clustering/health-service-overview.md)に新しい障害を追加しました。

PowerShell で、このエラーを表示するには、次のコマンドを実行します。

``` PowerShell
Get-HealthFault
```

これは、Windows Server 2019 で新しいフォールトであり、powershell、クラスター検証レポート、およびその他の場所の正常性の障害のビルドが表示されます。 

深いビューを取得するには、ように PowerShell で、時間シリーズのデータベースを照会できます。

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

特に、Windows Admin Center は、状態とクラスター ノードの色を設定するのに正常性の障害を使用します。 そのため、この新しい障害により、黄色の (再同期中) 緑 (アップ)、緑、赤から直接移動する代わりに (ダウン)、赤から移行するクラスター ノード HCI ダッシュ ボードでします。

![再同期の 2016 vs 2019 ビューの画像"](media/understand-storage-resync/compare.png)

全体的な記憶域再同期の進行状況を表示するには、データの量がとれていないと、システムが進捗を行うかどうかを正確に知ることができます。 Windows Admin Center を開いて、*ダッシュ ボード*に移動すると、次のように、新しいアラートが表示されます。

![Windows Admin Center でのアラートの画像"](media/understand-storage-resync/alert.png)

アラート、ときに通知する再同期が発生していて、サーバーを誤って実行しないようにに便利です (を引き起こします、影響を受けるに複数の障害ドメイン下方向に、クラスター内の結果) ダウンします。 

Windows Admin Center で*サーバー*ページに移動を*インベントリ*をクリックし、特定のサーバーを選択場合は、サーバーごとにこのストレージの再同期の外観の詳細が表示を取得できます。 サーバーに移動して*記憶域*グラフを見て、正確な数の線を*紫色*で修復する必要があるデータの量が表示されます上記右します。 この時間 (詳細データのニーズに再同期する)、下のサーバーが上下に徐々 にサーバーがオンラインに戻るとき (データを同期中です)。 ときの修復が 0 にする必要があるデータ量、記憶域は、再同期の実行は今すぐ自由にする必要がある場合は、サーバーをダウンします。 Windows Admin Center では、このエクスペリエンスのスクリーン ショットは、以下に示します。

![Windows Admin Center でサーバー ビューの画像"](media/understand-storage-resync/server.png)

## Windows Server 2016 で記憶域の再同期を表示する方法

ご覧のように、このアラートは、記憶域のレイヤーで何が起きるかの全体像を取得するのには特に便利です。 記憶域スペースの修復操作など、実行時間の長い記憶域のモジュール ジョブに関する情報を返す Get StorageJob コマンドレットから取得できます情報効果的にまとめたものです。 例は、以下に示します。

```PowerShell
Get-StorageJob
```

出力の例を次に示します。

```
Name                  ElapsedTime           JobState              PercentComplete       IsBackgroundTask
----                  -----------           --------              ---------------       ----------------
Regeneration          00:01:19              Running               50                    True

```

このビューは、表示されている記憶域ジョブが 1 つのボリュームは、実行されているジョブの一覧を確認できますおよび個々 の進行状況を追跡するため、多くのさらに細かくします。 このコマンドレットは、Windows Server 2016 および 2019 の両方で動作します。

## 関連項目

- [メンテナンスのためサーバーをオフラインにする](maintain-servers.md)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)