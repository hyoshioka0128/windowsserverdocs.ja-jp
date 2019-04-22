---
ms.assetid: a9f229eb-bef4-4231-97d0-0899e17cef32
title: 記憶域スペース ダイレクトのボリュームの作成
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 01/11/2017
ms.localizationpriority: medium
ms.openlocfilehash: 277a676d8e53a7847d54039aab6607be8e5a78c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823613"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの作成

>適用先:Windows Server 2016

このトピックでは、PowerShell またはフェールオーバー クラスター マネージャーを使って記憶域スペース ダイレクトでボリュームを作成する方法について説明します。

   >[!TIP]
   >  まだボリュームを計画していない場合は、まず「[記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)」をご覧ください。

## <a name="create-volumes-using-powershell"></a>PowerShell を使ったボリュームの作成

記憶域スペース ダイレクトのボリュームを作成するには、**New-Volume** コマンドレットを使うことをお勧めします。 この方法が最も早く、直感的です。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

**New-Volume** コマンドレットには、必須のパラメーターが 4 つあります。

- **FriendlyName:** 任意の文字列をたとえば *"Volume1"*
- **ファイル システム:** いずれか**CSVFS_ReFS** (推奨) または**CSVFS_NTFS**
- **StoragePoolFriendlyName:** たとえば、ストレージの名前がプール *「S2D でクラスター名」*
- **サイズ:** たとえば、ボリュームのサイズ *"10 TB"*

   >[!NOTE]
   >  Windows (PowerShell を含む) では 2 進数を使ってカウントされますが、ドライブのラベルには 10 進数が使われていることがよくあります。 1,000,000,000,000 バイトと定義される "1 テラバイト" のドライブが、Windows で約 "909 GB" となるのはこのためです。 これは正常な動作です。 **New-Volume** を使ってボリュームを作成するときは、**Size** パラメーターを 2 進数で指定してください。 たとえば、"909GB" または "0.909495TB" と指定すると約 1,000,000,000,000 バイトのボリュームが作成されます。

### <a name="example-with-2-or-3-servers"></a>以下に例を示します。2 または 3 つのサーバー

処理を簡単にするため、展開にサーバーが 2 台しかない場合、記憶域スペース ダイレクトは回復性のために双方向ミラーリングを自動的に使います。 展開にサーバーが 3 台しかない場合、3 方向ミラーリングを自動的に使います。

```
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>以下に例を示します。4 + サーバー

サーバーが 4 台以上の場合、オプションの **ResiliencySettingName** パラメーターを使って回復性の種類を選択できます。

-   **ResiliencySettingName:** いずれか**ミラー**または**パリティ**します。

次の例では、*"Volume2"* は 3 方向ミラーリングを使い、*"Volume3"* はデュアル パリティ (多くの場合 "イレイジャー コーディング" と呼ばれます) を使います。

```
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>以下に例を示します。記憶域階層を使用します。

3 種類のドライブが存在する展開では、1 つのボリュームが SSD 階層と HDD 階層をまたぐことができます。 同様に、サーバーが 4 台以上存在する展開では、1 つのボリュームにミラーリングとデュアル パリティを混在させることができます。

そのようなボリュームを作成できるようにするため、記憶域スペース ダイレクトには *Performance* および *Capacity* という既定の階層テンプレートが用意されています。 これらのテンプレートは、3 方向ミラーリングの定義をより高速なデータ格納用ドライブ (該当する場合) にカプセル化し、デュアル パリティの定義をより低速なデータ格納用ドライブ (該当する場合) にカプセル化します。

**Get-StorageTier** コマンドレットを実行すると、それらのドライブを表示できます。

```
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![記憶域階層の PowerShell のスクリーンショット](media/creating-volumes/storage-tiers-screenshot.png)

階層ボリュームを作成する場合は、**New-Volume** コマンドレットの **StorageTierFriendlyNames** パラメーターと **StorageTierSizes** パラメーターを使用して、これらの階層テンプレートを参照してください。 たとえば、次のコマンドレットは 30:70 の比率で 3 方向ミラーリングとデュアル パリティが混在した 1 つのボリュームを作成します。

```
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

## <a name="create-volumes-using-failover-cluster-manager"></a>フェールオーバー クラスター マネージャーを使ったボリュームの作成

フェイルオーバー クラスター マネージャーから*仮想ディスクの新規作成ウィザード (記憶域スペース ダイレクト)*、*ボリュームの新規作成ウィザード*の順に使ってボリュームを作成することもできますが、このワークフローは手動の手順が多いため推奨されません。

主に 3 つの手順があります。

### <a name="step-1-create-virtual-disk"></a>手順 1:仮想ディスクを作成します。

![仮想ディスクの新規作成](media/creating-volumes/GUI-Step-1.png)

1. フェールオーバー クラスター マネージャーで、**[記憶域]** -> **[プール]** の順に移動します。
2. 右側の操作ウィンドウで **[仮想ディスクの新規作成]** を選択するか、プールを右クリックして **[仮想ディスクの新規作成]** を選択します。
3. 記憶域プールを選択して **[OK]** をクリックします。 *仮想ディスクの新規作成ウィザード (記憶域スペース ダイレクト)* が開きます。
4. ウィザードを使って仮想ディスクに名前を付け、そのサイズを指定します。
5. 選択内容を確認し、**[作成]** をクリックします。
6. 閉じる前に **[このウィザードを閉じるときにボリュームを作成します]** チェック ボックスがオンになっていることを確認してください。

### <a name="step-2-create-volume"></a>手順 2:ボリュームを作成します。

*ボリュームの新規作成ウィザード*が開きます。

7. 前の手順で作成した仮想ディスクを選択し、**[次へ]** をクリックします。
8. ボリュームのサイズを指定し (既定値: 仮想ディスクと同じサイズ)、**[次へ]** をクリックします。 
9. ボリュームにドライブ文字を割り当てるか、**[ドライブ文字またはフォルダーに割り当てません]** を選択して **[次へ]** をクリックします。
10. 使用するファイルシステムを指定して、割り当て単位サイズを *[既定]* のままにし、ボリュームに名前を付けて **[次へ]** をクリックします。
11. 選択内容を確認し、**[作成]**、**[閉じる]** の順にクリックします。

### <a name="step-3-add-to-cluster-shared-volumes"></a>手順 3:クラスターの共有ボリュームへの追加します。

![クラスターの共有ボリュームへの追加](media/creating-volumes/GUI-Step-2.png)

12. フェールオーバー クラスター マネージャーで、**[記憶域]** -> **[ディスク]** の順に移動します。
13. 前の手順で作成した仮想ディスクを選択し、右側の操作ウィンドウから **[クラスターの共有ボリュームへの追加]** を選択するか、仮想ディスクを右クリックして **[クラスターの共有ボリュームへの追加]** を選択します。

これで完了です。 複数のボリュームを作成するには、必要に応じて手順を繰り返します。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
