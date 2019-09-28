---
title: ベスト プラクティス アナライザー スキャンの実行およびスキャン Results_1 の管理
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 232f1c80-88ef-4a39-8014-14be788c2766
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6edd561749ea0d224058b482992d357357c12505
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383083"
---
# <a name="run-best-practices-analyzer-scans-and-manage-scan-results"></a>ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理

>適用先:Windows Server 2016

Windows の管理の*ベスト プラクティス*とは、標準的な環境の下で、専門家の定義に従ってサーバーを構成するための望ましい方法と考えられるガイドラインです。 たとえば、ほとんどのサーバー アプリケーションでは、他のネットワーク コンピューターと通信するためのアプリケーションに必要なポートのみを開いておき、未使用のポートはブロックすることがベスト プラクティスと考えられます。 ベスト プラクティスへの非準拠は、それが深刻なものであっても必ずしも問題があるとは限りませんが、ベスト プラクティスに準拠していないサーバー構成には、パフォーマンスや信頼性の低下、予期しない競合、セキュリティ リスクの増大などの問題を引き起こす可能性があります。

ベスト プラクティス アナライザー (BPA) は、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 で利用可能なサーバー管理ツールです。 BPA は、Windows Server 2012 を実行している管理対象のサーバーまたは Windows Server 2008 R2 にインストールされている役割をスキャンし、管理者のベスト プラクティス非準拠をレポート作成のベスト プラクティス非準拠を軽減できます。

行うことができますベスト プラクティス アナライザー (BPA) スキャンするか、サーバー マネージャーから BPA GUI を使用するか、Windows PowerShell のコマンドレットを使用します。 Windows Server 2012 以降では、複数のサーバー上で1つまたは複数の役割を一度にスキャンできます。サーバーマネージャーコンソールの [ベストプラクティスアナライザー] タイルまたは Windows PowerShell コマンドレットを使用してスキャンを実行するかどうかを指定します。 BPA では、表示する必要のないスキャン結果を除外または非表示にする設定を行うこともできます。

このトピックは次のセクションで構成されます。

