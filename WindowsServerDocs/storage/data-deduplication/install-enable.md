---
ms.assetid: 07d6b251-c492-4d9f-bcc4-031023695b24
title: "データ重複除去のインストールと有効化"
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
description: "Windows Server でのデータ重複除去のインストール方法、ワークロードがデータ重複除去に適切であるかどうかを判断する、ボリュームでデータ重複除去を有効にする"
ms.openlocfilehash: 153b064b158028c696bad4eeb00764d3e10822e1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="install-and-enable-data-deduplication"></a>データ重複除去のインストールと有効化
> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、[データ重複除去](overview.md)のインストール、重複除去のワークロードの評価、および特定のボリュームでのデータ重複除去の有効化の方法について説明します。

> [!Note]  
> フェールオーバー クラスター内でデータ重複除去を実行する場合は、クラスター内のすべてのノードに、データ重複除去のサーバーの役割がインストールされている必要があります。

## <a id="install-dedup"></a>データ重複除去のインストール
> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334) には、信頼性についての重要な修正データを含め、重複除去に関する修正のロールアップが含まれているため、Windows Server 2016 でデータ重複除去を使う場合はインストールすることを強くお勧めします。

### <a id="install-dedup-via-server-manager"></a>サーバー マネージャーを使用してデータ重複除去をインストールする
1. 役割と機能の追加ウィザードで **[サーバーの役割]** を選択し、**[データ重複除去]** をオンにします。  
![サーバー マネージャーを使用したデータ重複除去のインストール: [サーバーの役割] で [データ重複除去] をオンにする](media/install-dedup-via-server-manager-1.png)
2. **[インストール]** がアクティブになるまで **[次へ]** をクリックし、**[インストール]**をクリックします。  
![サーバー マネージャーを使用したデータ重複除去のインストール: [インストール] をクリック](media/install-dedup-via-server-manager-2.png)

### <a id="install-dedup-via-powershell"></a>PowerShell を使用してデータ重複除去をインストールする
データ重複除去をインストールするには、管理者として次の PowerShell コマンドを実行します。  
`Install-WindowsFeature -Name FS-Data-Deduplication`

Nano Server のインストールにデータ重複除去をインストールするには:

1. [Nano Server の概要](../../get-started/getting-started-with-nano-server.md)に関する記事の説明に従ってインストールした 'Storage' に、Nano Server のインストールを作成します。
2. Nano Server ではないモードで Windows Server 2016 を実行しているサーバー、または[リモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520) (RSAT) がインストールされている Windows PC から、Nano Server インスタンスへの明示的な参照を使用して、データ重複除去をインストールします ('MyNanoServer' を Nano Server インスタンスの実名に置き換えてください)。  
    ```PowerShell
    Install-WindowsFeature -ComputerName <MyNanoServer> -Name FS-Data-Deduplication
    ```  
    <br />
    **-- または --**
    <br />
    PowerShell のリモート処理を使用して Nano Server インスタンスにリモートで接続し、DISM を使用してデータ重複除去をインストールします。  
    
    ```PowerShell
    Enter-PSSession -ComputerName MyNanoServer 
    dism /online /enable-feature /featurename:dedup-core /all
    ```

## <a id="enable-dedup"></a>データ重複除去の有効化
### <a id="enable-dedup-candidate-workloads"></a>データ重複除去の候補となるボリュームの決定
データ重複除去を使用すると、重複データによって消費されるディスク領域を削減して、サーバー アプリケーションのデータ消費コストを効率よく最小限に抑えることができます。 重複除去を有効にする前に、記憶域のパフォーマンスを最大限に活かすことができるようにワークロードの特性を理解する必要があります。 考慮すべきの 2 つのクラスのワークロードがあります。

