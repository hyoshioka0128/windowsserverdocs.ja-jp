---
title: 同じハードウェアを使用してフェールオーバー クラスターのアップグレード
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: この記事では、同じハードウェアを使用して 2 ノード フェールオーバー クラスターのアップグレードについて説明します
ms.localizationpriority: medium
ms.openlocfilehash: 0bfeb05c8cbc205745dc16bc7ef04052481668ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854833"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>同じハードウェア上でフェールオーバー クラスターのアップグレード

> 適用先:Windows Server 2019、Windows Server 2016

フェールオーバー クラスターとは、アプリケーションやサービスの可用性を向上するために、互いに連携する独立したコンピューターで構成されるグループを指します。 クラスター サーバー (ノード) は、物理ケーブルとソフトウェアにより接続されます。 クラスター ノードの 1 つに障害が発生すると、他のノードがサービスの提供を開始します (フェールオーバーと呼ばれる処理)。 ユーザーには、サービスの中断の最小値が発生します。

このガイドでは、同じハードウェアを使用して、以前のバージョンから Windows Server 2019 または Windows Server 2016 へのクラスター ノードをアップグレードする手順について説明します。

## <a name="overview"></a>概要

既存のフェールオーバーのオペレーティング システムをアップグレードするクラスターは場合にのみ Windows Server 2016 から Windows 2019 にしようとします。  フェールオーバー クラスターで以前のバージョンが実行されている場合のノードを結合など Windows Server 2012 R2 と以前では、クラスター サービスが実行中のアップグレードはできません。  同じハードウェアを使用する場合の手順を実行、新しいバージョンを入手します。  

