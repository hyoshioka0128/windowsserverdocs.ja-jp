---
ms.assetid: d44d4430-41e2-483a-9685-92610cdef32a
title: クラスター対応更新プラグインのしくみ
description: Windows Server でクラスター対応更新を使用してクラスターに更新プログラムをインストールするときに、プラグインを使用して更新プログラムを調整する方法について説明します。
ms.topic: article
ms.prod: windows-server
manager: lizross
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
ms.technology: storage-failover-clustering
ms.openlocfilehash: ac09163eb40045289a68287aa3eace20ff714d09
ms.sourcegitcommit: 145cf75f89f4e7460e737861b7407b5cee7c6645
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87409582"
---
# <a name="how-cluster-aware-updating-plug-ins-work"></a>クラスター対応更新プラグインのしくみ

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)(CAU) では、プラグインを使用して、フェールオーバークラスター内のノード間での更新プログラムのインストールを調整します。 このトピックでは、CAU 用にインストールされた組み込みの \- cau プラグイン \- またはその他のプラグインの使用方法について説明し \- ます。

## <a name="install-a-plug-in"></a><a name="BKMK_INSTALL"></a>プラグインをインストールする \-
\-CAU microsoft.windowsupdateplugin と microsoft.hotfixplugin と共にインストールされる既定のプラグイン以外のプラグインは、 \- 個別にインストールする \( **Microsoft.WindowsUpdatePlugin** **Microsoft.HotfixPlugin** \) 必要があります。 自己更新モードで CAU を使用する場合は、 \- \- すべてのクラスターノードにプラグインをインストールする必要があります。 CAU がリモート更新モードで使用されている場合は、 \- \- リモート更新コーディネーターコンピューターにプラグインがインストールされている必要があります。 インストールするプラグインには、 \- 各ノードで追加のインストール要件がある場合があります。

プラグインをインストールするには \- 、プラグインの発行元の指示に従い \- ます。 CAU にプラグインを手動で登録するには、 \- プラグインがインストールされている各コンピューターで[register-cauplugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin)コマンドレットを実行し \- ます。

## <a name="specify-a-plug-in-and-plug-in-arguments"></a>プラグイン引数と \- プラグイン引数の \- 指定

### <a name="specify-a-cau-plug-in"></a>CAU プラグインの指定 \-

Cau を使用して次の操作を実行する場合は、CAU UI で、 \- 使用可能なプラグインのドロップダウンリストからプラグインを選択し \- \- ます。

-   クラスターに更新プログラムを適用する

-   クラスターの更新プログラムをプレビューする

-   クラスターの自己 \- 更新オプションを構成する

既定では、CAU は Microsoft.windowsupdateplugin プラグインを選択し \- ます。 **Microsoft.WindowsUpdatePlugin** ただし、インストールされ、CAU に登録されている任意のプラグインを指定でき \- ます。

> [!TIP]
> CAU UI では、 \- 更新実行中に更新プログラムをプレビューまたは適用するために、cau が使用するプラグインを1つだけ指定できます。 CAU PowerShell コマンドレットを使用すると、1つまたは複数のプラグインを指定でき \- ます。クラスターに複数の種類の更新プログラムをインストールする必要がある場合は、 \- プラグインごとに個別の更新実行を使用するのではなく、1つの更新実行で複数のプラグインを指定する方が効率的です \- 。 たとえば、通常は、ノードの再起動の回数が少なくなります。

次の表に示す CAU PowerShell コマンドレットを使用すると、 \- **-CauPluginName**パラメーターを渡すことによって、更新実行またはスキャン用のプラグインを1つ以上指定できます。 複数のプラグイン名を \- コンマで区切って指定できます。 複数のプラグインを指定する場合は、 \- \- ** \- RunPluginsSerially**、 ** \- stoponpluginfailure**、および **– SeparateReboots**パラメーターを指定することによって、更新実行中にプラグインが相互にどのように影響するかを制御することもできます。 複数のプラグインの使用方法の詳細については \- 、次の表のコマンドレットのドキュメントに記載されているリンクを使用してください。

