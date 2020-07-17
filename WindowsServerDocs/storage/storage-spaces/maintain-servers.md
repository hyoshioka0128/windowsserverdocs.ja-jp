---
title: 記憶域スペース ダイレクト サーバーをメンテナンスのためオフラインにする
ms.prod: windows-server
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/08/2018
ms.assetid: 73dd8f9c-dcdb-4b25-8540-1d8707e9a148
ms.localizationpriority: medium
ms.openlocfilehash: a317f358c37f607475890efe773b57ee8efaeb14
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473479"
---
# <a name="taking-a-storage-spaces-direct-server-offline-for-maintenance"></a>記憶域スペース ダイレクト サーバーをメンテナンスのためオフラインにする

> 適用先:Windows Server 2019、Windows Server 2016

このトピックは、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)を持つサーバーを適切に再起動したりシャットダウンしたりする方法のガイダンスを提供します。

記憶域スペース ダイレクトでは、サーバーをオフラインにする (停止する) ことは、クラスター内のすべてのサーバーで共有されているストレージの一部をオフラインにすることも意味します。 これを行うためには、オフラインにするサーバーを一時停止 (中断) し、役割をクラスター内の他のサーバーに移動して、クラスター内の他のサーバー上ですべてのデータを利用できることを確認し、保守中にデータが安全でアクセス可能な状態になるようにする必要があります。

