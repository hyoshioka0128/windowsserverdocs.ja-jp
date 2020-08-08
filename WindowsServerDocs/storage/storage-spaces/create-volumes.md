---
title: 記憶域スペース ダイレクトのボリュームの作成
description: Windows 管理センターと PowerShell を使用して記憶域スペースダイレクトでボリュームを作成する方法。
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.date: 02/25/2020
ms.openlocfilehash: 417deaf61b111b6ba54939505c65e8e0f854e604
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960945"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの作成

> 適用先:Windows Server 2019、Windows Server 2016

このトピックでは、Windows 管理センターと PowerShell を使用して記憶域スペースダイレクトクラスターにボリュームを作成する方法について説明します。

> [!TIP]
> まだボリュームを計画していない場合は、まず「[記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)」をご覧ください。

## <a name="create-a-three-way-mirror-volume"></a>3 方向ミラー ボリュームを作成する

Windows 管理センターで3方向ミラーボリュームを作成するには、次のようにします。

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、 **[ツール]** ペインで **[ボリューム]** を選択します。
2. [ボリューム] ページで **[インベントリ]** タブを選択し、 **[ボリュームの作成]** を選択します。
3. **[ボリュームの作成]** ペインで、ボリュームの名前を入力し、 **[回復性]** を **[Three-way mirror]\(3 方向ミラー\)** のままにします。
4. **[Size on HDD]\(HDD 上のサイズ\)** で、ボリュームのサイズを指定します。 たとえば、5 TB (テラバイト) のように指定します。
5. **［作成］** を選択します

サイズによっては、ボリュームの作成に数分かかることがあります。 右上の通知により、ボリュームが作成されたことを知ることができます。 新しいボリュームが [インベントリ] の一覧に表示されます。

3 方向ミラー ボリュームの作成方法に関する簡単な動画をご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>ミラー高速パリティ ボリュームの作成

ミラー高速パリティによって、HDD 上のボリュームのフットプリントが減少します。 たとえば、3 方向ミラー ボリュームでは、10 テラバイトのサイズごとに、フットプリントとして 30 テラバイトが必要になることを意味します。 フットプリントのオーバーヘッドを削減するには、ミラー高速パリティを使用してボリュームを作成します。 これにより、最もアクティブな 20 % のデータをミラー化し、よりスペース効率の高いパリティを使用して残りを保管することで、4 台のサーバーのみでも、フットプリントを 30 テラバイトから 22 テラバイトまで削減できます。 このパリティとミラーの比率を調整して、ワークロードに適したパフォーマンスと容量のトレードオフを実現できます。 たとえば、90 % のパリティと 10 % のミラーでは、パフォーマンスが低下しますが、フットプリントはさらに合理化されます。

Windows Admin Center でミラー高速パリティを使用するボリュームを作成するには、次のようにします。

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、 **[ツール]** ペインで **[ボリューム]** を選択します。
2. [ボリューム] ページで **[インベントリ]** タブを選択し、 **[ボリュームの作成]** を選択します。
3. **[ボリュームの作成]** ペインで、ボリュームの名前を入力します。
4. **[回復性]** で、 **[Mirror-accelerated parity]\(ミラー高速パリティ\)** を選択します。
5. **[Parity percentage]\(パリティの割合\)** で、パリティの割合を選択します。
6. **［作成］** を選択します

ミラー高速パリティ ボリュームを作成する方法についての簡単な動画をご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>ボリュームを開いてファイルを追加する

Windows Admin Center でボリュームを開き、ボリュームにファイルを追加するには、次のようにします。

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、 **[ツール]** ペインで **[ボリューム]** を選択します。
2. [ボリューム] ページで、 **[インベントリ]** タブを選択します。
2. ボリュームの一覧で、開くボリュームの名前を選択します。

    ボリュームの詳細ページで、ボリュームのパスを確認できます。

4. ページの最上部で **[開く]** を選択します。 これにより、Windows dmin Center のファイル ツールが起動します。
5. ボリュームのパスに移動します。 ここで、ボリューム内のファイルを参照できます。
6. **[アップロード]** を選択し、アップロードするファイルを選択します。
7. ブラウザーの **[戻る]** ボタンを使用して、Windows Admin Center の [ツール] ペインに戻ります。

ボリュームを開いてファイルを追加する方法に関する簡単な動画をご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>重複除去と圧縮を有効にする

重複除去と圧縮はボリュームごとに管理されます。 重複除去と圧縮では後処理モデルが使用されるため、実行されるまで節約は確認されません。 実行されると、以前から存在するファイルであっても、すべてのファイルが処理されます。

