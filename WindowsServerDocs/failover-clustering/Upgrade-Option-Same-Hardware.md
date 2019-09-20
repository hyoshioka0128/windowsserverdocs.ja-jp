---
title: 同じハードウェアを使用したフェールオーバークラスターのアップグレード
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: この記事では、同じハードウェアを使用した2ノードフェールオーバークラスターのアップグレードについて説明します。
ms.localizationpriority: medium
ms.openlocfilehash: aa9a31b1faa48a4eaf2a17bc8ecda690b4cf1f12
ms.sourcegitcommit: ccec91c1d32a978159f9b8bb5e39ead5805c26c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71143792"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>同じハードウェアでのフェールオーバークラスターのアップグレード

> 適用対象:Windows Server 2019、Windows Server 2016

フェールオーバー クラスターとは、アプリケーションやサービスの可用性を向上するために、互いに連携する独立したコンピューターで構成されるグループを指します。 クラスター サーバー (ノード) は、物理ケーブルとソフトウェアにより接続されます。 クラスター ノードの 1 つに障害が発生すると、他のノードがサービスの提供を開始します (フェールオーバーと呼ばれる処理)。 ユーザーはサービスの中断を最小限に抑えます。

このガイドでは、同じハードウェアを使用して、以前のバージョンから Windows Server 2019 または Windows Server 2016 にクラスターノードをアップグレードする手順について説明します。

## <a name="overview"></a>概要

既存のフェールオーバークラスター上のオペレーティングシステムのアップグレードは、Windows Server 2016 から Windows 2019 に移行する場合にのみサポートされます。  フェールオーバークラスターで Windows Server 2012 R2 以前のバージョンが実行されている場合、クラスターサービスの実行中にアップグレードしても、ノードを結合することはできません。  同じハードウェアを使用する場合は、新しいバージョンにアクセスするための手順を実行できます。  

フェールオーバークラスターをアップグレードする前に、 [Windows Server のアップグレード](../upgrade/upgrade-overview.md)に関するコンテンツを参照してください。  Windows Server をインプレースアップグレードする場合は、既存のオペレーティングシステムのリリースからより新しいリリースに移行し、同じハードウェア上に保持します。 Windows Server は、少なくとも1つのインプレースでアップグレードでき、場合によっては2つのバージョンを転送できます。 たとえば、windows Server 2012 R2 と Windows Server 2016 は、windows Server 2019 にインプレースアップグレードできます。  また、[クラスター移行ウィザード](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/)を使用することはできますが、サポートされるバージョンは2つまでです。 次の図は、Windows Server のアップグレードパスを示しています。 下向き矢印は、以前のバージョンから Windows Server 2019 に移行するためにサポートされているアップグレードパスを表します。

![一括アップグレードの図](media/In-Place-Upgrade/In-Place-Upgrade-1.png)

次の手順は、同じハードウェアを使用して Windows Server 2012 フェールオーバークラスターサーバーから Windows Server 2019 に移行する例です。  

アップグレードを開始する前に、システム状態を含む現在のバックアップが完了していることを確認してください。  また、すべてのドライバーとファームウェアが、使用するオペレーティングシステムの認定レベルに更新されていることを確認します。  これらの2つの注意事項については、ここでは説明しません。

次の例では、フェールオーバークラスターの名前は CLUSTER、ノード名は NODE1 と NODE2 です。

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>手順 1:最初のノードを削除して Windows Server 2016 にアップグレードする

1. フェールオーバークラスターマネージャーで、ノードを右クリックし、[ロールの**一時停止**と**ドレイン**] を選択して、NODE1 から NODE2 にすべてのリソースをドレインします。  または、PowerShell コマンド[start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)を使用することもできます。

    ![ノードのドレイン](media/In-Place-Upgrade/In-Place-Upgrade-2.png)

2. ノードを右クリックして **[その他のアクション]** を選択し、 **[削除]** を選択して、クラスターから NODE1 を削除します。  または、PowerShell コマンド[start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)を使用することもできます。

    ![ノードのドレイン](media/In-Place-Upgrade/In-Place-Upgrade-3.png)

3. 念のため、使用している記憶域から NODE1 をデタッチしてください。  場合によっては、マシンからストレージケーブルを切断するだけで十分です。  必要に応じて適切なデタッチ手順については、記憶域のベンダーに問い合わせてください。  ストレージによっては、これは必要ない場合があります。

