---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: クラスター対応更新についてよく寄せられる質問
ms.topic: article
manager: lizross
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Windows Server でのクラスター対応更新に関してよく寄せられる質問への回答です。
ms.openlocfilehash: 0283f7f29ccc647508530d6cfdbf54b41086b90c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990907"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>クラスター対応更新: よく寄せられる質問

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md) \(CAU \) は、フェールオーバークラスター内のすべてのサーバーでソフトウェア更新を調整する機能であり、サービスの可用性に影響を与えることなく、クラスターノードの計画されたフェールオーバーを超えることはありません。 ライブマイグレーションを使用する Hyper-v、smb の透過的フェールオーバーを使用する SMB 3.x ファイルサーバーなど、継続的な可用性機能を備えた一部のアプリケーションで \( \- は \) 、CAU は自動クラスター更新を調整してサービスの可用性に影響を与えることはありません。

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU は記憶域スペースダイレクトクラスターの更新をサポートしていますか。
はい。 CAU では、展開の種類に関係なく[記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)クラスターの更新がサポートされています: ハイパー収束または収束。 具体的には、CAU オーケストレーションによって、各クラスターノードの中断が、基になるクラスター化された記憶域スペースが正常になるまで待機します。

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>Windows Server 2008 R2 または Windows 7 で CAU を使用できますか。
いいえ。 CAU は、windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10、Windows 8.1、または Windows 8 を実行しているコンピューターからのみクラスター更新操作を調整します。 更新するフェールオーバークラスターは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している必要があります。

## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU は特定のクラスター化されたアプリケーションに限定されますか。
いいえ。 CAU は、クラスター化アプリケーションの種類を選びません。 CAU は、 \- クラスタリング api と PowerShell コマンドレットの上に階層化された、外部のクラスター更新ソリューションです。 そのため、CAU は、Windows Server フェールオーバークラスターで構成されている任意のクラスター化アプリケーションの更新を調整できます。

> [!NOTE]
> 現時点では、次のクラスター化されたワークロードが CAU に対してテストおよび認定が行われています: SMB、Hyper-v \- 、DFS レプリケーション、DFS 名前空間、iSCSI、および NFS。

## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU は、Microsoft Update や Windows Update からの更新プログラムをサポートしていますか。
はい。 既定では、CAU は、 \- クラスターノードで Windows Update エージェント WUA ユーティリティ api を使用するプラグインを使用して構成され \( \) ます。 WUA インフラストラクチャは Microsoft Update を指すように構成し、 \( \) 更新のソースとして WSUS を Windows Update または Windows Server Update Services するように構成できます。

## <a name="does-cau-support-wsus-updates"></a>CAU は WSUS 更新プログラムをサポートしますか。
はい。 既定では、CAU は、 \- クラスターノードで Windows Update エージェント WUA ユーティリティ api を使用するプラグインを使用して構成され \( \) ます。 WUA インフラストラクチャは、Microsoft Update をポイントし、ローカル Windows Server Update Services \( WSUS \) サーバーを更新のソースとして Windows Update するように構成できます。

## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU で Limited Distribution Release の更新プログラムは適用されますか。
はい。 限定的な配布リリース \( LDR \) 更新プログラム (修正プログラムとも呼ばれます) は、Microsoft Update または Windows Update を通じて公開されないため、 \( \) \- 既定で CAU が使用する Windows Update エージェント WUA プラグインによってダウンロードすることはできません。

ただし、CAU には、修正プログラムの \- 更新プログラムを適用するために選択できる2番目のプラグインが含まれています。 この修正プログラムプラグインを \- カスタマイズ \- して、Microsoft 以外のドライバー、ファームウェア、BIOS の更新プログラムを適用することもできます。

## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU を使用して、累積的な更新プログラムを適用できますか。
はい。 累積的更新プログラムが一般配布リリースの更新プログラムまたは LDR 更新プログラムである場合、CAU によって適用できます。

## <a name="can-i-schedule-updates"></a>更新をスケジュールすることはできますか?
はい。 CAU は以下の更新モードをサポートしており、どちらの場合も更新をスケジューリングすることができます。

