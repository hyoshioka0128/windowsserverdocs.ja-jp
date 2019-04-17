---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: "クラスター対応更新のよく寄せられる質問"
ms.topic: article
ms.prod: storage-failover-clustering
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 4/28/2017
description: "Windows Server でのクラスター対応更新に関するよく寄せられる質問に対する回答。"
ms.openlocfilehash: 8417ea8b6b76e16c3f4db3bac5062d90a8da3ff2
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>クラスター対応更新: よく寄せられる質問

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)\(CAU\) はクラスター ノードの計画フェールオーバーかどうかをサービスの可用性に影響を与えないように、フェールオーバー クラスター内のすべてのサーバー上でソフトウェアの更新を調整する機能。 一部のアプリケーションで継続的可用性機能 \ CAU など (Hyper\-v とライブ マイグレーション、) または SMB 3.x のファイル サーバーと SMB 透過 Failover\、サービスの可用性に影響を及ぼさずのクラスターの自動更新をコーディネートできます。

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU は記憶域スペース ダイレクト クラスターの更新をサポートしますか。  
うん。 CAU の更新をサポートしている[記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)クラスター展開の種類に関係なく: ハイパー コンバージドまたはハイパーコンバージドします。 具体的には、CAU の指揮、基礎となるクラスター化された記憶域スペースの正常な状態にする各クラスター ノードを一時停止が待機するを確認します。

## <a name="does-cau-work-with-windows-server-2008-r2-or-windows-7"></a>Windows Server 2008 R2 または Windows 7 で CAU を使用しますか。  
違います。 CAU は、クラスターの操作を Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10、Windows 8.1、または Windows 8 を実行しているコンピューターからのみの更新を調整します。 更新されているフェールオーバー クラスターには、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行する必要があります。
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU は特定のクラスター化されたアプリケーションに制限されているか。  
違います。 CAU はクラスター化されたアプリケーションの種類に依存しません。 CAU は、上層クラスタ リング API と PowerShell のコマンドレットに位置する外部 cluster\ 更新ソリューションです。 そのため、CAU は、Windows Server フェールオーバー クラスターで構成されているあらゆるクラスター化アプリケーションの更新をコーディネートできます。  
  
> [!NOTE]  
> 現時点では、次のクラスター化されたワークロードがテストされ、認定が CAU の: SMB、Hyper\ V、DFS レプリケーション、DFS 名前空間、iSCSI、および NFS します。  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU は、Microsoft Update から更新プログラムと Windows Update をサポートしますか。  
うん。 既定では、CAU は、プラグインでは、クラスター ノードで Windows Update エージェント \(WUA\) ユーティリティ API を使用するように構成します。 更新プログラムのソースとして Microsoft Update と Windows Update、または Windows Server Update Services \(WSUS\) を指してに WUA インフラストラクチャを構成できます。  
  
## <a name="does-cau-support-wsus-updates"></a>CAU は WSUS 更新プログラムをサポートしますか。  
うん。 既定では、CAU は、プラグインでは、クラスター ノードで Windows Update エージェント \(WUA\) ユーティリティ API を使用するように構成します。 WUA インフラストラクチャは、更新プログラムのソースとして、ローカルの Windows Server Update Services \(WSUS\) サーバーまたは Microsoft Update と Windows Update をポイントするように構成できます。  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU は限定配布リリースの更新プログラムを適用できますか。  
うん。 限定配布リリース \(LDR\) 更新プログラム、修正プログラムとも呼ばれるは Microsoft Update や Windows Update で公開されないため、Windows Update エージェント \(WUA\) plug\ でダウンロードすることができません-ことで、既定で CAU を使用します。  
  
ただし、CAU は、次にプラグインに含まれる修正プログラムの更新プログラムを適用するように選択できます。 この修正プログラム プラグインでは、Microsoft 以外のドライバー、ファームウェア、および BIOS の更新プログラムを適用するもカスタマイズできます。  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU を使用して、累積的な更新プログラムを適用できますか。  
うん。 場合は、累積的な更新プログラムは、一般配布リリースの更新プログラムまたは LDR 更新プログラムには、CAU によって適用できます。  
  
