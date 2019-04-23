---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: クラスター対応更新 - よく寄せられる質問
ms.topic: article
ms.prod: windows-server-threshold
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Windows server クラスター対応更新の詳細についてよく寄せられる質問に対する回答。
ms.openlocfilehash: f9009811093823554f16295cc1205f1b99ead93f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882523"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>クラスター対応更新:よく寄せられる質問

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md) \(CAU\)より、計画的フェールオーバー クラスター ノードのサービスの可用性に影響を与えない方法でフェールオーバー クラスター内のすべてのサーバー上で更新プログラム ソフトウェアを調整する機能です。 一部のアプリケーションを継続的可用性を特徴と\(ハイパースレッディングなど\-V は、ライブ マイグレーション、または SMB 3.x ファイル サーバーと SMB 透過フェールオーバーを使った\)CAU が影響を及ぼさずにクラスターの自動更新を調整することができますサービスの可用性。

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU は、記憶域スペース ダイレクト クラスターの更新をサポートしますか。  
[はい]。 CAU の更新をサポートしている[記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)クラスター展開の種類に関係なく: ハイパー コンバージドまたは集約型します。 具体的には、CAU のオーケストレーションは、正常な状態にする基になるクラスター化された記憶域スペースを各クラスター ノードの中断が待機するようにします。

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>Windows Server 2008 R2 または Windows 7 で CAU を使用できますか。  
いいえ。 CAU は、クラスターの更新の Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10、Windows 8.1、または Windows 8 を実行しているコンピューターからのみ操作を調整します。 更新されているフェールオーバー クラスターには、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行する必要があります。
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU は、特定のクラスター化されたアプリケーションに制限されますか。  
いいえ。 CAU は、クラスター化アプリケーションの種類を選びません。 CAU は、外部のクラスター\-クラスタ リング Api と PowerShell コマンドレットの上に構築されたソリューションを更新します。 そのため、CAU では、Windows Server フェールオーバー クラスターで構成されているあらゆるクラスター化アプリケーションの更新を調整できます。  
  
> [!NOTE]  
> 現時点では、次のクラスター化されたワークロードがテストされ、CAU 用に認定。SMB、ハイパースレッディング\-V、DFS レプリケーション、DFS 名前空間、iSCSI、および NFS です。  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU は、Microsoft Update や Windows Update からの更新プログラムをサポートしていますか。  
[はい]。 プラグがある、既定では、CAU が構成されている\-を使用して、Windows Update エージェント\(WUA\)クラスター ノードでユーティリティ Api。 WUA インフラストラクチャは、Windows Server Update Services または Microsoft Update と Windows Update をポイントするように構成できる\(WSUS\)更新プログラムのソースとして。  
  
## <a name="does-cau-support-wsus-updates"></a>CAU は WSUS 更新プログラムをサポートしますか。  
[はい]。 プラグがある、既定では、CAU が構成されている\-を使用して、Windows Update エージェント\(WUA\)クラスター ノードでユーティリティ Api。 WUA インフラストラクチャは、ローカルの Windows Server Update Services または Microsoft Update と Windows Update をポイントするように構成できる\(WSUS\)サーバー更新プログラムのソースとして。  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU で Limited Distribution Release の更新プログラムは適用されますか。  
[はい]。 限定配布リリース\(LDR\) Microsoft Update や Windows Update では、Windows Update エージェントをダウンロードすることができないため、修正プログラムとも呼ばれる、更新プログラムは公開されない\(WUA\) プラグイン\-ことで、既定で CAU を使用します。  
  
ただし、CAU には、2 番目のプラグインが含まれます。\-ことで、修正プログラムの更新の適用を選択することができます。 この修正プログラム プラグイン\-でカスタマイズすることも非適用\-Microsoft ドライバー、ファームウェア、および BIOS の更新プログラム。  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU を使用して、累積的な更新プログラムを適用できますか。  
[はい]。 累積的更新プログラムが一般配布リリースの更新プログラムまたは LDR 更新プログラムである場合、CAU によって適用できます。  
  
## <a name="can-i-schedule-updates"></a>更新プログラムをスケジュールすることができますか。  
[はい]。 CAU は以下の更新モードをサポートしており、どちらの場合も更新をスケジューリングすることができます。  
  