**自己 \- 更新**を使用すると、定義されたプロファイルと定期的なスケジュールに従って、クラスターを自動的に更新できます (月次のメンテナンス期間中など)。 また、必要に応じていつでも自己更新実行を開始することもでき \- ます。 自己更新モードを有効にするには、CAU のクラスター化された \- 役割をクラスターに追加する必要があります。 CAU の自己 \- 更新機能は、他のクラスター化されたワークロードと同様に動作し、更新コーディネーターコンピューターの計画フェールオーバーおよび計画外フェールオーバーとシームレスに連携できます。

**リモート \- 更新**を使用すると、Windows または windows Server を実行しているコンピューターからいつでも更新実行を開始できます。 更新実行を開始するには、クラスター対応更新ウィンドウを使用するか、 ** \- caurun** PowerShell コマンドレットを呼び出します。 リモート \- 更新は、CAU の既定の更新モードです。 クラスター ノードに属していないリモート コンピューターから、タスク スケジューラを使って、[Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) コマンドレットを目的のスケジュールで実行できます。

## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>バックアップ中に適用する更新をスケジュールすることはできますか。
はい。 CAU では、この点に制約はありません。 ただし、サーバーのバックアップ中に再起動が伴う可能性があるサーバーでソフトウェアの更新を実行する \( \) ことは、IT のベストプラクティスではありません。 CAU によるリソースのフェールオーバーとフェールバックの判断は、クラスタリング API だけで実現されている点に注意してください。CAU は、サーバーのバックアップ ステータスを関知しません。

## <a name="can-cau-work-with-configuration-manager"></a>CAU は Configuration Manager と連携できますか。
CAU は、クラスターノード上のソフトウェア更新プログラムを調整するツールであり、Configuration Manager サーバーソフトウェア更新プログラムも実行します。 これらのツールは、さまざまな Windows Server Update Services サーバーを使用するなど、データセンターの配置において同じサーバーのカバレッジが重複しないように構成することが重要です。 これにより、Configuration Manager \- 駆動型の更新にクラスター認識が組み込まれていないため、CAU を使用している目的が誤って解決されることはありません。

## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU を実行するために管理者の資格情報は必要ですか。
はい。 CAU ツールを実行するためには、ローカル サーバーに対する管理者の資格情報か、ツールが実行されるローカル サーバー (またはクライアント コンピューター) の**認証後にクライアントを偽装**というユーザー権利が必要です。 ただし、クラスター ノードでのソフトウェア更新を調整するには、すべてのノードに対するクラスター管理者の資格情報が CAU に必要です。 資格情報がなくても CAU の UI は起動できますが、クラスターインスタンスに接続して更新をプレビューまたは適用するときに、クラスター管理者の資格情報の入力を求められます。

## <a name="can-i-script-cau"></a>CAU をスクリプト化することはできますか。
はい。 CAU には、スクリプト作成オプションの豊富なセットを提供する PowerShell コマンドレットが付属しています。 CAU の UI が CAU のアクションを実行するときにも、同じコマンドレットが呼び出されます。

## <a name="what-happens-to-active-clustered-roles"></a>アクティブなクラスター化された役割はどうなりますか。

\(以前は、ノード上でアクティブになっているアプリケーションとサービスと呼ばれるクラスター化され \) た役割は、ソフトウェア更新を開始する前に他のノードにフェールオーバーします。 CAU はメンテナンス モードを使ってこれらのフェールオーバーを調整し、すべてのクラスター化されたアクティブな役割のノードは一時停止されて、ドレインされます。 ソフトウェアの更新処理が完了すると、CAU によってノードが再開され、クラスター化された役割は、更新済みのノードにフェールバックされます。 これにより、ノードに対してクラスター化された役割の配分は、クラスターに対して CAU Updating Run を実行した後も同じように維持されます。

## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU がクラスター化された役割のターゲットノードを選択する方法

CAU は、クラスタリング API を使って、フェールオーバーを調整します。 クラスタリング API の実装では、内部のメトリックや \( \) 、ターゲットノード全体のワークロードレベルなどのインテリジェントな配置ヒューリスティックに基づいて、ターゲットノードを選択します。

## <a name="does-cau-load-balance-the-clustered-roles"></a>CAU はクラスター化された役割の負荷を分散しますか。

