---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: "クラスター対応更新プラグインのしくみ"
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
ms.technology: storage-failover-clustering
description: "クラスターに更新プログラムをインストールする Windows Server のクラスター対応更新を使用する場合は、更新を調整するプラグインを使用する方法。"
ms.openlocfilehash: eb606dfbe6596ecabd35e6ac36624fab2b4436b9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>クラスター対応更新プラグインのしくみ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)(CAU) では、プラグインを使用して、フェールオーバー クラスターのノード間で更新プログラムのインストールを調整します。 このトピックでは、情報を使用して、組み込みの CAU プラグイン アドインまたはその他のプラグインのプラグインを CAU 用にインストールする方法を説明します。

## <a name="BKMK_INSTALL"></a>プラグインをインストールします。  
CAU と共にインストールされている既定のプラグイン、アドイン以外のプラグインを \ (**Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin**\) とは別にインストールする必要があります。 自己更新モードで CAU を使用する場合、プラグインをインストールしなければなりませんすべてのクラスター ノードで。 Remote\ 更新モードで CAU を使用する場合、プラグインをインストールしなければなりませんリモート Update Coordinator コンピューター上。 プラグインを各ノードで追加のインストール要件をインストールする必要があります。  
  
プラグインをインストールするにプラグインを発行元からの指示に従います。 CAU にプラグインを手動で登録するには、実行、[Register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin)プラグインがインストールされている各コンピューターでコマンドレット。  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>プラグインとプラグインを引数を指定します。  
  
### <a name="specify-a-cau-plug-in"></a>CAU プラグインを指定します。

CAU UI で選択プラグインを利用可能なプラグイン アドインのドロップダウン リストから CAU を使用して、次の操作を実行する場合。  
  
-   クラスターに更新プログラムを適用します。  
  
-   クラスターの更新プログラムのプレビュー  
  
-   クラスターの自己更新オプションを構成します。  
  
既定では、CAU はプラグインを選択**Microsoft.WindowsUpdatePlugin**します。 ただし、いずれかを指定できるプラグインがインストールされ、CAU に登録します。

> [!TIP]  
> CAU UI をプレビューまたは更新プログラムを適用、更新実行中に使用する CAU のプラグインを 1 つのみ指定できます。 CAU の PowerShell コマンドレットを使用すると、1 つまたは複数のプラグインのプラグインを指定できます。を、クラスターに複数の種類の更新プログラムをインストールする必要がある場合は 1 つの更新実行で複数のプラグインのプラグインを指定する方が効率的ではなく更新実行ごとに個別を使用してプラグインをします。 たとえばより少ないノードの再起動が通常発生します。

次の表に記載されている CAU PowerShell コマンドレットを使用するを指定できます 1 つまたは複数のプラグイン、アドイン、更新実行やスキャン用を渡すことによって、**– CauPluginName**パラメーター。 複数のプラグイン名をコンマで区切って指定できます。 複数のプラグインのプラグインを指定する場合も制御できますプラグイン、アドイン相互の影響の各更新実行中に指定することによって、**\-RunPluginsSerially**、**\-StopOnPluginFailure**、および**– SeparateReboots**パラメーター。 詳細については、複数のプラグインを使用して、次の表に、コマンドレットのドキュメントに記載されているリンクを使用します。  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Add-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole)|指定したクラスターに自己更新機能を提供する CAU のクラスター化された役割を追加します。|  
|[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)|該当する更新プログラムについてクラスター ノードのスキャンを実行し、指定したクラスター上で、更新実行のこれらの更新プログラムをインストールします。|  
|[Invoke-CauScan](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan)|該当する更新プログラムについてクラスター ノードのスキャンを実行し、指定したクラスター内の各ノードに適用される更新プログラムの初期セットの一覧を返します。|  
|[Set-CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)|指定したクラスターに CAU のクラスター化された役割の構成プロパティを設定します。|  
  
これらのコマンドレットを使用して CAU プラグインをパラメーターを指定しない場合、既定は、プラグインは**Microsoft.WindowsUpdatePlugin**します。  
  
### <a name="specify-cau-plug-in-arguments"></a>CAU プラグインを引数を指定します。  
更新実行オプションを構成するときに、1 つまたは複数を指定することができます*名前 \/値の =*ペアを使用するプラグインを選択した \(arguments\) します。 たとえば、CAU UI でことができますを指定する複数の引数とおり。  
  
**Name1\ =; Value1Name2\ =; Value2Name3\ 値 3 =**  
  