**Self\-更新**自己更新する定義済みのプロファイルと定期的なスケジュールに従ってなど、月次のメンテナンス期間中にクラスターを使用します。 自己を開始することもできます。\-、いつでもオンデマンドで実行を更新しています。 自己を有効にする\-モードを更新する必要があります、CAU のクラスター化された役割クラスターに追加します。 CAU 自己\-などその他のクラスター化されたワークロードを実行機能を更新し、シームレスに、更新コーディネーター コンピューターのフェールオーバーや計画外フェールオーバーで使用します。  
  
**リモート\-更新**Windows または Windows Server を実行するコンピューターからいつでも更新実行を開始することができます。 更新またはを使用して、クラスター対応更新 ウィンドウから実行を開始することができます、 **Invoke\-CauRun** PowerShell コマンドレット。 リモート\-の CAU 更新モードの既定の更新です。 クラスター ノードに属していないリモート コンピューターから、タスク スケジューラを使って、 [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) コマンドレットを目的のスケジュールで実行できます。  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>バックアップ中に適用する更新プログラムをスケジュールすることができますか。  
[はい]。 CAU は、この点ですべての制約を適用しません。 ただし、ソフトウェア更新プログラムを実行するサーバーで\(関連付けられている可能性があります再起動\)進行状況が IT のベスト プラクティスではないサーバーのバックアップ中にします。 CAU によるリソースのフェールオーバーとフェールバックの判断は、クラスタリング API だけで実現されている点に注意してください。CAU は、サーバーのバックアップ ステータスを関知しません。  
  
## <a name="can-cau-work-with-system-center-configuration-manager"></a>CAU は System Center Configuration Manager を操作できますか。  
CAU はクラスター ノードでソフトウェア更新プログラムを調整するツールと Configuration Manager では、サーバー ソフトウェアの更新も実行します。 別の Windows Server Update Services サーバーを使用するなど、任意のデータ センター展開内の同じサーバーのカバレッジの重複があるないように、これらのツールを構成するのには重要です。 これにより、CAU を使用して、目的がおろそかにするではないことため、Configuration Manager\-クラスターの認識は取り込まれません駆動型を更新しています。  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU を実行するために管理者の資格情報は必要ですか。  
[はい]。 CAU ツールを実行するためには、ローカル サーバーに対する管理者の資格情報か、ツールが実行されるローカル サーバー (またはクライアント コンピューター) の **認証後にクライアントを偽装** というユーザー権利が必要です。 ただし、クラスター ノードでのソフトウェア更新を調整するには、すべてのノードに対するクラスター管理者の資格情報が CAU に必要です。 CAU UI は、資格情報がなくても起動できます、プレビューまたは更新プログラムの適用、クラスター インスタンスに接続するときに、クラスター管理者の資格情報の要求されます。  
  
## <a name="can-i-script-cau"></a>CAU をスクリプトすることができますか。  
[はい]。 CAU 機能豊富なスクリプト作成オプションのセットを提供する PowerShell コマンドレットが付属します。 CAU の UI が CAU のアクションを実行するときにも、同じコマンドレットが呼び出されます。  

## <a name="what-happens-to-active-clustered-roles"></a>アクティブなクラスター化された役割はどうなるか

クラスター化された役割\(アプリケーションとサービスと呼ばれていました\)ノード上でアクティブには、ソフトウェアの更新を開始する前に、その他のノードにフェールオーバーします。 CAU はメンテナンス モードを使ってこれらのフェールオーバーを調整し、すべてのクラスター化されたアクティブな役割のノードは一時停止されて、ドレインされます。 ソフトウェアの更新処理が完了すると、CAU によってノードが再開され、クラスター化された役割は、更新済みのノードにフェールバックされます。 これにより、ノードに対してクラスター化された役割の配分は、クラスターに対して CAU Updating Run を実行した後も同じように維持されます。  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU のクラスター化された役割のターゲット ノードへの選択

CAU は、クラスタリング API を使って、フェールオーバーを調整します。 クラスタ リング API の実装は、内部的なメトリックとインテリジェントな配置のヒューリスティックに依存することにより、ターゲット ノードを選択します\(ワークロード レベルなど\)ターゲット ノード間で。  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>負荷は、クラスター化された役割を分散しますか。