CAU はクラスター化されたノードの負荷を分散しませんが、クラスター化された役割の分散を維持しようとします。 クラスター ノードの更新が完了すると、更新前にホストされていたクラスター化された役割のそのノードへのフェールバックが試みられます。 CAU は、クラスタリング API を使って、一時停止プロセスの最初の状態に、リソースをフェールバックします。 したがって、計画外のフェールオーバーおよび優先所有者の設定がない場合は、クラスター化された役割の配分は変化しません。

## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>ノードの更新順序はどのようにして決まるのですか。
既定では、アクティビティのレベルに基づいてノードの更新順序が選択されます。 ホストしているクラスター化された役割の少ないノードから先に更新されます。 ただし、管理者は、CAU UI で更新実行のパラメーターを指定するか、PowerShell コマンドレットを使用して、ノードを更新するための特定の順序を指定できます。

## <a name="what-happens-if-a-cluster-node-is-offline"></a>クラスターノードがオフラインの場合はどうなりますか。

更新実行を開始する管理者は、オフラインを許容するノード数のしきい値を指定できます。 したがって、クラスター ノードの一部がオフラインだったとしても、クラスターに対する CAU 更新実行は続行できます。

## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU を使用して1つのノードのみを更新できますか。
いいえ。 CAU はクラスター \- スコープ更新ツールであるため、更新するクラスターを選択できます。 単一のノードを更新する場合は、CAU は使わずに、既存のサーバー更新ツールを利用できます。

## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>Cau の外部から開始されたレポートの更新を CAU で実行できますか。
いいえ。 CAU が生成できるレポートの対象は、CAU 内から実行された Updating Run に限られます。 ただし、その後の CAU 更新実行が開始されると、非 CAU メソッドによってインストールされた更新プログラムは、 \- 各クラスターノードに適用できる追加の更新プログラムを決定するために適切に検討されます。

## <a name="can-cau-support-my-unique-it-process-needs"></a>独自の IT プロセスのニーズに合わせて CAU をサポートできますか。
はい。 それぞれの企業ユーザーが抱える IT プロセスのニーズを満たすために、CAU には次の手段が用意されています。

**スクリプト**更新実行では、更新前の \- powershell スクリプトと更新後の powershell スクリプトを指定でき \- ます。 更新前 \- スクリプトは、ノードが一時停止される前に、各クラスターノードで実行されます。 更新後 \- スクリプトは、ノードの更新プログラムのインストール後に各クラスターノードで実行されます。

> [!NOTE]
> \-更新前スクリプトと更新後スクリプトを実行する各クラスターノードには、.NET Framework 4.6 または4.5 と PowerShell をインストールする必要があり \- ます。 また、クラスターノードで PowerShell リモート処理を有効にする必要があります。 システム要件の詳細については、「[クラスター対応更新の要件とベストプラクティス](cluster-aware-updating-requirements.md)」を参照してください。

**高度な更新実行オプション**管理者はさらに、各ノードで更新プロセスが再試行される最大回数など、多数の高度な更新実行オプションから指定することもできます。 これらのオプションは、CAU UI または CAU PowerShell コマンドレットのいずれかを使用して指定できます。 カスタム設定は、更新実行プロファイルに保存し、以降の更新実行に再利用することができます。

**パブリックプラグ \- インアーキテクチャ**cau には、プラグインを登録、登録解除、および選択するための機能が含まれて \- います。 cau には2つの既定のプラグインが付属しています。 \- 1 つは \( 各クラスターノードで Windows Update エージェント WUA api を調整し \) 、もう1つはクラスターノードからアクセスできるファイル共有に手動でコピーされた修正プログラムを これらの2つのプラグインで満たすことのできない独自のニーズがある企業では、 \- \- パブリック API 仕様に従って新しい CAU プラグインを構築できます。 詳細については、「[クラスター \- 対応更新のプラグイン \- リファレンス](/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)」を参照してください。

さまざまな更新シナリオをサポートするための CAU プラグインの構成とカスタマイズの詳細につい \- ては、「[プラグインのしくみ \- ](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)」を参照してください。

## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU のプレビュー結果や更新結果をエクスポートするにはどうすればよいですか。
CAU は、コマンドラインインターフェイスと UI を通じてエクスポートオプションを提供し \- ます。

**コマンド \- ラインインターフェイスのオプション:**

