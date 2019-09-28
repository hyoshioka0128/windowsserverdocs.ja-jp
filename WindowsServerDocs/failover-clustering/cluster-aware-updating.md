---
title: クラスター対応更新の概要
ms.topic: article
ms.prod: windows-server
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: クラスター対応更新 (CAU) は、Windows Server を実行しているクラスターへのソフトウェア更新プログラムのインストールを自動化します。
ms.assetid: 3c2993b4-aa81-452b-a5c3-3724ad95d892
ms.openlocfilehash: e96223e0b4b44e87ade9dc8eb875f9aa7104f451
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361250"
---
# <a name="cluster-aware-updating-overview"></a>クラスター対応更新の概要

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、クラスター化されたサーバー上で可用性を維持しながらソフトウェア更新プロセスを自動化する機能であるクラスター @ no__t 対応更新 \(CAU @ no__t-2 の概要について説明します。

> [!NOTE]
> [記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)クラスターを更新する場合は、クラスター対応更新を使用することをお勧めします。
  
## <a name="BKMK_OVER"></a>機能の説明  
クラスター対応更新は自動化された機能で、[フェールオーバークラスター](failover-clustering-overview.md)内のサーバーを更新するときに、更新プロセス中に可用性をほとんどまたはまったく失わないようにすることができます。 更新実行中、クラスター対応更新は、次のタスクを透過的に実行します。  

1. クラスターの各ノードをノードメンテナンスモードにします。
2. クラスター化された役割をノードから移動します。
3. 更新プログラムとその依存関係のある更新プログラムをインストールします。
4. 必要に応じて、再起動を実行します。
5. ノードをメンテナンスモードから除外します。
6. ノード上のクラスター化された役割を復元します。
7. 次のノードを更新するために移動します。

多くのクラスター役割がクラスターにある場合、自動更新プロセスにより計画フェールオーバーがトリガーされます。 これにより、接続されたクライアントに対するサービスが一時的に中断されることがあります。 ただし、Hyper-v のライブマイグレーションや、SMB 透過フェールオーバーを使用したファイルサーバーなど、継続的に使用可能なワークロードの場合、クラスター対応更新では、サービスの可用性に影響を与えることなくクラスターの更新を調整できます。    
  
## <a name="practical-applications"></a>実際の適用例  
  
-   CAU によって、クラスター化されたサービスのサービスの停止が軽減され、手動更新の回避策の必要性が軽減され、管理者にとって、@ no__t ~ 0to のクラスター更新プロセスがより信頼性の高いものになります。 継続的に使用できるファイル @no__t サーバーなど、継続的に使用可能なクラスターワークロードと共に CAU 機能を使用した場合、SMB Transparent Failover @ no__t またはハイパー @ no__t-2V を使用すると、クラスターの更新を実行できます。クライアントのサービスの可用性にゼロの影響を与えます。  
  
-   CAU によって、全社的に統一された IT プロセスを導入しやすくなります。 実行プロファイルの更新は、異なるクラスのフェールオーバークラスターに対して作成し、ファイル共有で一元的に管理することにより、クラスターが異なる方法で管理されている場合でも、IT 組織全体の CAU 展開で更新が一貫して適用されるようにすることができます。@ no__t-1business または管理者の行 @ no__t。  
  
-   CAU では、更新実行のスケジュールを設定できます。毎日、毎週、毎月など、定期的に実行することで、他の IT 管理プロセスとの間でクラスターの更新を調整することができます。  
  
-   CAU は、クラスターのソフトウェアインベントリを更新するための拡張可能なアーキテクチャをクラスターの @ no__t に対応した方法で提供します。 発行元はこれを使用して、Windows Update または Microsoft Update に発行されていないソフトウェア更新プログラムや、Microsoft からは利用できないソフトウェア更新プログラム (たとえば、@ no__t-0Microsoft デバイスドライバーの更新プログラムなど) のインストールを調整できます。  
  
-   CAU self @ no__t-0updating モードを使用すると、1つの筐体のクラスター化された物理マシン (通常は1つのシャーシにパッケージ化された、1つのシャーシにパッケージ化された物理マシン) のアプライアンス @no__t 1a を更新できます。 通常、このようなアプライアンスは、現場での IT のサポートが限られているブランチ オフィスで、クラスターを管理することを目的に展開されます。 Self @ no__t-0updating モードでは、これらのデプロイシナリオで優れた価値を提供します。  
  
## <a name="important-functionality"></a>重要な機能  
次に、クラスター対応更新の重要な機能について説明します。  
  
-   ユーザーインターフェイス \(UI @ no__t-クラスター対応更新ウィンドウと、更新プログラムのプレビュー、適用、監視、およびレポートに使用できる一連のコマンドレット。  
  
-   クラスター @ no__t-2updating 操作の end @ no__t-0to @ no__t-1 end automation は、1つまたは複数の更新コーディネーターコンピューターによって調整された更新実行 @ no__t-4 を @no__t します。  
  
-   既存の Windows Update エージェントと統合されるの既定のプラグ @ no__t-0in WUA @ no__t-2 と Windows Server Update Services Windows Server の \(WSUS @ no__t インフラストラクチャを使用して重要な Microsoft 更新プログラムを適用する  
  
-   Microsoft 修正プログラムを適用するために使用できるの2番目のプラグ @ no__t ~ 0in および @ no__t-1Microsoft 更新プログラムを適用するようにカスタマイズすることができます。  
  
-   更新実行プロファイル。更新実行オプション (1 ノードあたりの再試行回数の上限など) 設定を構成するときに使います。 複数の更新実行で同じ設定を再利用でき、更新設定を他のフェールオーバー クラスターと簡単に共有することができます。  
  
-   開発での新しいプラグ @ no__t をサポートする拡張可能なアーキテクチャ。これにより、カスタムソフトウェアインストーラー、BIOS 更新ツール、ネットワークアダプターやホストバスアダプター \(HBA @ no__t-3 など、クラスター全体の他のノード @ no__t 更新ツールを調整することができるようになります。ツールを更新しています。  
  
クラスター対応更新では、次の2つのモードで完全なクラスター更新操作を調整できます。  
  
-   **Self @ no__t-1 更新モード**このモードでは、CAU のクラスター化された役割は、更新対象のフェールオーバークラスター上のワークロードとして構成され、関連する更新スケジュールが定義されます。 予定の時刻になると、クラスターが既定またはカスタムの更新実行プロファイルを使って自己更新します。 更新実行中、その時点で CAU のクラスター化された役割を所有しているノード上の CAU 更新コーディネーター プロセスが起動し、それぞれのクラスター ノードに対する更新処理を順番に実行します。 現在のクラスター ノードを更新するために、CAU のクラスター化された役割は別のクラスター ノードにフェールオーバーされ、そのノード上の新しい更新コーディネーター プロセスが更新実行の制御を引き継ぎます。 Self @ no__t-0updating モードでは、CAU は完全に自動化された終了 @ no__t-1to @ no__t-2end プロセスを使用して、フェールオーバークラスターを更新できます。 また、管理者はこのモードで @ no__t-0demand の更新をトリガーすることもできます。または、必要に応じて、リモートの @ no__t 更新アプローチを使用することもできます。 Self @ no__t-0updating モードでは、管理者はクラスターに接続し、 **get @ no__t-2CauRun** Windows PowerShell コマンドレットを実行することで、進行中の更新実行に関する概要情報を取得できます。  
  
-   **Remote @ no__t-1 更新モード**このモードでは、更新コーディネーターと呼ばれるリモートコンピューターが CAU ツールで構成されます。 更新コーディネーターは、更新実行中に更新されるクラスターのメンバーではありません。 管理者は、リモートコンピューターから、既定またはカスタムの更新実行プロファイルを使用して @ no__t-0demand 更新実行をトリガーします。 Remote @ no__t-0updating モードは、更新実行中の実際の @ no__t の進行状況と、Server Core インストールで実行されているクラスターの監視に役立ちます。  
  
## <a name="hardware-and-software-requirements"></a>ハードウェアとソフトウェアの要件  

CAU は、Server Core インストールを含む、Windows Server のすべてのエディションで使用できます。 要件の詳細については、「[クラスター対応更新の要件とベストプラクティス](cluster-aware-updating-requirements.md)」を参照してください。

### <a name="installing-cluster-aware-updating"></a>クラスター対応更新のインストール
CAU を使用するには、Windows Server のフェールオーバークラスタリング機能をインストールし、フェールオーバークラスターを作成します。 CAU 機能に必要なコンポーネントは、各クラスター ノードに自動的にインストールされます。

フェールオーバー クラスタリング機能は、次のツールを使ってインストールできます。
- 役割と機能の追加ウィザード (サーバー マネージャー)
- [Install-add-windowsfeature](https://docs.microsoft.com/powershell/module/servermanager/Install-WindowsFeature?view=winserver2012r2-ps&viewFallbackFrom=win10-ps) windows PowerShell コマンドレット
- 展開イメージのサービスと管理 (DISM) のコマンド ライン ツール

詳細については、「[フェールオーバークラスタリング機能のインストール](create-failover-cluster.md#install-the-failover-clustering-feature)」を参照してください。

また、フェールオーバークラスタリングツールをインストールする必要があります。これはリモートサーバー管理ツールの一部でありサーバーマネージャーでフェールオーバークラスタリング機能をインストールすると、既定でインストールされます。 フェールオーバークラスタリングツールには、クラスター対応更新のユーザーインターフェイスと PowerShell コマンドレットが含まれています。 

サポートする CAU 更新モードに応じて、フェールオーバー クラスタ リング ツールを次の方法でインストールする必要があります。

- 自己 @ no__t-0updating モードで CAU を使用するには、各クラスターノードにフェールオーバークラスタリングツールをインストールします。   
  
- リモートの @ no__t-0updating モードを有効にするには、フェールオーバークラスターへのネットワーク接続があるコンピューターにフェールオーバークラスタリングツールをインストールします。  
  
> [!NOTE]  
> -   Windows server 2012 のフェールオーバークラスタリングツールを使用して、新しいバージョンの Windows Server でクラスター対応更新を管理することはできません。 
> -   CAU をリモートの @ no__t 更新モードでのみ使用する場合、クラスターノードにフェールオーバークラスタリングツールをインストールする必要はありません。 ただし、特定の CAU の機能は使用できなくなります。 詳細については、「[クラスター @ No__t 対応更新の要件とベストプラクティス](cluster-aware-updating-requirements.md)」を参照してください。  
> -   自己 @ no__t-0updating モードでのみ CAU を使用している場合を除き、CAU ツールがインストールされていて、更新を調整するコンピューターをフェールオーバークラスターのメンバーにすることはできません。  
  
### <a name="enabling-self-updating-mode"></a>自己更新モードを有効にする
自己更新モードを有効にするには、クラスター対応更新のクラスター化された役割をフェールオーバークラスターに追加する必要があります。 これを行うには、次のいずれかの方法を使用します。
- サーバーマネージャーで、@no__t **[ツール]** 、クラスター **[対応]** 更新 の順に選択し、クラスター対応更新 ウィンドウで **[クラスターの自己更新オプションの構成]** を選択します。 
- PowerShell セッションで、 [add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps)コマンドレットを実行します。  
  
CAU をアンインストールするには、サーバーマネージャー、 [uninstall](https://docs.microsoft.com/powershell/module/servermanager/Uninstall-WindowsFeature?view=win10-ps)コマンドレット、または DISM コマンド @ no__t-1line ツールを使用して、フェールオーバークラスタリング機能またはフェールオーバークラスタリングツールをアンインストールします。  
  
### <a name="additional-requirements-and-best-practices"></a>その他の要件とベスト プラクティス  

CAU によりクラスター ノードが正常に更新できることを確認するには、また、CAU を使用するようにフェールオーバー クラスター環境を構成するための追加のガイダンスを参照するには、CAU ベスト プラクティス アナライザーを実行できます。  
  
CAU の使用に関する詳細な要件とベストプラクティス、および CAU ベストプラクティスアナライザーの実行に関する情報については、「[クラスター @ No__t 対応更新の要件とベストプラクティス](cluster-aware-updating-requirements.md)」を参照してください。  
  
### <a name="starting-cluster-aware-updating"></a>クラスター対応更新の開始  
  
##### <a name="to-start-cluster-aware-updating-from-server-manager"></a>サーバーマネージャーからクラスター対応更新を開始するには  
  
1.  サーバー マネージャーを起動します。  
  
2.  次のいずれかの操作を行います。  
  
    -   **[ツール]** メニューの **[クラスター @ No__t-2aware 更新]** をクリックします。  
  
    -   1つ以上のクラスターノードまたはクラスターがサーバーマネージャーに追加された場合は、 **[すべてのサーバー]** ページで右 @ no__t を右クリックして、ノードの名前 \( またはクラスターの名前 @ no__t をクリックし、 **[クラスターの更新]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
クラスター対応更新の使用方法の詳細については、次のリンクを参照してください。  
  
-   [クラスター @ no__t 対応更新の要件とベストプラクティス](cluster-aware-updating.md)  
  
-   [Cluster @ no__t-1 対応更新:よく寄せられる質問](cluster-aware-updating-faq.md)  
  
-   [CAU の詳細オプションと更新実行プロファイル](cluster-aware-updating-options.md)  
  
-   [CAU プラグ @ no__t の動作のしくみ](cluster-aware-updating-plug-ins.md)  
  
-   [クラスター @ no__t-1 対応更新コマンドレット (Windows PowerShell)](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps&viewFallbackFrom=winserverr2-ps)  
  
-   [クラスター @ no__t-1 対応更新プラグ @ no__t-2in リファレンス](https://docs.microsoft.com/previous-versions/windows/desktop/mscs/cluster-aware-update-plug-in-interfaces-and-classes)  
  