CAU に負荷分散クラスターのノードがクラスター化された役割の配分を保持しようを使用しません。 クラスター ノードの更新が完了すると、更新前にホストされていたクラスター化された役割のそのノードへのフェールバックが試みられます。 CAU は、クラスタリング API を使って、一時停止プロセスの最初の状態に、リソースをフェールバックします。 したがって、計画外のフェールオーバーおよび優先所有者の設定がない場合は、クラスター化された役割の配分は変化しません。  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>ノードの更新順序はどのようにして決まるのですか。  
既定では、アクティビティのレベルに基づいてノードの更新順序が選択されます。 ホストしているクラスター化された役割の少ないノードから先に更新されます。 ただし、管理者は、CAU UI で更新実行のパラメーターを指定することで、または PowerShell コマンドレットを使用して、ノードを更新するための特定の順序を指定できます。  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>クラスター ノードがオフラインとどうなりますか。

更新実行を開始する管理者は、オフラインを許容するノード数のしきい値を指定できます。 したがって、クラスター ノードの一部がオフラインだったとしても、クラスターに対する CAU 更新実行は続行できます。  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU を使用して、1 つのノードのみを更新するのにことができますか。  
いいえ。 CAU はクラスター\-スコープを更新するクラスターを選択することのみできますので、ツールを更新します。 単一のノードを更新する場合は、CAU は使わずに、既存のサーバー更新ツールを利用できます。  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>CAU は外部 CAU から開始する更新プログラムを報告できますか。  
いいえ。 CAU が生成できるレポートの対象は、CAU 内から実行された Updating Run に限られます。 ただし、後続 CAU 更新実行が起動したときに、非でインストールされた更新\-CAU メソッドは適切に各クラスター ノードに該当する可能性がある追加の更新プログラムを確認すると見なされます。  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>CAU のサポート、一意の IT プロセスの必要があることができますか?  
[はい]。 それぞれの企業ユーザーが抱える IT プロセスのニーズを満たすために、CAU には次の手段が用意されています。  
  
**スクリプト**更新実行では、プリトリガーを指定できます\-PowerShell スクリプトと、投稿を更新\-PowerShell スクリプトを更新します。 前の\-ノードが一時停止する前に、各クラスター ノードの更新スクリプトが実行されます。 投稿\-ノードの更新プログラムをインストールした後、各クラスター ノードの更新スクリプトが実行されます。  
  
> [!NOTE]  
> 前を実行する各クラスター ノードでは、.NET framework 4.6 または 4.5 と PowerShell をインストールする必要が\-更新し、投稿\-スクリプトを更新します。 また、クラスター ノード上で PowerShell リモート処理を有効にする必要があります。 詳細なシステム要件は、次を参照してください。[要件とクラスター対応更新のベスト プラクティス](cluster-aware-updating-requirements.md)します。  
  
**更新実行オプションを高度な**管理者は、多くの各ノードで、更新プロセスが再試行される最大回数などの高度な更新実行オプションを追加指定できます。 CAU UI または CAU の PowerShell コマンドレットを使用して、これらのオプションを指定できます。 カスタム設定は、更新実行プロファイルに保存し、以降の更新実行に再利用することができます。  
  
**パブリック プラグ\-アーキテクチャで**CAU には、登録、登録解除、機能が含まれていて、選択プラグイン\-アドイン。CAU は、2 つの既定のプラグインが付属しています\-ins: 1 つの座標、Windows Update エージェント\(WUA\) Api では、各クラスター ノードは、2 つ目は、クラスター ノードにアクセスできるファイル共有に手動でコピーされる修正プログラムを適用します。 プラグインに 2 つの企業は独自のニーズを満たすことはできません\-、アドイン、企業は新しい CAU プラグインを構築できます\-でパブリック API 仕様に従っています。 詳細については、次を参照してください。[クラスター\-対応更新プラグイン\-リファレンス](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)します。  
  
プラグインを構成して、CAU のカスタマイズについて\-さまざまなサポートをアドイン シナリオでは、更新を参照してください[方法プラグイン\-アドイン機能](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)。  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU のプレビュー結果や更新結果をエクスポートするにはどうすればよいですか。  
CAU は、コマンドを使用してオプションをエクスポートする\-ライン インターフェイスと UI を使用します。  
  
**コマンド\-ライン インターフェイスのオプション。**  
  
