---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: クラスター対応更新プラグインのしくみ
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: プラグインを使用して、クラスターで更新プログラムをインストールする Windows Server をクラスター対応更新を使用する場合は、更新プログラムを調整する方法。
ms.openlocfilehash: d09addb5e6787a8386d50570c0d27640646aa587
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854563"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>クラスター対応更新プラグインのしくみ

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)(CAU) は、フェールオーバー クラスター内のノード間で更新プログラムのインストールを調整するプラグインを使用します。 このトピックでは、組み込みの使用に関する情報を提供します。\-CAU プラグインで\-アドインまたはその他のプラグ\-CAU 用にインストールするアドイン。

## <a name="BKMK_INSTALL"></a>インストール、プラグ\-で  
プラグ\-で既定以外プラグイン\-CAU と共にインストールされたスナップイン\( **Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin** \)個別にインストールする必要があります。 CAU を自己で使用する場合\-更新モード、プラグ\-では、すべてのクラスター ノードにインストールする必要があります。 CAU をリモートで使用する場合\-更新モード、プラグ\-では、リモート更新コーディネーター コンピューターにインストールする必要があります。 プラグ\-をインストールすることでは各ノードで追加のインストール要件が可能性があります。  
  
プラグをインストールする\-、指示に従って、プラグインから\-publisher でします。 プラグを手動で登録する\-、CAU を使用して実行、 [Register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin)コマンドレットを各コンピューターでプラグ\-がインストールされています。  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>プラグを指定\-でプラグインと\-引数  
  
### <a name="specify-a-cau-plug-in"></a>CAU プラグインを指定\-で

CAU ui で、プラグインを選択します\-で、ドロップダウンから\-使用可能なプラグインの一覧を下\-CAU を使用して、次の操作を実行するときにアドイン。  
  
-   クラスターに更新プログラムを適用する  
  
-   クラスターの更新プログラムをプレビューする  
  
-   構成するクラスターの自己\-更新オプション  
  
既定では、CAU は、プラグインを選択します\-で**Microsoft.WindowsUpdatePlugin**します。 ただし、任意のプラグを指定できます\-がインストールされ、CAU に登録します。

> [!TIP]  
> CAU ui で、1 つのプラグを指定することができますのみ\-で CAU 更新実行中に更新プログラムを適用するまたはプレビューを使用するのです。 CAU の PowerShell コマンドレットを使用すると、1 つまたは複数のプラグインを指定できます\-アドイン。クラスターに複数の種類の更新プログラムをインストールする必要がある場合は、複数のプラグインを指定する方が効率的\-、独立した更新実行を使用して、各プラグインのではなく、1 つ更新実行で ins\-でします。 たとえば、通常は、ノードの再起動の回数が少なくなります。

次の表に記載されている CAU PowerShell コマンドレットを使用すると、1 つまたは複数のプラグインを指定できます\-更新実行やスキャンを渡すことによって、 **– CauPluginName**パラメーター。 複数のプラグインを指定する\-コンマで区切ることにより、名前にします。 複数のプラグインを指定する場合\-アドインを制御することもどのプラグ\-アドインに影響を与える他の更新実行中に指定することによって、  **\-RunPluginsSerially**、  **\-StopOnPluginFailure**、および **– SeparateReboots**パラメーター。 複数のプラグインを使用しての詳細については\-アドインを使用して、次の表に、コマンドレットのドキュメントを提供されるリンク。  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|Self は、CAU のクラスター化された役割を追加します。\-機能を、指定したクラスターに更新します。|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、更新実行で、指定したクラスターにその更新プログラムをインストールします。|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、指定したクラスターの各ノードに適用される更新プログラムの初期セットの一覧を返します。|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|指定したクラスターに CAU のクラスター化された役割の構成プロパティを設定します。|  
  
CAU プラグインを指定しない場合\-でこれらのコマンドレットを使用して、パラメーター、既定値は、プラグ\-で**Microsoft.WindowsUpdatePlugin**します。  
  
### <a name="specify-cau-plug-in-arguments"></a>CAU プラグインを指定\-引数  
更新実行オプションを構成するときに、1 つまたは複数を指定することができます*名前\=値*ペア\(引数\)選択したプラグインの\-のロックを使用します。 たとえば、CAU UI では、次のように複数の引数を指定できます。  
  
**Name1\=Value1;Name2\=Value2;Name3\=Value3**  
  
