---
title: 記憶域スペース ダイレクトのボリュームの作成
description: Windows 管理センターと PowerShell を使用して記憶域スペースダイレクトでボリュームを作成する方法。
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 02/25/2020
ms.openlocfilehash: fb53ae74e471d590f83e1017662f33bb5a4b7c1d
ms.sourcegitcommit: 92e0e4224563106adc9a7f1e90f27da468859d90
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77608804"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの作成

> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、Windows 管理センターと PowerShell を使用して記憶域スペースダイレクトクラスターにボリュームを作成する方法について説明します。

> [!TIP]
> まだボリュームを計画していない場合は、まず「[記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)」をご覧ください。

## <a name="create-a-three-way-mirror-volume"></a>3方向ミラーボリュームを作成する

Windows 管理センターで3方向ミラーボリュームを作成するには、次のようにします。 

1. Windows 管理センターで、記憶域スペースダイレクトクラスターに接続し、 **[ツール]** ウィンドウで **[ボリューム]** を選択します。
2. ボリューム ページで、**インベントリ** タブを選択し、**ボリュームの作成** を選択します。
3. **[ボリュームの作成]** ウィンドウで、ボリュームの名前を入力し、 **[回復性]** を**3 方向ミラー**のままにします。
4. **[HDD のサイズ**] で、ボリュームのサイズを指定します。 たとえば、5 TB (テラバイト) のようになります。
5. **[作成]** を選択します。

サイズによっては、ボリュームの作成に数分かかることがあります。 右上の通知を使用すると、ボリュームがいつ作成されたかを知ることができます。 新しいボリュームが [インベントリ] の一覧に表示されます。

3方向ミラーボリュームの作成方法に関する簡単なビデオをご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>ミラーアクセラレータによるパリティボリュームの作成

ミラーアクセラレータによって、HDD 上のボリュームのフットプリントが減少します。 たとえば、3方向ミラーボリュームは、10テラバイトのサイズごとに、フットプリントとして 30 tb が必要になることを意味します。 フットプリントのオーバーヘッドを軽減するには、ミラーアクセラレータによるパリティを使用してボリュームを作成します。 これにより、最大でアクティブな20% のデータをミラー化し、残りの領域を効率的に使用することで、4台のサーバーのみで、30テラバイトから 22 tb までのフットプリントを削減できます。 このパリティとミラーの比率を調整して、ワークロードに適したパフォーマンスと容量のトレードオフを実現できます。 たとえば、90% のパリティと10% のミラーはパフォーマンスが低下しますが、フットプリントはさらに合理化されます。

Windows 管理センターでミラーアクセラレータを使用してボリュームを作成するには、次のようにします。

1. Windows 管理センターで、記憶域スペースダイレクトクラスターに接続し、 **[ツール]** ウィンドウで **[ボリューム]** を選択します。
2. ボリューム ページで、**インベントリ** タブを選択し、**ボリュームの作成** を選択します。
3. **[ボリュームの作成]** ウィンドウで、ボリュームの名前を入力します。
4. **[回復性]** で **[ミラーアクセラレータパリティ]** を選択します。
5. **[パリティの割合]** で、パリティの割合を選択します。
6. **[作成]** を選択します。

ミラーアクセラレータのパリティボリュームを作成する方法については、クイックビデオをご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>ボリュームを開き、ファイルを追加する

ボリュームを開き、Windows 管理センターでボリュームにファイルを追加するには、次のようにします。

1. Windows 管理センターで、記憶域スペースダイレクトクラスターに接続し、 **[ツール]** ウィンドウで **[ボリューム]** を選択します。
2. ボリューム ページで、**インベントリ** タブを選択します。
2. ボリュームの一覧で、開くボリュームの名前を選択します。

    [ボリュームの詳細] ページで、ボリュームのパスを確認できます。

4. ページの上部にある **[開く]** を選択します。 これにより、Windows 管理センターの [ファイル] ツールが起動します。
5. ボリュームのパスに移動します。 ここでは、ボリューム内のファイルを参照できます。
6. **[アップロード]** を選択し、アップロードするファイルを選択します。
7. ブラウザーの **戻る** ボタンを使用して、Windows 管理センターの ツール ウィンドウに戻ります。

ボリュームを開いてファイルを追加する方法に関する簡単なビデオをご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>重複除去と圧縮を有効にする

重複除去と圧縮はボリュームごとに管理されます。 重複除去と圧縮では後処理モデルが使用されるため、実行されるまで節約されることはありません。 これが行われると、以前のファイルであっても、すべてのファイルに対して機能します。