-   [BPA の検索](#BKMK_find)

-   [BPA のしくみ](#BKMK_how)

-   [ロールでのベストプラクティスアナライザースキャンの実行](#BKMK_BPAscan)

-   [スキャン結果の管理](#BKMK_manage)

## <a name="BKMK_find"></a>BPA の検索
サーバー グループのページ Windows Server 2012 R2 と Windows Server 2012 では、サーバー マネージャーがベスト プラクティス アナライザー コマンドレットを実行する管理者特権で Windows PowerShell セッションを開くことができますおよびロールのベスト プラクティス アナライザーのタイルを検索できます。

## <a name="BKMK_how"></a>BPA のしくみ
BPA は、有効性、信頼性、および信頼性の 8 つのカテゴリでベスト プラクティスの規則とロールの対応を測定することによって機能します。 測定の結果は、次の表で説明する 3 つの重大度レベルで表されます。

|重大度レベル|説明|
|---------|--------|
|Error|エラー結果は、役割がベストプラクティス規則の条件を満たしておらず、機能上の問題が想定される場合に返されます。|
|[情報]|情報結果は、役割がベスト プラクティス規則の条件を満たしている場合に返されます。|
|警告|警告結果は、準拠していない状態を変更しない場合、問題が発生する可能性があるときに返されます。 アプリケーションが現時点では動作していて準拠しているが、構成やポリシー設定を変更しない場合に規則の条件を満たさない可能性がある場合、警告が返されます。 たとえば、リモート デスクトップ サービスのスキャンでは、役割でライセンス サーバーを使用できない場合、警告が表示される可能性があります。これは、スキャン時にアクティブなリモート接続がない場合でも、ライセンス サーバーを利用できないと、新しいリモート接続で有効なクライアント アクセス ライセンスを取得できないためです。|

### <a name="rule-categories"></a>規則のカテゴリ
次の表に、ベスト プラクティス ルールのカテゴリに対して、ベスト プラクティス アナライザーで役割を測定をスキャンします。

|カテゴリ名|説明|
|---------|--------|
|セキュリティ|未承認または悪意のあるユーザー、損失や機密情報や機密データの盗難などの脅威にさらされるロールの相対的なリスクを測定するセキュリティの規則が適用されます。|
|パフォーマンス|要求を処理し、ロールのワークロードを指定された予定期間内で、企業内、指定された処理を実行する役割の能力を測定するパフォーマンス ルールが適用されます。|
|構成|構成規則は、役割が最適に実行されるために変更が必要と思われる役割設定を特定するために適用します。 構成規則によって、エラー メッセージが表示される、または役割が企業での所定の作業を実行できなくなる可能性がある設定の競合を回避することができます。|
|ポリシー|ポリシー規則は、役割が最適かつ安全に動作するために変更を必要とするグループポリシーまたは Windows レジストリ設定を特定するために適用されます。|
|操作|操作規則は、企業で所定のタスクを実行する際に発生する可能性がある役割のエラーを特定するために適用します。|
|展開前|展開前規則は、インストールされた役割を企業で展開する前に適用します。 管理者は、役割を運用環境で使う前に、ベスト プラクティスを満たしているかどうかを評価できます。|
|展開後|展開後規則は、すべての必要なサービスが役割で開始され、役割が企業で実行された後に適用します。|
|前提条件|前提条件規則は、BPA で他のカテゴリの特定の規則を適用するために、役割に必要な構成設定、ポリシー設定、機能について説明します。 スキャン結果の前提条件は、間違った設定、不足しているプログラム、誤って有効または無効にされたポリシー、レジストリ キー設定、またはその他の構成により、スキャン中に BPA で 1 つ以上の規則が適用できなかったことを示しています。 前提条件の結果は、準拠や非準拠を示すものではなく、 規則を適用できなかったため、スキャン結果に規則が含まれていないことを示すものです。|

## <a name="BKMK_BPAscan"></a>ロールでのベストプラクティスアナライザースキャンの実行
行うことができます BPA スキャンの役割を使用して、BPA GUI サーバー マネージャーで、または Windows PowerShell コマンドレットを使用します。

Windows Server 2012 R2 および Windows Server 2012 では、いくつかの役割は、特定のサーバーまたは BPA スキャンを開始する前に、その役割の一部またはサブモデルの Id を実行している共有の名前などの他のパラメーターを指定することを求められます。 パラメーターの追加入力が必要なモデルに対する BPA スキャンでは、BPA コマンドレットを使います。BPA GUI では、サブモデル ID などの追加のパラメーターは受け付けられません。 たとえば、サブモデル ID **FSRM** は、ファイル サービスおよび記憶域サービスの役割サービスの 1 つであるファイル サーバー リソース マネージャーに対応する、ファイル サービス BPA サブモデルを表します。 スキャンを実行するだけでファイル サーバー リソース マネージャーの役割サービスでは、Windows PowerShell コマンドレットを使用して BPA スキャンを実行し、パラメーターを追加する `SubmodelId` コマンドレットです。

BPA GUI で開始したスキャンには、追加のパラメーターを渡すことはできません、BPA タイル サーバー マネージャーでは、スキャンが開始された方法に関係なく、最新の BPA スキャンの結果を表示します。

-   [BPA GUI を使用したロールのスキャン](#BKMK_GUIscan)

-   [Windows PowerShell コマンドレットを使用して役割をスキャンする](#BKMK_PSscan)

### <a name="BKMK_GUIscan"></a>BPA GUI を使用したロールのスキャン
BPA GUI を使用して 1 つまたは複数の役割をスキャンするには、次の手順を実行します。

##### <a name="to-scan-roles-by-using-the-bpa-gui"></a>BPA GUI を使用して役割をスキャンするには

1.  既に開かれていない場合は、サーバー マネージャーを開くには、次のいずれかの操作を行います。

    -   Windows タスク バーで、サーバー マネージャ ボタンをクリックします。

    -   **スタート**画面で、[サーバーマネージャー] タイルをクリックします。

2.  ナビゲーション ウィンドウで、役割またはグループのページを開きます。

    役割またはグループのページから BPA スキャンを実行すると、そのグループのサーバーにインストールされているすべての役割がスキャンされます。

3.  **[ベストプラクティスアナライザー]** タイルの **[タスク]** メニューで、 **[BPA スキャンの開始]** をクリックします。

4.  選択した役割またはグループの評価に使用される規則の数に応じて、BPA スキャンが完了するまでには数分かかる場合があります。

### <a name="BKMK_PSscan"></a>Windows PowerShell コマンドレットを使用して役割をスキャンする
Windows PowerShell コマンドレットを使用して 1 つまたは複数の役割をスキャンするのにには、次の手順を使用します。

> [!NOTE]
> ここに示す手順では、BPA のコマンドレットとパラメーターをすべて表示していません。 Windows PowerShell での BPA 操作の詳細については、Windows PowerShell セッションで「 **Get-help***bpacmdlet***-full**」と入力してください。 *bpacmdlet*には、次のいずれかの値を指定できます。 BPA コマンドレットのヘルプトピックは、 [Windows Server TechCenter](https://go.microsoft.com/fwlink/p/?LinkId=240177)でも確認できます。

-   **Invoke-bpamodel**

-   **Invoke-bpamodel**

-   **取得-BPAResult**

-   **設定-BPAResult**

#### <a name="BKMK_singlerole"></a>Windows PowerShell コマンドレットを使用して1つの役割をスキャンするには

1.  管理者特権で Windows PowerShell を実行するには、次のいずれかの操作を行います。

    -   Windows PowerShell を**スタート**画面から管理者として実行するには、 **[アプリ]** の結果で **[windows powershell]** タイルを右クリックし、アプリバーの **[管理者として実行]** をクリックします。

    -   デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックしてタスク バーで、 **管理者として実行**します。

2.  Windows PowerShell 3.0 以降では、コマンドレットモジュールは、モジュールのコマンドレットが初めて使用されるときに、Windows PowerShell セッションに自動的にインポートされます。 BPA コマンドレット モジュールをインポートまたは読み込む必要はありません。

3.  次の例に示すように、 **invoke-bpamodel**コマンドレットを入力して、BPA スキャンを実行できるすべてのロールのモデル id を検索します。

    `Get-Bpamodel`

4.  手順 3. の結果で、BPA スキャンを実行する役割のモデル ID を探します。

5.  次のいずれかのコマンドを入力して、特定の役割に対する BPA スキャンを開始します。 複数の役割に対して実行する場合は、モデル ID をコンマで区切ります。

    `Invoke-BPAmodel -modelId <modelID_from_Step3>`

    `Invoke-BPAmodel <modelID_from_Step3>`

    **例:** `Invoke-BPAmodel -modelId Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    > [!NOTE]
    > モデル ID には、**Microsoft/Windows/Hyper-V** のように、**Id** 列に示されたパス全体を指定します。

    また、次の例に示すように、 `Get-BPAmodel` コマンドレットの結果を `Invoke-BPAmodel` コマンドレットにパイプして、手順 3. の結果の特定の役割に対するスキャンを開始することもできます。

    `Get-BPAmodel <model_ID> | Invoke-BPAmodel`

    によって返されるすべてのモデル パイプを使用してモデル ID を指定せずにこのコマンドレットを実行する、 `Get-BPAmodel` コマンドレットに、 `Invoke-BPAmodel` コマンドレットは、サーバー マネージャー サーバー プールに追加されているサーバーで使用可能なすべてのモデルに対するスキャンを開始します。

#### <a name="BKMK_allroles"></a>Windows PowerShell コマンドレットを使用してすべての役割をスキャンするには

1.  いずれかがまだ開いていない場合は、管理者特権で Windows PowerShell セッションを開きます。 手順については、前に示した手順を参照してください。

2.  BPA スキャンを実行できるすべての役割を `Invoke-BPAmodel` コマンドレットにパイプして、スキャンを開始します。

    `Get-BPAmodel | Invoke-BPAmodel`

3.  スキャンが完了したら、Windows PowerShell 結果を返しますスキャンされた各ロールに対して、次に似ています。

    ```
    modelId                 :  Microsoft/Windows/FileServices
    SubmodelId              :
    Success                 :  True
    Scantime                :  1/01/2012  12:18:40 PM
    ScantimeUtcOffset       :  -08:00:00
    detail                  :  {server_name1, server_name2}

    ```

## <a name="BKMK_manage"></a>スキャン結果の管理
GUI を使った BPA スキャンの実行後、BPA タイルでスキャン結果を確認できます。 タイルで結果を選択すると、関連付けられたベスト プラクティスに役割が準拠しているかどうかを示す情報などの結果のプロパティが、タイルのプレビュー ウィンドウに表示されます。 結果が準拠していない場合に、結果のプロパティで説明されている問題の解決方法を知りたい場合は、「エラーと警告の結果プロパティ」のハイパーリンクで、Windows Server TechCenter の詳細な解決方法に関するヘルプトピックを開きます。

> [!NOTE]
> BPA スキャンの結果は、自動的に保存またはアーカイブされません。 モデルまたはサブモデルに対するスキャンを新規で実行すると、その前のスキャン結果は上書きされます。 アーカイブ、印刷、または他のユーザーに送信するために BPA スキャン結果を保存するには、このセクションの「 [To view BPA results from Windows PowerShell sessions in different formats](#BKMK_formats) 」を参照してください。

### <a name="exclude-and-include-bpa-results"></a>BPA 結果を除外および含めるには
bpa スキャンで頻繁に発生し、解決する必要がない結果など、一部の BPA 結果を表示する必要がない場合は、BPA GUI または Windows PowerShell の BPA コマンドレットのいずれかを使用して、結果を除外できます。 結果は、いつでも再度含めることができます。

> [!NOTE]
> 除外した結果は、管理対象サーバー上の表示からも除外されます。 除外された結果は、他の管理者が管理対象サーバー上で見ることもできません。 ビューのみにローカル サーバー マネージャー コンソールで、結果を除外するには、使用する代わりにカスタム クエリを作成、 **結果を除外する** コマンドです。

#### <a name="BKMK_exclude"></a>スキャン結果を除外する
**"除外"** の設定は永続的です。除外した結果は、改めて含める設定を行わない限り、同一コンピューター上で同一モデルに対してその後実行されるスキャンでも除外されます。

`Set-BPAResult` コマンドレットと `Exclude` パラメーターを使用して、スキャン結果を除外できます。 ベスト プラクティス アナライザー タイル サーバー マネージャーで、個々 の結果オブジェクトを除外することやフィールド (カテゴリ、タイトル、および重要度など) に等しいか、指定した値を含む結果セットを除外することもできます。 たとえば、モデルのスキャン結果のセットから、 **パフォーマンス** に関する結果をすべて除外できます。

> [!NOTE]
> このセクションの手順を実行するには、モデルに対する BPA スキャンが少なくとも 1 回実行されている必要があります。

###### <a name="to-exclude-scan-results-by-using-the-gui"></a>GUI を使用してスキャン結果を除外するには

1.  サーバー マネージャーで、役割またはサーバー グループのページを開きます。

2.  役割またはサーバー グループのベスト プラクティス アナライザーのタイルの一覧で、結果を右クリックし、 **結果を除外する**です。

    操作対象とした結果は、結果の一覧に表示されなくなります。

3.  GUI で除外された結果を表示するには、組み込みの **[除外される結果]** クエリを実行します。 **[保存されている検索クエリ]** をクリックし、 **[除外される結果]** をクリックします。

    **[除外される結果]** クエリの実行後、タイルの小見出し (一覧に表示されている結果の説明) は **"除外される結果"** に変わります。 除外される結果のみが一覧に表示されます。

###### <a name="to-exclude-scan-results-by-using-windows-powershell-cmdlets"></a>Windows PowerShell コマンドレットを使用してスキャン結果を除外するには

1.  管理者特権で Windows PowerShell セッションを開きます。

2.  モデルのスキャン結果から特定の結果を除外するには、次のコマンドを実行します。

    `Get-BPAResult -modelId <model ID> | Where { $_.<Field Name> -eq "Value"} | Set-BPAResult -Exclude $true`

    上記のコマンドは、*モデル id*によって表されるモデル ID の BPA スキャン結果項目を取得します。

    コマンドの 2 番目の部分では、 `Get-BPAResult` コマンドレットの結果をフィルター処理し、 *Field Name*によって示される結果フィールドの値が引用符内のテキストに一致するスキャン結果だけを取得します。

    コマンドの最後の部分 (2 つ目のパイプ文字の後) では、コマンドレットの 2 番目の部分でフィルター処理された結果を除外します。

    **例:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq "Information"} | Set-BPAResult -Exclude $true`

#### <a name="include-scan-results"></a>スキャン結果を含める
除外したスキャン結果を表示する場合は、そのスキャン結果を含めることができます。 **"含める"** 設定は永続的です。含めることにした結果は、同一コンピューター上で同一モデルに対してその後実行されるスキャンでも含まれます。

##### <a name="BKMK_gui"></a>GUI を使用してスキャン結果を含めるには

1.  サーバー マネージャーで、役割またはサーバー グループのページを開きます。

2.  役割またはサーバー グループのベスト プラクティス アナライザーのタイルで除外される結果を右クリックし、 **結果を除外**  ボックスの一覧を照会し、クリックして **結果を含める**します。

    操作対象とした結果は、除外される結果の一覧に表示されなくなります。 含まれるすべての結果の一覧に、含まれる結果を表示するには、 **[すべてクリア]** をクリックしてクエリをクリアします。

##### <a name="BKMK_cmdlets"></a>Windows PowerShell コマンドレットを使用してスキャン結果を含めるには

1.  管理者特権で Windows PowerShell セッションを開きます。

2.  モデルのスキャン結果の特定の結果を含めるには、次のコマンドを入力し、 **Enter**キーを押します。

    `Get-BPAResult -modelId <model Id> | Where { $_.<Field Name> -eq "Value" } | Set-BPAResult -Exclude $false`

    上記のコマンドは、*モデル Id*によって表されるモデルの BPA スキャン結果項目を取得します。

    最初のパイプ文字の後に、コマンドの 2 番目の部分 ( **|** ) の結果をフィルター処理、 **Get-bparesult** スキャン結果のフィールドの値がで示される結果だけを取得するコマンドレット *フィールド名*, 、引用符で囲まれた文字列と一致します。

    コマンドの最後の部分 (2 つ目のパイプ文字の後) では、 **-Exclude** パラメーターの値を **false**に設定することによってコマンドレットの 2 番目の部分でフィルター処理された結果を組み込みます。

    **例:** `Get-BPAResult -Microsoft/Windows/FileServices | Where { $_.Severity -eq "Information"} | Set-BPAResult -Exclude $false`

### <a name="view-and-export-bpa-scan-results-in-windows-powershell"></a>Windows PowerShell での BPA スキャン結果の表示とエクスポート
表示し、Windows PowerShell コマンドレットを使用してスキャン結果の管理は、次の手順を参照してください。 次に示す手順のいずれかを実行するには、少なくとも 1 つのモデルまたはサブモデルに対する BPA スキャンが少なくとも 1 回実行されている必要があります。

#### <a name="BKMK_recentPS"></a>Windows PowerShell を使用して、役割の最新のスキャン結果を表示するには

1.  管理者特権で Windows PowerShell セッションを開きます。

2.  特定のモデル ID の最新のスキャン結果を取得します。 次のように入力します。モデルは*モデル ID*で表され **、enter キー**を押します。 モデル ID をコンマで区切ると、複数のモデル ID の結果を取得できます。

    `Get-BPAResult <model ID>`

    **例:** `Get-BPAResult Microsoft/Windows/DNSServer,Microsoft/Windows/FileServices`

    ロールサービスなどのモデルのサブモデルをスキャンした場合、サブモデル ID をコマンドレットに含めることで、そのサブモデルの結果のみを取得します。

    **例:** `Get-BPAResult Microsoft/Windows/FileServices -SubmodelID FSRM`

#### <a name="BKMK_formats"></a>Windows PowerShell セッションから BPA 結果を異なる形式で表示または保存するには

-   Windows PowerShell で、BPA 結果には、次に似ています。

    ```
    ResultNumber     :  14
    ResultId         :  1557706192
    modelId          :  Microsoft/Windows/FileServices
    SubmodelId       :  FSRM
    RuleId           :  16
    computerName     :  server_name1, server_name2
    Context          :  FileServices
    Source           :  server_name1
    Severity         :  Information
    Category         :  Configuration
    Title            :  Access Denied remediation requires remote management be enabled on this server
    Problem          :
    Impact           :
    Resolution       :
    compliance       :  The File Server Best Practices Analyzer scan has determined that you are in compliance with this best practice.
    help             :
    Excluded         :  False

    ```

    次のいずれかを実行します。

    -   BPA 結果を表形式にするには、前に示した例から表示する結果プロパティを追加して、次のコマンドレットを実行します。

        `Get-BPAResult model ID | format-Table -Property <property1,property2,property3...>`

        **例:** `Get-BPAResult Microsoft/Windows/FileServices | format-Table -Property modelId,SubmodelId,computerName,Source,Severity,Category,Title,Problem,Impact,Resolution,compliance,help`

    -   BPA 結果を、テキスト文字列のフィルターと、クリックすると結果の並べ替えを実行できる列見出しのある GUI ベースのグリッド ビューアー形式にするには、次のコマンドレットを実行します。

        `Get-BPAResult <model ID> | OGV`

    -   アーカイブまたは電子メール受信者に送信できる HTML ファイルに BPA 結果をエクスポートするには、次のコマンドレットを実行します。ここで、 *path*は、html 結果を保存するパスとファイル名を表します。

        `Get-BPAResult <model ID> | convertTo-Html | Set-Content <path>`

        **例:** `Get-BPAResult Microsoft/Windows/FileServices | convertTo-Html | Set-Content C:\BPAResults\FileServices.htm`

    -   BPA 結果をコンマ区切り値 (CSV) テキストファイルにエクスポートするには、次のコマンドレットを実行します。 *path*は、csv 結果の保存先のパスとテキストファイル名を表します。 CSV 結果は、スプレッドシートまたはグリッドにデータを表示するその他のプログラムと Microsoft Excel にインポートすることができます。

        `Get-BPAResult <model ID> | Export-CSV <path>`

        **例:** `Get-BPAResult Microsoft/Windows/FileServices | Export-CSV C:\BPAResults\FileServices.txt`

## <a name="see-also"></a>関連項目
[Windows Server TechCenter のベストプラクティスアナライザー解決コンテンツ](https://go.microsoft.com/fwlink/p/?LinkId=241597)
[サーバーマネージャータイルのデータのフィルター処理、並べ替え、クエリ](filter-sort-and-query-data-in-server-manager-tiles.md)の実行 
[複数のリモートサーバーを使用した管理サーバーマネージャー](manage-multiple-remote-servers-with-server-manager.md)