|コマンドレット|説明|
|----------|---------------|
|[Add-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/add-cauclusterrole)|指定されたクラスターに自己更新機能を提供する CAU のクラスター化された役割を追加し \- ます。|
|[Invoke-CauRun](https://docs.microsoft.com/powershell/module/clusterawareupdating/invoke-caurun)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、更新実行で、指定したクラスターにその更新プログラムをインストールします。|
|[Invoke-CauScan](https://docs.microsoft.com/powershell/module/clusterawareupdating/invoke-causcan)|適用可能な更新プログラムについてクラスター ノードのスキャンを実行し、指定したクラスターの各ノードに適用される更新プログラムの初期セットの一覧を返します。|
|[Set-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/set-cauclusterrole)|指定したクラスターに CAU のクラスター化された役割の構成プロパティを設定します。|

これらのコマンドレットを使用して CAU プラグインパラメーターを指定しない場合 \- 、既定値は \- **microsoft.windowsupdateplugin**にあります。

### <a name="specify-cau-plug-in-arguments"></a>CAU プラグイン \- 引数の指定
更新実行オプションを構成するときに、 * \= * \( 選択し \) たプラグインが使用する1つまたは複数の名前と値のペアの引数を指定でき \- ます。 たとえば、CAU UI では、次のように複数の引数を指定できます。

**Name1 \= Value1;Name2 \= Value2;Name3 \= Value3**

これらの*名前と \= 値*のペアは、指定するプラグインにとって意味のあるものである必要があり \- ます。 一部のプラグインで \- は、引数は省略可能です。

CAU プラグイン引数の構文は、次 \- の一般的な規則に従います。

-   複数の*名前と \= 値*のペアは、セミコロンで区切られます。

-   空白が含まれている値は、引用符で囲みます (例: **Name1 \= "Value with spaces"**)。

-   *値*の正確な構文は、プラグインによって異なり \- ます。

\- **– CauPluginParameters**パラメーターをサポートする CAU PowerShell コマンドレットを使用してプラグイン引数を指定するには、次の形式のパラメーターを渡します。

**\-CauPluginArguments @ {Name1 \= Value1;Name2 \= Value2;Name3 \= Value3}**

定義済みの PowerShell ハッシュテーブルを使用することもできます。 複数のプラグインに対してプラグイン引数を指定するに \- \- は、引数の複数のハッシュテーブルをコンマで区切って渡します。 CauPluginName で指定されたプラグインの順序で、プラグインの引数を渡し \- \- ます。 **CauPluginName**

### <a name="specify-optional-plug-in-arguments"></a>オプションのプラグイン \- 引数の指定
\-CAU が microsoft.windowsupdateplugin と microsoft.hotfixplugin をインストールするプラグインは、 \( **Microsoft.WindowsUpdatePlugin** **Microsoft.HotfixPlugin** \) 選択できる追加のオプションを提供します。 CAU UI では、プラグインの更新実行オプションを構成した後、[**追加オプション**] ページにこれらの UI が表示され \- ます。 CAU の PowerShell コマンドレットを使用している場合、これらのオプションはオプションのプラグイン引数として構成され \- ます。 詳細については、このトピックで説明する「[Microsoft.WindowsUpdatePlugin の使用](#BKMK_WUP)」と「[Microsoft.HotfixPlugin の使用](#BKMK_HFP)」を参照してください。

## <a name="manage-plug-ins-using-windows-powershell-cmdlets"></a>\-Windows PowerShell コマンドレットを使用してプラグインを管理する

|コマンドレット|説明|
|----------|---------------|
|[Get-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/get-cauplugin)|ローカルコンピューターに登録されている1つまたは複数のソフトウェア更新プラグインに関する情報を取得 \- します。|
|[Register-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/register-cauplugin)|ローカルコンピューター上の CAU ソフトウェア更新プラグインを登録 \- します。|
|[Unregister-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/unregister-cauplugin)|\-CAU で使用できるプラグインの一覧から、ソフトウェア更新プラグインを削除し \- ます。 **注:**\-CAU microsoft.windowsupdateplugin および microsoft.hotfixplugin と共にインストールされたプラグインの \( **Microsoft.WindowsUpdatePlugin** **Microsoft.HotfixPlugin** \) 登録を解除することはできません。|

## <a name="using-the-microsoftwindowsupdateplugin"></a><a name="BKMK_WUP"></a>Microsoft.windowsupdateplugin の使用

CAU の既定のプラグインである Microsoft.windowsupdateplugin では、 \- 次のアクションが実行されます。 **Microsoft.WindowsUpdatePlugin**
- 各フェールオーバー クラスター ノード上の Windows Update エージェントと通信し、各ノードで実行されている Microsoft 製品に必要な更新プログラムを適用します。
- Windows Update または Microsoft Update から直接、またはオンプレミス Windows Server Update Services WSUS サーバーからクラスターの更新プログラムをインストール \- \( \) します。
- 選択された汎用配布リリースの GDR 更新プログラムのみをインストールし \( \) ます。 既定では、プラグインは \- 重要なソフトウェア更新プログラムのみを適用します。 構成は必要ありません。 既定の構成で、重要な GDR 更新プログラムが各ノードにダウンロードされ、インストールされます。

> [!NOTE]
> 既定で選択されている重要なソフトウェア更新プログラム (ドライバーの更新プログラムなど) 以外の更新プログラムを適用するに \( \) は、オプションのプラグインパラメーターを構成し \- ます。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="requirements"></a>必要条件

- フェールオーバークラスターとリモート更新コーディネーターコンピューターが \( 使用されている場合は、 \) cau の要件と、「 [cau の要件とベストプラクティス](cluster-aware-updating-requirements.md)」に記載されているリモート管理に必要な構成を満たしている必要があります。
- 「[Microsoft 更新プログラムを適用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_WUA)」を参照し、フェールオーバー クラスター ノードに合わせて Microsoft Update に必要な変更を加えます。
- 最適な結果を得るために、CAU ベストプラクティスアナライザー BPA を実行して、 \( \) cau を使用して更新プログラムを適用するようにクラスターと更新プログラムの環境が正しく構成されていることを確認することをお勧めします。 詳細については、「[CAU の更新処理の準備に関するテスト (英語)](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。

> [!NOTE]
> Microsoft の利用規約に同意する必要がある更新プログラムや、ユーザー操作が必要な更新プログラムは除外されるため、手動でインストールする必要があります。

### <a name="additional-options"></a>追加オプション

必要に応じて、次のプラグインの引数を指定し \- て、プラグインによって適用される更新プログラムのセットを拡張または制限することができ \- ます。
- \-各ノードの重要な更新プログラムだけでなく、推奨される更新プログラムを適用するようにプラグインを構成するには、CAU UI の [**追加のオプション**] ページで、[推奨される更新**プログラムを受信する方法と同じ方法で重要な更新プログラムを受信**する] チェックボックスをオンにします。
<br>または、 **' IncludeRecommendedUpdates ' \= ' True '** プラグイン引数を構成し \- ます。
- \-各クラスターノードに適用される GDR 更新プログラムの種類をフィルター処理するようにプラグインを構成するには、 **QueryString**プラグイン引数を使用して Windows Update エージェントクエリ文字列を指定し \- ます。 詳細については、「[Windows Update Agent クエリ文字列を構成する](#BKMK_QUERY)」を参照してください。

### <a name="configure-the-windows-update-agent-query-string"></a><a name="BKMK_QUERY"></a>Windows Update Agent クエリ文字列を構成する
\- \- Windows Update エージェントの**Microsoft.WindowsUpdatePlugin** \( WUA クエリ文字列で構成される既定のプラグインである microsoft.windowsupdateplugin に対して、プラグイン引数を構成できます \) 。 この手順では、WUA API を使用して、1 つまたは複数のグループの Microsoft 更新プログラムを指定して、指定した条件に基づいて各ノードに適用します。 複数の条件を組み合わせるには、論理 AND または論理 OR を使用できます。 WUA クエリ文字列は、次のようにプラグイン引数で指定し \- ます。

**QueryString \= "Criterion1 \= Value1 And \/ or Criterion2 \= Value2 and \/ or..."**

たとえば、**Microsoft.WindowsUpdatePlugin** では、既定の **QueryString** 引数を使用して重要な更新プログラムを自動的に選択します。この引数は、**IsInstalled**、**Type**、**IsHidden**、および **IsAssigned** の条件を使用して構築します。

**QueryString \= "IsInstalled \= 0 and Type \= ' Software ' and IsHidden \= 0 and isassigned \= 1"**

**QueryString**引数を指定すると、プラグインに対して構成されている既定の**querystring**の代わりに使用され \- ます。

#### <a name="example-1"></a>例 1

ID *f6ce46c1 \- 971c \- 43f9 \- a2aa \- 783df125f003*によって識別される特定の更新をインストールする**QueryString**引数を構成するには、次のようにします。

**QueryString \= "updateid \= ' f6ce46c1 \- 971c \- 43f9 \- a2aa \- 783df125f003 ' and IsInstalled \= 0"**

> [!NOTE]
> 前の例は、クラスター対応更新ウィザードを使用して更新プログラムを適用する場合に有効です \- 。 \-CAU UI を使用して自己更新オプションを構成するか、 ** \- Add-cauclusterrole**または**Set \- add-cauclusterrole**PowerShell コマンドレットを使用して、特定の更新プログラムをインストールする場合は、次の2つの単一引用符で updateid 値を設定する必要があり \- ます。
>
> **QueryString \= "updateid \= ' ' f6ce46c1 \- 971c \- 43f9 \- a2aa \- 783df125f003 ' ' and IsInstalled \= 0"**

#### <a name="example-2"></a>例 2

ドライバーのみをインストールする **QueryString** 引数を構成するには:

**QueryString \= "IsInstalled \= 0 and Type \= ' Driver ' and IsHidden \= 0"**

既定のプラグイン、 \- **microsoft.windowsupdateplugin**、検索条件 (IsInstalled など)、およびクエリ文字列に含めることができる構文のクエリ文字列の詳細については、「 \( **IsInstalled** \) [Windows Update エージェント (WUA) API リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=223304)」の検索条件に関するセクションを参照してください。

## <a name="use-the-microsofthotfixplugin"></a><a name="BKMK_HFP"></a>Microsoft.HotfixPlugin の使用
Microsoft.hotfixplugin プラグイン \- を**Microsoft.HotfixPlugin**使用すると、修正プログラムとも呼ばれる microsoft の制限付き配布リリース LDR の更新プログラムを適用でき \( \) \( ます。以前は、 \) 特定の microsoft ソフトウェアの問題に対処するために個別にダウンロードする qfe と呼ばれていました。 このプラグインは、SMB ファイル共有のルートフォルダーから更新プログラムをインストールし \- ます。また、Microsoft 以外のドライバー、ファームウェア、BIOS の更新プログラムを適用するようにカスタマイズすることもできます。

> [!NOTE]
> 修正プログラムは、サポート技術情報の記事に記載されている Microsoft からダウンロードできますが、必要に応じてお客様に提供されることもあり \- ます。

### <a name="requirements"></a>必要条件

- フェールオーバークラスターとリモート更新コーディネーターコンピューターが \( 使用されている場合は、 \) cau の要件と、「 [cau の要件とベストプラクティス](cluster-aware-updating-requirements.md)」に記載されているリモート管理に必要な構成を満たしている必要があります。
- 「[Microsoft.HotfixPlugin を使用する場合の推奨事項 (英語)](cluster-aware-updating-requirements.md#BKMK_BP_HF)」を参照してください。
- 最適な結果を得るために、CAU ベストプラクティスアナライザー BPA モデルを実行して、 \( \) cau を使用して更新プログラムを適用するようにクラスターと更新プログラムの環境が正しく構成されていることを確認することをお勧めします。 詳細については、「[CAU の更新処理の準備に関するテスト (英語)](cluster-aware-updating-requirements.md#BKMK_BPA)」を参照してください。
- 発行元から更新プログラムを取得して、 \( \) \( \) smb 2.0 以降をサポートし、 \( CAU がリモート更新モードで使用されている場合は、すべてのクラスターノードとリモート更新コーディネーターコンピューターからアクセス可能な、サーバーメッセージブロック smb ファイル共有修正プログラムルートフォルダー \- \) にそれらをコピーするか、展開します。 詳細については、このトピックの「[修正プログラム ルート フォルダー構造を構成する](#BKMK_HF_ROOT)」を参照してください。

    > [!NOTE]
    > 既定では、このプラグインによってインストールされるのは、 \- ファイル名拡張子が .msu、.msi、および .msp の修正プログラムのみです。

- \(作成した修正プログラムルートフォルダーに CAU ツールがインストールされているコンピューターの **% systemroot% \\ System32 \\ windowspowershell v1.0 \\ \\ Modules \\ clusterawareupdating.dll**フォルダーにある DefaultHotfixConfig.xml ファイルをコピーして、 \) 修正プログラムを抽出します。 たとえば、構成ファイルを* \\ \\ myfileserver の \\ 修正プログラムの \\ ルート \\ *にコピーします。

    > [!NOTE]
    > Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムをインストールするには、既定の修正プログラム構成ファイルを変更せずに使用できます。 変更が必要な場合は、高度なタスクとして構成ファイルをカスタマイズできます。 構成ファイルには、カスタム規則を含めることができます。たとえば、特定の拡張子を持つ修正プログラム ファイルの処理、特定の終了条件に関する動作の定義などです。 詳細については、このトピックの「[修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE)」を参照してください。

### <a name="configuration"></a>構成

次の設定を構成します。 詳細については、このトピックで後述するセクションのリンクを参照してください。
- 適用する更新プログラムと修正プログラムの構成ファイルが保存される、共有される修正プログラム ルート フォルダーのパス。 このパスは、CAU UI で入力するか、 ** \= \<Path> HotfixRootFolderPath** PowerShell プラグイン引数を構成することができ \- ます。

   > [!NOTE]
   > 修正プログラムルートフォルダーは、ローカルフォルダーパスとして指定することも、 * \\ \\ ServerName \\ Share \\ rootfoldername*という形式の UNC パスとして指定することもできます。 ドメイン \- ベースまたはスタンドアロンの DFS 名前空間パスを使用できます。 ただし、 \- 修正プログラム構成ファイルのアクセス許可を確認するプラグイン機能は、DFS 名前空間パスと互換性がありません。そのため、構成する場合は、CAU UI を使用するか、 **disableaclchecks \= ' True '** プラグイン引数を構成して、アクセス許可の確認を無効にする必要があり \- ます。
- 修正プログラムルートフォルダーをホストするサーバーの設定。このフォルダーにアクセスするための適切なアクセス許可があるかどうかを確認し、smb 共有フォルダー \( smb 署名または Smb 暗号化からアクセスされるデータの整合性を確認し \) ます。 詳細については、「[修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」を参照してください。

### <a name="additional-options"></a>追加オプション

- 必要に応じて、 \- 修正プログラムのファイル共有からデータにアクセスするときに SMB 暗号化が適用されるようにプラグインを構成します。 CAU UI の [**追加オプション**] ページで、[**修正プログラムルートフォルダーへのアクセス時に SMB 暗号化を要求**する] オプションをオンにするか、 **RequireSMBEncryption \= ' True '** PowerShell プラグイン引数を構成し \- ます。
  > [!IMPORTANT]
  > SMB データの SMB 署名または SMB 暗号化との整合性を有効にするには、SMB サーバーで追加の構成手順を実行する必要があります。 詳細については、「[修正プログラム ルート フォルダーへのアクセスを制限する](#BKMK_ACL)」の手順 4 を参照してください。 SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用したアクセスに対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。
- 必要に応じて、修正プログラム ルート フォルダーと修正プログラムの構成ファイルに十分なアクセス許可があるかどうかに関する既定の確認を無効にします。 CAU UI で、[**修正プログラムルートフォルダーおよび構成ファイルへの管理者アクセスの確認を無効**にする] を選択するか、 **disableaclchecks \= ' True '** プラグイン引数を構成し \- ます。
- 必要に応じて **、 \= <Integer> HotfixInstallerTimeoutMinutes**引数を構成して、修正プログラムプラグインが \- 修正プログラムのインストーラープロセスを返すまで待機する時間を指定します。 \(既定値は30分です。 \)たとえば、2時間のタイムアウト期間を指定するには、 **HotfixInstallerTimeoutMinutes \= 120**を設定します。
- 必要に応じて **、 \= <name> HotfixConfigFileName**プラグイン引数を構成して、 \- 修正プログラムルートフォルダーにある修正プログラムの構成ファイルの名前を指定します。 指定しない場合、既定の名前である DefaultHotfixConfig.xml が使用されます。

### <a name="configure-a-hotfix-root-folder-structure"></a><a name="BKMK_HF_ROOT"></a>修正プログラム ルート フォルダー構造を構成する

修正プログラムプラグインを \- 機能させるには、SMB ファイル共有修正プログラムルートフォルダー内の適切に定義された構造に修正プログラムを保存する必要があり \- \( \) \- ます。また、Cau UI または cau PowerShell コマンドレットを使用して、修正プログラムルートフォルダーへのパスを使用して修正プログラムプラグインを構成する必要があります。 このパスは、 \- **HotfixRootFolderPath**引数としてプラグインに渡されます。 次の例のように、実際の更新のニーズに応じて、修正プログラム ルート フォルダーに対応するいくつかの構造からいずれかを選択できます。 この構造に従っていないファイルまたはフォルダーは無視されます。

#### <a name="example-1---folder-structure-used-to-apply-hotfixes-to-all-cluster-nodes"></a>例 1-すべてのクラスターノードに修正プログラムを適用するために使用されるフォルダー構造

修正プログラムがすべてのクラスターノードに適用されるように指定するには、修正プログラムルートフォルダーの下の**CAUHotfix \_ all**という名前のフォルダーにコピーします。 この例では、 **HotfixRootFolderPath**プラグインの \- 引数が* \\ \\ myfileserver の \\ 修正プログラム \\ の \\ ルート*に設定されています。 **CAUHotfix \_ all**フォルダーには、拡張子が .msu、.msi、および .msp の3つの更新プログラムが含まれており、すべてのクラスターノードに適用されます。 この更新プログラム ファイル名は、説明のためにのみ使用されています。

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

特定のノードにのみ適用する修正プログラムを指定するには、修正プログラム ルート フォルダー以下にあるノード名を持つサブフォルダーを使用します。 クラスター ノードの NetBIOS 名を使用します。たとえば、*ContosoNode1* などです。 次に、そのノードにのみ適用する更新プログラムを、このサブフォルダーに移動します。 次の例では、 **HotfixRootFolderPath**プラグインの \- 引数が* \\ \\ myfileserver の \\ 修正プログラム \\ の \\ ルート*に設定されています。 **CAUHotfix \_ all**フォルダー内の更新プログラムはすべてのクラスターノードに適用され、 *Node1 \_ 固有の \_ 更新*プログラムは*ContosoNode1*にのみ適用されます。

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

既定では、**Microsoft.HotfixPlugin** は拡張子が .msu、.msi、または .msp の更新プログラムのみを適用します。 ただし、一部の更新プログラムは拡張子が異なり、別のインストール コマンドが必要な場合があります。 たとえば、場合によっては、拡張子が .exe のファームウェアの更新プログラムをクラスター内のノードに適用する必要があります。 特定の既定以外の更新プログラムの種類をインストールすることを示すサブフォルダーを使用して、修正プログラムルートフォルダーを構成することができ \- ます。 また、対応するフォルダーのインストール規則を構成して、修正プログラムの構成 XML ファイルで `<FolderRules>` 要素にインストール コマンドを指定する必要もあります。

次の例では、 **HotfixRootFolderPath**プラグインの \- 引数が* \\ \\ myfileserver の \\ 修正プログラム \\ の \\ ルート*に設定されています。 一部の更新プログラムはすべてのクラスター ノードに適用されます。またファームウェアの更新プログラムの *SpecialHotfix1.exe* は、*FolderRule1* を使用して *ContosoNode1* に適用されます。 修正プログラムの構成ファイルで *FolderRule1* を構成する場合の詳細については、このトピックの「[修正プログラムの構成ファイルをカスタマイズする](#BKMK_CONFIG_FILE)」を参照してください。

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

### <a name="customize-the-hotfix-configuration-file"></a><a name="BKMK_CONFIG_FILE"></a>修正プログラムの構成ファイルをカスタマイズする
修正プログラムの構成ファイルは、フェールオーバー クラスターに特定の修正プログラム ファイルの種類を **Microsoft.HotfixPlugin** でインストールする方法を制御します。 構成ファイルの XML スキーマは HotfixConfigSchema.xsd で定義されています。この xsd ファイルは、CAU ツールがインストールされているコンピューターの次のフォルダーに保存されています。

**% systemroot% \\ System32 \\ windowspowershell V1.0 \\ \\ モジュール \\ clusterawareupdating.dll フォルダー**

修正プログラムの構成ファイルをカスタマイズするには、この場所にあるサンプルの構成ファイル DefaultHotfixConfig.xml を修正プログラム ルート フォルダーにコピーし、実際のシナリオに合わせて変更します。

> [!IMPORTANT]
> Microsoft が提供するほとんどの修正プログラムやその他の更新プログラムを適用するには、既定の修正プログラム構成ファイルを変更せずに使用できます。 修正プログラムの構成ファイルのカスタマイズは、高度な使用シナリオでのみ実行されるタスクです。

修正プログラムの構成 XML ファイルは、次の 2 つのカテゴリの修正プログラムについて、既定でインストール規則と終了条件を定義しています。

-   \-既定の \( .msu、.msi、および .msp ファイルでプラグインによってインストールできる拡張子を持つ修正プログラムファイル \) 。

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

-   .Msi、.msu、または .msp ファイルではない修正プログラムファイル (Microsoft 以外の \- ドライバー、ファームウェア、BIOS の更新プログラムなど)。

    既定以外の各 \- ファイルの種類は `<Folder>` 、要素内の要素として構成され `<FolderRules>` ます。 `<Folder>` 要素の name 属性は、対応する種類の更新プログラムを保存する修正プログラム ルート フォルダー内のフォルダー名と同じにする必要があります。 フォルダーは、 **CAUHotfix \_ All**フォルダーまたはノード固有のフォルダーに配置でき \- ます。 たとえば、*FolderRule1* を修正プログラム ルート フォルダー内に構成する場合、XML ファイルに次の要素を構成して、そのフォルダー内の更新プログラムについてインストール テンプレートと終了条件を定義します。

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
|`path`|`<Extension name>` 属性に定義されているファイルの種類に関する、インストール プログラムの完全なパス。<p>修正プログラム ルート フォルダー構造にある更新プログラム ファイルのパスを指定するには、 `$update$`を使用します。|
|`parameters`|`path`に指定されているプログラムの必要なパラメーターと省略可能なパラメーターの文字列。<p>修正プログラム ルート フォルダー構造にある更新プログラム ファイルのパスのパラメーターを指定するには、 `$update$`を使用します。|

|`<ExitConditions>` サブ要素|説明|
|---------------------------------|---------------|
|`<Success>`|指定した更新プログラムが成功したことを示す終了コードを 1 つまたは複数定義します。 これは必須のサブ要素です。|
|`<Success_RebootRequired>`|必要に応じて、指定した更新プログラムが成功し、ノードを再起動する必要があることを示す終了コードを 1 つまたは複数定義します。 <br>**注:** 必要に応じて、 `<Folder>` 要素に属性を含めることができ `alwaysReboot` ます。 この属性を設定すると、この規則でインストールされる修正プログラムが `<Success>`に定義されている終了コードのいずれかを返した場合、 `<Success_RebootRequired>` 終了条件として解釈されます。|
|`<Fail_RebootRequired>`|必要に応じて、指定した更新プログラムが失敗し、ノードを再起動する必要があることを示す終了コードを 1 つまたは複数定義します。|
|`<AlreadyInstalled>`|必要に応じて、指定した更新プログラムは既にインストールされているため、適用されなかったことを示す終了コードを 1 つまたは複数定義します。|
|`<NotApplicable>`|必要に応じて、指定した更新プログラムはクラスター ノードに適用されていないため、適用されなかったことを示す終了コードを 1 つまたは複数定義します。|

> [!IMPORTANT]
> `<ExitConditions>` に明示的に定義されていない終了コードは、更新プログラムが失敗したと解釈され、ノードは再起動しません。

### <a name="restrict-access-to-the-hotfix-root-folder"></a><a name="BKMK_ACL"></a>修正プログラム ルート フォルダーへのアクセスを制限する
SMB ファイル サーバーとファイル共有を構成して、**Microsoft.HotfixPlugin** のコンテキストでのみアクセスするように修正プログラム ルート フォルダー ファイルと修正プログラムの構成ファイルをセキュリティで保護するには、いくつかの手順を実行する必要があります。 これらの手順によって、フェールオーバー クラスターのセキュリティを侵害するような方法で修正プログラム ファイルを改ざんする危険性を回避できます。

一般的な手順は次のとおりです。

1.  プラグインを使用して、更新実行に使用するユーザーアカウントを特定します。 \-

2.  SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する

3.  修正プログラム ルート フォルダーのアクセス許可を構成する

4.  SMB データの整合性に関する設定を構成する

5.  SMB サーバーで Windows ファイアウォール規則を有効にする

#### <a name="step-1-identify-the-user-account-that-is-used-for-updating-runs-by-using-the-hotfix-plug-in"></a>手順 1. 修正プログラムプラグインを使用して、更新実行に使用するユーザーアカウントを特定します。 \-

**Microsoft.hotfixplugin**を使用して更新実行を実行するときに、cau でセキュリティ設定を確認するために使用されるアカウントは、次のように、cau がリモート \- 更新モードと自己更新モードのどちらで使用されているかによって異なり \- ます。

-   **リモート \- 更新モード**クラスターで管理者特権を持つアカウントで、更新プログラムをプレビューして適用します。

-   **自己 \- 更新モード**CAU のクラスター化された役割の Active Directory で構成された仮想コンピューターオブジェクトの名前。 この名前は、Active Directory で CAU のクラスター化された役割用に事前設定された仮想コンピューター オブジェクトの名前か、クラスター化された役割用に CAU によって生成された名前です。 CAU によって生成された名前を取得するには、 **Get \- Add-cauclusterrole** cau PowerShell コマンドレットを実行します。 出力の **ResourceGroupName** は、生成された仮想コンピューター オブジェクト アカウントの名前です。

#### <a name="step-2-configure-this-user-account-in-the-necessary-groups-on-an-smb-file-server"></a>手順 2. SMB ファイル サーバーで必要なグループにユーザー アカウントを構成する

> [!IMPORTANT]
> 更新実行に使用するアカウントは、SMB サーバーのローカルの管理者アカウントとして追加する必要があります。 組織のセキュリティ ポリシーで、このようなアカウントを追加できない場合は、次の手順を使用して、SMB サーバーに必要なアクセス許可を持つ管理者アカウントを構成します。

##### <a name="to-configure-a-user-account-on-the-smb-server"></a>SMB サーバーでユーザー アカウントを構成するには

1.  更新実行に使用するアカウントを Distributed COM Users グループに追加し、さらに、Power User、Server Operation、Print Operator のいずれかに追加します。

2.  アカウントに必要な WMI のアクセス許可を有効にするには、SMB サーバーで WMI 管理コンソールを開始します。 PowerShell を起動し、次のコマンドを入力します。

    ```
    wmimgmt.msc
    ```

3.  コンソールツリーで、[ \- **WMI コントロール \( ローカル \) **] を右クリックし、[**プロパティ**] をクリックします。

4.  [**セキュリティ**] をクリックし、[**ルート**] を展開します。

5.  [**CIMV2**] をクリックし、[**セキュリティ**] をクリックします。

6.  更新実行に使用するアカウントを [**グループ名またはユーザー名**] リストに追加します。

7.  [**メソッドの実行**] および [**リモートの有効化**] のアクセス許可を更新実行に使用するアカウントに付与します。

#### <a name="step-3-configure-permissions-to-access-the-hotfix-root-folder"></a>手順 3. 修正プログラム ルート フォルダーのアクセス許可を構成する

既定では、更新プログラムを適用しようとすると、修正プログラムプラグインは、 \- 修正プログラムルートフォルダーへのアクセスに関して NTFS ファイルシステムのアクセス許可の構成を確認します。 フォルダーのアクセス許可が適切に構成されていない場合は、修正プログラムプラグインを使用した更新実行が \- 失敗する可能性があります。

修正プログラムプラグインの既定の構成を使用する場合は \- 、フォルダーのアクセス許可が次の要件を満たしていることを確認してください。

-   Users グループに読み取りアクセス許可があります。

-   プラグインによって \- .exe 拡張子の付いた更新プログラムが適用される場合、Users グループには実行アクセス許可があります。

-   特定のセキュリティプリンシパルのみが許可され \( ますが、 \) 書き込みまたは変更のアクセス許可が必要ではありません。 許可されるプリンシパルは、ローカルの Administrators グループ、SYSTEM、CREATOR OWNER、および TrustedInstaller です。 その他のアカウントまたはグループには、修正プログラム ルート フォルダーで書き込みまたは修正のアクセス許可は付与されません。

必要に応じて、プラグインが既定で実行する上記のチェックを無効にすることができ \- ます。 2 つの方法のいずれかでこれを行うことができます。

-   CAU の PowerShell コマンドレットを使用している場合は、修正プログラムプラグインの**CauPluginArguments**パラメーターで**disableaclchecks の \= ' True '** 引数を構成し \- ます。

-   CAU UI を使用している場合、更新実行オプションの構成に使用するウィザードの [**追加の更新オプション**] ページで、[**修正プログラム ルート フォルダーおよび構成ファイルへの管理者アクセスのチェックを無効にする**] オプションをオンにします。

ただし、多くの環境では、ベスト プラクティスとして、既定の構成を使用してこれらの確認を実行することをお勧めします。

#### <a name="step-4-configure-settings-for-smb-data-integrity"></a>手順 4. SMB データの整合性に関する設定を構成する

クラスターノードと SMB ファイル共有間の接続でデータの整合性を確認するには、修正プログラムプラグインで smb \- ファイル共有の設定を smb 署名または Smb 暗号化に対して有効にする必要があります。 多くの環境でセキュリティを強化し、パフォーマンスを向上させる SMB 暗号化は、Windows Server 2012 以降でサポートされています。 次のように、これらの設定のいずれかまたは両方を有効にすることができます。

-   SMB 署名を有効にするには、Microsoft サポート技術情報の [記事 887429](https://support.microsoft.com/kb/887429) の手順を参照してください。

-   Smb 共有フォルダーの SMB 暗号化を有効にするには、SMB サーバーで次の PowerShell コマンドレットを実行します。

    ```PowerShell
    Set-SmbShare <ShareName> -EncryptData $true
    ```

    ここで、<*ShareName*> は SMB 共有フォルダーの名前です。

必要に応じて、SMB サーバーへの接続で smb 暗号化の使用を強制するには、CAU UI で [**修正プログラムルートフォルダーへのアクセス時に Smb 暗号化を要求**する] オプションをオンにするか、cau PowerShell コマンドレットを使用して**RequireSMBEncryption \= ' True '** プラグイン引数を構成し \- ます。

> [!IMPORTANT]
> SMB 暗号化を使用するオプションを選択しても、SMB 暗号化を使用した接続に対応するように修正プログラム ルート フォルダーが構成されていない場合、更新実行は失敗します。

#### <a name="step-5-enable-a-windows-firewall-rule-on-the-smb-server"></a>手順 5. SMB サーバーで Windows ファイアウォール規則を有効にする

SMB ファイルサーバーの Windows ファイアウォールのルール** \( \- で \) 、ファイルサーバーのリモート管理 smb**を有効にする必要があります。 これは、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 では既定で有効になっています。

## <a name="additional-references"></a>その他のリファレンス

-   [クラスター対応更新の概要](cluster-aware-updating.md)

-   [クラスター対応更新の Windows PowerShell コマンドレット](https://docs.microsoft.com/powershell/module/clusterawareupdating)

-   [クラスター対応更新プラグインのリファレンス](https://msdn.microsoft.com/library/hh418084.aspx)