これら*名前\=値*ペアは、プラグインにとって意味のあるである必要があります\-を指定することにします。 一部のプラグを\-ins 引数は省略可能です。  
  
CAU プラグインの構文\-引数でこれらの一般的な規則に従います。  
  
-   複数*名前\=値*のペアをセミコロンで区切られます。  
  
-   値にスペースを含める場合は、次のように引用符で囲みます。**Name1\="Value with Spaces"** します。  
  
-   正確な構文*値*プラグに依存\-でします。  
  
プラグインを指定する\-in 引数をサポートする CAU の PowerShell コマンドレットを使用して、 **– CauPluginParameters**パラメーターの形式でパラメーターを渡します。  
  
**\-@{Name1\=Value1;Name2\=Value2;Name3\=:value3}**  
  
定義済みの PowerShell ハッシュ テーブルを使用することもできます。 プラグインを指定する\-プラグを 1 つ以上の引数で\-引数をコンマ区切りで複数のハッシュ テーブルを渡します。 プラグを渡す\-引数プラグに\-で指定された順序で**CauPluginName**します。  
  
### <a name="specify-optional-plug-in-arguments"></a>省略可能なプラグインを指定\-引数  
プラグ\-CAU によってインストールされる ins \( **Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin** \)選択できる追加のオプションを提供します。 表示されます、CAU UI で、**追加オプション**プラグの更新実行オプションを構成した後にページ\-でします。 省略可能なプラグインとしてこれらのオプションを構成する場合は、CAU の PowerShell コマンドレットを使用している\-引数。 詳細については、後の「 [Microsoft.WindowsUpdatePlugin の使用](#BKMK_WUP) 」および「 [Microsoft.HotfixPlugin の使用](#BKMK_HFP) 」を参照してください。  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>プラグインの管理\-Windows PowerShell コマンドレットを使用してアドイン  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|プラグを更新する 1 つまたは複数のソフトウェアに関する情報を取得\-ローカル コンピューターに登録されているアドイン。|  
|[Register-cauplugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|プラグインを更新する CAU ソフトウェアを登録します\-でローカル コンピューターにします。|  
|[登録を解除 CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|ソフトウェア更新プラグインを削除します\-でプラグインの一覧から\-CAU で使用できるアドインです。 **注:** プラグ\-CAU と共にインストールされたスナップイン\( **Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin** \)登録を解除することはできません。|  
  
## <a name="BKMK_WUP"></a>Microsoft.WindowsUpdatePlugin の使用  

既定のプラグイン\-で、CAU の**Microsoft.WindowsUpdatePlugin**、次の操作を実行します。
- 各フェールオーバー クラスター ノード上の Windows Update エージェントと通信し、各ノードで実行されている Microsoft 製品に必要な更新プログラムを適用します。
- Windows Update や Microsoft Update、またはからクラスター更新プログラムを直接のインストールで\-オンプレミス Windows Server Update Services \(WSUS\)サーバー。
- 選択されているのみのインストール、一般配布リリース\(GDR\)更新します。 既定では、プラグ\-で重要なソフトウェアの更新プログラムのみ適用されます。 構成は必要ありません。 既定の構成で、重要な GDR 更新プログラムが各ノードにダウンロードされ、インストールされます。 

> [!NOTE]
> 既定で選択されている重要なソフトウェア更新プログラム以外の更新プログラムを適用する\(ドライバーの更新など、\)、省略可能なプラグインを構成する\-パラメーターにします。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="requirements"></a>要件

- フェールオーバー クラスターとリモート更新コーディネーター コンピューター\(使用されている場合\)CAU と記載リモート管理のために必要な構成の要件を満たす必要があります[要件と CAU のベスト プラクティス](cluster-aware-updating-requirements.md).
- 「[Microsoft 更新プログラムを適用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_WUA)」を参照し、フェールオーバー クラスター ノードに合わせて Microsoft Update に必要な変更を加えます。
- 最良の結果をお勧め、CAU ベスト プラクティス アナライザーを実行する\(BPA\) CAU を使用して更新プログラムを適用するクラスターと更新プログラムの環境が正しく構成されていることを確認します。 詳細については、「 [Test CAU updating readiness](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。

> [!NOTE]
> Microsoft の利用規約に同意する必要がある更新プログラムや、ユーザー操作が必要な更新プログラムは除外されるため、手動でインストールする必要があります。

### <a name="additional-options"></a>[追加オプション]

必要に応じて、次のプラグインを指定できます\-拡張またはプラグによって適用される更新プログラムのセットを制限する引数の\-で。
- プラグを構成する\-の各ノードは、CAU UI で、重要な更新プログラムだけでなく、推奨される更新プログラムを適用するに、**追加オプション**] ページで、[、**同じ更新プログラムの推奨 me 付与方法重要な更新プログラムを受信する**チェック ボックスをオンします。
<br>また、構成、 **'IncludeRecommendedUpdates'\='True'** プラグイン\-引数にします。
- プラグを構成する\-でを各クラスター ノードに適用する GDR 更新プログラムの種類をフィルター処理する、Windows Update エージェント クエリ文字列を使用して指定、 **QueryString**プラグイン\-引数にします。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="BKMK_QUERY"></a>Windows Update Agent クエリ文字列を構成します。  
プラグを構成する\-、既定の引数でプラグイン\-、 **Microsoft.WindowsUpdatePlugin**、Windows Update エージェントで構成される\(WUA\)クエリ文字列。 この手順では、WUA API を使用して、1 つまたは複数のグループの Microsoft 更新プログラムを指定して、指定した条件に基づいて各ノードに適用します。 複数の条件を組み合わせるには、論理 AND または論理 OR を使用できます。 WUA クエリ文字列が、プラグインで指定された\-よう引数で。  
  
**QueryString\="Criterion1\=Value1 と\/または Criterion2\=Value2 と\/または..."**  
  
たとえば、**Microsoft.WindowsUpdatePlugin** では、既定の **QueryString** 引数を使用して重要な更新プログラムを自動的に選択します。この引数は、**IsInstalled**、**Type**、**IsHidden**、および **IsAssigned** の条件を使用して構築します。  
  
**QueryString\="IsInstalled\=0 と種類\='ソフトウェア' および IsHidden\=0 と IsAssigned\=1"**  
  
指定した場合、 **QueryString**引数、既定値の代わりに使用されます**QueryString**プラグ用に構成された\-で。  
  
#### <a name="example-1"></a>例 1
  
構成する、 **QueryString** ID によって識別される特定の更新プログラムをインストールする引数*f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\="UpdateID\=' f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003' や IsInstalled\=0"**  
  
> [!NOTE]  
> 前の例は、クラスターを使用して更新プログラムを適用するために有効な\-更新ウィザードを注意してください。 自己を構成することによって、特定の更新プログラムをインストールするかどうか\-CAU UI を使用した、またはを使用して、更新オプション、**追加\-CauClusterRole**または**設定\-CauClusterRole**PowerShell コマンドレットでは、2 つの 1 つを使用して UpdateID 値を書式設定する必要があります\-区切り記号。  
>   
> **QueryString\="UpdateID\=' f6ce46c1\-971 c\-43f9\-a2aa\-783df125f003 '、IsInstalled\=0"**  
  
#### <a name="example-2"></a>例 2
  
ドライバーのみをインストールする **QueryString** 引数を構成するには:  
  
**QueryString\="IsInstalled\=0 と種類\='ドライバー' と IsHidden\=0"**  
  
既定のクエリ文字列の詳細については、プラグイン\-、 **Microsoft.WindowsUpdatePlugin**、検索条件\(など**IsInstalled**\)、クエリ文字列に含めることができる構文で検索条件に関するセクションを参照してくださいと、 [Windows Update エージェント (WUA) API リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=223304)します。  
  
## <a name="BKMK_HFP"></a>Microsoft.HotfixPlugin を使用します。  
プラグ\-で**Microsoft.HotfixPlugin** Microsoft の限定配布リリースを適用するために使用できる\(LDR\)更新\(、修正プログラムとも呼ばれ、旧称は Qfe\)ことを個別にダウンロードに特定の Microsoft ソフトウェアの問題に対処します。 プラグインは、SMB ファイル共有上のルート フォルダーから更新プログラムをインストールして適用以外にもカスタマイズできます\-Microsoft ドライバー、ファームウェア、および BIOS の更新プログラム。

> [!NOTE]
> 修正プログラムは、サポート技術情報の記事で Microsoft からダウンロードできる場合がありますが、としてお客様にも提供されている\-必要に応じて。

### <a name="requirements"></a>必要条件

- フェールオーバー クラスターとリモート更新コーディネーター コンピューター\(使用されている場合\)CAU と記載リモート管理のために必要な構成の要件を満たす必要があります[要件と CAU のベスト プラクティス](cluster-aware-updating-requirements.md).
- 「[Microsoft.HotfixPlugin を使用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_HF)」を参照してください。
- 最良の結果をお勧め、CAU ベスト プラクティス アナライザーを実行する\(BPA\) CAU を使用して更新プログラムを適用するクラスターと更新プログラムの環境が正しく構成されていることを確認するモデル。 詳細については、「 [Test CAU updating readiness](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。
- パブリッシャーで更新プログラムを入手し、コピーまたはサーバー メッセージ ブロックに抽出\(SMB\)ファイル共有\(修正プログラム ルート フォルダー\)以上をサポートする SMB 2.0 とは、すべてのクラスターからアクセス可能なノードとリモート更新コーディネーター コンピューター \(CAU をリモートで使用する場合\-更新モード\)します。 詳細については、後述する「 [修正プログラム ルート フォルダー構造を構成する](#BKMK_HF_ROOT) 」を参照してください。 

    > [!NOTE]
    > 既定では、このプラグインによって\-で次のファイル名拡張子を持つのみの修正プログラムをインストール: .msu、.msi、および .msp します。

- DefaultHotfixConfig.xml ファイル コピー\(で表示されている、 **%systemroot%\\System32\\WindowsPowerShell\\v1.0\\モジュール\\ClusterAwareUpdating** CAU ツールがインストールされているコンピューター上のフォルダー\)修正プログラムを抽出およびを作成した修正プログラム ルート フォルダー。 たとえば、構成ファイルのコピー  *\\ \\MyFileServer\\修正プログラム\\ルート\\*します。 

    > [!NOTE]
    > Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムをインストールするには、既定の修正プログラム構成ファイルを変更せずに使用できます。 変更が必要な場合は、高度なタスクとして構成ファイルをカスタマイズできます。 構成ファイルには、カスタム規則を含めることができます。たとえば、特定の拡張子を持つ修正プログラム ファイルの処理、特定の終了条件に関する動作の定義などです。 詳細については、このトピックの「[修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE)」を参照してください。

### <a name="configuration"></a>構成

次の設定を構成します。 詳細については、このトピックで後述するセクションのリンクを参照してください。
- 適用する更新プログラムと修正プログラムの構成ファイルが保存される、共有される修正プログラム ルート フォルダーのパス。 CAU UI でこのパスを入力するか、または構成、 **HotfixRootFolderPath\=\<パス >** PowerShell プラグ\-引数にします。 

   > [!NOTE]
   > 修正プログラム ルート フォルダーを指定するには、ローカル フォルダーのパス、または形式の UNC パスとして *\\ \\ServerName\\共有\\RootFolderName*します。 ドメイン\-ベースまたはスタンドアロン DFS Namespace パスを使用できます。 ただし、プラグ\-へのアクセスを確認する機能の修正プログラムの構成ファイルのアクセス許可と互換性がない DFS Namespace パスでは、いずれかを構成する場合、CAU UI を使用して、または構成することでアクセス許可のチェックを無効にする必要がありますので、**DisableAclChecks\='True'** プラグイン\-引数にします。
- 共有フォルダーのフォルダーにアクセスし、SMB からアクセスされるデータの整合性を確保するには、適切なアクセス許可を確認する修正プログラム ルート フォルダーをホストするサーバーで設定\(SMB 署名または SMB 暗号化\)します。 詳細については、「[修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」を参照してください。

### <a name="additional-options"></a>[追加オプション]

- プラグを必要に応じて、構成\-でのでその SMB 暗号化を実行、修正プログラムのファイル共有からのデータにアクセスするとき。 CAU ui での**追加オプション**] ページで、[、**修正プログラム ルート フォルダーへのアクセスに SMB 暗号化を要求**オプション、または構成、 **RequireSMBEncryption\='True'** PowerShell プラグ\-引数にします。 
  > [!IMPORTANT]
  > SMB データの SMB 署名または SMB 暗号化との整合性を有効にするには、SMB サーバーで追加の構成手順を実行する必要があります。 詳細については、「 [修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」の手順 4. を参照してください。 SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用したアクセスに対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。
- 必要に応じて、修正プログラム ルート フォルダーと修正プログラムの構成ファイルに十分なアクセス許可があるかどうかに関する既定の確認を無効にします。 CAU ui で選択**修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする**、または構成、 **DisableAclChecks\='True'** プラグイン\-で引数。
- 必要に応じて、構成、 **HotfixInstallerTimeoutMinutes\= <Integer>** 修正プログラムはどのくらいの時間を指定する引数のプラグイン\-で修正プログラムのインストーラー プロセスから戻るまで待機します。 \(既定では 30 分です。\)たとえば、2 時間のタイムアウト期間を指定するには、次のように設定します。 **HotfixInstallerTimeoutMinutes\=120**します。
- 必要に応じて、構成、 **HotfixConfigFileName \= <name>** プラグイン\-では、修正プログラム ルート フォルダーにある修正プログラム構成ファイルの名前を指定する引数。 指定しない場合、既定の名前である DefaultHotfixConfig.xml が使用されます。
  
### <a name="BKMK_HF_ROOT"></a>修正プログラム ルート フォルダー構造を構成します。

修正プログラム プラグイン\-にするには、修正プログラムする必要がありますに格納する適切な\-構造体を SMB ファイル共有で定義されている\(修正プログラム ルート フォルダー\)、および修正プログラム プラグインを構成する必要があります\-へのパスを使用して、CAU UI または CAU の PowerShell コマンドレットを使用して修正プログラム ルート フォルダー。 このパスは、プラグインに渡される\-でとして、 **HotfixRootFolderPath**引数。 次の例のように、実際の更新のニーズに応じて、修正プログラム ルート フォルダーに対応するいくつかの構造からいずれかを選択できます。 この構造に従っていないファイルまたはフォルダーは無視されます。  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>例 1: フォルダーの構造体のすべてのクラスター ノードに修正プログラムを適用するために使用
  
すべてのクラスター ノードに修正プログラムを適用することを指定するという名前のフォルダーにコピー **CAUHotfix\_すべて**修正プログラム ルート フォルダー。 この例で、 **HotfixRootFolderPath**プラグイン\-引数でに設定されて *\\ \\MyFileServer\\修正プログラム\\ルート\\*. **CAUHotfix\_すべて**フォルダーには、拡張子が .msu、.msi、および .msp のすべてのクラスター ノードに適用されると次の 3 つの更新プログラムが含まれています。 この更新プログラム ファイル名は、説明のためにのみ使用されています。  
  
> [!NOTE]  
> この例と以降の例で、DefaultHotfixConfig.xml という既定の名前の修正プログラム構成ファイルは、修正プログラム ルート フォルダーの必要な場所に表示されます。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>例 2 - フォルダー構造の特定のノードにのみ特定の更新プログラムを適用するために使用
  
特定のノードにのみ適用する修正プログラムを指定するには、修正プログラム ルート フォルダー以下にあるノード名を持つサブフォルダーを使用します。 クラスター ノードの NetBIOS 名を使用します。たとえば、*ContosoNode1* などです。 次に、そのノードにのみ適用する更新プログラムを、このサブフォルダーに移動します。 次の例では、 **HotfixRootFolderPath**プラグイン\-引数でに設定されて *\\ \\MyFileServer\\修正プログラム\\ルート\\*. 内の更新、 **CAUHotfix\_すべて**フォルダーはすべてのクラスター ノードに適用されると*Node1\_特定\_Update.msu* にのみ適用される*ContosoNode1*します。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
   ContosoNode1\   
      Node1_Specific_Update.msu   
      ...  
```  
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>例 3 - フォルダー構造が .msu、.msi、および .msp ファイル以外の更新プログラムを適用するために使用
  
既定では、**Microsoft.HotfixPlugin** は拡張子が .msu、.msi、または .msp の更新プログラムのみを適用します。 ただし、一部の更新プログラムは拡張子が異なり、別のインストール コマンドが必要な場合があります。 たとえば、場合によっては、拡張子が .exe のファームウェアの更新プログラムをクラスター内のノードに適用する必要があります。 修正プログラム ルート フォルダーを構成するには、特定の非を示す名前のサブフォルダー\-既定の更新プログラムの種類をインストールする必要があります。 また、対応するフォルダーのインストール規則を構成して、修正プログラムの構成 XML ファイルで `<FolderRules>` 要素にインストール コマンドを指定する必要もあります。  
  
次の例では、 **HotfixRootFolderPath**プラグイン\-引数でに設定されて *\\ \\MyFileServer\\修正プログラム\\ルート\\*. 一部の更新プログラムはすべてのクラスター ノードに適用されます。またファームウェアの更新プログラムの *SpecialHotfix1.exe* は、*FolderRule1* を使用して *ContosoNode1* に適用されます。 修正プログラムの構成ファイルで *ContosoNode1* を構成する場合の詳細については、このトピックの「 [修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE) 」を参照してください。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
  
   ContosoNode1\   
      FolderRule1\  
          SpecialHotfix1.exe  
      ...  
```

### <a name="BKMK_CONFIG_FILE"></a>修正プログラム構成ファイルをカスタマイズします。  
修正プログラムの構成ファイルは、フェールオーバー クラスターに特定の修正プログラム ファイルの種類を **Microsoft.HotfixPlugin** でインストールする方法を制御します。 構成ファイルの XML スキーマは HotfixConfigSchema.xsd で定義されています。この xsd ファイルは、CAU ツールがインストールされているコンピューターの次のフォルダーに保存されています。  
  
**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\モジュール\\ClusterAwareUpdating フォルダー**  
  
修正プログラムの構成ファイルをカスタマイズするには、この場所にあるサンプルの構成ファイル DefaultHotfixConfig.xml を修正プログラム ルート フォルダーにコピーし、実際のシナリオに合わせて変更します。  
  
> [!IMPORTANT]  
> Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムを適用するには、既定の修正プログラム構成ファイルを変更せずに使用できます。 修正プログラムの構成ファイルのカスタマイズは、高度な使用シナリオでのみ実行されるタスクです。  
  
修正プログラムの構成 XML ファイルは、次の 2 つのカテゴリの修正プログラムについて、既定でインストール規則と終了条件を定義しています。  
  
-   拡張機能の修正プログラム ファイルをプラグ\-で既定でインストールできます\(.msu、.msi、および .msp ファイル\)します。  
  
    これらは、 `<ExtensionRules>` 要素内の `<DefaultRules>` 要素として定義されます。 既定のサポートされるファイルの種類ごとに、1 つの `<Extension>` 要素があります。 一般的な XML 構造は次のとおりです。  
  
    ```xml  
    <DefaultRules>  
        <ExtensionRules>  
          <Extension name="MSI">  
            <!-- Template and ExitConditions elements for installation of .msi files follow -->  
             ...  
          </Extension>  
          <Extension name="MSU">  
            <!-- Template and ExitConditions elements for installation of .msu files follow -->  
             ...  
          </Extension>  
          <Extension name="MSP">  
            <!-- Template and ExitConditions elements for installation of .msp files follow -->  
             ...  
          </Extension>  
             ...  
       </ExtensionRules>  
    </DefaultRules>  
    ```  
  
    一部の更新プログラムの種類を環境内のすべてのクラスター ノードに適用する必要がある場合、追加の `<Extension>` 要素を定義できます。  
  
-   修正プログラムまたはその他の更新されていない、.msi、.msu、または .msp ファイルがないファイル\-Microsoft ドライバー、ファームウェア、および BIOS の更新プログラム。  
  
    各非\-として構成されている既定のファイルの種類、`<Folder>`内の要素、`<FolderRules>`要素。 `<Folder>` 要素の name 属性は、対応する種類の更新プログラムを保存する修正プログラム ルート フォルダー内のフォルダー名と同じにする必要があります。 フォルダーを指定できます、 **CAUHotfix\_すべて**フォルダーまたはノードで\-特定のフォルダー。 たとえば、 *FolderRule1* を修正プログラム ルート フォルダー内に構成する場合、XML ファイルに次の要素を構成して、そのフォルダー内の更新プログラムについてインストール テンプレートと終了条件を定義します。  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
次の表は、 `<Template>` 属性と使用できる `<ExitConditions>` サブ要素の説明です。  
  
|`<Template>` 属性|説明|  
|--------------------------|---------------|  
|`path`|`<Extension name>` 属性に定義されているファイルの種類に関する、インストール プログラムの完全なパス。<br /><br />修正プログラム ルート フォルダー構造にある更新プログラム ファイルのパスを指定するには、 `$update$`を使用します。|  
|`parameters`|`path`に指定されているプログラムの必要なパラメーターと省略可能なパラメーターの文字列。<br /><br />修正プログラム ルート フォルダー構造にある更新プログラム ファイルのパスのパラメーターを指定するには、 `$update$`を使用します。|  
  
|`<ExitConditions>` サブ要素|説明|  
|---------------------------------|---------------|  
|`<Success>`|指定した更新プログラムが成功したことを示す終了コードを 1 つまたは複数定義します。 これは必須のサブ要素です。|  
|`<Success_RebootRequired>`|必要に応じて、指定した更新プログラムが成功し、ノードを再起動する必要があることを示す終了コードを 1 つまたは複数定義します。 <br>**注:** 必要に応じて、`<Folder>` 要素には `alwaysReboot` 属性を含めることができます。 この属性を設定すると、この規則でインストールされる修正プログラムが `<Success>`に定義されている終了コードのいずれかを返した場合、 `<Success_RebootRequired>` 終了条件として解釈されます。|  
|`<Fail_RebootRequired>`|必要に応じて、指定した更新プログラムが失敗し、ノードを再起動する必要があることを示す終了コードを 1 つまたは複数定義します。|  
|`<AlreadyInstalled>`|必要に応じて、指定した更新プログラムは既にインストールされているため、適用されなかったことを示す終了コードを 1 つまたは複数定義します。|  
|`<NotApplicable>`|必要に応じて、指定した更新プログラムはクラスター ノードに適用されていないため、適用されなかったことを示す終了コードを 1 つまたは複数定義します。|  
  
> [!IMPORTANT]  
> `<ExitConditions>` に明示的に定義されていない終了コードは、更新プログラムが失敗したと解釈され、ノードは再起動しません。  
  
### <a name="BKMK_ACL"></a>修正プログラム ルート フォルダーへのアクセスを制限します。  
SMB ファイル サーバーとファイル共有を構成して、 **Microsoft.HotfixPlugin**のコンテキストでのみアクセスするように修正プログラム ルート フォルダー ファイルと修正プログラムの構成ファイルをセキュリティで保護するには、いくつかの手順を実行する必要があります。 これらの手順によって、フェールオーバー クラスターのセキュリティを侵害するような方法で修正プログラム ファイルを改ざんする危険性を回避できます。  
  
一般的な手順は次のとおりです。  
  
1.  プラグを使用して更新実行に使用されるユーザー アカウントを識別する\-で  
  
2.  SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する  
  
3.  修正プログラム ルート フォルダーのアクセス許可を構成する  
  
4.  SMB データの整合性に関する設定を構成する  
  
5.  SMB サーバーで Windows ファイアウォール規則を有効にする  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>手順 1. 修正プログラム プラグインを使用して更新実行に使用されるユーザー アカウントを識別する\-で
  
CAU 更新実行を使用して、実行中にセキュリティ設定を確認するために使用するアカウント**Microsoft.HotfixPlugin** CAU をリモートで使用するかどうかによって異なります\-更新モードや self\-としてモードの更新次に示します。  
  
-   **リモート\-更新モード**をプレビューし、更新プログラムを適用するクラスター上で管理者特権を持つアカウント。  
  
-   **Self\-更新モード**クラスター化された役割を CAU の Active Directory で構成されている仮想コンピューター オブジェクトの名前。 この名前は、Active Directory で CAU のクラスター化された役割用に事前設定された仮想コンピューター オブジェクトの名前か、クラスター化された役割用に CAU によって生成された名前です。 CAU によって生成される場合は、名前を取得、実行、**取得\-CauClusterRole** CAU PowerShell コマンドレット。 出力の **ResourceGroupName** は、生成された仮想コンピューター オブジェクト アカウントの名前です。  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>手順 2.  SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する
  
> [!IMPORTANT]  
> 更新実行に使用するアカウントは、SMB サーバーのローカルの管理者アカウントとして追加する必要があります。 組織のセキュリティ ポリシーで、このようなアカウントを追加できない場合は、次の手順を使用して、SMB サーバーに必要なアクセス許可を持つ管理者アカウントを構成します。  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB サーバーでユーザー アカウントを構成するには  
  
1.  更新実行に使用するアカウントを Distributed COM Users グループに追加し、Power User、Server Operation、または Print Operator のいずれかに追加します。  
  
2.  アカウントに必要な WMI のアクセス許可を有効にするには、SMB サーバーで WMI 管理コンソールを開始します。 PowerShell を起動し、次のコマンドを入力します。  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  コンソール ツリーで、右\-クリックして**WMI コントロール\(ローカル\)**、順にクリックします**プロパティ**します。  
  
4.  **[セキュリティ]** をクリックし、**[ルート]** を展開します。  
  
5.  **[CIMV2]** をクリックし、**[セキュリティ]** をクリックします。  
  
6.  更新実行に使用するアカウントを **[グループ名またはユーザー名]** リストに追加します。  
  
7.  **[メソッドの実行]** および **[リモートの有効化]** のアクセス許可を更新実行に使用するアカウントに付与します。  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>手順 3. 修正プログラム ルート フォルダーのアクセス許可を構成する
  
既定では、更新プログラムを適用しようとしたときに、修正プログラム プラグイン\-で修正プログラム ルート フォルダーへのアクセスの NTFS ファイル システム権限の構成を確認します。 フォルダーのアクセス許可が正しく構成されていない、更新実行の修正プログラム プラグインを使用して場合\-でが失敗します。  
  
修正プログラム プラグインの既定の構成を使用するかどうかは\-フォルダーのアクセス許可が、次の要件を満たしていることを確認します。  
  
-   Users グループに読み取りアクセス許可があります。  
  
-   場合、プラグ\-では、.exe 拡張子を持つ更新プログラムを適用、ユーザー グループが Execute 権限があります。  
  
-   特定のセキュリティ プリンシパルのみが許可されている\(は必要ありませんが、\)書き込みまたはアクセス許可を変更します。 許可されるプリンシパルは、ローカルの Administrators グループ、SYSTEM、CREATOR OWNER、および TrustedInstaller です。 その他のアカウントまたはグループには、修正プログラム ルート フォルダーで書き込みまたは修正のアクセス許可は付与されません。  
  
必要に応じて、前のチェックを無効にするをプラグ\-では、既定では実行します。 2 つの方法のいずれかでこれを行うことができます。  
  
-   CAU の PowerShell コマンドレットを使用している場合は、構成、 **DisableAclChecks\='True'** 引数、**で**の修正プログラム プラグイン パラメーター\-でします。  
  
-   CAU UI を使用している場合、更新実行オプションの構成に使用するウィザードの **[追加の更新オプション]** ページで、**[修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする]** オプションをオンにします。  
  
ただし、多くの環境では、ベスト プラクティスとして、既定の構成を使用してこれらの確認を実行することをお勧めします。  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>手順 4. SMB データの整合性に関する設定を構成する
  
修正プログラムがプラグインのクラスター ノードと、SMB ファイル共有間の接続でデータの整合性を確認する\-で SMB 署名または SMB 暗号化の SMB ファイル共有の設定を有効にすることが必要です。 Windows Server 2012 以降では、セキュリティを強化し、多くの環境でパフォーマンスの向上を提供する SMB 暗号化がサポートされていること。 次のように、これらの設定のいずれかまたは両方を有効にすることができます。  
  
-   SMB 署名を有効にするには、Microsoft サポート技術情報の [記事 887429](https://support.microsoft.com/kb/887429) の手順を参照してください。  
  
-   SMB 共有フォルダーの SMB 暗号化を有効にするには、SMB サーバーで、次の PowerShell コマンドレットを実行します。  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    ここで、<*ShareName*> は SMB 共有フォルダーの名前です。  
  
必要に応じて、SMB サーバーの接続に SMB 暗号化の使用を強制する次のように選択します、**修正プログラム ルート フォルダーへのアクセスに SMB 暗号化を要求**オプション、CAU UI または、構成、 **RequireSMBEncryption。\='True'** プラグイン\-で CAU の PowerShell コマンドレットを使用して引数。  
  
> [!IMPORTANT]  
> SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用した接続に対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>手順 5. SMB サーバーで Windows ファイアウォール規則を有効にする
  
有効にする必要があります、**ファイル サーバー リモート管理\(SMB\-で\)** SMB ファイル サーバーで Windows ファイアウォールの規則。 これは、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では既定で有効です。  
  
## <a name="see-also"></a>関連項目  
  
-   [クラスター対応更新の概要](cluster-aware-updating.md)
  
-   [クラスター対応更新の Windows PowerShell コマンドレット](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [クラスター対応更新プラグインのリファレンス](https://msdn.microsoft.com/library/hh418084.aspx)  
  