-   PowerShell コマンドレットを使用して、結果をプレビュー **Invoke\-CauScan |ConvertTo\-Xml**します。 出力:XML  
  
-   PowerShell コマンドレットを使用して結果を報告**Invoke\-CauRun |ConvertTo\-Xml**します。 出力:XML  
  
-   PowerShell コマンドレットを使用して結果を報告**取得\-CauReport |エクスポート\-CauReport**します。 出力:HTML、CSV  
  
**UI オプション:**  
  
-   **[更新プログラムのプレビュー]** 画面からレポートの結果をコピーする。 出力:CSV  
  
-   **[レポートの作成]** 画面からレポートの結果をコピーする。 出力:CSV  
  
-   **[レポートの作成]** 画面からレポートの結果をエクスポートする。 出力:HTML (HTML)  
  
## <a name="how-do-i-install-cau"></a>CAU はどうすればインストールできますか。  
CAU のインストールは、フェールオーバー クラスタリング機能にシームレスに統合されています。 CAU は次のようにインストールされます。  
  
-   CAU Windows Management Instrumentation、クラスター ノードにフェールオーバー クラスタ リングのインストールと\(WMI\)プロバイダーが自動的にインストールします。  
  
-   フェールオーバー クラスタ リング ツールの機能は、サーバーまたはクライアント コンピューターにインストールするときに、クラスター対応更新の UI と PowerShell コマンドレットが自動的にインストールします。
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU が更新されているクラスター ノードで実行されているコンポーネントを必要がありますか。  
CAU のクラスター ノードで実行されているサービスを必要はありません。 ただし、CAU には、ソフトウェアのコンポーネント必要があります。 \(WMI プロバイダー\)クラスター ノードにインストールします。 このコンポーネントは、フェールオーバー クラスタリング機能と一緒にインストールされます。  
  
自己を有効にする\-モードを更新するには、CAU のクラスター化された役割する必要があります追加することも、クラスターにします。  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU と VMM の使用方法の違いは何ですか。  
  
-   System Center Virtual Machine Manager \(VMM\)更新のみハイパーにフォーカスがある\-V クラスター、CAU は、ハイパースレッディングを含め、サポートされているフェールオーバー クラスターの任意の型を更新できますが、\-V クラスター。  
  
-   VMM は、CAU は、すべての Windows Server のライセンスが、追加のライセンスでは、必要です。 CAU の機能、ツール、UI は、フェールオーバー クラスタリングのコンポーネントと一緒にインストールされます。  
  
-   System Center ライセンスを既に所有している場合は、VMM を使用してハイパースレッディングを更新する続行することができます\-V クラスターのため、統合の管理とソフトウェアの更新エクスペリエンスを提供します。  
  
-   CAU は、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行しているクラスターでのみサポートされます。 VMM は、ハイパースレッディングもサポートしています。\-V は、Windows Server 2008 R2 および Windows Server 2008 を実行するコンピューターでクラスター。  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>使用できますリモート\-セルフ用に構成されたクラスターで更新\-を更新していますか?  
[はい]。 フェールオーバー クラスターの自動\-構成の更新は、リモートで更新できます\-で更新\-に Windows Update が構成されている場合でも、コンピューターには、いつでも Windows の更新プログラムのスキャンを強制でき、同様、需要更新プログラムを自動的にインストールします。 ただし、更新実行が実行されていないことを確認する必要はあります。  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>クラスター更新設定を複数のクラスターで再利用することはできますか。  
[はい]。 CAU には、クラスター更新時の Updating Run の動作を決める更新実行オプションが多数あります。 これらのオプションは更新実行プロファイルとして保存でき、他のクラスターで再利用することができます。 更新に関して同様のニーズを持つフェールオーバー クラスターには、保存しておいた設定を再利用することをお勧めします。 たとえば、作成する、"ビジネス\-クリティカルな SQL Server クラスター更新実行プロファイル"ビジネスをサポートするすべての Microsoft SQL Server クラスターの\-重要なサービスです。  
  
## <a name="where-is-the-cau-plug-in-specification"></a>CAU プラグインが\-仕様のでしょうか。  
  
-   [クラスター\-対応更新プラグイン\-リファレンス](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [クラスター対応更新プラグイン\-サンプル](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>関連項目  
  
-   [クラスター\-対応更新の概要](cluster-aware-updating.md)  
  
