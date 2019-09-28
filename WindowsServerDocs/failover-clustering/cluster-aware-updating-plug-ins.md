---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: クラスター対応更新プラグインのしくみ
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
description: Windows Server でクラスター対応更新を使用してクラスターに更新プログラムをインストールするときに、プラグインを使用して更新プログラムを調整する方法について説明します。
ms.openlocfilehash: f6c572a397530704dd91d9c67c5c1758ccc085c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361289"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>クラスター対応更新プラグインのしくみ

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)(CAU) では、プラグインを使用して、フェールオーバークラスター内のノード間での更新プログラムのインストールを調整します。 このトピックでは、cau 用にインストールした CAU プラグ @ no__t のプラグインまたはその他のプラグインの @ no__t を使用する方法について説明します。

## <a name="BKMK_INSTALL"></a>Install @ no__t-1 をインストールします。  
CAU \(**microsoft.windowsupdateplugin**および**microsoft.hotfixplugin**@no__t と共にインストールされた既定のプラグ @ no__t は、別のプラグ @ no__t をインストールする必要があります。 CAU が self @ no__t-0updating モードで使用されている場合は、すべてのクラスターノードにプラグ @ no__t をインストールする必要があります。 CAU がリモートの @ no__t-0updating モードで使用されている場合は、リモート更新コーディネーターコンピューターにプラグ @ no__t をインストールする必要があります。 インストールするのプラグ @ no__t-0in は、各ノードに追加のインストール要件がある場合があります。  
  
にプラグイン @ no__t をインストールするには、「プラグ @ no__t-1」の手順に従います。 CAU にプラグインを手動で登録するには、プラグインがインストールされている各コンピューターで [register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) コマンドレットを実行します。  
  
## <a name="specify-a-plug-in-and-plug-in-arguments"></a>プラグ @ no__t を指定し、@ no__t 引数を指定します。  
  
### <a name="specify-a-cau-plug-in"></a>CAU プラグを指定する @ no__t-0in

Cau を使用して次のアクションを実行する場合は、CAU UI で、使用可能なプラグ @ no__t のドロップ @ no__t-1 のドロップダウンリストから、プラグイン @ no__t-0in を選択します。  
  
-   クラスターに更新プログラムを適用する  
  
-   クラスターの更新プログラムをプレビューする  
  
-   Cluster self @ no__t 更新オプションの構成  
  
既定では、CAU は**microsoft.windowsupdateplugin**のプラグ @ no__t-0in 選択します。 ただし、にインストールされ、CAU に登録されている任意のプラグ @ no__t-0in 指定できます。

> [!TIP]  
> CAU UI では、CAU が更新実行中に更新プログラムをプレビューまたは適用するために使用する、1つのプラグ @ no__t-0in CAU でのみ指定できます。 CAU の PowerShell コマンドレットを使用すると、1つ以上のプラグ @ no__t を指定できます。クラスターに複数の種類の更新プログラムをインストールする必要がある場合は、通常、1つの更新実行で複数のプラグ @ no__t を指定する方が効率的です。これは、各プラグ @ no__t に個別の更新実行を使用することではありません。 たとえば、通常は、ノードの再起動の回数が少なくなります。

次の表に示す CAU PowerShell コマンドレットを使用すると、 **– CauPluginName**パラメーターを渡すことによって、更新実行またはスキャン用に1つ以上のプラグ @ no__t を指定できます。 名前に複数のプラグ @ no__t-0in 指定するには、コンマで区切ります。 複数のプラグ @ no__t を指定した場合は、更新実行中にプラグ @ no__t が相互にどのように影響するかを制御することもできます。これを行うには、 **\-RunPluginsSerially**、 **\-StopOnPluginFailure**、および **– SeparateReboots を指定します。** パラメーター。 複数のプラグ @ no__t を使用する方法の詳細については、次の表のコマンドレットのドキュメントに記載されているリンクを参照してください。  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/add-cauclusterrole)|指定されたクラスターに自己 @ no__t-0updating 機能を提供する CAU のクラスター化された役割を追加します。|  
|[呼び出し-CauRun](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-caurun)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、更新実行で、指定したクラスターにその更新プログラムをインストールします。|  
|[Invoke-CauScan](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/invoke-causcan)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、指定したクラスターの各ノードに適用される更新プログラムの初期セットの一覧を返します。|  
|[Add-cauclusterrole](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/set-cauclusterrole)|指定したクラスターに CAU のクラスター化された役割の構成プロパティを設定します。|  
  