-   PowerShell コマンドレットを使用して結果をプレビューする** \- causcan |Convertto-html \- Xml**。 出力結果: XML

-   PowerShell コマンドレットを使用して結果を報告する** \- caurun |Convertto-html \- Xml**。 出力結果: XML

-   PowerShell コマンドレット**Get get-caureport export-caureport | を使用して結果を報告する \-\-Get-caureport export-caureport をエクスポート**します。 出力結果: HTML、CSV

**UI オプション:**

-   **[更新プログラムのプレビュー]** 画面からレポートの結果をコピーする。 出力結果: CSV

-   **[レポートの作成]** 画面からレポートの結果をコピーする。 出力結果: CSV

-   **[レポートの作成]** 画面からレポートの結果をエクスポートする。 出力結果: HTML

## <a name="how-do-i-install-cau"></a>CAU はどうすればインストールできますか。
CAU のインストールは、フェールオーバー クラスタリング機能にシームレスに統合されています。 CAU は次のようにインストールされます。

-   クラスターノードにフェールオーバークラスタリングをインストールすると、CAU Windows Management Instrumentation \( WMI \) プロバイダーが自動的にインストールされます。

-   サーバーまたはクライアントコンピューターにフェールオーバークラスタリングツール機能がインストールされている場合は、クラスター対応更新の UI と PowerShell コマンドレットが自動的にインストールされます。

## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU では、更新されるクラスターノードで実行されているコンポーネントが必要ですか。
CAU は、クラスターノードで実行されているサービスを必要としません。 ただし、CAU には、 \( WMI プロバイダーが \) クラスターノードにインストールされているソフトウェアコンポーネントが必要です。 このコンポーネントは、フェールオーバー クラスタリング機能と一緒にインストールされます。

自己更新モードを有効にするには、CAU のクラスター化された \- 役割をクラスターに追加する必要もあります。

## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU と VMM の使用にはどのような違いがありますか。

-   \(VMM \) は、hyper-v クラスターを更新することに重点を置いていますが \- 、CAU は、hyper-v クラスターを含むサポートされている任意の種類のフェールオーバークラスターを更新することができ \- ます。 System Center Virtual Machine Manager

-   VMM には追加のライセンスが必要ですが、CAU はすべての Windows Server にライセンスが付与されます。 CAU の機能、ツール、UI は、フェールオーバー クラスタリングのコンポーネントと一緒にインストールされます。

-   既に System Center ライセンスを所有している場合は、VMM を使用して Hyper-v クラスターを更新し続けることができ \- ます。これは、統合された管理およびソフトウェア更新エクスペリエンスを提供するためです。

-   CAU は、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行するクラスターでのみサポートされます。 VMM \- では、Windows server 2008 R2 および Windows server 2008 を実行しているコンピューター上の hyper-v クラスターもサポートされます。

## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>\-自己更新用に構成されているクラスターでリモート更新を使用でき \- ますか。
はい。 自己更新構成のフェールオーバークラスターは、 \- 必要に応じてリモート更新することで更新でき \- \- ます。更新プログラムを自動的にインストールするように Windows Update が構成されている場合でも、コンピューターで Windows Update スキャンを強制的に実行することができます。 ただし、更新実行が実行されていないことを確認する必要はあります。

## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>クラスター更新設定を複数のクラスターで再利用することはできますか。
はい。 CAU には、クラスター更新時の Updating Run の動作を決める更新実行オプションが多数あります。 これらのオプションは更新実行プロファイルとして保存でき、他のクラスターで再利用することができます。 更新に関して同様のニーズを持つフェールオーバー クラスターには、保存しておいた設定を再利用することをお勧めします。 たとえば、 \- ビジネスクリティカルなサービスをサポートするすべての Microsoft SQL Server クラスターに対して、"ビジネスクリティカルな SQL Server クラスター更新実行プロファイル" を作成でき \- ます。

## <a name="where-is-the-cau-plug-in-specification"></a>CAU プラグインの仕様はどこにあり \- ますか。

-   [クラスター \- 対応更新プラグイン \- の参照](/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)

-   [クラスター対応更新プラグイン \- のサンプル](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)

## <a name="additional-references"></a>その他の参照情報

-   [クラスター \- 対応更新の概要](cluster-aware-updating.md)