1. Windows 管理センターで、記憶域スペースダイレクトクラスターに接続し、 **[ツール]** ウィンドウで **[ボリューム]** を選択します。
2. ボリューム ページで、**インベントリ** タブを選択します。
3. ボリュームの一覧で、管理するボリュームの名前を選択します。
4. [ボリュームの詳細] ページで、[**重複除去と圧縮] と**いうラベルの付いたスイッチをクリックします。
5. [重複除去を有効にする] ウィンドウで、重複除去モードを選択します。

    Windows 管理センターでは、複雑な設定の代わりに、さまざまなワークロードに対応した既製のプロファイルを選択できます。 わからない場合は、既定の設定を使用します。

6. **[有効化]** を選びます。

重複除去と圧縮を有効にする方法に関する簡単なビデオをご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>PowerShell を使ったボリュームの作成

記憶域スペース ダイレクトのボリュームを作成するには、**New-Volume** コマンドレットを使うことをお勧めします。 この方法が最も早く、直感的です。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

**New-Volume** コマンドレットには、必須のパラメーターが 4 つあります。

- **FriendlyName:** 任意の文字列。 *"Volume1"* など
- **FileSystem:** **CSVFS_ReFS** (推奨) または **CSVFS_NTFS**
- **StoragePoolFriendlyName:** 記憶域プールの名前。 *"S2D on ClusterName"* など
- **Size:** ボリュームのサイズ。 *"10TB"* など

   > [!NOTE]
   > Windows (PowerShell を含む) では 2 進数を使ってカウントされますが、ドライブのラベルには 10 進数が使われていることがよくあります。 1,000,000,000,000 バイトと定義される "1 テラバイト" のドライブが、Windows で約 "909 GB" となるのはこのためです。 これは正常な動作です。 **New-Volume** を使ってボリュームを作成するときは、**Size** パラメーターを 2 進数で指定してください。 たとえば、"909GB" または "0.909495TB" と指定すると約 1,000,000,000,000 バイトのボリュームが作成されます。

### <a name="example-with-2-or-3-servers"></a>例: サーバーが 2 台または 3 台の場合

処理を簡単にするため、展開にサーバーが 2 台しかない場合、記憶域スペース ダイレクトは回復性のために双方向ミラーリングを自動的に使います。 展開にサーバーが 3 台しかない場合、3 方向ミラーリングを自動的に使います。

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>例: サーバーが 4 台以上の場合

サーバーが 4 台以上の場合、オプションの **ResiliencySettingName** パラメーターを使って回復性の種類を選択できます。

-   **ResiliencySettingName:** **Mirror** または **Parity**。

次の例では、 *"Volume2"* は 3 方向ミラーリングを使い、 *"Volume3"* はデュアル パリティ (多くの場合 "イレイジャー コーディング" と呼ばれます) を使います。

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>例: 記憶域階層の使用

3 種類のドライブが存在する展開では、1 つのボリュームが SSD 階層と HDD 階層をまたぐことができます。 同様に、サーバーが 4 台以上存在する展開では、1 つのボリュームにミラーリングとデュアル パリティを混在させることができます。

そのようなボリュームを作成できるようにするため、記憶域スペース ダイレクトには *Performance* および *Capacity* という既定の階層テンプレートが用意されています。 これらのテンプレートは、3 方向ミラーリングの定義をより高速なデータ格納用ドライブ (該当する場合) にカプセル化し、デュアル パリティの定義をより低速なデータ格納用ドライブ (該当する場合) にカプセル化します。

**Get-StorageTier** コマンドレットを実行すると、それらのドライブを表示できます。

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![記憶域階層の PowerShell のスクリーンショット](media/creating-volumes/storage-tiers-screenshot.png)

階層ボリュームを作成する場合は、**New-Volume** コマンドレットの **StorageTierFriendlyNames** パラメーターと **StorageTierSizes** パラメーターを使用して、これらの階層テンプレートを参照してください。 たとえば、次のコマンドレットは 30:70 の比率で 3 方向ミラーリングとデュアル パリティが混在した 1 つのボリュームを作成します。

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

書き込みが完了しました。 複数のボリュームを作成するには、必要に応じて手順を繰り返します。

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペースダイレクトのボリュームの計画](plan-volumes.md)
- [記憶域スペースダイレクトでのボリュームの拡張](resize-volumes.md)
- [記憶域スペースダイレクトのボリュームの削除](delete-volumes.md)