## <a name="can-i-schedule-updates"></a>更新プログラムをスケジュールすることができますか。  
うん。 CAU は、どちらも更新をスケジューリングするを許可する、以下の更新モードをサポートしています。  
  
**自己更新**により、クラスターは自動的に更新される定義済みプロファイルと定期的なスケジュールに従ってなど、毎月のメンテナンス期間中にします。 必要に応じていつでも上で、自己更新実行を開始することもできます。 自己更新モードを有効にするには、クラスターに CAU のクラスター化された役割を追加する必要があります。 CAU 自己更新機能は、その他のクラスター化されたワークロードと同じようと、更新コーディネーター コンピューターの計画済みおよび計画外フェールオーバーとシームレスに連携できます。  
  
**Remote\ 更新**Windows または Windows Server を実行するコンピューターからいつでも更新実行を開始することができます。 更新またはを使用して、クラスター対応更新] ウィンドウの実行を開始することができます、**Invoke\ CauRun** PowerShell コマンドレット。 Remote\ 更新は、既定の cau 更新モードです。 タスク スケジューラを使用してを実行することができます、[Invoke-caurun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun)コマンドレットを 1 つのクラスター ノードではないリモート コンピューターから目的のスケジュールします。  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>バックアップ中に適用する更新プログラムをスケジュールすることができますか。  
うん。 CAU が適用されません制約はすべてこの点です。 ただし、ソフトウェアの更新を実行するサーバーで \ (関連付けられている潜在的な restarts\) で、サーバーのバックアップ中に進行状況は IT のベスト プラクティスです。 CAU は、クラスタ リング リソースのフェールオーバーとフェールバック; 決定 API でのみことに注意してください。したがって、CAU では、サーバー バックアップの状態の認識しません。  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>CAU は System Center Configuration Manager でを使用できますか。  
CAU はクラスター ノード上のソフトウェアの更新を調整するためのツールと Configuration Manager もサーバーのソフトウェア更新プログラムを実行します。 ことが重要などのさまざまな Windows Server Update Services サーバーを使用して、任意のデータ センター展開内の同じサーバーのカバレッジが重複している必要があるないように、これらのツールを構成します。 これにより、せっかくの CAU いないおろそかにする、クラスターが認識を組み込む構成 Manager\ 駆動を更新しないためです。  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU を実行する管理者の資格情報が必要ですか。  
うん。 CAU CAU ツールを実行するためには、ローカル サーバーに管理者の資格情報が必要なまたは、必要な**認証後にクライアントを偽装**ユーザー権限をローカル サーバーまたはが実行されているクライアント コンピューター。 ただし、CAU のクラスター ノードにソフトウェアの更新を調整するすべてのノードに対するクラスター管理者の資格情報が必要です。 資格情報がない、CAU UI を起動できるをプレビューまたは適用更新プログラムのクラスタ インスタンスに接続するときにクラスターの管理者資格情報を要求されます。  
  
## <a name="can-i-script-cau"></a>CAU のスクリプトはできますか。  
うん。 CAU 豊富なスクリプト オプションを提供する PowerShell コマンドレットが用意されています。 これらは、同じコマンドレット、CAU UI が CAU のアクションを実行するために呼び出すことです。  

## <a name="what-happens-to-active-clustered-roles"></a>アクティブなクラスター化された役割はどうなりますか。

クラスター化された役割 \ (アプリケーションとサービスと呼ばれていました) ノード上でアクティブである、ソフトウェアの更新を開始する前に、その他のノードにフェールオーバーします。 CAU はメンテナンス モードは一時停止されて、ドレインのすべてのアクティブなクラスター化された役割のノードを使用してこれらのフェールオーバーを調整します。 ソフトウェアの更新が完了すると、CAU は、ノードを再開し、クラスター化された役割は、更新済みのノードにフェールバックします。 これにより、ノードを基準にして、クラスター化された役割の配分は変わりません、CAU Updating run を実行するクラスター間でします。  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU のクラスター化された役割のターゲット ノードへの選択

CAU は、クラスタ リング API、フェールオーバーを調整するために依存します。 クラスタ リング API の実装では、ターゲット ノードを選択内部的なメトリックとインテリジェント配置のヒューリスティックに依存して \ (ワークロード levels\) など、ターゲット ノード間します。  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>負荷分散クラスター化された役割は行わですか。