これら*名前 \/値 =*ペアは、プラグインに意味のあるである必要がありますを指定すること。 一部のプラグインの場合は、引数はオプションです。  
  
CAU プラグイン引数の構文は、これらの一般的な規則を次に示します。  
  
-   複数*名前 \/値の =*ペアは、セミコロンで区切られました。  
  
-   たとえば空白が含まれる値が引用符で囲まれた: **Name1\ ="Value with Spaces"**します。  
  
-   正確な構文*値*で、プラグインによって異なります。  
  
引数を指定するプラグインをサポートする CAU の PowerShell コマンドレットを使用して、**– CauPluginParameters**パラメーターの形式でパラメーターを渡します。  
  
**\-CauPluginArguments @{Name1\ =; Value1Name2\ =; Value2Name3\ 値 3 =}**  
  
また、定義済みの PowerShell のハッシュ テーブルを使用することができます。 複数のプラグインを引数を指定するには、プラグインをコンマで区切り、引数の複数のハッシュ テーブルを渡します。 指定されているプラグインを順序でプラグイン引数を渡す**CauPluginName**します。  
  
### <a name="specify-optional-plug-in-arguments"></a>オプションのプラグイン引数を指定します。  
CAU によってインストールされるプラグイン、アドイン \ (**Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin**\) その他のオプションを選択できます。 CAU UI で表示されます、**追加オプション**ページで、プラグインの更新実行オプションを構成した後です。 CAU の PowerShell コマンドレットを使用している場合、これらのオプションは省略可能なプラグインを引数として構成されます。 詳細については、次を参照してください。[Microsoft.WindowsUpdatePlugin の使用](#BKMK_WUP)と[Microsoft.HotfixPlugin の使用](#BKMK_HFP)このトピックで後述します。  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>プラグイン、アドインを管理する Windows PowerShell コマンドレットを使用します。  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Get-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/get-cauplugin)|1 つまたは複数のソフトウェア更新プラグインのプラグインをローカル コンピューターに登録されてに関する情報を取得します。|  
|[Register-CauPlugin]((https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin))|CAU ソフトウェア更新をローカル コンピューター上でプラグインを登録します。|  
|[Unregister-CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/unregister-cauplugin)|プラグインのプラグインを CAU で使用できるの一覧からプラグインを更新ソフトウェアを削除します。 **注:**、プラグインのプラグインを CAU と共にインストールされる \ (**Microsoft.WindowsUpdatePlugin**と**Microsoft.HotfixPlugin**\) 登録を解除することはできません。|  
  
## <a name="BKMK_WUP"></a>Microsoft.WindowsUpdatePlugin の使用  

既定値、CAU のプラグインを**Microsoft.WindowsUpdatePlugin**、次の操作を実行します。
- 各ノードで実行されている Microsoft 製品の必要な更新プログラムを適用する各フェールオーバー クラスター ノードで Windows Update エージェントと通信します。
- Windows Update や Microsoft Update から直接または on\ 内部設置型 Windows Server Update Services \(WSUS\) サーバーからは、クラスター更新プログラムをインストールします。
- インストールのみ選択すると、一般配布 \(GDR\) 更新プログラムをリリースします。 既定では、プラグインを重要なソフトウェアの更新のみを適用します。 構成する必要はありません。 既定の構成は、ダウンロードされ、各ノードで重要な GDR 更新プログラムをインストールします。 

> [!NOTE]
> 既定で選択されている重要なソフトウェアの更新以外の更新を適用する \ (たとえば、ドライバー updates\) は省略可能なプラグインをパラメーターを構成することができます。 詳細については、次を参照してください。[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)します。

### <a name="requirements"></a>要件

- CAU の要件を満たす必要があります、フェールオーバー クラスターとリモート更新コーディネーター コンピューター \(if used\) とリモート管理に必要な構成に示されている[要件とベスト プラクティス CAU の](cluster-aware-updating-requirements.md)します。
- レビュー [Microsoft 更新プログラムを適用するための推奨事項](cluster-aware-updating-requirements.md#BKMK_BP_WUA)、フェールオーバー クラスター ノード用の Microsoft Update の構成に必要な変更を行います。
- 最良の結果を CAU を使用して更新プログラムを適用するクラスターと更新プログラムの環境が正しく構成されていることを確認する CAU ベスト プラクティス アナライザー \(BPA\) を実行することをお勧めします。 詳細については、次を参照してください。[テスト CAU の更新の準備](cluster-aware-updating-requirements.md#BKMK_BPA)します。

> [!NOTE]
> マイクロソフト ライセンス条項の同意またはユーザーの操作が必要な更新プログラムが除外され、手動でインストールする必要があります。

### <a name="additional-options"></a>その他のオプション

必要に応じて、次でプラグイン引数を補強したり、プラグインでは、適用される更新のセットを制限を指定できます。
- 各ノードで、CAU UI で重要な更新プログラムだけでなく、推奨される更新プログラムを適用するプラグインを構成する、**追加オプション**] ページで、[、**推奨される更新プログラムは重要な更新プログラムを受け取っている同じように通知**チェック ボックスをオンします。
<br>また、構成、**'IncludeRecommendedUpdates' \ = 'True'**プラグインの引数。
- を各クラスター ノードに適用する GDR 更新プログラムの種類をフィルター処理するプラグインを構成するには、Windows Update Agent クエリ文字列を使用して、を指定、**QueryString**プラグインの引数。 詳細については、次を参照してください。[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)します。

### <a name="BKMK_QUERY"></a>Windows Update Agent クエリ文字列を構成します。  
プラグインを既定のプラグインを引数を構成する**Microsoft.WindowsUpdatePlugin**、Windows Update エージェント \(WUA\) クエリ文字列で構成されます。 この命令では、WUA API を使用して、指定した条件に基づいて、各ノードに適用する Microsoft 更新プログラムの 1 つまたは複数のグループを識別します。 論理 AND または論理 OR を使用して、複数の条件を組み合わせることができます。 WUA クエリ文字列は、次のようにプラグインを引数で指定されます。  
  
**QueryString\ ="Criterion1\ = Value1 and\/または Criterion2\ = Value2 and\/... または"**  
  
たとえば、**Microsoft.WindowsUpdatePlugin**、既定値を使用して、重要な更新プログラムを自動的に選択**QueryString**引数を使用して作成されますが、**IsInstalled**、**種類**、**IsHidden**、および**IsAssigned**条件。  
  
**QueryString\ ="IsInstalled\ = 0 および Type\ 'ソフトウェア' と IsHidden\ = = 0 および IsAssigned\ = 1"**  
  
指定した場合、**クエリ文字列**引数、既定値の代わりに使用されます**QueryString**でプラグインに対して構成されています。  
  
#### <a name="example-1"></a>例 1
  
構成するのには**QueryString** ID によって識別される特定の更新プログラムをインストールする引数*f6ce46c1\-971c\-43f9\-a2aa\-783df125f003*:  
  
**QueryString\ ="UpdateID\ ='f6ce46c1\-971c\-43f9\-a2aa\-783df125f003' と IsInstalled\ = 0"**  
  
> [!NOTE]  
> 上記の例は、Cluster\ 対応の更新ウィザードを使用して更新プログラムを適用する有効です。 CAU UI での自己更新オプションを構成することによって、またはを使用して、特定の更新プログラムをインストールするかどうか、**アドオン CauClusterRole**または**になって CauClusterRole**PowerShell コマンドレットでは、シングル引用符を 2 文字 UpdateID 値を指定する必要があります。  
>   
> **QueryString\ ="UpdateID\ = 'f6ce46c1\-971c\-43f9\-a2aa\-783df125f003' と IsInstalled\ = 0"**  
  
#### <a name="example-2"></a>例 2
  
構成するのには**QueryString**ドライバーのみをインストールする引数。  
  
**QueryString\ ="IsInstalled\ = 0 および Type\「ドライバー」と IsHidden\ = = 0"**  
  
プラグインを既定のクエリ文字列の詳細については**Microsoft.WindowsUpdatePlugin**、検索条件 \ (など**IsInstalled**\)、および、クエリ文字列に含めることができる構文で検索条件に関するセクションを参照してください、[Windows Update エージェント (WUA) API リファレンス](http://go.microsoft.com/fwlink/p/?LinkId=223304)します。  
  
## <a name="BKMK_HFP"></a>Microsoft.HotfixPlugin を使用します。  
プラグインを**Microsoft.HotfixPlugin** Microsoft の限定配布リリース \(LDR\) 更新プログラムを適用するために使用できる \ (修正プログラムとも呼ばれるおよび QFEs\ と呼ばれていました) をダウンロードすることできません個別に特定の Microsoft ソフトウェアの問題に対処します。 プラグインのルート フォルダーに SMB ファイル共有から更新プログラムをインストールし、Microsoft 以外のドライバー、ファームウェア、および BIOS の更新プログラムを適用するカスタマイズすることもします。

> [!NOTE]
> 修正プログラムは、Microsoft サポート技術情報の記事でのダウンロードの利用可能な場合がありますが、as\ 必要な場合にユーザーにも提供されています。

### <a name="requirements"></a>要件

- CAU の要件を満たす必要があります、フェールオーバー クラスターとリモート更新コーディネーター コンピューター \(if used\) とリモート管理に必要な構成に示されている[要件とベスト プラクティス CAU の](cluster-aware-updating-requirements.md)します。
- レビュー [Microsoft.HotfixPlugin の使用に関する推奨事項](cluster-aware-updating-requirements.md#BKMK_BP_HF)します。
- 最良の結果を CAU を使用して更新プログラムを適用するクラスターと更新プログラムの環境が正しく構成されていることを確認する CAU ベスト プラクティス アナライザー \(BPA\) モデルを実行することをお勧めします。 詳細については、次を参照してください。[テスト CAU の更新の準備](cluster-aware-updating-requirements.md#BKMK_BPA)します。
- 、発行元から更新プログラムの入手し、それらをコピーまたはサーバー メッセージ ブロック \(SMB\) ファイル共有に展開 \ (修正プログラム ルート folder\) をサポートするには、少なくとも SMB 2.0 とは、すべてのクラスター ノードおよびリモート更新コーディネーター コンピューターによってアクセス可能な \ (remote\ 更新 mode\ で CAU を使用) 場合。 詳細については、次を参照してください。[修正プログラム ルート フォルダー構造を構成する](#BKMK_HF_ROOT)このトピックで後述します。 

    > [!NOTE]
    > 既定では、このプラグインをインストールのみ修正プログラム、次のファイル名拡張子を持つ: .msu、.msi、および .msp します。

- DefaultHotfixConfig.xml ファイルをコピー \ (で提供されているが、**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating** CAU ツールはどこに installed\ コンピューター上のフォルダー) に作成した修正プログラム ルート フォルダーにある修正プログラムを抽出します。 たとえば、構成ファイルのコピー *\\\MyFileServer\\Hotfixes\\Root\\*します。 

    > [!NOTE]
    > Microsoft およびその他の更新プログラムによって提供されるほとんどの修正プログラムをインストールするには、変更せず、既定の修正プログラム構成ファイルを使用できます。 自分のシナリオで必要とする場合は、高度なタスクとして構成ファイルをカスタマイズできます。 構成ファイルは、特定の拡張子を持つ修正プログラム ファイルを処理するか、特定の終了条件に関する動作の定義、カスタムの規則を含めることができます。 詳細については、次を参照してください。[修正プログラム構成ファイルをカスタマイズ](#BKMK_CONFIG_FILE)このトピックで後述します。

### <a name="configuration"></a>構成

次の設定を構成します。 詳細については、このトピックの後半のセクションへのリンクを参照してください。
- 適用する更新プログラムに含まれている共有される修正プログラム ルート フォルダーへのパスには、修正プログラム構成ファイルが含まれています。 CAU UI でこのパスを入力するか、または構成、**HotfixRootFolderPath\ = \ < パス >** PowerShell プラグインの引数。 

   > [!NOTE]
   > ローカル フォルダーのパス、または形式の UNC パスとして、修正プログラム ルート フォルダーを指定することができます*\\\ServerName\\Share\\RootFolderName*します。 \Servername ベースまたはスタンドアロン DFS Namespace パスを使用できます。 ただし、1 つを構成する場合のチェックを無効にする必要がありますので、修正プログラム構成ファイルのアクセス許可に、DFS Namespace パスと互換性がありませんを確認するプラグインを機能アクセス許可、CAU UI を使用するか、構成することによって、**DisableAclChecks\ = 'True'**プラグインの引数。
- 共有フォルダーのフォルダーにアクセスし、SMB からアクセスされるデータの整合性を確保するには、適切なアクセス許可を確認する修正プログラム ルート フォルダーをホストしているサーバー上の設定 \ (SMB 署名または SMB Encryption\)。 詳細については、次を参照してください。[修正プログラム ルート フォルダーへのアクセスを制限](#BKMK_ACL)します。

### <a name="additional-options"></a>その他のオプション

- 必要に応じて、修正プログラム ファイル共有からデータにアクセスするときに SMB 暗号化が適用されるようにプラグインを構成します。 CAU UI で上、**追加オプション**] ページで、[、**修正プログラム ルート フォルダーへのアクセスに SMB 暗号化を要求する**オプション、または構成、**RequireSMBEncryption\ = 'True'** PowerShell プラグインを引数。 
  > [!IMPORTANT]
  > SMB 署名または SMB 暗号化の SMB データの整合性を有効にする、SMB サーバーで、追加の構成手順を実行する必要があります。 詳細については、手順 4. を参照してください。[修正プログラム ルート フォルダーへのアクセスを制限](#BKMK_ACL)します。 オプションを選択した場合は、SMB 暗号化を使用して、修正プログラム ルート フォルダーに適用するが構成されていないアクセスの SMB 暗号化を使用して、更新実行は失敗します。
- 必要に応じて、修正プログラム ルート フォルダーと修正プログラム構成ファイルのための十分なアクセス許可の既定の確認を無効にします。 CAU UI で選択**修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする**、または構成、**DisableAclChecks\ = 'True'**プラグインを引数。
- 必要に応じて、構成、**HotfixInstallerTimeoutMinutes\ =<Integer>**修正プログラムのインストーラー プロセスから戻るため、修正プログラム プラグインが待機する時間を指定する引数です。 \ (既定では 30 分。\) などを 2 時間のタイムアウト時間を指定するには、次のように設定します。**HotfixInstallerTimeoutMinutes\ = 120**します。
- 必要に応じて、構成、**HotfixConfigFileName \ = <name>**プラグインを引数に修正プログラム ルート フォルダーに配置されている修正プログラム構成ファイルの名前を指定します。 指定しない場合、既定の名前 DefaultHotfixConfig.xml が使用されます。
  
### <a name="BKMK_HF_ROOT"></a>修正プログラム ルート フォルダー構造を構成します。

修正プログラム プラグインをするには、修正プログラム格納する必要が、SMB ファイル共有されません。これで定義された構造体で \ (修正プログラム ルート folder\) と修正プログラム ルート フォルダーへのパスと、CAU UI または CAU の PowerShell コマンドレットを使用して、修正プログラム プラグインを構成する必要があります。 このパスは、プラグインとしてに渡される、**HotfixRootFolderPath**引数。 次の例に示すように、更新のニーズに応じた、修正プログラム ルート フォルダーのいくつかの構造のいずれかを選択できます。 ファイルまたはフォルダー構造に従っていないは無視されます。  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>例 1 - フォルダー構造のすべてのクラスター ノードに修正プログラムを適用するために使用
  
すべてのクラスター ノードに修正プログラムが適用されることを指定するという名前のフォルダーにコピー **CAUHotfix\_All**修正プログラム ルート フォルダーの下にあります。 この例では、**HotfixRootFolderPath**プラグインを引数に設定されて*\\\MyFileServer\\Hotfixes\\Root\\*します。 **CAUHotfix\_All**フォルダーには、拡張子が .msu、.msi、および .msp のすべてのクラスター ノードに適用されるこれらの更新プログラムが含まれています。 更新プログラムのファイル名は、図目的専用です。  
  
> [!NOTE]  
> この例と次の例としての必要な場所に修正プログラム ルート フォルダーに修正プログラム構成ファイル DefaultHotfixConfig.xml 既定の名前が表示されます。  
  
```
\\MyFileServer\Hotfixes\Root\   
   DefaultHotfixConfig.xml  
   CAUHotfix_All\   
      Update1.msu   
      Update2.msi   
      Update3.msp  
      ...  
```  
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>例 2 - フォルダー構造が特定のノードにのみ特定の更新プログラムを適用するために使用
  
特定のノードにのみ適用される修正プログラムを指定するには、ノードの名前と修正プログラム ルート フォルダーの下のサブフォルダーを使用します。 たとえば、クラスター ノードの NetBIOS 名を使用して*ContosoNode1*します。 次に、このサブフォルダーに、このノードにのみ適用される更新プログラムを移動します。 次の例では、**HotfixRootFolderPath**プラグインを引数に設定されて*\\\MyFileServer\\Hotfixes\\Root\\*します。 内の更新プログラム、**CAUHotfix\_All**フォルダーがすべてのクラスター ノードに適用されると*Node1\_Specific\_Update.msu*にのみ適用されます*ContosoNode1*します。  
  
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
  
既定では、**Microsoft.HotfixPlugin**のみ拡張子が .msu、.msi、または .msp の更新プログラムを適用します。 ただし、特定の更新プログラムは、別の拡張機能があるし、別のインストール コマンドを必要とします。 たとえば、クラスター内のノードに、拡張子が .exe のファームウェアの更新プログラムを適用する必要があります。 特定を示すサブフォルダーと修正プログラム ルート フォルダーを構成することができます、既定以外の更新プログラムの種類をインストールする必要があります。 インストール コマンドを指定する対応するフォルダーのインストール規則を構成する必要がありますも、`<FolderRules>`、修正プログラム構成 XML ファイル内の要素。  
  
次の例では、**HotfixRootFolderPath**プラグインを引数に設定されて*\\\MyFileServer\\Hotfixes\\Root\\*します。 複数の更新プログラムがすべてのクラスター ノードとファームウェアの更新プログラムに適用される*SpecialHotfix1.exe*に適用される*ContosoNode1*を使用して*FolderRule1*します。 構成する方法について*FolderRule1*、修正プログラム構成ファイルで、次を参照してください。[修正プログラム構成ファイルをカスタマイズ](#BKMK_CONFIG_FILE)このトピックで後述します。  
  
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
修正プログラムの構成ファイルのどのコントロール**Microsoft.HotfixPlugin**フェールオーバー クラスターに特定の修正プログラム ファイルの種類をインストールします。 構成ファイルの XML スキーマは HotfixConfigSchema.xsd、CAU ツールがインストールされているコンピューターで、次のフォルダーにあるで定義されています。  
  
**%systemroot%\\System32\\WindowsPowerShell\\v1.0\\Modules\\ClusterAwareUpdating フォルダー**  
  
修正プログラム構成ファイルをカスタマイズするには、サンプルの構成ファイル DefaultHotfixConfig.xml をこの場所から修正プログラム ルート フォルダーにコピーし、シナリオに合った適切な変更を加えます。  
  
> [!IMPORTANT]  
> Microsoft およびその他の更新プログラムによって提供されるほとんどの修正プログラムを適用するには、変更せず、既定の修正プログラム構成ファイルを使用できます。 修正プログラム構成ファイルのカスタマイズは、高度な使用シナリオでのみ作業です。  
  
既定では、修正プログラム構成 XML ファイルは、インストール規則と修正プログラムの次の 2 つのカテゴリの終了条件を定義します。  
  
-   プラグインを既定でインストールできる拡張子を持つ修正プログラム ファイル \ (.msu、.msi、および .msp files \)。  
  
    として定義される`<ExtensionRules>`内の要素、`<DefaultRules>`要素です。 いずれかを使用する必要がある`<Extension>`既定のサポートされるファイルの種類の各要素です。 一般的な XML 構造は次のとおりです。  
  
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
  
    特定の更新の種類を環境内のすべてのクラスター ノードに適用する場合を定義できます追加`<Extension>`要素です。  
  
-   修正プログラムまたは .msi、.msu、または .msp ファイルではない他の更新ファイルでは、たとえば、Microsoft 以外のドライバー、ファームウェア、および BIOS を更新します。  
  
    既定以外の各ファイルの種類として構成されている、`<Folder>`内の要素、`<FolderRules>`要素です。 Name 属性、`<Folder>`要素は、対応する種類の更新プログラムにが含まれている修正プログラム ルート フォルダー内のフォルダーの名前と同じである必要があります。 フォルダーを使用できます、**CAUHotfix\_All**フォルダーまたは node\ 固有のフォルダーにします。 たとえば場合、*FolderRule1*はインストール テンプレートを定義し、そのフォルダーにある更新プログラムの条件を終了する XML ファイルで次の要素を構成する修正プログラム ルート フォルダーに構成されています。  
  
    ```xml  
    <FolderRules>  
          <Folder name="FolderRule1">  
            <!-- Template and ExitConditions elements for installation of updates in FolderRule1 follow -->  
             ...  
          </Folder>  
          ...  
    </FolderRules>  
    ```  
  
次の表に、説明、`<Template>`属性と使用できる`<ExitConditions>`サブ要素です。  
  
|`<Template>` 属性|説明|  
|--------------------------|---------------|  
|`path`|定義されているファイルの種類のインストール プログラムへの完全パス、`<Extension name>`属性です。<br /><br />修正プログラム ルート フォルダー構造にある更新プログラム ファイルへのパスを指定するには、使用`$update$`します。|  
|`parameters`|指定されているプログラムの必須およびオプションのパラメーターの文字列`path`します。<br /><br />修正プログラム ルート フォルダー構造にある更新プログラム ファイルへのパスのパラメーターを指定するには、使用`$update$`します。|  
  
|`<ExitConditions>` サブ要素|説明|  
|---------------------------------|---------------|  
|`<Success>`|指定した更新プログラムが成功を示す終了コードを 1 つまたは複数を定義します。 これは、必須のサブ要素です。|  
|`<Success_RebootRequired>`|必要に応じて、指定した更新プログラムが成功し、ノードを再起動する必要がありますを示す終了コードを 1 つまたは複数を定義します。 <br>**注:**、必要に応じて、`<Folder>`要素を含めることができます、`alwaysReboot`属性です。 この属性を設定すると、ことを示している場合、このルールによってインストールされる修正プログラムで定義されている終了コードのいずれかを返します`<Success>`、として解釈されます、`<Success_RebootRequired>`終了条件。|  
|`<Fail_RebootRequired>`|必要に応じて指定した更新に失敗し、ノードを再起動する必要がありますを示す終了コードを 1 つまたは複数を定義します。|  
|`<AlreadyInstalled>`|必要に応じてが既にインストールされているために、指定した更新プログラムが適用されていないことを示す終了コードを 1 つまたは複数を定義します。|  
|`<NotApplicable>`|必要に応じて、クラスター ノードには適用されないために、指定した更新プログラムが適用されていないことを示す終了コードを 1 つまたは複数を定義します。|  
  
> [!IMPORTANT]  
> 終了で明示的に定義されていないコード`<ExitConditions>`更新に失敗し、ノードは再起動せず解釈されます。  
  
### <a name="BKMK_ACL"></a>修正プログラム ルート フォルダーへのアクセスを制限します。  
修正プログラム ルート フォルダー ファイルと修正プログラム構成ファイルのコンテキストでのみアクセスをセキュリティで保護する SMB ファイル サーバーとファイル共有を構成するいくつかの手順を実行する必要があります**Microsoft.HotfixPlugin**します。 次の手順は、フェールオーバー クラスターを損なう可能性があるように修正プログラム ファイルを改ざんを防ぐためのいくつかの機能を有効にします。  
  
一般的な手順は次のとおりです。  
  
1.  プラグインを使用して更新実行に使用するユーザー アカウントを指定します。  
  
2.  SMB ファイル サーバーで必要なグループにこのユーザー アカウントを構成します。  
  
3.  修正プログラム ルート フォルダーにアクセスするアクセス許可を構成します。  
  
4.  SMB データの整合性の設定を構成します。  
  
5.  SMB サーバーで Windows ファイアウォール ルールを有効にします。  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>手順 1 です。 修正プログラム プラグインを使用して更新実行に使用するユーザー アカウントを指定します。
  
アカウントを使用して更新実行の実行中にセキュリティ設定を確認する CAU で使用されている**Microsoft.HotfixPlugin**かどうか CAU で使用 remote\ 更新モードまたは自己更新モードでは、次のように異なります。  
  
-   **Remote\ 更新モード**をプレビューし、更新プログラムを適用するようにクラスターで管理者特権を持つアカウントです。  
  
-   **自己更新モード**クラスター化された役割を CAU の Active Directory で構成されている仮想コンピューター オブジェクトの名前。 これは、Active Directory で CAU のクラスター化された役割の事前登録された仮想コンピューター オブジェクトの名前またはクラスター化された役割用に CAU によって生成された名前です。 名前を取得するの CAU によって生成された場合、実行、**Get\ CauClusterRole** CAU PowerShell コマンドレット。 出力では、**ResourceGroupName**は、生成された仮想コンピューター オブジェクト アカウントの名前です。  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>手順 2 です。 SMB ファイル サーバーで必要なグループにこのユーザー アカウントを構成します。
  
> [!IMPORTANT]  
> Updating run を実行、SMB サーバーでローカル管理者アカウントとして使用するアカウントを追加する必要があります。 これは、組織内のセキュリティ ポリシーのためには許可されていない場合、は、次の手順を使用して、SMB サーバーで必要なアクセス許可を持つこのアカウントを構成します。  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB サーバーでユーザー アカウントを構成するには  
  
1.  Updating run を実行し、次のグループのいずれかに Distributed COM Users グループに使用するアカウントを追加: Power User、Server Operation、または Print Operator します。  
  
2.  アカウントのために必要な WMI アクセス許可を有効にするには、SMB サーバーで WMI 管理コンソールを開始します。 PowerShell を起動し、次のコマンドを入力します。  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  コンソール ツリーで、右クリック**WMI コントロール \(Local\)**、] をクリックし、**プロパティ**します。  
  
4.  をクリックして**セキュリティ**、し、展開**ルート**します。  
  
5.  をクリックして**CIMV2**、] をクリックし、**セキュリティ**します。  
  
6.  Updating run を実行するのに使用するアカウントを追加、**グループ名またはユーザー名**一覧します。  
  
7.  付与、**メソッドの実行**と**リモートの有効化**更新実行に使用するアカウントへのアクセス許可。  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>手順 3 です。 修正プログラム ルート フォルダーにアクセスするアクセス許可を構成します。
  
既定では、更新プログラムを適用しようとしたときに、修正プログラム プラグインは修正プログラム ルート フォルダーへのアクセスは、NTFS ファイル システムのアクセス許可の構成を確認します。 フォルダーのアクセス許可が正しく構成されていない場合、更新実行、修正プログラム プラグインを使用してが失敗します。  
  
プラグインの修正プログラムの既定の構成を使用する場合は、フォルダーのアクセス許可が、次の要件を満たしていることを確認します。  
  
-   Users グループには読み取りアクセス許可を指定します。  
  
-   プラグインには拡張子 .exe が付いて更新プログラムに適用される場合は、Users グループは、実行権限を持っています。  
  
-   特定のセキュリティ プリンシパルが許可されている \ (ではない required\) に書き込みまたはアクセス許可を変更します。 許可されるプリンシパルは、ローカル Administrators グループ、SYSTEM、CREATOR OWNER、および TrustedInstaller です。 その他のアカウントまたはグループは、書き込みまたは修正プログラム ルート フォルダーに対するアクセス許可を変更するのには許可されません。  
  
必要に応じて、プラグインを既定で実行する上記の確認を無効にすることができます。 2 つの方法のいずれかでこれを行うことができます。  
  
-   CAU の PowerShell コマンドレットを使用している場合は、構成、**DisableAclChecks\ = 'True'**の引数、**CauPluginArguments**修正プログラム プラグインをパラメーター。  
  
-   CAU UI を使用している場合は、選択、**修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする**] オプションを選択、**追加の更新オプション**更新実行オプションを構成するために使用するウィザードのページです。  
  
ただし、多くの環境でのベスト プラクティスとしては、これらのチェックを強制するのには、既定の構成を使用することを勧めします。  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>手順 4 です。 SMB データの整合性の設定を構成します。
  
クラスター ノードと SMB ファイル共有間の接続でデータの整合性を確認するには、修正プログラム プラグインは、SMB 署名または SMB 暗号化の SMB ファイル共有上の設定を有効にすることが必要です。 セキュリティを強化し、多くの環境でパフォーマンスの向上、SMB 暗号化は、Windows Server 2012 以降でサポートされています。 できますを有効にした、これらの設定は、どちらも次のようにします。  
  
-   SMB 署名を有効にする」の手順を参照してください、[記事 887429](http://support.microsoft.com/kb/887429)、Microsoft サポート技術情報でします。  
  
-   SMB 共有フォルダーの SMB 暗号化を有効にするには、SMB サーバーで、次の PowerShell コマンドレットを実行します。  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    ここで <*ShareName*> は SMB 共有フォルダーの名前です。  
  
必要に応じて、SMB サーバーへの接続に SMB 暗号化の使用を強制する] を選択、**修正プログラム ルート フォルダーへのアクセスに SMB 暗号化を要求する**、CAU UI でオプション、または構成、**RequireSMBEncryption\ = 'True'** CAU PowerShell コマンドレットを使用してプラグインを引数。  
  
> [!IMPORTANT]  
> オプションを選択した場合は、SMB 暗号化を使用して、修正プログラム ルート フォルダーに適用するが構成されていない SMB 暗号化を使用する接続に対して、更新実行は失敗します。  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>手順 5 です。 SMB サーバーで Windows ファイアウォール ルールを有効にします。
  
有効にする必要があります、**ファイル サーバーのリモート管理 \(SMB\-in\)** SMB ファイル サーバーで Windows ファイアウォールの規則。 これは、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では既定で有効です。  
  
## <a name="see-also"></a>参照してください。  
  
-   [クラスター対応更新の概要](cluster-aware-updating.md)
  
-   [クラスター対応更新の Windows PowerShell コマンドレット](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating)  
  
-   [クラスター対応更新プラグインのリファレンス](http://msdn.microsoft.com/library/hh418084.aspx)  
  