これらのコマンドレットを使用して CAU プラグインの @ no__t-0in パラメーターを指定しない場合、既定値はプラグ @ no__t- **microsoft.windowsupdateplugin**になります。  
  
### <a name="specify-cau-plug-in-arguments"></a>CAU プラグインの @ no__t-0in 引数を指定します  
更新実行オプションを構成するときに、1つまたは複数の名前を指定することができます *@ no__t 値*のペア \(arguments @ no__t-3 選択されたプラグを使用する @ no__t-4 です。 たとえば、CAU UI では、次のように複数の引数を指定できます。  
  
**Name1 @ no__t-1Value1;Name2 @ no__t-2Value2;Name3 @ no__t-3Value3**  
  
これらの*名前 @ no__t 値*のペアは、指定したのプラグ @ no__t-2in 意味がある必要があります。 一部のプラグ @ no__t では、引数は省略可能です。  
  
CAU プラグインの @ no__t-0in 引数の構文は、次の一般的な規則に従います。  
  
-   複数の*名前 @ no__t 値の*ペアは、セミコロンで区切られます。  
  
-   値にスペースを含める場合は、次のように引用符で囲みます。**Name1 @ no__t-1 "値にスペース" を指定**します。  
  
-   *値*の正確な構文は、プラグ @ no__t によって異なります。  
  
**– CauPluginParameters**パラメーターをサポートする CAU PowerShell コマンドレットを使用して、引数に plug @ no__t を指定するには、次の形式のパラメーターを渡します。  
  
**\-CauPluginArguments @ {Name1 @ no__t-2Value1;Name2 @ no__t-3Value2;Name3 @ no__t-4Value3}**  
  
定義済みの PowerShell ハッシュテーブルを使用することもできます。 複数のプラグ @ no__t に対して plug @ no__t-0in 引数を指定するには、引数の複数のハッシュテーブルをコンマで区切って渡します。 **CauPluginName**に指定されているプラグ @ no__t-no__t の引数に、プラグ @-0in 渡します。  
  
### <a name="specify-optional-plug-in-arguments"></a>省略可能なプラグ @ no__t-0in 引数を指定します。  
CAU によってインストールされるプラグ @ no__t の \(**microsoft.windowsupdateplugin**と**microsoft.hotfixplugin**\) には、選択できる追加のオプションが用意されています。 CAU UI では、プラグ @ no__t-a の更新実行オプションを構成した後に、**追加のオプション**ページに表示されます。 CAU の PowerShell コマンドレットを使用している場合、これらのオプションは省略可能なプラグ @ no__t-0in 引数として構成されます。 詳細については、後の「 [Microsoft.WindowsUpdatePlugin の使用](#BKMK_WUP) 」および「 [Microsoft.HotfixPlugin の使用](#BKMK_HFP) 」を参照してください。  
  
## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>Windows PowerShell コマンドレットを使用してプラグ @ no__t を管理する  
  
|コマンドレット|説明|  
|----------|---------------|  
|[Register-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/get-cauplugin)|ローカルコンピューターに登録されている、1つまたは複数のソフトウェア更新プログラムのプラグイン @ no__t に関する情報を取得します。|  
|[Register-cauplugin]((https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/register-cauplugin))|ローカルコンピューター上の CAU ソフトウェア更新プラグイン @ no__t を登録します。|  
|[登録解除-Register-cauplugin](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating/unregister-cauplugin)|CAU で使用できるプラグ @ no__t の一覧から、のソフトウェア更新プラグイン @ no__t-0in 削除します。 **注:** CAU \(**microsoft.windowsupdateplugin**と**microsoft.hotfixplugin**\) と共にインストールされるプラグ @ no__t は、登録を解除できません。|  
  
## <a name="BKMK_WUP"></a>Microsoft.windowsupdateplugin の使用  

CAU の既定のプラグ @ no__t- **0In**では、次のアクションが実行されます。
- 各フェールオーバー クラスター ノード上の Windows Update エージェントと通信し、各ノードで実行されている Microsoft 製品に必要な更新プログラムを適用します。
- Windows Update または Microsoft Update から直接、または @ no__t-0premises Windows Server Update Services \( WSUS @ no__t サーバーからクラスターの更新プログラムをインストールします。
- 選択された汎用配布リリース \(GDR @ no__t-1 更新プログラムのみをインストールします。 既定では、のプラグ @ no__t-0in 重要なソフトウェア更新プログラムのみを適用します。 構成は必要ありません。 既定の構成で、重要な GDR 更新プログラムが各ノードにダウンロードされ、インストールされます。 

> [!NOTE]
> 既定で選択されている重要なソフトウェア更新プログラム以外の更新プログラムを適用するには \(for-1 の場合、オプションのプラグ @ no__t-2in パラメーターを構成できます。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="requirements"></a>必要条件

- フェールオーバークラスターとリモート更新コーディネーターコンピューター @no__t 使用する場合、@ no__t-1 を使用する場合は、CAU の要件[と cau の要件とベストプラクティス](cluster-aware-updating-requirements.md)に記載されているリモート管理に必要な構成を満たす必要があります。
- 「[Microsoft 更新プログラムを適用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_WUA)」を参照し、フェールオーバー クラスター ノードに合わせて Microsoft Update に必要な変更を加えます。
- 最適な結果を得るために、CAU ベストプラクティスアナライザー \(BPA @ no__t-1 を実行して、CAU を使用して更新プログラムを適用するようにクラスターと更新プログラムの環境が正しく構成されていることを確認することをお勧めします。 詳細については、「 [Test CAU updating readiness](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。

> [!NOTE]
> Microsoft の利用規約に同意する必要がある更新プログラムや、ユーザー操作が必要な更新プログラムは除外されるため、手動でインストールする必要があります。

### <a name="additional-options"></a>[追加オプション]

必要に応じて、次のプラグ @ no__t-0in 引数を指定して、プラグ @ no__t によって適用される更新プログラムのセットを拡張または制限することができます。
- 各ノードの重要な更新プログラムだけでなく、推奨される更新プログラムを適用するようにのプラグ @ no__t を構成するには、CAU UI の **[追加オプション]** ページで、 **[推奨される更新プログラムを受信したときと同じ方法で重要な更新プログラムを受信する]** チェックボックスをオンにします。箱.
<br>または、 **' IncludeRecommendedUpdates ' \= ' True '** プラグ @ no__t-2in 引数を構成します。
- 各クラスターノードに適用される GDR 更新プログラムの種類をフィルター処理するために、のプラグ @ no__t-0in 構成するには、 **QueryString**プラグ @ no__t-2in 引数を使用して Windows Update エージェントクエリ文字列を指定します。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="BKMK_QUERY"></a>Windows Update エージェントのクエリ文字列を構成する  
Windows Update エージェント \(WUA @ no__t-4 クエリ文字列で構成されている、既定のプラグ @ no__t-1、 **microsoft.windowsupdateplugin**のプラグ @ no__t-0in 引数を構成できます。 この手順では、WUA API を使用して、1 つまたは複数のグループの Microsoft 更新プログラムを指定して、指定した条件に基づいて各ノードに適用します。 複数の条件を組み合わせるには、論理 AND または論理 OR を使用できます。 WUA クエリ文字列は、次のように、プラグ @ no__t-0in 引数で指定します。  
  
**QueryString @ no__t-1 "Criterion1 @ no__t-2Value1 and @ no__t-3or Criterion2 @ no__t-4Value2 and @ no__t-5or..."**  
  
たとえば、**Microsoft.WindowsUpdatePlugin** では、既定の **QueryString** 引数を使用して重要な更新プログラムを自動的に選択します。この引数は、**IsInstalled**、**Type**、**IsHidden**、および **IsAssigned** の条件を使用して構築します。  
  
**QueryString @ no__t-1 "IsInstalled @ no__t-20 and Type @ no__t-3' Software ' and IsHidden @ no__t-40 and IsAssigned @ no__t-51"**  
  
**Querystring**引数を指定すると、のプラグ @ no__t-2in 構成されている既定の**querystring**の代わりに使用されます。  
  
#### <a name="example-1"></a>例 1
  
ID によって識別される特定の更新をインストールする**QueryString**引数を構成するには*f6ce46c1 @ no__t-2971c @ no__t-343f9 @ no__t-4a2aa @ no__t-5783df125f003*:  
  
**QueryString @ no__t-1 "UpdateID @ no__t-2' f6ce46c1 @ no__t-3971c @ no__t-44 3f9 @ no__t-5a2aa @ no__t-6783df125f003 ' および IsInstalled @ no__t-70"**  
  
> [!NOTE]  
> 前の例は、クラスターの @ no__t 対応更新ウィザードを使用して更新プログラムを適用する場合に有効です。 CAU UI を使用するか、 **Add @ no__t-2CauClusterRole**または**Set @ no__t-4CauClusterRole**PowerShell コマンドレットを使用して、self @ no__t-0updating オプションを構成することによって特定の更新プログラムをインストールする場合は、updateid 値を2つに設定する必要があります。単一の @ no__t-5 引用符文字:  
>   
> **QueryString @ no__t-1 "UpdateID @ no__t-2' ' f6ce46c1 @ no__t-3971c @ no__t-44 3f9 @ no__t-5a2aa @ no__t-6783df125f003 ' ' および IsInstalled @ no__t-70"**  
  
#### <a name="example-2"></a>例 2
  
ドライバーのみをインストールする **QueryString** 引数を構成するには:  
  
**QueryString @ no__t-1 "IsInstalled @ no__t-20 and Type @ no__t-3' Driver ' and IsHidden @ no__t-40"**  
  
**Microsoft.windowsupdateplugin**の既定のプラグ @ no__t のクエリ文字列の詳細については、 **IsInstalled**\) などの検索 @no__t 条件、およびクエリ文字列に含めることができる構文については、「」を参照してください。[Windows Update エージェント (WUA) API リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=223304)の検索条件について  
  
## <a name="BKMK_HFP"></a>Microsoft.hotfixplugin を使用する  
Microsoft.hotfixplugin のプラグ @ no__t-0in、Microsoft の制限付き配布 @no__t リリースを適用するために使用できます。これには、修正プログラムとも呼ばれ**ます。** また、以前は qfe @ no__t-5 と呼ばれていました。これらの更新 @no__t プログラムは、個別にダウンロードします特定の Microsoft ソフトウェアの問題。 このプラグインでは、SMB ファイル共有のルートフォルダーから更新プログラムがインストールされます。また、@ no__t-0Microsoft ドライバー、ファームウェア、BIOS の更新プログラムを適用するようにカスタマイズすることもできます。

> [!NOTE]
> 修正プログラムは、サポート技術情報の記事に記載されている Microsoft からダウンロードできる場合もありますが、@ no__t が必要な場合には、お客様にも提供されます。

### <a name="requirements"></a>必要条件

- フェールオーバークラスターとリモート更新コーディネーターコンピューター @no__t 使用する場合、@ no__t-1 を使用する場合は、CAU の要件[と cau の要件とベストプラクティス](cluster-aware-updating-requirements.md)に記載されているリモート管理に必要な構成を満たす必要があります。
- 「[Microsoft.HotfixPlugin を使用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_HF)」を参照してください。
- 最適な結果を得るために、CAU ベストプラクティスアナライザー \(BPA @ no__t モデルを実行して、CAU を使用して更新プログラムを適用するようにクラスターと更新プログラムの環境が正しく構成されていることを確認することをお勧めします。 詳細については、「 [Test CAU updating readiness](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。
- 発行元から更新プログラムを取得し、それらをコピーするか、サーバーメッセージブロックに抽出します。そのためには、SMB 2.0 以降をサポートし、すべてのクラスターノードおよびリモート更新プログラムからアクセス可能な no__t-1 ファイル共有 \( 修正プログラムルートフォルダー @ no__t-3 を @no__t します。コーディネーターコンピューター \).x がリモート @ no__t-5updating モード @ no__t で使用されている場合は44。 詳細については、後述する「 [修正プログラム ルート フォルダー構造を構成する](#BKMK_HF_ROOT) 」を参照してください。 

    > [!NOTE]
    > 既定では、このプラグ @ no__t-0in は、ファイル名拡張子が .msu、.msi、および .msp の修正プログラムのみをインストールします。

- ' **% Systemroot% \\System32 @ no__t-3WindowsPowerShell @ no__t-4v @ no__t-5Modules @ no__t-6ClusterAwareUpdating**フォルダーにある DefaultHotfixConfig ファイルをコピーします。この @no__t ファイルは、CAU ツールが置かれているコンピューターにあります。作成した修正プログラムルートフォルダーに @ no__t-7 をインストールし、修正プログラムを抽出しました。 たとえば、構成ファイルを *\\ @ no__t-2MyFileServer @ no__t-3Hotfixes @ no__t-4Root @ no__t-5*にコピーします。 

    > [!NOTE]
    > Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムをインストールするには、既定の修正プログラム構成ファイルを変更せずに使用できます。 変更が必要な場合は、高度なタスクとして構成ファイルをカスタマイズできます。 構成ファイルには、カスタム規則を含めることができます。たとえば、特定の拡張子を持つ修正プログラム ファイルの処理、特定の終了条件に関する動作の定義などです。 詳細については、このトピックの「[修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE)」を参照してください。

### <a name="configuration"></a>構成

次の設定を構成します。 詳細については、このトピックで後述するセクションのリンクを参照してください。
- 適用する更新プログラムと修正プログラムの構成ファイルが保存される、共有される修正プログラム ルート フォルダーのパス。 このパスは、CAU UI で入力するか、 **HotfixRootFolderPath @ no__t-1 @ no__t-2path >** PowerShell プラグ @ no__t-3in 引数で構成することができます。 

   > [!NOTE]
   > 修正プログラムルートフォルダーは、ローカルフォルダーパスとして指定することも、 *\\ @ no__t-2ServerName @ no__t-3Share @ no__t-4RootFolderName*という形式の UNC パスとして指定することもできます。 ドメイン @ no__t またはスタンドアロンの DFS 名前空間パスを使用できます。 ただし、修正プログラムの構成ファイルのアクセス許可をチェックする機能のプラグ @ no__t は、DFS 名前空間パスと互換性がありません。そのため、構成する場合は、CAU UI を使用するか、 **DisableAclChecks @ no__t-2' True '** プラグ @ no__t-3in 引数。
- 修正プログラムルートフォルダーをホストするサーバーの設定。このフォルダーにアクセスするための適切なアクセス許可があるかどうかを確認し、SMB 共有フォルダーからアクセスされるデータの整合性を確認するには、\(SMB 署名または SMB 暗号化 @ no__t-1 を使用します。 詳細については、「[修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」を参照してください。

### <a name="additional-options"></a>[追加オプション]

- 必要に応じて、修正プログラムのファイル共有からデータにアクセスするときに SMB 暗号化を適用するように、のプラグ @ no__t-0in 構成します。 CAU UI の **[追加オプション]** ページで、 **[修正プログラムルートフォルダーへのアクセス時に SMB 暗号化を要求]** する オプションをオンにするか、 **RequireSMBEncryption @ no__t-3' True '** PowerShell プラグ @ no__t-4in 引数を構成します。 
  > [!IMPORTANT]
  > SMB データの SMB 署名または SMB 暗号化との整合性を有効にするには、SMB サーバーで追加の構成手順を実行する必要があります。 詳細については、「 [修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」の手順 4. を参照してください。 SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用したアクセスに対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。
- 必要に応じて、修正プログラム ルート フォルダーと修正プログラムの構成ファイルに十分なアクセス許可があるかどうかに関する既定の確認を無効にします。 CAU UI で、[**修正プログラムルートフォルダーおよび構成ファイルへの管理者アクセスの確認を無効**にする] を選択するか、 **disableaclchecks @ no__t-2' True '** プラグ @ no__t-3in 引数を構成します。
- 必要に応じて、 **HotfixInstallerTimeoutMinutes @ no__t-1 @ no__t**引数を構成して、修正プログラムプラグインがを返すまでの時間を指定します。 @no__t 既定値は30分です。 \)たとえば、2時間のタイムアウト期間を指定するには、 **HotfixInstallerTimeoutMinutes @ no__t-1120**を設定します。
- 必要に応じて、 **HotfixConfigFileName \= <name>** プラグ @ no__t-3in 引数を構成して、修正プログラムルートフォルダーにある修正プログラムの構成ファイルの名前を指定します。 指定しない場合、既定の名前である DefaultHotfixConfig.xml が使用されます。
  
### <a name="BKMK_HF_ROOT"></a>修正プログラムルートフォルダー構造を構成する

修正プログラムのプラグ @ no__t を機能させるには、SMB ファイル @no__t 共有の適切な @ no__t-1defined 構造に修正プログラムを保存する必要があります。この場合、修正プログラムルートフォルダー @ no__t-3 を指定します。また、CAU UI またはを使用して、修正プログラムルートフォルダーへのパスを含む修正プログラムプラグをCAU の PowerShell コマンドレット。 このパスは、プラグ @ no__t-0in **HotfixRootFolderPath**引数として渡されます。 次の例のように、実際の更新のニーズに応じて、修正プログラム ルート フォルダーに対応するいくつかの構造からいずれかを選択できます。 この構造に従っていないファイルまたはフォルダーは無視されます。  
  
#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>例 1-すべてのクラスターノードに修正プログラムを適用するために使用されるフォルダー構造
  
修正プログラムがすべてのクラスターノードに適用されるように指定するには、修正プログラムルートフォルダーの下の**CAUHotfix @ no__t-1All**という名前のフォルダーにコピーします。 この例では、 **HotfixRootFolderPath**プラグ @ no__t-a 引数を *\\ @ No__t-4myfileserver @ No__t-5hotfixes @ No__t-6root @ no__t-7*に設定します。 **CAUHotfix @ no__t-1all**フォルダーには、拡張子が .msu、.msi、および .msp の3つの更新プログラムが含まれており、すべてのクラスターノードに適用されます。 この更新プログラム ファイル名は、説明のためにのみ使用されています。  
  
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
  
#### <a name="example-2---folder-structure-used-to-apply-certain-updates-only-to-a-specific-node"></a>例 2-特定のノードにのみ特定の更新プログラムを適用するために使用されるフォルダー構造
  
特定のノードにのみ適用する修正プログラムを指定するには、修正プログラム ルート フォルダー以下にあるノード名を持つサブフォルダーを使用します。 クラスター ノードの NetBIOS 名を使用します。たとえば、*ContosoNode1* などです。 次に、そのノードにのみ適用する更新プログラムを、このサブフォルダーに移動します。 次の例では、 **HotfixRootFolderPath**プラグ @ no__t-a 引数が *\\ @ No__t-4myfileserver @ No__t-5hotfixes @ No__t-6root @ no__t-7*に設定されています。 **CAUHotfix @ no__t-1all**フォルダー内の更新プログラムはすべてのクラスターノードに適用され、 *Node1 @ no__t-3Specific\_Update.msu*は*ContosoNode1*にのみ適用されます。  
  
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
  
#### <a name="example-3---folder-structure-used-to-apply-updates-other-than-msu-msi-and-msp-files"></a>例 3-.msu、.msi、および .msp ファイル以外の更新プログラムを適用するために使用されるフォルダー構造
  
既定では、**Microsoft.HotfixPlugin** は拡張子が .msu、.msi、または .msp の更新プログラムのみを適用します。 ただし、一部の更新プログラムは拡張子が異なり、別のインストール コマンドが必要な場合があります。 たとえば、場合によっては、拡張子が .exe のファームウェアの更新プログラムをクラスター内のノードに適用する必要があります。 修正プログラムルートフォルダーには、既定以外の特定の更新プログラムの種類をインストールする必要があることを示すサブフォルダーを構成することができます。 また、対応するフォルダーのインストール規則を構成して、修正プログラムの構成 XML ファイルで `<FolderRules>` 要素にインストール コマンドを指定する必要もあります。  
  
次の例では、 **HotfixRootFolderPath**プラグ @ no__t-a 引数が *\\ @ No__t-4myfileserver @ No__t-5hotfixes @ No__t-6root @ no__t-7*に設定されています。 一部の更新プログラムはすべてのクラスター ノードに適用されます。またファームウェアの更新プログラムの *SpecialHotfix1.exe* は、*FolderRule1* を使用して *ContosoNode1* に適用されます。 修正プログラムの構成ファイルで *ContosoNode1* を構成する場合の詳細については、このトピックの「 [修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE) 」を参照してください。  
  
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

### <a name="BKMK_CONFIG_FILE"></a>修正プログラムの構成ファイルをカスタマイズする  
修正プログラムの構成ファイルは、フェールオーバー クラスターに特定の修正プログラム ファイルの種類を **Microsoft.HotfixPlugin** でインストールする方法を制御します。 構成ファイルの XML スキーマは HotfixConfigSchema.xsd で定義されています。この xsd ファイルは、CAU ツールがインストールされているコンピューターの次のフォルダーに保存されています。  
  
**% systemroot% \\System32 @ no__t-2WindowsPowerShell @ no__t-3v 1.0 @ no__t-4Modules @ no__t-5ClusterAwareUpdating フォルダー**  
  
修正プログラムの構成ファイルをカスタマイズするには、この場所にあるサンプルの構成ファイル DefaultHotfixConfig.xml を修正プログラム ルート フォルダーにコピーし、実際のシナリオに合わせて変更します。  
  
> [!IMPORTANT]  
> Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムを適用するには、既定の修正プログラム構成ファイルを変更せずに使用できます。 修正プログラムの構成ファイルのカスタマイズは、高度な使用シナリオでのみ実行されるタスクです。  
  
修正プログラムの構成 XML ファイルは、次の 2 つのカテゴリの修正プログラムについて、既定でインストール規則と終了条件を定義しています。  
  
-   @No__t 既定では、プラグ @ no__t がインストールできる拡張子を持つ修正プログラムファイルは、、.msi、および .msp の各ファイル @ no__t からインストールできます。  
  
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
  
-   .Msi、.msu、または .msp ファイルではない修正プログラムまたはその他の更新プログラムファイル。たとえば、@ no__t-0Microsoft ドライバー、ファームウェア、BIOS の更新プログラムがありません。  
  
    それぞれの非 @ no__t-0default ファイルの種類は、@no__t 要素の `<Folder>` 要素として構成されています。 `<Folder>` 要素の name 属性は、対応する種類の更新プログラムを保存する修正プログラム ルート フォルダー内のフォルダー名と同じにする必要があります。 このフォルダーは、 **CAUHotfix @ no__t-1All**フォルダー内、またはノード @ no__t-2specific のフォルダーにあります。 たとえば、 *FolderRule1* を修正プログラム ルート フォルダー内に構成する場合、XML ファイルに次の要素を構成して、そのフォルダー内の更新プログラムについてインストール テンプレートと終了条件を定義します。  
  
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
  
### <a name="BKMK_ACL"></a>修正プログラムルートフォルダーへのアクセスを制限する  
SMB ファイル サーバーとファイル共有を構成して、 **Microsoft.HotfixPlugin**のコンテキストでのみアクセスするように修正プログラム ルート フォルダー ファイルと修正プログラムの構成ファイルをセキュリティで保護するには、いくつかの手順を実行する必要があります。 これらの手順によって、フェールオーバー クラスターのセキュリティを侵害するような方法で修正プログラム ファイルを改ざんする危険性を回避できます。  
  
一般的な手順は次のとおりです。  
  
1.  のプラグ @ no__t-0in を使用して、更新実行に使用するユーザーアカウントを特定します。  
  
2.  SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する  
  
3.  修正プログラム ルート フォルダーのアクセス許可を構成する  
  
4.  SMB データの整合性に関する設定を構成する  
  
5.  SMB サーバーで Windows ファイアウォール規則を有効にする  
  
#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>手順 1. 更新プログラムの実行に使用されるユーザーアカウントを特定するには、の修正プログラムプラグを使用します。
  
Microsoft.hotfixplugin を使用して更新実行を実行するときに、CAU でセキュリティ設定を確認するために使用されるアカウントは、次のように、リモートの @ no__t 更新モードまたは自己 @ no__t-2updating モードで CAU が使用されるかどうかによって異なります **。**  
  
-   **Remote @ no__t-1 更新モード**更新プログラムをプレビューして適用するために、クラスターの管理者特権を持つアカウント。  
  
-   **Self @ no__t-1 更新モード**CAU のクラスター化された役割の Active Directory で構成された仮想コンピューターオブジェクトの名前。 この名前は、Active Directory で CAU のクラスター化された役割用に事前設定された仮想コンピューター オブジェクトの名前か、クラスター化された役割用に CAU によって生成された名前です。 CAU によって生成された名前を取得するには、 **Get @ no__t-1CauClusterRole** cau PowerShell コマンドレットを実行します。 出力の **ResourceGroupName** は、生成された仮想コンピューター オブジェクト アカウントの名前です。  
  
#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>手順 2. SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する
  
> [!IMPORTANT]  
> 更新実行に使用するアカウントは、SMB サーバーのローカルの管理者アカウントとして追加する必要があります。 組織のセキュリティ ポリシーで、このようなアカウントを追加できない場合は、次の手順を使用して、SMB サーバーに必要なアクセス許可を持つ管理者アカウントを構成します。  
  
##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB サーバーでユーザー アカウントを構成するには  
  
1.  更新実行に使用するアカウントを Distributed COM Users グループに追加し、Power User、Server Operation、または Print Operator のいずれかに追加します。  
  
2.  アカウントに必要な WMI のアクセス許可を有効にするには、SMB サーバーで WMI 管理コンソールを開始します。 PowerShell を起動し、次のコマンドを入力します。  
  
    ```  
    wmimgmt.msc  
    ```  
  
3.  コンソールツリーで、右 @ no__t をクリックし、[ **WMI コントロール \(Local @ no__t**] をクリックして、 **[プロパティ]** をクリックします。  
  
4.  **[セキュリティ]** をクリックし、 **[ルート]** を展開します。  
  
5.  **[CIMV2]** をクリックし、 **[セキュリティ]** をクリックします。  
  
6.  更新実行に使用するアカウントを **[グループ名またはユーザー名]** リストに追加します。  
  
7.  **[メソッドの実行]** および **[リモートの有効化]** のアクセス許可を更新実行に使用するアカウントに付与します。  
  
#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>手順 3. 修正プログラム ルート フォルダーのアクセス許可を構成する
  
既定では、更新プログラムを適用しようとすると、修正プログラムプラグ @ no__t-0in は、修正プログラムルートフォルダーへのアクセスに関して NTFS ファイルシステムのアクセス許可の構成を確認します。 フォルダーのアクセス許可が適切に構成されていない場合は、の修正プログラムプラグ @ no__t を使用した更新実行が失敗する可能性があります。  
  
の修正プログラムプラグ @ no__t の既定の構成を使用する場合は、フォルダーのアクセス許可が次の要件を満たしていることを確認します。  
  
-   Users グループに読み取りアクセス許可があります。  
  
-   のプラグ @ no__t-0in .exe 拡張子の更新プログラムを適用する場合、Users グループには実行アクセス許可があります。  
  
-   特定のセキュリティプリンシパルのみが @no__t 許可されますが、書き込みまたは変更のアクセス許可を与えるには、no__t-1 を指定する必要はありません。 許可されるプリンシパルは、ローカルの Administrators グループ、SYSTEM、CREATOR OWNER、および TrustedInstaller です。 その他のアカウントまたはグループには、修正プログラム ルート フォルダーで書き込みまたは修正のアクセス許可は付与されません。  
  
必要に応じて、のプラグ @ no__t が既定で実行する上記のチェックを無効にすることができます。 2 つの方法のいずれかでこれを行うことができます。  
  
-   CAU の PowerShell コマンドレットを使用している場合は、の修正プログラムプラグイン @ no__t の**CauPluginArguments**パラメーターで、 **disableaclchecks の @ no__t-1' True '** 引数を構成します。  
  
-   CAU UI を使用している場合、更新実行オプションの構成に使用するウィザードの **[追加の更新オプション]** ページで、 **[修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする]** オプションをオンにします。  
  
ただし、多くの環境では、ベスト プラクティスとして、既定の構成を使用してこれらの確認を実行することをお勧めします。  
  
#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>手順 4. SMB データの整合性に関する設定を構成する
  
クラスターノードと SMB ファイル共有間の接続でデータの整合性を確認するには、の修正プログラムプラグ @ no__t で、smb ファイル共有の設定を SMB 署名または SMB 暗号化に対して有効にする必要があります。 多くの環境でセキュリティを強化し、パフォーマンスを向上させる SMB 暗号化は、Windows Server 2012 以降でサポートされています。 次のように、これらの設定のいずれかまたは両方を有効にすることができます。  
  
-   SMB 署名を有効にするには、Microsoft サポート技術情報の [記事 887429](https://support.microsoft.com/kb/887429) の手順を参照してください。  
  
-   Smb 共有フォルダーの SMB 暗号化を有効にするには、SMB サーバーで次の PowerShell コマンドレットを実行します。  
  
    ```PowerShell  
    Set-SmbShare <ShareName> -EncryptData $true  
    ```  
  
    ここで、<*ShareName*> は SMB 共有フォルダーの名前です。  
  
必要に応じて、SMB サーバーへの接続で smb 暗号化の使用を強制するには、CAU UI で [**修正プログラムルートフォルダーへのアクセス時に Smb 暗号化を要求**する] オプションをオンにするか、 **RequireSMBEncryption @ no__t-2' True '** プラグ @ no__ を構成します。CAU PowerShell コマンドレットを使用した t-3in 引数。  
  
> [!IMPORTANT]  
> SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用した接続に対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。  
  
#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>手順 5. SMB サーバーで Windows ファイアウォール規則を有効にする
  
SMB ファイルサーバーの Windows ファイアウォールで、**ファイルサーバーのリモート管理 \(SMB @ no__t-2in の @** ルールで有効にする必要があります。 これは、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では既定で有効になっています。  
  
## <a name="see-also"></a>関連項目  
  
-   [クラスター対応更新の概要](cluster-aware-updating.md)
  
-   [クラスター対応更新の Windows PowerShell コマンドレット](https://docs.microsoft.com/en-us/powershell/module/clusterawareupdating)  
  
-   [クラスター対応更新プラグインのリファレンス](https://msdn.microsoft.com/library/hh418084.aspx)  
  
