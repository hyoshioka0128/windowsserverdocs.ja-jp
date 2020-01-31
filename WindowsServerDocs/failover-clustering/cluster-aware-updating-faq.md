---
ms.assetid: 6416d125-bcaf-433d-971a-2f0283bca2c2
title: クラスター対応更新についてよく寄せられる質問
ms.topic: article
ms.prod: windows-server
manager: dongill
ms.author: jgerend
author: JasonGerend
ms.date: 04/28/2017
description: Windows Server でのクラスター対応更新に関してよく寄せられる質問への回答です。
ms.openlocfilehash: 736b49222ae4c9e2a27229341f0d886bd3e0343c
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822135"
---
# <a name="cluster-aware-updating-frequently-asked-questions"></a>クラスター対応更新: よく寄せられる質問

> 適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

[クラスター対応更新](cluster-aware-updating.md)\(CAU\) は、フェールオーバークラスター内のすべてのサーバーでソフトウェア更新を調整する機能です。この機能は、クラスターノードの計画されたフェールオーバーよりも、サービスの可用性に影響を与えません。 ライブマイグレーションを使用したハイパー\-V、SMB の透過的なフェールオーバー\)を備えた SMB 3.x ファイルサーバーなど、継続的な可用性 \(機能を備えた一部のアプリケーションでは、CAU は、サービスの可用性に影響を与えることなく、自動クラスター更新を調整できます。

## <a name="does-cau-support-updating-storage-spaces-direct-clusters"></a>CAU は記憶域スペースダイレクトクラスターの更新をサポートしていますか。  
対応 CAU では、展開の種類に関係なく[記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)クラスターの更新がサポートされています: ハイパー収束または収束。 具体的には、CAU オーケストレーションによって、各クラスターノードの中断が、基になるクラスター化された記憶域スペースが正常になるまで待機します。

## <a name="does-cau-work-with-windowsserver-2008r2-or-windows7"></a>Windows Server 2008 R2 または Windows 7 で CAU を使用できますか。  
いいえ。 CAU は、windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10、Windows 8.1、または Windows 8 を実行しているコンピューターからのみクラスター更新操作を調整します。 更新するフェールオーバークラスターは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している必要があります。
  
## <a name="is-cau-limited-to-specific-clustered-applications"></a>CAU は特定のクラスター化されたアプリケーションに限定されますか。  
いいえ。 CAU は、クラスター化アプリケーションの種類を選びません。 CAU は、クラスタリング Api と PowerShell コマンドレットの上に階層化されているソリューションを更新する外部クラスター\-します。 そのため、CAU は、Windows Server フェールオーバークラスターで構成されている任意のクラスター化アプリケーションの更新を調整できます。  
  
> [!NOTE]  
> 現時点では、次のクラスター化されたワークロードが CAU に対してテストおよび認定が行われています: SMB、\-Hyper-v、DFS レプリケーション、DFS 名前空間、iSCSI、NFS。  
  
## <a name="does-cau-support-updates-from-microsoft-update-and-windows-update"></a>CAU は、Microsoft Update や Windows Update からの更新プログラムをサポートしていますか。  
対応 既定では、CAU は、クラスターノードで Windows Update エージェント \(WUA\) ユーティリティ Api を使用するのプラグ\-で構成されます。 WUA インフラストラクチャを構成して、Microsoft Update を参照したり、\(WSUS\) を更新のソースとして Windows Server Update Services Windows Update したりすることができます。  
  
## <a name="does-cau-support-wsus-updates"></a>CAU は WSUS 更新プログラムをサポートしますか。  
対応 既定では、CAU は、クラスターノードで Windows Update エージェント \(WUA\) ユーティリティ Api を使用するのプラグ\-で構成されます。 WUA インフラストラクチャは Microsoft Update をポイントするように構成し、WSUS\) サーバーのローカル \(Windows Server Update Services を更新のソースとして Windows Update します。  
  
## <a name="can-cau-apply-limited-distribution-release-updates"></a>CAU で Limited Distribution Release の更新プログラムは適用されますか。  
対応 限定的な配布リリース \(LDR\) 更新プログラム (修正プログラムとも呼ばれます) は Microsoft Update または Windows Update を通じて公開されないため、Windows Update エージェントではダウンロードできません。そのため、CAU は既定で使用します。  
  
ただし、CAU には、修正プログラムの更新プログラムを適用するために選択できるの2つ目のプラグ\-が含まれています。 この修正プログラム\-プラグインは、\-Microsoft ドライバー、ファームウェア、BIOS の更新プログラムを適用しないようにカスタマイズすることもできます。  
  
## <a name="can-i-use-cau-to-apply-cumulative-updates"></a>CAU を使用して、累積的な更新プログラムを適用できますか。  
対応 累積的更新プログラムが一般配布リリースの更新プログラムまたは LDR 更新プログラムである場合、CAU によって適用できます。  
  
## <a name="can-i-schedule-updates"></a>更新をスケジュールすることはできますか?  
対応 CAU は以下の更新モードをサポートしており、どちらの場合も更新をスケジューリングすることができます。  
  
**自己\-更新**定義されたプロファイルと定期的なスケジュールに従って、クラスターが自身を更新できるようにします (月次のメンテナンス期間中など)。 また、必要に応じていつでも、セルフ\-更新実行を開始することもできます。 自己\-更新モードを有効にするには、CAU のクラスター化された役割をクラスターに追加する必要があります。 CAU の自己\-更新機能は、他のクラスター化されたワークロードと同様に動作し、更新コーディネーターコンピューターの計画されたフェールオーバーと計画外のフェールオーバーとシームレスに連携します。  
  
**リモート\-の更新**Windows または Windows Server を実行しているコンピューターから、いつでも更新実行を開始できます。 更新実行を開始するには、クラスター対応更新ウィンドウを使用するか、 **Invoke\-CauRun** PowerShell コマンドレットを使用します。 リモート\-更新は、CAU の既定の更新モードです。 クラスター ノードに属していないリモート コンピューターから、タスク スケジューラを使って、 [Invoke-CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-caurun) コマンドレットを目的のスケジュールで実行できます。  
  
## <a name="can-i-schedule-updates-to-apply-during-a-backup"></a>バックアップ中に適用する更新をスケジュールすることはできますか。  
対応 CAU では、この点に制約はありません。 ただし、サーバーのバックアップが進行している間に、関連する可能性のある再起動\) を使用してサーバー \(でソフトウェアの更新を実行することは、IT のベストプラクティスではありません。 CAU によるリソースのフェールオーバーとフェールバックの判断は、クラスタリング API だけで実現されている点に注意してください。CAU は、サーバーのバックアップ ステータスを関知しません。  
  
## <a name="can-cau-work-with-configuration-manager"></a>CAU は Configuration Manager と連携できますか。  
CAU は、クラスターノード上のソフトウェア更新プログラムを調整するツールであり、Configuration Manager サーバーソフトウェア更新プログラムも実行します。 これらのツールは、さまざまな Windows Server Update Services サーバーを使用するなど、データセンターの配置において同じサーバーのカバレッジが重複しないように構成することが重要です。 これにより、Configuration Manager\-の更新によってクラスター認識が組み込まれないため、CAU を使用する目的が誤って解決されることはありません。  
  
## <a name="do-i-need-administrative-credentials-to-run-cau"></a>CAU を実行するために管理者の資格情報は必要ですか。  
対応 CAU ツールを実行するためには、ローカル サーバーに対する管理者の資格情報か、ツールが実行されるローカル サーバー (またはクライアント コンピューター) の **認証後にクライアントを偽装** というユーザー権利が必要です。 ただし、クラスター ノードでのソフトウェア更新を調整するには、すべてのノードに対するクラスター管理者の資格情報が CAU に必要です。 資格情報がなくても CAU の UI は起動できますが、クラスターインスタンスに接続して更新をプレビューまたは適用するときに、クラスター管理者の資格情報の入力を求められます。  
  
## <a name="can-i-script-cau"></a>CAU をスクリプト化することはできますか。  
対応 CAU には、スクリプト作成オプションの豊富なセットを提供する PowerShell コマンドレットが付属しています。 CAU の UI が CAU のアクションを実行するときにも、同じコマンドレットが呼び出されます。  

## <a name="what-happens-to-active-clustered-roles"></a>アクティブなクラスター化された役割はどうなりますか。

クラスター化された役割 \(以前は、ノード上でアクティブになっているアプリケーションとサービス\) と呼ばれています。ソフトウェア更新プログラムを開始する前に、他のノードにフェールオーバーします。 CAU はメンテナンス モードを使ってこれらのフェールオーバーを調整し、すべてのクラスター化されたアクティブな役割のノードは一時停止されて、ドレインされます。 ソフトウェアの更新処理が完了すると、CAU によってノードが再開され、クラスター化された役割は、更新済みのノードにフェールバックされます。 これにより、ノードに対してクラスター化された役割の配分は、クラスターに対して CAU Updating Run を実行した後も同じように維持されます。  
  
## <a name="how-does-cau-select-target-nodes-for-clustered-roles"></a>CAU がクラスター化された役割のターゲットノードを選択する方法

CAU は、クラスタリング API を使って、フェールオーバーを調整します。 クラスタリング API の実装では、内部のメトリックとインテリジェントな配置ヒューリスティック (ワークロードレベル\) など) に依存することによってターゲットノードを選択します。これ \(、ターゲットノード全体にわたります。  
  
## <a name="does-cau-load-balance-the-clustered-roles"></a>CAU はクラスター化された役割の負荷を分散しますか。

CAU はクラスター化されたノードの負荷を分散しませんが、クラスター化された役割の分散を維持しようとします。 クラスター ノードの更新が完了すると、更新前にホストされていたクラスター化された役割のそのノードへのフェールバックが試みられます。 CAU は、クラスタリング API を使って、一時停止プロセスの最初の状態に、リソースをフェールバックします。 したがって、計画外のフェールオーバーおよび優先所有者の設定がない場合は、クラスター化された役割の配分は変化しません。  
  
## <a name="how-does-cau-select-the-order-of-nodes-to-update"></a>ノードの更新順序はどのようにして決まるのですか。  
既定では、アクティビティのレベルに基づいてノードの更新順序が選択されます。 ホストしているクラスター化された役割の少ないノードから先に更新されます。 ただし、管理者は、CAU UI で更新実行のパラメーターを指定するか、PowerShell コマンドレットを使用して、ノードを更新するための特定の順序を指定できます。  
  
## <a name="what-happens-if-a-cluster-node-is-offline"></a>クラスターノードがオフラインの場合はどうなりますか。

更新実行を開始する管理者は、オフラインを許容するノード数のしきい値を指定できます。 したがって、クラスター ノードの一部がオフラインだったとしても、クラスターに対する CAU 更新実行は続行できます。  
  
## <a name="can-i-use-cau-to-update-only-a-single-node"></a>CAU を使用して1つのノードのみを更新できますか。  
いいえ。 CAU はクラスター\-スコープ更新ツールであるため、更新するクラスターを選択できます。 単一のノードを更新する場合は、CAU は使わずに、既存のサーバー更新ツールを利用できます。  
  
## <a name="can-cau-report-updates-that-are-initiated-from-outside-cau"></a>Cau の外部から開始されたレポートの更新を CAU で実行できますか。  
いいえ。 CAU が生成できるレポートの対象は、CAU 内から実行された Updating Run に限られます。 ただし、その後の CAU 更新実行が開始されると、非\-の CAU メソッドによってインストールされた更新プログラムは、各クラスターノードに適用できる追加の更新プログラムを決定するために適切に検討されます。  
  
## <a name="can-cau-support-my-unique-it-process-needs"></a>独自の IT プロセスのニーズに合わせて CAU をサポートできますか。  
対応 それぞれの企業ユーザーが抱える IT プロセスのニーズを満たすために、CAU には次の手段が用意されています。  
  
**スクリプト**更新実行では、プリ\-更新 PowerShell スクリプトと、PowerShell スクリプトの post\-を指定できます。 事前\-更新スクリプトは、ノードが一時停止される前に各クラスターノードで実行されます。 Post\-更新スクリプトは、ノードの更新プログラムのインストール後に各クラスターノードで実行されます。  
  
> [!NOTE]  
> .NET Framework 4.6 または4.5 と PowerShell は、pre\-update と post\-更新プログラムを実行する各クラスターノードにインストールする必要があります。 また、クラスターノードで PowerShell リモート処理を有効にする必要があります。 システム要件の詳細については、「[クラスター対応更新の要件とベストプラクティス](cluster-aware-updating-requirements.md)」を参照してください。  
  
**高度な更新実行オプション**管理者はさらに、各ノードで更新プロセスが再試行される最大回数など、多数の高度な更新実行オプションから指定することもできます。 これらのオプションは、CAU UI または CAU PowerShell コマンドレットのいずれかを使用して指定できます。 カスタム設定は、更新実行プロファイルに保存し、以降の更新実行に再利用することができます。  
  
**アーキテクチャのパブリックプラグ\-** CAU には、\-プラグインを登録、登録解除、選択するための機能が含まれています。 CAU には、次の2つの既定のプラグイン\-が付属しています。1つは Windows Update エージェント \(WUA\) Api を各クラスターノードに調整することです。2番目の方法では、クラスターノードからアクセスできるファイル共有に手動でコピーされた修正プログラムを適用します。 企業がこれら2つの\-プラグインで満たすことのできない独自のニーズを持っている場合は、パブリック API 仕様に従って、で新しい CAU プラグ\-を構築できます。 詳細については、「[クラスター\-対応更新プラグ\-」](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)を参照してください。  
  
さまざまな更新シナリオをサポートするための CAU プラグイン\-の構成とカスタマイズの詳細については、「[プラグイン\-のしくみ](assetId:///847b571b-12b3-473c-953f-75a5a1f51333)」を参照してください。  
  
## <a name="how-can-i-export-the-cau-preview-and-update-results"></a>CAU のプレビュー結果や更新結果をエクスポートするにはどうすればよいですか。  
CAU では、コマンド\-ラインインターフェイスと UI を使用してエクスポートオプションを提供します。  
  
**コマンド\-ラインインターフェイスのオプション:**  
  
-   PowerShell コマンドレット Invoke を使用して結果をプレビューする **\-CauScan |Convertto-html\-Xml**。 出力結果: XML  
  
-   PowerShell コマンドレットを使用して結果を報告する **\-CauRun |Convertto-html\-Xml**。 出力結果: XML  
  
-   PowerShell コマンドレット**Get\-get-caureport export-caureport | を使用して結果を報告する\-Get-caureport export-caureport をエクスポート**します。 出力結果: HTML、CSV  
  
**UI オプション:**  
  
-   **[更新プログラムのプレビュー]** 画面からレポートの結果をコピーする。 出力結果: CSV  
  
-   **[レポートの作成]** 画面からレポートの結果をコピーする。 出力結果: CSV  
  
-   **[レポートの作成]** 画面からレポートの結果をエクスポートする。 出力結果: HTML  
  
## <a name="how-do-i-install-cau"></a>CAU はどうすればインストールできますか。  
CAU のインストールは、フェールオーバー クラスタリング機能にシームレスに統合されています。 CAU は次のようにインストールされます。  
  
-   クラスターノードにフェールオーバークラスタリングをインストールすると、CAU Windows Management Instrumentation \(WMI\) プロバイダーが自動的にインストールされます。  
  
-   サーバーまたはクライアントコンピューターにフェールオーバークラスタリングツール機能がインストールされている場合は、クラスター対応更新の UI と PowerShell コマンドレットが自動的にインストールされます。
  
## <a name="does-cau-need-components-running-on-the-cluster-nodes-that-are-being-updated"></a>CAU では、更新されるクラスターノードで実行されているコンポーネントが必要ですか。  
CAU は、クラスターノードで実行されているサービスを必要としません。 ただし、CAU には、WMI プロバイダー\) クラスターノードにインストールされて \(ソフトウェアコンポーネントが必要です。 このコンポーネントは、フェールオーバー クラスタリング機能と一緒にインストールされます。  
  
自己\-更新モードを有効にするには、CAU のクラスター化された役割をクラスターに追加する必要もあります。  
  
## <a name="what-is-the-difference-between-using-cau-and-vmm"></a>CAU と VMM の使用にはどのような違いがありますか。  
  
-   System Center Virtual Machine Manager \(VMM\) は、\-Hyper-v クラスターのみを更新することに重点を置いていますが、CAU は、\-Hyper-v クラスターなど、サポートされているあらゆる種類のフェールオーバークラスターを更新できます。  
  
-   VMM には追加のライセンスが必要ですが、CAU はすべての Windows Server にライセンスが付与されます。 CAU の機能、ツール、UI は、フェールオーバー クラスタリングのコンポーネントと一緒にインストールされます。  
  
-   System Center ライセンスを既に所有している場合は、VMM を使用して\-Hyper-v クラスターを更新し続けることができます。これは、統合された管理およびソフトウェア更新エクスペリエンスを提供するためです。  
  
-   CAU は、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行するクラスターでのみサポートされます。 VMM では、Windows Server 2008 R2 および Windows Server 2008 を実行しているコンピューター上のハイパー\-V クラスターもサポートします。  
  
## <a name="can-i-use-remote-updating-on-a-cluster-that-is-configured-for-self-updating"></a>自己\-更新用に構成されているクラスターでリモート\-更新を使用できますか。  
対応 自己\-更新構成のフェールオーバークラスターは\-要求に応じてリモート\-更新できます。更新プログラムを自動的にインストールするように Windows Update が構成されている場合でも、コンピューターで Windows Update スキャンを強制的に実行することができます。 ただし、更新実行が実行されていないことを確認する必要はあります。  
  
## <a name="can-i-reuse-my-cluster-update-settings-across-clusters"></a>クラスター更新設定を複数のクラスターで再利用することはできますか。  
対応 CAU には、クラスター更新時の Updating Run の動作を決める更新実行オプションが多数あります。 これらのオプションは更新実行プロファイルとして保存でき、他のクラスターで再利用することができます。 更新に関して同様のニーズを持つフェールオーバー クラスターには、保存しておいた設定を再利用することをお勧めします。 たとえば、ビジネス\-重要なサービスをサポートするすべての Microsoft SQL Server クラスターの "Business\-Critical SQL Server Cluster 更新実行プロファイル" を作成できます。  
  
## <a name="where-is-the-cau-plug-in-specification"></a>CAU プラグ\-の仕様はどこにありますか?  
  
-   [参照に含まれるクラスター\-対応更新プラグイン\-](https://msdn.microsoft.com/library/hh418084(VS.85).aspx)  
  
-   [サンプルのクラスター対応更新プラグインの\-](https://code.msdn.microsoft.com/windowsdesktop/Cluster-Aware-Updating-6a8854c9)  
  
## <a name="see-also"></a>「  
  
-   [クラスター対応更新の概要](cluster-aware-updating.md)  
  