CAU 負荷を分散クラスターのノードがクラスター化された役割の配分を保持するしようとしません。 試行が失敗する CAU では、クラスター ノードの更新が完了したら、背面にそのノードへのクラスター化された役割がホストされていた。 CAU は、クラスタ リング API を一時停止プロセスの最初のリソースをフェールバックします。 したがっての計画外フェールオーバーおよび優先所有者の設定がない場合、クラスター化された役割の配分は変化します。  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>CAU がノードの更新順序を選択する方法  
既定では、CAU は、アクティビティのレベルに基づいてノードの更新順序で選択します。 最小限のクラスター化された役割をホストしているノードが最初に更新します。 ただし、管理者は、CAU UI で更新実行のパラメーターを指定するか、PowerShell コマンドレットを使用して、ノードの更新の特定の順序を指定することができます。  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>クラスター ノードがオフラインにするとどうなりますか。

更新実行が開始した管理者は、使用可能なしきい値をオフラインにできるノードの数を指定できます。 そのため、更新実行を続行できます、クラスターの場合でも、すべてのクラスター ノードがオンラインではありません。  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU を使用して、1 つのノードのみを更新するのにことができますか。  
違います。 CAU は、cluster\ スコープ更新ツール、ため、クラスターを更新する] を選択することのみできます。 1 つのノードを更新するには、CAU とは別のツールの更新の既存のサーバーを使用することができます。  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>CAU が CAU 以外から開始する更新プログラムを報告できますか。  
違います。 CAU には、のみレポート Updating run を実行 CAU 内から開始することができます。 ただし、以降 CAU 更新実行を開始すると、CAU 以外の方法でインストールされた更新プログラムきちんと考慮されます。各クラスター ノードに適用される可能性のある追加の更新プログラムを確認します。  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>CAU のサポート [抱える IT プロセスが必要なことができますか?  
うん。 CAU には、企業のお客様の一意の IT プロセスのニーズに合わせて柔軟に次のディメンションが用意されています。  
  
**スクリプト**ファイル更新の PowerShell スクリプトと post\ 更新 PowerShell スクリプトを指定、更新実行できます。 ファイル更新スクリプトは、ノードが一時停止前に、各クラスター ノードで実行されます。 Post\ 更新スクリプトは、ノードの更新プログラムのインストール後に、各クラスター ノードで実行されます。  
  
> [!NOTE]  
> .NET framework 4.6 または 4.5 および PowerShell は、ファイルの更新および post\ 更新スクリプトを実行する各クラスター ノードにインストールする必要があります。 クラスター ノード上で PowerShell リモート処理を有効にする必要があります。 詳しいシステム要件は、次を参照してください。[要件とクラスター対応更新のベスト プラクティス](cluster-aware-updating-requirements.md)します。  
  
**更新実行オプションを高度な**、管理者は、多数の各ノードに更新プロセスを再試行の最大回数などの高度な更新実行オプションのセットを追加指定できます。 CAU UI または CAU の PowerShell コマンドレットを使用してこれらのオプションを指定することができます。 これらのカスタム設定を更新実行プロファイルに保存し、以降の更新実行に再利用します。  
  
**公開プラグインをアーキテクチャ**CAU には、登録、登録解除、機能が含まれますと選択プラグイン該当 CAU 付属して 2 つの既定のプラグインを使用します。いずれかの座標を各クラスター ノードで Windows Update エージェント \(WUA\) API。2 つ目には、クラスター ノードからアクセスできるファイル共有に手動でコピーされる修正プログラムが適用されます。 これら 2 つのプラグインのプラグインで満たすことができない独自のニーズを企業には、企業は、公開されている API 仕様に従ってプラグインに新しい CAU を構築できます。 詳細については、次を参照してください。[Cluster\ 対応更新プラグインのリファレンス](http://msdn.microsoft.com/library/hh418084(VS.85).aspx)します。  
  
構成して、CAU のカスタマイズについてはさまざまなをサポートするプラグイン アドイン更新シナリオを参照してください[プラグイン プラグインのしくみ](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)します。  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU のプレビューをエクスポートし、結果を更新する方法は?  
CAU には、コマンド ライン インターフェイスと UI からエクスポート オプションが用意されています。  
  
**コマンド ライン インターフェイスのオプション:**  
  
-   PowerShell コマンドレットを使用して結果をプレビュー **Invoke\ CauScan |ConvertTo\ Xml**します。 出力: XML  
  
-   PowerShell コマンドレットを使用して結果を報告**Invoke\ CauRun |ConvertTo\ Xml**します。 出力: XML  
  
-   PowerShell コマンドレットを使用して結果を報告**Get\ CauReport |では CauReport**します。 出力結果: HTML、CSV  
  
**UI オプション:**  
  
-   コピーからレポートの結果、**更新プログラムのプレビュー**画面です。 出力: CSV  
  
-   コピーからレポートの結果、**レポートを生成する**画面です。 出力: CSV  
  
-   レポートの結果をエクスポート、**レポートを生成する**画面です。 出力: HTML  
  
## <a name="how-do-i-install-cau"></a>CAU のインストール方法  
CAU のインストールは、フェールオーバー クラスタ リング機能にシームレスに統合されています。 CAU は次の手順としてインストールされます。  
  
-   クラスター ノードには、フェールオーバー クラスタ リングをインストールするときに、CAU Windows Management Instrumentation \(WMI\) プロバイダーが自動的にインストールします。  
  
-   フェールオーバー クラスタ リング ツール機能がサーバーまたはクライアント コンピューターにインストールされると、クラスター対応更新の UI と PowerShell のコマンドレットが自動的にインストールします。
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU には更新されているクラスター ノードで実行されているコンポーネントが必要か。  
CAU のクラスター ノードで実行されているサービスを必要はありません。 ただし、CAU には、ソフトウェア コンポーネント必要があります。\ (WMI プロバイダー) は、クラスター ノードにインストールします。 このコンポーネントには、フェールオーバー クラスタ リング機能がインストールされます。  
  
自己更新モードを有効にするには、CAU のクラスター化された役割をクラスターに追加もする必要があります。  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU と VMM の使用の違いは何ですか。  
  
-   CAU Hyper\ V クラスターも含め、サポートされているフェールオーバー クラスターの任意の型を更新できますが、system Center Virtual Machine Manager \(VMM\) が唯一の Hyper\ V クラスターを更新する方法のフォーカスしています。  
  
-   VMM は、CAU は、すべての Windows Server のライセンスは、追加のライセンスを要求します。 CAU の機能、ツール、および UI は、フェールオーバー クラスタ リングのコンポーネントと共にインストールされます。  
  
-   System Center のライセンスを既に所有している場合、VMM を使用して、統合された管理とソフトウェア更新エクスペリエンスが提供されるため、Hyper\ V クラスターを更新する続行することができます。  
  
-   CAU は、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行しているクラスターでのみサポートされます。 VMM では、Windows Server 2008 R2 および Windows Server 2008 を実行するコンピューターで Hyper\ V クラスターもサポートします。  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>使用できます remote\ 更新に構成されているクラスターの自己更新しますか。  
うん。 更新プログラムを自動的にインストールする Windows Update が構成されている場合でも、コンピューターで Windows Update スキャンはいつでもを強制でき、同様、remote\ 更新オンデマンド、を通じて自己更新の構成でフェールオーバー クラスターを更新できます。 ただし、こと、更新実行されていない場合の進行状況を確認する必要があります。  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>クラスター間でクラスター更新設定再利用できますか。  
うん。 CAU には、クラスターを更新するときの動作、Updating Run を決定する更新実行オプションの数がサポートしています。 これらのオプションは、更新実行プロファイル、として保存することし、他のクラスターで再利用することができます。 保存する更新と同様のニーズを持つフェールオーバー クラスター全体の設定を再利用することをお勧めします。 たとえば、「Business\ クリティカルな SQL Server クラスター更新実行プロファイル」business\ 重要なサービスをサポートするすべての Microsoft SQL Server クラスターを作成する場合があります。  
  
## <a name="where-is-the-cau-plug-in-specification"></a>CAU プラグインを仕様はどこでしょう?  
  
-   [Cluster\ 対応更新プラグインのリファレンス](http://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [クラスター対応更新プラグインのサンプル](http://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>参照してください。  
  
-   [Cluster\ 対応更新の概要](cluster-aware-updating.md)  
  