フェールオーバー クラスターのアップグレードの前に参照してください、 [Windows アップグレード Center](https://www.microsoft.com/upgradecenter)します。  場所で Windows Server をアップグレードすると、同じハードウェアに移るより新しいリリースを既存のオペレーティング システム リリースから移動します。 Windows Server は、アップグレードされたインプレース、少なくとも 1 つとも 2 バージョン フォワードできます。 たとえば、Windows Server 2012 R2 および Windows Server 2016 をアップグレードできます Windows Server 2019 を適用します。  またことに注意、[クラスターの移行ウィザード](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/)使用できますが、2 つのバージョンに戻すまではのみサポートされます。 次の図は、Windows Server のアップグレードのパスを示します。 ポインティングの下向きの矢印は、Windows Server 2019 までの以前のバージョンからの移行サポートされるアップグレード パスを表します。

![インプレース アップグレードの図](media\In-Place-Upgrade\In-Place-Upgrade-1.png)

次の手順では、同じハードウェアを使用して Windows Server 2019 に、Windows Server 2012 フェールオーバー クラスターのサーバーから移動の例があります。  

アップグレードを開始する前に確認してくださいシステムの状態を含む、現在のバックアップが行われてきました。  またすべてのドライバーとファームウェアが使用する場合は、オペレーティング システムの認定レベルに更新されたことを確認します。  これら 2 つの注意事項がここで取り上げていないされます。

次の例ではクラスターのフェールオーバー クラスターの名前であり、ノード名は NODE1 および NODE2 します。

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>手順 1:最初のノードを削除し、Windows Server 2016 にアップグレード

1. フェールオーバー クラスター マネージャーでは、すべてのリソース NODE1 から NODE2 にノードをクリックしを選択するとマウスの右のドレイン**一時停止**と**役割をドレイン**します。  PowerShell コマンドを使用する代わりに、 [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)します。

    ![ノードをドレインします。](media\In-Place-Upgrade\In-Place-Upgrade-2.png)

2. マウスの右ノードをクリックして、選択して、クラスターからノード 1 を削除**その他のアクション**と**削除**します。  PowerShell コマンドを使用する代わりに、[クラスタ ノードの削除](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)します。

    ![ノードをドレインします。](media\In-Place-Upgrade\In-Place-Upgrade-3.png)

3. 念のため、NODE1 を使用しているストレージからデタッチします。  場合によっては、マシンから記憶域のケーブルの切断は十分です。  必要な場合、デタッチを適切な手順については、記憶域ベンダーに確認します。  によって、ストレージでは、これは必要ありません。

4. Windows Server 2016 で NODE1 を再構築します。  すべての必要な役割、機能、ドライバーおよびセキュリティ更新プログラムを追加したことを確認します。

5. NODE1 と CLUSTER1 と呼ばれる新しいクラスターを作成します。  フェールオーバー クラスター マネージャーを開くと、**管理**ウィンドウで、選択**クラスターの作成**ウィザードの指示に従います。

    ![ノードをドレインします。](media\In-Place-Upgrade\In-Place-Upgrade-4.png)

6. クラスターが作成されると、ロールは、元のクラスターからこの新しいクラスターに移行する必要があります。  マウスを右に、新しいクラスターをクラスター名 (CLUSTER1) をクリックし、選択**他の操作**と**クラスターの役割のコピー**。  役割を移行するウィザードで作業を進めるにします。

    ![ノードをドレインします。](media\In-Place-Upgrade\In-Place-Upgrade-5.png)

7.  すべてのリソースを移行すると後の電源を切る NODE2 (元のクラスター) と、干渉が発生しないため、記憶域を切断します。  NODE1 を記憶域を接続します。  すべてが接続されると、すべてのリソースをオンラインとどおりに機能していることを確認します。

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>手順 2:Windows Server 2019 に 2 番目のノードを再構築します。

すべてが動作することを確認、NODE2 を Windows Server 2019 に再構築し、クラスターに参加していることができます。

1. NODE2 で Windows Server 2019 のクリーン インストールを実行します。 すべての必要な役割、機能、ドライバーおよびセキュリティ更新プログラムを追加したことを確認します。

2. これで、元のクラスター (クラスター) が削除されている CLUSTER1 として新しいクラスターの名前をそのまままたは元の名前に戻ることがことができます。  元の名前に戻る場合は、次の手順に従います。
   
   a.  Node1 で、マウスの右にフェールオーバー クラスター マネージャーでクラスター (CLUSTER1) の名前をクリックして、**プロパティ**します。
   
   b.  **全般** タブで、クラスターにクラスターの名前を変更します。

   c. 適用する または ok を選択すると表示されます、次のダイアログ ポップアップします。

    ![ノードをドレインします。](media\In-Place-Upgrade\In-Place-Upgrade-6.png)

    d. クラスター サービスは停止し、名前の変更を完了するためもう一度開始するために必要な。

3. Node1 で、フェールオーバー クラスター マネージャーを開きます。  マウスの右クリック**ノード**選択**ノードの追加**します。  クラスター NODE2 の追加ウィザードを実行します。

4. NODE2 に記憶域をアタッチします。 これには、記憶域のケーブルの再接続が含まれます。 

5. すべてのリソース NODE1 から NODE2 にノードをクリックしを選択するとマウスの右のドレイン**一時停止**と**役割をドレイン**します。  PowerShell コマンドを使用する代わりに、 [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)します。  すべてのリソースがオンラインでありが機能していることを確認します。

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>手順 3:Windows Server 2019 する最初のノードを再構築します。

1. クラスターからノード 1 を削除してから方法 ノードから、記憶域を切断した以前。

2. 再構築または Windows Server 2019 に NODE1 をアップグレードします。  すべての必要な役割、機能、ドライバーおよびセキュリティ更新プログラムを追加したことを確認します。

3. 記憶域を再アタッチし、NODE1 をクラスターに追加します。

4. NODE1 にすべてのリソースを移動して、オンラインにして必要に応じて機能できるようにします。

5. 現在のクラスターの機能レベルは、Windows 2016 のままです。  PowerShell コマンドを使用する Windows 2019 の機能レベルを更新[UPDATE-CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)します。

完全に機能の Windows Server 2019 のフェールオーバー クラスターとしているようになりました。

## <a name="additional-notes"></a>追加説明

- 前述のように、記憶域を切断することがあります。 または必要ありません。  このドキュメントでは、慎重を期してします。  記憶域のベンダーに問い合わせてください。
- 開始点は、Windows Server 2008 または 2008 R2 クラスターには場合の手順で追加の実行が必要です。
- クラスターで仮想マシンが実行されている場合は、PowerShell コマンドを使用して、クラスターの機能レベルが完了したら、仮想マシンのレベルをアップグレードすることを確認[更新 VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)します。
- など、SQL Server、Exchange Server などのアプリケーションを実行している場合、アプリケーションは移行されませんクラスターの役割のコピー ウィザードを使用に注意してください。  アプリケーションの適切な移行手順については、アプリケーションの開発を参照してください。