4. Windows Server 2016 で NODE1 を再構築します。  必要なすべての役割、機能、ドライバー、およびセキュリティ更新プログラムが追加されていることを確認します。

5. NODE1 と CLUSTER1 という名前の新しいクラスターを作成します。  フェールオーバークラスターマネージャーを開き、 **[管理]** ウィンドウで **[クラスターの作成]** を選択し、ウィザードの指示に従います。

    ![ノードのドレイン](media/In-Place-Upgrade/In-Place-Upgrade-4.png)

6. クラスターが作成されたら、役割を元のクラスターからこの新しいクラスターに移行する必要があります。  新しいクラスターで、クラスター名 (CLUSTER1) を右クリックし、 **[その他の操作]** を選択して、**クラスターの役割をコピー**します。  ウィザードの指示に従って、役割を移行します。

    ![ノードのドレイン](media/In-Place-Upgrade/In-Place-Upgrade-5.png)

7.  すべてのリソースが移行されたら、NODE2 (元のクラスター) の電源を切り、記憶域を切断して、干渉が発生しないようにします。  記憶域を NODE1 に接続します。  すべてのリソースをオンラインにして、必要に応じて機能していることを確認します。

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>手順 2:2番目のノードを Windows Server 2019 に再構築する

すべてが正常に動作していることを確認したら、NODE2 を Windows Server 2019 に再構築し、クラスターに参加させることができます。

1. NODE2 で Windows Server 2019 のクリーンインストールを実行します。 必要なすべての役割、機能、ドライバー、およびセキュリティ更新プログラムが追加されていることを確認します。

2. 元のクラスター (クラスター) が失われたので、新しいクラスター名を CLUSTER1 として使用するか、元の名前に戻すことができます。  元の名前に戻る場合は、次の手順を実行します。
   
   a. NODE1 でフェールオーバークラスターマネージャー右マウスをクリックし、クラスターの名前 (CLUSTER1) をクリックして、 **[プロパティ]** を選択します。
   
   b. **[全般]** タブで、クラスターの名前を cluster に変更します。

   c. [OK] または [適用] を選択すると、次のダイアログポップアップが表示されます。

    ![ノードのドレイン](media/In-Place-Upgrade/In-Place-Upgrade-6.png)

    d. クラスターサービスは停止され、名前の変更を完了するために再起動する必要があります。

3. NODE1 でフェールオーバークラスターマネージャーを開きます。  **ノード**を右クリックし、 **[ノードの追加]** を選択します。  クラスターに NODE2 を追加するウィザードを実行します。

4. NODE2 にストレージを接続します。 これには、ストレージケーブルの再接続が含まれる場合があります。 

5. ノードを右クリックし、[ロールの**一時停止**と**ドレイン**] を選択して、NODE1 から NODE2 にすべてのリソースをドレインします。  または、PowerShell コマンド[start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)を使用することもできます。  すべてのリソースがオンラインであり、必要に応じて機能していることを確認します。

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>手順 3:最初のノードを Windows Server 2019 に再構築する

1. クラスターから NODE1 を削除し、以前の方法でノードから記憶域を切断します。

2. NODE1 を Windows Server 2019 に再構築またはアップグレードします。  必要なすべての役割、機能、ドライバー、およびセキュリティ更新プログラムが追加されていることを確認します。

3. 記憶域を再接続し、クラスターに NODE1 を追加し直します。

4. すべてのリソースを NODE1 に移動し、必要に応じてオンラインで機能していることを確認します。

5. 現在のクラスターの機能レベルは、Windows 2016 のままです。  PowerShell コマンド[CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)を使用して、機能レベルを Windows 2019 に更新します。

これで、完全に機能する Windows Server 2019 フェールオーバークラスターを使用して実行されます。

## <a name="additional-notes"></a>補足メモ

- 既に説明したように、記憶域を切断する必要があるか、または必要でない場合があります。  このドキュメントでは、注意を払う必要があります。  ストレージベンダーに問い合わせてください。
- 開始位置が Windows Server 2008 または 2008 R2 のクラスターの場合は、手順を追加で実行する必要があります。
- クラスターが仮想マシンを実行している場合は、PowerShell コマンド[更新プログラム VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)でクラスターの機能レベルが完了したら、必ず仮想マシンレベルをアップグレードしてください。
- SQL Server、Exchange Server などのアプリケーションを実行している場合は、クラスターの役割のコピーウィザードを使用してアプリケーションを移行することはできないことに注意してください。  アプリケーションの適切な移行手順については、アプリケーションベンダーに問い合わせてください。