* *"推奨ワークロード"*: 重複除去によって大きなメリットが得られるデータセットと、リソース消費パターンがデータ重複除去の処理後モデルに適合しているデータセットの両方が含まれることが実証されているワークロード。 次のワークロードに対しては、常に[データ重複除去を有効](install-enable.md#enable-dedup-lights-on)にすることをお勧めします。
    * チーム共有、ユーザー ホーム フォルダー、ワーク フォルダー、ソフトウェア開発共有などの、共有のための汎用ファイル サーバー (GPFS)
    * 仮想デスクトップ インフラストラクチャ (VDI) サーバー
    * [Microsoft Data Protection Manager (DPM)](https://technet.microsoft.com/library/hh758173.aspx) などの仮想化バックアップ アプリケーション
* 重複除去によってメリットを得る可能性があるものの、常に重複除去に適しているとは限らないワークロード。 たとえば、以下のワークロードでは重複除去が有効な可能性はありますが、まず重複除去のメリットを評価する必要があります。
    * 汎用 Hyper-V ホスト
    * SQL Server
    * 基幹業務 (LOB) サーバー

### <a id="enable-dedup-evaluating-sometimes-workloads"></a>データ重複除去のワークロードの評価
> [!Important]  
> 推奨ワークロードを実行している場合は、このセクションをスキップして、ワークロードの[データ重複除去の有効化](install-enable.md#enable-dedup-lights-on)に進むことができます。

ワークロードで重複除去によるメリットが得られるかどうかを判定するには、次の質問に回答します。 よくわからないワークロードの場合は、ワークロードのテスト データセットにデータ重複除去をパイロット展開し、そのパフォーマンスを確認することを検討してください。

1. **重複除去の有効化のメリットを得るのに十分な重複がワークロードのデータセットに含まれていますか。**  
    ワークロードのデータ重複除去を有効にする前に、Data Deduplication Savings Evaluation Tool (DDPEval) を使用して、ワークロードのデータセットに含まれている重複の量を調査します。 データ重複除去をインストールすると、このツールは `C:\Windows\System32\DDPEval.exe` にあります。 DDPEval では、直接接続されているボリューム (ローカル ドライブやクラスターの共有ボリュームなど) と、(マップの有無にかかわらず) ネットワーク共有の最適化の可能性を評価できます。  
    &nbsp;   
    DDPEval.exe を実行すると、以下のような出力が返されます。  
    &nbsp;  
    `Data Deduplication Savings Evaluation Tool`  
    `Copyright 2011-2012 Microsoft Corporation.  All Rights Reserved.`    
    &nbsp;   
    `Evaluated folder: E:\Test`     
    `Processed files: 34`  
    `Processed files size: 12.03MB`  
    `Optimized files size: 4.02MB`  
    `Space savings: 8.01MB`  
    `Space savings percent: 66`  
    `Optimized files size (no compression): 11.47MB`  
    `Space savings (no compression): 571.53KB`  
    `Space savings percent (no compression): 4`  
    `Files with duplication: 2`  
    `Files excluded by policy: 20`  
    `Files excluded by error: 0`  

2. **データセットに対するワークロードの I/O パターンはどのようなものですか。 ワークロードのパフォーマンスはどのようになりますか。**  
     データ重複除去によるファイルの最適化は、ディスクへのファイルの書き込み時ではなく定期的に行われます。 このため、ワークロードで想定される重複除去対象ボリュームの読み取りパターンを調査する必要があります。 データ重複除去では、ファイル コンテンツをチャンク ストアに移動してから、チャンク ストアをできる限りファイル別に整理しようとするため、読み取り操作のパフォーマンスはファイルの順次範囲に対して適用した場合に最高となります。  

    データベースでは、実行される可能性があるすべてのクエリに対してデータベース レイアウトが最適ではない可能性があります。したがって、データベースのようなワークロードでは、通常、順次読み取りパターンよりもランダム読み取りパターンの方が多くなります。 チャンク ストアのセクションはボリューム全体に存在することがあるため、データベース クエリのチャンク ストア内のデータ範囲にアクセスすると、待機時間が増加する可能性があります。 高パフォーマンス ワークロードはこの待機時間の増加の影響を特に受けやすいのですが、他のデータベースのようなワークロードには影響が特に生じないものもあります。

    > [!Note]  
    > こうした懸念の主な対象は、従来の回転記憶域メディア (別名ハード ディスク ドライブ (HDD)) から成るボリュームの記憶域ワークロードです。 フラッシュ メディアの特徴の 1 つは、ディスクのどの場所へのアクセス時間も同じであることです。そのため、オールフラッシュ記憶域インフラストラクチャ (別名ソリッド ステート ドライブ (SSD)) では、ランダム IO パターンの影響が低くなります。 したがって、オールフラッシュ メディアに格納されているワークロードのデータセットの読み取りでは、重複除去によって従来の回転記憶域メディアと同じ長さの待機時間が発生することはありません。

3. **ワークロードは、サーバーのどのようなリソースを必要としますか。**  
    データ重複除去では処理後モデルが使用されることから、データ重複除去が[最適化ジョブと他のジョブ](understand.md#job-info)を完了するのに十分なシステム リソースが定期的に必要になります。 つまり、夜間や週末などにアイドル時間があるワークロードは重複除去に適していますが、一日中実行されるワークロードは適さない可能性があります。 アイドル時間がないワークロードでも、必要とするサーバー リソースが多くない場合は、重複除去に適している可能性があります。

### <a id="enable-dedup-lights-on"></a>データ重複除去の有効化
データ重複除去を有効にする前に、ワークロードに最もよく似た[使用法の種類](understand.md#usage-type)を選択する必要があります。 データ重複除去には 3 つの使用法の種類が含まれています。

* [既定](understand.md#usage-type-default) - 汎用ファイル サーバー用
* [Hyper-V](understand.md#usage-type-hyperv) - VDI サーバー専用
* [バックアップ](understand.md#usage-type-backup) - 仮想化バックアップ アプリケーション ([Microsoft DPM](https://technet.microsoft.com/library/hh758173.aspx) など) 専用

#### <a id="enable-dedup-via-server-manager"></a>サーバー マネージャーを使用してデータ重複除去を有効にする
1. サーバー マネージャーで **[ファイル サービスと記憶域サービス]** を選択します。  
![[ファイル サービスと記憶域サービス] をクリック](media/enable-dedup-via-server-manager-1.PNG)
2. **[ファイル サービスと記憶域サービス]** で **[ボリューム]** をクリックします。  
![[ボリューム] をクリック](media/enable-dedup-via-server-manager-2.png)
3. 目的のボリュームを右クリックして、**[データ重複除去の構成]** を選択します。  
![[データ重複除去の構成] をクリック](media/enable-dedup-via-server-manager-3.png)
4. ドロップダウン ボックスから目的とする**使用法の種類**を選択して、**[OK]** を選択します。  
![ドロップダウン ボックスからの目的とする使用法の種類の選択](media/enable-dedup-via-server-manager-4.png)
5. 推奨ワークロードを実行している場合は、これで終了です。 他のワークロードの場合は、「[他の考慮事項](#enable-dedup-sometimes-considerations)」を参照してください。

> [!Note]  
> ファイル拡張子やフォルダーの除外、および重複除去スケジュールの選択 (これを実行する理由など) の詳細は、[データ重複除去の構成](advanced-settings.md)に関するページに記載されています。

#### <a id="enable-dedup-via-powershell"></a>PowerShell を使用してデータ重複除去を有効にする
1. 管理者のコンテキストで、次の PowerShell コマンドを実行します。  
    ```PowerShell
    Enable-DedupVolume -Volume <Volume-Path> -UsageType <Selected-Usage-Type>
    ```

2. 推奨ワークロードを実行している場合は、これで終了です。 他のワークロードの場合は、「[他の考慮事項](#enable-dedup-sometimes-considerations)」を参照してください。

> [!Note]  
> データ重複除去の PowerShell コマンドレット ([`Enable-DedupVolume`](https://technet.microsoft.com/library/hh848441.aspx) など) は、`-CimSession` パラメーターで CIM セッションを指定するとリモートで実行できます。 これは、Nano Server インスタンスに対してデータ重複除去の PowerShell コマンドレットをリモートで実行するのに特に役立ちます。 新しい CIM セッションを作成するには、[`New-CimSession`](https://technet.microsoft.com/library/jj590760.aspx) を実行します。

#### <a id="enable-dedup-sometimes-considerations"></a>他の考慮事項
> [!Important]  
> 推奨ワークロードを実行している場合、このセクションはスキップできます。

* データ重複除去の各使用方法の種類では推奨ワークロードに適した既定値が提供されますが、ほかのワークロードにとってもこれらの値は適切な出発点となります。 推奨ワークロードではないワークロードの場合は、重複除去のパフォーマンスを向上させるために、[データ重複除去の詳細設定](advanced-settings.md)を変更することもできます。
* ワークロードに必要なサーバー リソースが多い場合は、データ重複除去ジョブが[そのワークロードがアイドルであると見込まれる時間中に実行されるようにスケジュールする必要があります](advanced-settings.md#modifying-job-schedules-change-schedule)。 業務が予定されている時間中にデータ重複除去を実行すると仮想メモリが不足する可能性があるため、ハイパーコンバージド ホストで重複除去を実行する場合には、これは特に重要です。
* ワークロードに必要なリソースがそれほど多くない場合、またはワークロードの要求を満たすよりも最適化ジョブを完了する方が重要である場合は、[データ重複除去ジョブのメモリ、CPU、および優先順位を調整できます](advanced-settings.md#modifying-job-schedules)。

## <a id="faq"></a>よく寄せられる質問 (FAQ)
**X ワークロードのデータセットに対してデータ重複除去を実行したいのですが、 これはサポートされていますか。**  
[データ重複除去との同時使用に未対応であることが確認されている](interop.md)ワークロードを除いて、どんなワークロードであってもデータ重複除去のデータの整合性は完全にサポートされています。 推奨ワークロードについてはパフォーマンスもサポートされます。 他のワークロードのパフォーマンスは、サーバー上での操作に大きく左右されます。 お客様のワークロードにデータ重複除去が及ぼすパフォーマンス上の影響を確認して、そのワークロードに適しているかどうかを判断してください。

**重複除去されるボリュームには、どのようなボリューム サイズ設定が必要ですか。**  
Windows Server 2012 および Windows Server 2012 R2 では、データ重複除去がボリュームのチャーンについていけるように、ボリュームのサイズを注意して設定する必要があります。 一般的には、高チャーンのワークロードで重複除去されるボリュームの平均最大サイズは 1 ～ 2 TB であり、推奨される絶対最大サイズは 10 TB です。 Windows Server 2016 では、これらの制約がなくなりました。 詳細については、「[データ重複除去の新機能](whats-new.md#large-volume-support)」を参照してください。

**推奨ワークロードの場合、スケジュールなどのデータ重複除去設定を変更する必要はありますか。**  
いいえ。推奨ワークロードに適した既定値を設定するための[使用法の種類](understand.md#usage-type)が用意されています。

**データ重複除去にはどれだけのメモリが必要ですか。**  
最小でも、データ重複除去では 300 MB に加えて、1 TB の論理データにつき 50 MB が必要です。 たとえば、10 TB のボリュームを最適化する場合は、最小で 800 MB のメモリが重複除去に割り当てられている必要があります (`300 MB + 50 MB * 10 = 300 MB + 500 MB = 800 MB`)。 データ重複除去では、この少量のメモリでボリュームを最適化できますが、そのようなリソース制約があると、データ重複除去ジョブの速度が低下します。

データ重複除去を最適に行うには、1 TB の論理データにつき 1 GB のメモリが必要です。 たとえば、10 TB のボリュームを最適化する場合、好ましい状況とするには、10 GB のメモリが重複除去に割り当てられている必要があります (`1 GB * 10`)。 この比率であれば、データ重複除去ジョブのパフォーマンスを最大化することができます。

**データ重複除去にはどれだけの記憶域が必要ですか。**  
Windows Server 2016 において、データ重複除去では 64 TB までのボリューム サイズをサポートできます。 詳細については、「[What's New in Data Deduplication (データ重複除去の新機能)](whats-new.md#large-volume-support)」を参照してください。