1. Windows Admin Center で、記憶域スペース ダイレクト クラスターに接続し、 **[ツール]** ペインで **[ボリューム]** を選択します。
2. [ボリューム] ページで、 **[インベントリ]** タブを選択します。
3. ボリュームの一覧で、管理するボリュームの名前を選択します。
4. ボリュームの詳細ページで、 **[Deduplication and compression]\(重複除去と圧縮\)** というラベルの付いたスイッチをクリックします。
5. [Enable deduplication]\(重複除去を有効にする\) ペインで、重複除去モードを選択します。

    Windows Admin Center では、複雑な設定の代わりに、さまざまなワークロードに対応した既製のプロファイルを選択できます。 わからない場合は、既定の設定を使用します。

6. **[有効化]** を選択します。

重複除去と圧縮を有効にする方法に関する簡単な動画をご覧ください。

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>PowerShell を使ったボリュームの作成

記憶域スペース ダイレクトのボリュームを作成するには、**New-Volume** コマンドレットを使うことをお勧めします。 これは、高速で操作が非常に分かりやすいです。 このコマンドレット 1 つだけで、仮想ディスクが作成されて、パーティション化およびフォーマットされ、一致する名前を持つボリュームが作成されて、クラスター共有ボリュームに追加されます。すべて 1 つの簡単な手順で行うことができます。

**New-Volume** コマンドレットには、次の 4 つのパラメーターを常に指定する必要があります。

- **FriendlyName:** 任意の文字列 (たとえば *"Volume1")*
- **[FileSystem]:** **CSVFS_ReFS** (推奨) または **CSVFS_NTFS**
- **StoragePoolFriendlyName:** 記憶域プールの名前 (たとえば *"S2D on ClusterName"* )
- **Size:** ボリュームのサイズ (たとえば *"10 TB"* )

   > [!NOTE]
   > PowerShell を含む Windows では、バイナリ (基数 2) の数値を使用してカウントされますが、ドライブには 10 進数 (基数 10) の数値でラベルが付けれていることがよくあります。 これが理由で、1 兆バイトとして定義された "1 テラバイト" のドライブは Windows で約 "909 GB" として表示されます。 これは予期されることです。 **New-Volume** を使用してボリュームを作成する場合は、**Size** パラメーターをバイナリ (基数 2) の数値で指定する必要があります。 たとえば、"909 GB" または "0.909495 TB" を指定すると、約 1 兆バイトのボリュームが作成されます。

### <a name="example-with-2-or-3-servers"></a>例:2 台または 3 台のサーバー

設定を簡単にするために、デプロイにサーバーが 2 台しかない場合は、回復性を確保するために、記憶域スペース ダイレクトによって双方向のミラーリングが自動的に使用されます。 デプロイにサーバーが 3 台しかない場合は、自動的に 3 方向のミラーリングが使用されます。

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>例:4 台以上のサーバー

4 台以上のサーバーがある場合は、オプションの **ResiliencySettingName** パラメーターを使用して、回復性の種類を選択できます。

-   **ResiliencySettingName:** **Mirror** または **Parity** のいずれか。

次の例では *"Volume2"* で 3 方向ミラーリングを使用し、 *"Volume3"* でデュアル パリティを使用しています ("イレージャー コーディング" とよく呼ばれます)。

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>例:ストレージ層の使用

3 種類のドライブを使用したデプロイでは、1 つのボリュームが SSD および HDD 階層にまたがり、それぞれに部分的に存在することができます。 同様に、4 台以上のサーバーを使用したデプロイでは、1 つのボリュームにミラーリングとデュアル パリティを混在させ、両方に部分的に配置できます。

このようなボリュームを作成できるように、記憶域スペース ダイレクトには "*Performance*" と "*Capacity*" という名前の既定の層テンプレートが用意されています。 これらは、高速な容量のドライブの 3 方向ミラーリング (該当する場合)、および低速な容量のドライブのデュアル パリティ (該当する場合) の定義をカプセル化したものです。

これを確認するには、**Get-StorageTier** コマンドレットを実行します。

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![ストレージ層の PowerShell のスクリーンショット](media/creating-volumes/storage-tiers-screenshot.png)

階層化ボリュームを作成するには、**New-Volume** コマンドレットの **StorageTierFriendlyNames** と **StorageTierSizes** パラメーターを使用して、これらの層テンプレートを参照します。 たとえば、次のコマンドレットは、3 方向のミラーリングとデュアル パリティを30:70 の比率で混合するボリュームを 1 つ作成します。

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

以上で終わりです。 必要なだけ繰り返して、複数のボリュームを作成します。

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
- [記憶域スペース ダイレクトのボリュームの拡張](resize-volumes.md)
- [記憶域スペースダイレクトのボリュームの削除](delete-volumes.md)