次の手順を使用して、記憶域スペース ダイレクトのクラスター内のサーバーを適切に一時停止してから、オフラインにします。

   > [!IMPORTANT]
   > 記憶域スペース ダイレクトのクラスターに更新をインストールするには、クラスター対応更新 (CAU) を使用します。これによりこのトピックの手順が自動的に実行されるため、更新をインストールするときに手順を別途実行する必要がありません。 詳しくは、「[クラスター対応更新 (CAU)](https://technet.microsoft.com/library/hh831694.aspx)」をご覧ください。

## <a name="verifying-its-safe-to-take-the-server-offline"></a>サーバーを安全にオフラインにできることを確認する

メンテナンスのためにサーバーをオフラインにする前に、すべてのボリュームが正常であることを確認します。

これを行うには、管理者権限を使用して PowerShell セッションを開き、次のコマンドを実行して、ボリュームの状態を確認します。

```PowerShell
Get-VirtualDisk
```

この出力の例を次に示します。
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

すべてのボリューム (仮想ディスク) の **HealthStatus** プロパティが **Healthy** であることを確認します。

フェールオーバークラスターマネージャーでこれを行うには、[**記憶域**ディスク] にアクセスし  >  **Disks**ます。

すべてのボリューム (仮想ディスク) の **[状態]** 列が **[オンライン]** であることを確認します。

## <a name="pausing-and-draining-the-server"></a>サーバーの一時停止とドレイン

サーバーを再起動またはシャットダウンする前に、その上で実行されている仮想マシンなどすべての役割を一時停止してドレイン (移動) します。 これによって記憶域スペース ダイレクトは、データを適切にフラッシュしてコミットし、サーバー上で実行されているすべてのアプリケーションにシャットダウンが透過的になるようにします。

   > [!IMPORTANT]
   > クラスター化されたサーバーは、必ず一時停止してドレインしてから、再起動またはシャットダウンを行います。

PowerShell で次のコマンドレットを (管理者として) 実行して、一時停止とドレインを行います。

```PowerShell
Suspend-ClusterNode -Drain
```

これを行うには、フェールオーバー クラスター マネージャーで、**[ノード]** に移動し、ノードを右クリックして、**[一時停止]** > **[役割のドレイン]** の順に選択します。

![一時停止とドレイン](media/maintain-servers/pause-drain.png)

すべての仮想マシンでは、クラスター内の他のサーバーへのライブ マイグレーションが開始されます。 これには数分かかることがあります。

   > [!NOTE]
   > クラスター ノードの一時停止とドレインが適切に行われると、Windows は自動的に安全性チェックを実行して、安全に続行できることを確認します。 正常でないボリュームがある場合は、停止して、安全に続行できないことを警告します。

![安全性チェック](media/maintain-servers/safety-check.png)

## <a name="shutting-down-the-server"></a>サーバーのシャットダウン

サーバーのドレインが完了すると、フェールオーバー クラスター マネージャーと PowerShell で **[一時停止]** と表示されます。

![Paused](media/maintain-servers/paused.png)

これ通常どおり、安全に再起動したり、シャットダウンすることができます (たとえば、Restart-Computer や Stop-Computer PowerShell を使用できます)。

```PowerShell
Get-VirtualDisk

FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                Incomplete        Warning      True           1 TB
MyVolume2    Mirror                Incomplete        Warning      True           1 TB
MyVolume3    Mirror                Incomplete        Warning      True           1 TB
```

ノードがシャットダウンしているとき、またはノードでクラスターサービスを開始または停止しているときに、正常でない、または低下している操作の状態は通常です。問題を引き起こすことはありません。 すべてのボリュームは、オンラインでアクセス可能なままです。

## <a name="resuming-the-server"></a>サーバーの再開

サーバーでワークロードを再度ホストする準備ができたら、サーバーを再開します。

再開するには、PowerShell で次のコマンドレットを (管理者として) 実行します。

```PowerShell
Resume-ClusterNode
```

以前にこのサーバーで実行されていた役割を戻すには、オプションの **-Failback** フラグを使用します。

```PowerShell
Resume-ClusterNode –Failback Immediate
```

これを行うには、フェールオーバー クラスター マネージャーで、**[ノード]** に移動し、ノードを右クリックして、**[再開]** > **[役割のフェールバック]** の順に選択します。

![再開 - フェールバック](media/maintain-servers/resume-failback.png)

## <a name="waiting-for-storage-to-resync"></a>ストレージの再同期を待つ

サーバーが再開されると、利用できなくなったときに発生した新しい書き込みは再同期が必要になります。 これは自動的に行われます。 インテリジェントな変更の追跡により、*すべて*のデータのスキャンと同期を行う必要はなく、変更のみが同期されます。 このプロセスは、実稼働ワークロードへの影響を軽減するために調整されます。 サーバーが一時停止されていた期間と、新しく書き込まれたデータの量に応じて、完了までに時間がかかる場合があります。

再同期の完了を待ってから、クラスター内の他のサーバーをオフラインにする必要があります。

進行状況を監視するには、PowerShell で次のコマンドレットを (管理者として) 実行します。

```PowerShell
Get-StorageJob
```
再同期 (修復) ジョブを示す、出力の例を次に示します。
```
Name   IsBackgroundTask ElapsedTime JobState  PercentComplete BytesProcessed BytesTotal
----   ---------------- ----------- --------  --------------- -------------- ----------
Repair True             00:06:23    Running   65              11477975040    17448304640
Repair True             00:06:40    Running   66              15987900416    23890755584
Repair True             00:06:52    Running   68              20104802841    22104819713
```

**BytesTotal** は、再同期する必要があるストレージの量を示します。 **PercentComplete** は進行状況を示します。

   > [!WARNING]
   > これらの修復ジョブが完了するまでは、他のサーバーを安全にオフラインにすることはできません。

この間、ボリュームは引き続き **Warning** と表示されます。これは通常な動作です。

たとえば、`Get-VirtualDisk` コマンドレットを使用すると、次のような出力となる場合があります。
```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                InService         Warning      True           1 TB
MyVolume2    Mirror                InService         Warning      True           1 TB
MyVolume3    Mirror                InService         Warning      True           1 TB
```

ジョブが完了したら、再度 `Get-VirtualDisk` コマンドレットを使用して、ボリュームが **Healthy** と表示されることを確認します。 出力例を次に示します。

```
FriendlyName ResiliencySettingName OperationalStatus HealthStatus IsManualAttach Size
------------ --------------------- ----------------- ------------ -------------- ----
MyVolume1    Mirror                OK                Healthy      True           1 TB
MyVolume2    Mirror                OK                Healthy      True           1 TB
MyVolume3    Mirror                OK                Healthy      True           1 TB
```

これで、クラスター内の他のサーバーの一時停止や再起動を安全に行うことができます。

## <a name="how-to-update-storage-spaces-direct-nodes-offline"></a>記憶域スペースダイレクトノードをオフラインで更新する方法
記憶域スペースダイレクトシステムをすばやくパスするには、次の手順に従います。 メンテナンス期間のスケジュール設定と、修正プログラムの適用のためにシステムを停止する作業が含まれます。 迅速に適用する必要がある重要なセキュリティ更新プログラムがある場合、またはメンテナンス期間中に修正プログラムの適用を完了する必要がある場合は、この方法が適している可能性があります。 このプロセスでは、記憶域スペースダイレクトクラスターを停止し、修正プログラムを適用して、すべてを再度実行します。 トレードオフは、ホストされているリソースに対するダウンタイムです。

1. メンテナンス期間を計画します。
2. 仮想ディスクをオフラインにします。
3. クラスターを停止して、記憶域プールをオフラインにします。 **クラスターの停止コマンドレット**を実行するか、フェールオーバークラスターマネージャーを使用してクラスターを停止します。
4. 各ノードの services.msc で、クラスターサービスを**無効**に設定します。 これにより、修正プログラムの適用中にクラスターサービスが起動しなくなります。
5. すべてのノードに Windows Server の累積更新プログラムと必要なサービススタックの更新プログラムを適用します。 (すべてのノードを同時に更新できます。クラスターが停止してから待つ必要はありません)。
6. ノードを再起動し、すべてが適切であることを確認します。
7. 各ノードでクラスターサービスを [**自動**」に戻します。
8. クラスターを起動します。 クラスターの**起動**コマンドレットを実行するか、フェールオーバークラスターマネージャーを使用します。

   数分で指定します。  記憶域プールが正常であることを確認してください。
9. 仮想ディスクをオンラインに戻します。
10. **Get Volume**および**VirtualDisk**コマンドレットを実行して、仮想ディスクの状態を監視します。


## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [クラスター対応更新 (CAU)](https://technet.microsoft.com/library/hh831694.aspx)
