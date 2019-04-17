---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: "Active Directory ドメイン サービス (AD DS) Virtualization (Level 100) の概要"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3c7fdc2e20bc4a27f2555af54f396a15f664d6c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>Active Directory ドメイン サービス (AD DS) Virtualization (Level 100) の概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory ドメイン サービス (AD DS) 環境の仮想化は、数年間の継続的なされています。 Windows Server 2012 以降では、AD DS は、安全に仮想化できる機能を導入しての仮想ドメイン コントローラーの複製による迅速な展開によってドメイン コントローラーの仮想化のサポートが強化を提供します。 これらの仮想化の新機能では、パブリック クラウドとプライベート クラウドに優れたサポートを提供、ハイブリッド環境 AD DS の各部が社内に存在し、クラウド、および完全に存在する AD DS インフラストラクチャの内部設置型です。

**このドキュメントで**

-   [ドメイン コントローラーの安全な仮想化](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#safe_virt_dc)

-   [仮想化ドメイン コントローラーの複製](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#virtualized_dc_cloning)

-   [複製仮想化ドメイン コントローラーを展開するための手順](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)

-   [トラブルシューティング](../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#troubleshooting)

## <a name="safe_virt_dc"></a>ドメイン コントローラーの安全な仮想化
仮想環境では、論理クロック ベースのレプリケーション スキームに依存する分散ワークロードに固有の課題を提示します。 AD DS レプリケーションは、たとえば、各ドメイン コントローラー上でトランザクションに割り当てられている (USN や Update Sequence Number と呼ばれます) 単調に増加値を使用します。 各ドメイン コントローラーのデータベースのインスタンスが、InvocationID と呼ばれる、id とも与えられます。 ドメイン コントローラーの InvocationID と USN 併せてように各書き込みトランザクションに関連付けられている一意の識別子が各ドメイン コントローラーに対して実行され、フォレスト内で一意である必要があります。

AD DS レプリケーションの InvocationID と Usn 各ドメイン コントローラーを使用して他のドメイン コントローラーにレプリケートされる必要がある変更を特定します。 ドメイン コントローラーがドメイン コントローラーに認識適時にロールバックすると、まったく異なるトランザクションの USN が再利用、レプリケーションは他のドメイン コントローラーが既にその InvocationID のコンテキストで再使用された USN に関連付けられている更新プログラムを受信すると思われる場合があるために収束しません。

たとえば、次の図は、USN ロールバックが VDC2、仮想マシンで実行されている移行先のドメイン コントローラーで検出された場合、Windows Server 2008 R2 およびそれ以前のオペレーティング システムで一連のイベントが発生したことを示します。 この図では、レプリケーション パートナーが vdc2 からを示すこと VDC2 のデータベースが適時にロールバック正しくレプリケーション パートナーに以前に表示された最新の USN 値に送信されたことを検出すると USN ロールバックの検出は VDC2 で発生します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

仮想マシン (VM) 簡単ハイパーバイザー管理者をロールバックするドメイン コントローラーの Usn (その論理クロック) によって、たとえば、ドメイン コントローラーに認識されないままスナップショットの適用できます。 USN と USN の詳細については、USN ロールバック未検出インスタンスを示した他の図を含む、ロールバックを参照してください[USN と USN ロールバック](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)します。

Windows Server 2012 以降では、VM-Generation ID と呼ばれる識別子を公開するハイパーバイザー プラットフォームでホストされている AD DS 仮想ドメイン コントローラーは検出し、バーチャル マシンが適時にロールバック VM スナップショットの適用によって場合に、AD DS 環境を保護するために必要な安全対策を使用します。 VM-GenerationID 設計では、ハイパーバイザー ベンダーに依存しないメカニズムを使用して、安全な仮想化が一貫して使用できる VM-GenerationID をサポートするあらゆるハイパーバイザーのために、ゲスト仮想マシンのアドレス空間でこの識別子を公開します。 この識別子は、サービスとアプリケーションが仮想マシン内で実行しているかどうか、仮想マシンが適時にロールバックされたを検出するためにでサンプリングされることができます。

### <a name="BKMK_HowSafeguardsWork"></a>これらの仮想化セーフガードのしくみ
ドメイン コントローラーのインストール時に AD DS は最初にそのデータベース (ディレクトリ情報ツリーまたは DIT とも呼ばれます) 内のドメイン コントローラーのコンピューター オブジェクトの Msds-generationid 属性の一部として VM GenerationID 識別子を格納します。 VM GenerationID が仮想マシン内の Windows ドライバーによって単独に追跡されません。

管理者は、以前のスナップショットから仮想マシンを復元、仮想マシン ドライバーからの VM GenerationID の現在の値が DIT 内の値と比較します。

2 つの値が異なる場合、invocationID がリセットし、なるため USN の再利用、RID プールが破棄されます。 値が同じ場合は、トランザクションは通常どおりコミットされます。

AD DS は、ドメイン コントローラーが再起動されると、異なる、invocationID をリセットする場合、RID プールを破棄し、新しい値を使用して DIT を更新するたびに値が DIT 内のバーチャル マシンから VM GenerationID の現在の値も比較します。 安全な復元を完了するために、SYSVOL フォルダーを同期も権限のない入力します。 これにより、シャット ダウンされた Vm 上のスナップショットのアプリケーションに拡張するセーフガードできます。 Windows Server 2012 で導入されたこれらのセーフガードには、展開と管理を仮想環境でドメイン コントローラーの一意の利点を活用する AD DS 管理者が有効にします。

次の図は、VM-GenerationID をサポートするハイパーバイザーで Windows Server 2012 を実行する仮想化ドメイン コントローラーで同一の USN ロールバックが検出されたときに仮想化セーフガードを適用する方法を示します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

この場合は、ハイパーバイザーが VM-GenerationID 値に変更を検出、(A から B 前の例) 仮想化 DC の InvocationID がリセットを含む、仮想化セーフガードがトリガーされ、ハイパーバイザーによって保存された新しい値 (G2) と一致するように VM に保存されている VM-GenerationID 値を更新します。 これらのセーフガードは、両方のドメイン コントローラーのレプリケーションの収束を確認します。

Windows Server 2012 では、AD DS は VM-GenerationID を認識するハイパーバイザーでホストされている仮想ドメイン コントローラーにセーフガードを採用しています、偶発的なアプリケーションを確実のスナップショットまたは他のようなハイパーバイザー対応メカニズム ロールバックする可能性のあるバーチャル マシンの状態が中断されません (USN バブルなどのレプリケーションの問題を防止または残留オブジェクト) を AD DS 環境です。 ただし、ドメイン コントローラーをバックアップするための代替手段として、ドメイン コントローラーを復元する仮想マシンのスナップショットを適用することでは推奨されません。 引き続き Windows Server バックアップまたはその他の VSS ライター ベース バックアップ ソリューションを使用することをお勧めします。

> [!CAUTION]
> 運用環境でドメイン コントローラーがスナップショットに戻った誤って場合、は、アプリケーションのベンダーを参照して、スナップショット後にこれらのプログラムの状態の確認に関するガイダンスについては、そのバーチャル マシンでホストされているサービスの復元ことをお勧めします。

詳細については、次を参照してください。[仮想ドメイン コントローラーの安全な復元アーキテクチャ](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)します。

## <a name="virtualized_dc_cloning"></a>仮想化ドメイン コントローラーの複製
Windows Server 2012 以降では、管理者は簡単かつ安全に展開レプリカ ドメイン コントローラー既存の仮想ドメイン コントローラーをコピーしています。 仮想環境では、管理者が不要になった繰り返し sysprep.exe を使用して準備されたサーバー イメージの展開は、サーバーのドメイン コントローラーに昇格する必要があるし、各レプリカ ドメイン コントローラーを展開するための追加の構成要件です。

> [!NOTE]
> 管理者は sysprep.exe を使用して、サーバー仮想ハード_ディスク (VHD) を準備する、サーバーのドメイン コントローラーに昇格し、他の構成要件を完了するなど、ドメイン内の最初のドメイン コントローラーを展開する既存のプロセスに従う必要があります。 障害回復シナリオでは、ドメイン内の最初のドメイン コントローラーを復元するのに、最新のサーバー バックアップを使用します。

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>仮想ドメイン コントローラーの複製の利点

-   新しいドメインの追加のドメイン コントローラーの迅速な展開

-   障害回復中に複製を使用してドメイン コントローラーの迅速な展開で AD DS 容量を復元することによって業務の継続性をすばやく戻したり

-   増大したスケール要件に対応するドメイン コントローラーの柔軟なプロビジョニングを利用して、プライベート クラウドの展開を最適化します。

-   テスト環境の展開を有効にして、実稼働展開する前に新しい機能のテストの迅速なプロビジョニング

-   ブランチ オフィス内の既存のドメイン コントローラーの複製によって、ブランチ オフィス内に迅速に対応の高まる容量ニーズ

多数のドメイン コントローラーを迅速に展開するには、引き続きインストールが完了した後、各ドメイン コントローラーの正常性を検証するため、既存の手順に従います。 各インストール バッチが完了した後に、正常性を検証できるように、適度なサイズのバッチでドメイン コントローラーを展開します。 推奨されるバッチ サイズは 10 です。 詳細については、次を参照してください。[を複製仮想化ドメイン コントローラーを展開する手順](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)します。

### <a name="clear-separation-of-responsibilities"></a>役割を明確に分離
仮想化ドメイン コントローラーの複製の承認では、AD DS 管理者の制御下です。 ハイパーバイザー管理者は、仮想ドメイン コントローラーをコピーすることによって追加のドメイン コントローラーを展開するためには、AD DS 管理者が] を選択し、ドメイン コントローラーを承認し、複製のソースとして有効にする準備手順を実行します。

バーチャル マシン プロビジョニングは通常、ハイパーバイザー管理者の責任範囲である下にある、ハイパーバイザー管理者は、承認されている AD DS 管理者により複製のための準備を仮想化ドメイン コントローラーをコピーすることによってレプリカ ドメイン コントローラーの仮想マシンをプロビジョニングできます。

> [!WARNING]
> 仮想ドメイン コントローラーをホストするハイパーバイザーの管理を許可される人物必要があります高信頼され、環境を監査します。

### <a name="how-does-virtual-domain-controller-cloning-work"></a>仮想ドメイン コントローラーの複製のしくみについて教えてください。
複製プロセスの既存の仮想ドメイン コントローラーの VHD (またはより複雑な構成では、ドメイン コントローラー VM) のコピーを作成する認証を行い、AD DS 内のクローン作成と複製構成ファイルを作成します。 これが、いくつかの手順を削減し、時間が関係するそれ以外の場合がなくなるため、レプリカ仮想ドメイン コントローラーを展開する反復的な展開タスクです。

複製ドメイン コントローラーは、別のドメイン コントローラーのコピーであることを検出するために、次の条件を使用します。

1.  仮想マシンから提供された VM-Generation ID の値は、DIT に格納されている VM-Generation ID の値と異なるです。

    > [!NOTE]
    > ハイパーバイザー プラットフォームが VM-Generation ID をサポートする必要があります (Windows Server 2012 の Hyper-V VM-Generation ID をサポートしています)。

2.  ファイルの存在には、次の場所のいずれかに DCCloneConfig.xml が呼び出されます。

    -   DIT が存在するディレクトリ

    -   %windir%\NTDS

    -   リムーバブル メディア ドライブのルート

条件が満たされると、プロビジョニング自体をレプリカ ドメイン コントローラーとして複製のプロセスを移動します。

複製ドメイン コントローラーは、ソース ドメイン コントローラー (ドメイン コントローラーのコピー) のセキュリティ コンテキストを使用すると、Windows Server 2012 プライマリ ドメイン コントローラー (PDC) エミュレータ操作マスタの役割所有者 (フレキシブル シングル マスター操作または FSMO とも呼ばれます) にお問い合わせください。 PDC エミュレーターでは、Windows Server 2012 が実行されている必要がありますが、ハイパーバイザーで実行されている必要はありません。

> [!NOTE]
> 場合は、ソース ドメイン コントローラーを参照している属性を持つスキーマ拡張があり、コピーされるオブジェクト (コンピューター オブジェクト、NTDS 設定オブジェクト) の複製の作成のいずれかにその属性がその属性をコピーまたはされません、複製ドメイン コントローラーを参照するように更新します。

要求側のドメイン コントローラーが複製の承認されていることを確認したら PDC エミュレーターは新しいアカウント、SID、名前、およびレプリカ ドメイン コントローラーとしてこのコンピューターを識別するパスワードを含む新しいマシン ID を作成して、この情報を複製に送信します。 複製ドメイン コントローラーは、レプリカとして機能するように AD DS データベース ファイルを準備し、およびも、コンピューターの状態をクリーンアップしてされます。

詳細については、次を参照してください。[仮想化ドメイン コントローラーの複製アーキテクチャ](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)します。

### <a name="cloning-components"></a>複製コンポーネント
複製コンポーネントには、Windows PowerShell と関連付けられた XML ファイルを Active Directory モジュール内の新しいコマンドレットがあります。

-   **New-addccloneconfigfile** "このコマンドレットは、作成し、複製のトリガーに利用可能ないることを確認、適切な場所に DCCloneConfig.xml を配置します。 また、複製の成功したことを確認する前提条件のチェックを実行します。 Windows PowerShell 用 Active Directory モジュールに含まれています。 複製に準備している仮想化ドメイン コントローラー上にローカルで実行できるかを使用してリモートで実行することができます、-offline オプションです。 その名前、サイト、および IP アドレスなど、複製ドメイン コントローラーの設定を指定することができます。

    これを実行する前提条件のチェックは次のとおりです。

    > [!NOTE]
    > 前提条件のチェックが実行されるときに、"offline オプションを使用します。 詳細については、次を参照してください。[オフライン モードで実行されている New-ADDCCloneConfigFile](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)します。

    -   複製が承認を準備中の DC (のメンバーである、**Cloneable Domain Controllers**グループ)

    -   PDC エミュレーターは、Windows Server 2012 を実行します。

    -   実行されているプログラムやサービスが一覧表示**Get-addccloningexcludedapplicationlist** (この複製コンポーネントの一覧の最後にさらに詳しく説明しています) CustomDCCloneAllowList.xml に含まれています。

-   **DCCloneConfig.xml** "を仮想化ドメイン コントローラーを正常に複製するには、このファイルは、DIT が存在するディレクトリ内に存在する必要があります*%windir%\NTDS*、またはリムーバブル メディア ドライブのルートです。 検出し、複製を開始、トリガーの 1 つとして使用されているだけでなく、複製ドメイン コントローラーの構成設定を指定するための手段も提供します。

    スキーマと、DCCloneConfig.xml ファイルのファイルの例は、のすべての Windows Server 2012 コンピューターに格納されます。

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.xml

    DCCloneConfig.xml ファイルを作成するのには、New-ADDCCloneConfigFile コマンドレットを使用することをお勧めします。 XML 対応エディターを使用してスキーマ ファイルを使用して、このファイルを作成する可能性がありますも、ファイルを手動で編集すると、エラーの可能性が高まります。 ファイルを編集する場合は、Visual Studio などの XML 対応エディターを使用して行う必要があります[XML Notepad](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973)、またはサード パーティ製のアプリケーション (メモ帳は使用しないでください)。

-   **Get-addccloningexcludedapplicationlist** "を判断するどのサービスまたはプログラムがインストールされている既定のサポート リスト、DefaultDCCloneAllowList.xml ではなく、複製プロセスを開始する前に、ソース ドメイン コントローラーでこのコマンドレットを実行またはユーザー定義の包含名前付きの CustomDCCloneAllowList.xml ファイルを一覧表示し、それによってが評価されていない複製の影響します。

    このコマンドレットは、サービス コントロール マネージャで、サービスのソース ドメイン コントローラーを検索し、下に表示されるインストール済みプログラム**\software\microsoft\windows\currentversion\uninstall**を既定の一覧 (DefaultDCCloneAllowList.xml) で指定されていない、または 1 つの場合は、ユーザー定義の包含リスト (CustomDCCloneAllowList.xml file) します。 コマンドレットを実行して返されるアプリケーションとサービスの一覧は、DefaultDCCloneAllowList.xml または CustomDCCloneAllowList.xml ファイルと、ソース DC にインストールされている内容に基づいて、実行時に作成されますが、一覧に既に含まれて新機能の違いです。 いるサービスとプログラムに安全に複製できると判断した場合、Get-ADDCCloningExcludedApplicationList からの出力をサービスとプログラムを CustomDCCloneAllowList.xml ファイルに追加できます。 サービスまたはインストール済みプログラムを安全に複製かどうかを判断するのには、次の条件を評価します。

    -   サービスまたはインストールされているプログラムの名前、SID、パスワードなど、マシン ID によって影響を受けるですか。

    -   サービスまたは複製では、その機能に影響を与える可能性があります、コンピューターにプログラム ストアのいずれかの状態をローカルにインストールしますか。

    かどうか、サービスまたはプログラムが安全に複製可能かを判断するアプリケーションのソフトウェア ベンダーと連携する必要があります。

    > [!NOTE]
    > CustomDCCloneAllowList.xml ファイル内のプログラムや追加のサービスをプロビジョニングする前に、そのバーチャル マシンに収録されているソフトウェアをコピーするために必要なライセンスがあるかどうかを確認します。

    アプリケーションが複製可能な場合は、複製メディアを作成する前に、ソース ドメイン コントローラーから削除します。 アプリケーションは、コマンドレットの出力に表示されますが、CustomDCCloneAllowList.xml ファイルにも記載されていない、複製は失敗します。 複製を確実に、コマンドレットの出力は必要がありますサービスまたはプログラムには表示されません。 つまり、アプリケーション必要がある CustomDCCloneAllowList.xml ファイルに含まれるまたはソース ドメイン コントローラーから削除します。

    次の表では、Get-ADDCCloningExcludedApplicationList を実行するためのオプションについて説明します。

    |||
    |-|-|
    |引数|説明|
    |*<no argument specified>*|対象に複製されていない本体上のサービスまたはプログラムの一覧を表示します。 許容される場所のいずれかに CustomDCCloneAllowList.XML が既に存在して、そのファイルをで表示、残りのサービスし、プログラムの (これは何も、リストが一致する場合) が使用されます。|
    |-GenerateXml|サービスが設定された CustomDCCloneAllowList.XML ファイルと、コンソールに表示するプログラムを作成します。|
    |フォース|既存の CustomDCCloneAllowList.XML ファイルが上書きされます。|
    |パス|CustomDCCloneAllowList.XML を作成するフォルダーのパス。|

-   **DefaultDCCloneAllowList.xml** "このファイルはすべての Windows では既定で存在 Server 2012 ドメイン コントローラーで、*%windir%\system32*します。 サービスが一覧表示し、既定で安全に複製できるプログラムをインストールします。 場所またはこのファイルの内容を変更する必要がありますしないと複製は失敗します。

-   **CustomDCCloneAllowList.xml** "サービスまたはインストール済みのプログラムのソース ドメイン コントローラー上に存在する、DefaultDCCloneAllowList.xml ファイルに表示されている場合は、これらのサービスとプログラム含める必要がありますこのファイルにします。 検索サービスまたはインストール済みプログラムには表示されませんが、DefaultDCCloneAllowList.xml ファイルに、実行、**Get-addccloningexcludedapplicationlist**コマンドレット。 使用する必要があります、**"GenerateXml** XML ファイルを生成する引数です。

    複製プロセスでは、このファイルの順序で、次の場所を確認しが見つかると、その他のフォルダーの内容に関係なく、最初の XML ファイルを使用します。

    1.  次のレジストリ キー:

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  DSA 作業ディレクトリ

    3.  %systemroot%\NTDS

    4.  リムーバブル読み取り/書き込みメディアのドライブのルートにある、ドライブ文字の順序で、

### <a name="deployment-scenarios"></a>展開シナリオ
仮想ドメイン コントローラーの複製は、次の展開シナリオがサポートされています。

-   ソース ドメイン コントローラーの仮想ハード_ディスク (vhd) ファイルのコピーを作成することによって、複製ドメイン コントローラーを展開します。

-   ハイパーバイザーによって公開されているエクスポート/インポート セマンティクスを使用して、ソース ドメイン コントローラーの仮想マシンをコピーすることによって、複製ドメイン コントローラーを展開します。

> [!NOTE]
> セクションの手順に[を複製仮想化ドメイン コントローラーを展開する手順](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)の Windows Server 2012 Hyper-V のエクスポート/インポート機能を使用してバーチャル マシンをコピーすることを示します。

## <a name="steps_deploy_vdc"></a>複製仮想化ドメイン コントローラーを展開するための手順

-   [前提条件](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [手順 1: は、ソース仮想化ドメイン コントローラーに複製対象となる許可を与える](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [手順 2: 実行 Get-ADDCCloningExcludedApplicationList コマンドレット](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [手順 3: New-ADDCCloneConfigFile を実行します。](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [手順 4: エクスポートし、ソース ドメイン コントローラーの仮想マシンをインポート](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>前提条件

-   次の手順を完了するには、Domain Admins グループのメンバーであるまたはが同等のアクセス許可が割り当てられています。

-   このガイドで使用される Windows PowerShell のコマンドは、管理者特権のコマンド プロンプトから実行する必要があります。 これを行うには、右クリックし、**Windows PowerShell** ] アイコンをクリックして**管理者として実行**します。

-   Hyper-V サーバーの役割がインストールされている Windows Server 2012 サーバー (**HyperV1**)。

-   Hyper-V サーバーの役割がインストールされている 2 番目の Windows Server 2012 サーバー (**HyperV2**)。

    > [!NOTE]
    > -   他のハイパーバイザーを使用している場合は、ハイパーバイザーが VM-Generation id。をサポートしているかを確認する、そのハイパーバイザーのベンダーに連絡する必要があります。 ハイパーバイザーが VM-Generation ID をサポートしていないに DCCloneConfig.xml を提供する場合は、新しい VM がディレクトリ サービス復元モード (DSRM) にではブートします。
    > -   AD DS サービスの可用性を上げるためには、このガイドはことをお勧めし、可能性のある単一障害点を防ぎやすく、別の 2 つの Hyper-V ホストを使用する手順について説明します。 ただし、仮想ドメイン コントローラーの複製を実行する 2 つの Hyper-V ホストにする必要はありません。
    > -   各 Hyper-V サーバー上のローカルの Administrators グループのメンバーである必要があります (**HyperV1**と**HyperV2**)。
    > -   正常にインポート、Hyper-V を使用して VHD ファイルをエクスポートするために両方の Hyper-V ホスト上の仮想ネットワーク スイッチに同じ名前を付ける必要があります。 たとえばがある場合、仮想ネットワーク スイッチ**HyperV1** VNet という名前の仮想ネットワークをオンにする必要があります**HyperV2** VNet という名前です。
    > -   場合は 2 つの Hyper-V ホスト (**HyperV1**と**HyperV2**) 別のプロセッサを持つ、仮想マシンをシャット ダウン (**VirtualDC1**) エクスポート、VM を右クリックし、をクリックする**設定**、] をクリックして**プロセッサ**、し、[**プロセッサの互換性を**選択**プロセッサ バージョンが異なる物理コンピューターへの移行**] をクリック**[OK]**します。

-   展開された Windows Server 2012 ドメイン コントローラー (仮想または物理) PDC エミュレーターの役割をホストしている (**DC1**)。 Windows Server 2012 ドメイン コントローラーで PDC エミュレーターの役割がホストされているかどうかを確認するには、次の Windows PowerShell コマンドを実行します。

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    OperatingSystemVersion 値はバージョン 6.2 として返すはずです。 必要に応じて、Windows Server 2012 を実行しているドメイン コントローラーに PDC エミュレーターの役割を転送できます。 詳細については、次を参照してください。[ドメイン コントローラーに FSMO の役割を強制または転送するのを使用する Ntdsutil.exe](https://support.microsoft.com/kb/255504)します。

-   展開された Windows Server 2012 ゲスト仮想ドメイン コントローラー (**VirtualDC1**) PDC エミュレーターの役割をホストしている Windows Server 2012 ドメイン コントローラーと同じドメインにある (**DC1**)。 複製するためのソース ドメイン コントローラーになります。 Windows Server 2012 の Hyper-V サーバー上でホストされるゲスト仮想ドメイン コントローラー (**HyperV1**)。

    > [!NOTE]
    > -   複製を確実に、複製の作成に使用するソース ドメイン コントローラーは、ソース VHD メディアの作成以降に降格された DC からすることはできません。
    > -   VM またはその VHD を複製する前に、ソース ドメイン コントローラーをシャット ダウンします。
    > -   VHD を複製またはスナップショットが廃棄 (tombstone) の有効期間値 (または Active Directory のごみ箱が有効にした場合、削除されたオブジェクトの有効期間値) よりも古いを復元する必要がありますできません。 既存のドメイン コントローラーの VHD をコピーする場合、VHD ファイルが古いは必ず廃棄 (tombstone) の有効期間値 (既定では 60 日間) のことです。 複製メディアを作成するには、実行中のドメイン コントローラーの VHD をコピーする必要がありますできません。

    すべてのバーチャル フロッピー ドライブ (VFD)、ソース DC が必要がありますを取り出します。 新しい VM をインポートするときは、共有問題が発生することができます。

    Windows Server 2012 ドメイン コントローラーのみ VM-GenerationID ハイパーバイザーでホストされているは、複製のソースとして使用できます。 正常な状態で、ソース Windows Server 2012 ドメイン コントローラーの複製するための必要があります。 ソース ドメイン コントローラーの実行の状態を確認する[dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx)します。 Dcdiag が返す出力の理解を深めるためには、次を参照してください。[DCDIAG を実際にはどのような... しないでください。](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx).

    ソース ドメイン コントローラーが DNS サーバーの場合、複製されたドメイン コントローラーは、DNS サーバーもできます。 そのホストのみ Active Directory 統合ゾーンの DNS サーバーを選択してください。

    DNS クライアント設定は複製されませんは、代わりに DCCloneConfig.xml ファイルに指定します。 指定されていない場合、複製されたドメイン コントローラーがそれ自体を指し示します優先 DNS サーバーとして既定でします。 複製されたドメイン コントローラーには、DNS 委任はありません。 親 DNS ゾーンの管理者は、必要に応じて、複製されたドメイン コントローラーの DNS 委任を更新する必要があります。

    > [!WARNING]
    > 仮想化セーフガードは、Active Directory ライトウェイト ディレクトリ サービス (AD LDS) には適用されません。 そのためこの AD LDS インスタンスを CustomDCCloneAllowList.xml に追加することで、AD LDS インスタンスをホストする AD DS ドメイン コントローラーの複製しないでください。 AD LDS が VM-Generation ID を認識しないので、AD LDS でドメイン コントローラーの複製可能性があります USN ロールバックによる相違ことで、その AD LDS 構成セット。

    次のサーバーの役割は複製はサポートされていません。

    -   動的ホスト構成プロトコル (DHCP)

    -   Active Directory 証明書サービス (AD CS)

    -   Active Directory ライトウェイト ディレクトリ サービス (AD LDS)

### <a name="bkmk4_grant_source"></a>手順 1: は、ソース仮想化ドメイン コントローラーに複製対象となる許可を与える
この手順で、ソース ドメイン コントローラー、アクセス許可を付与を使用して複製対象となる**Active Directory 管理センター**にソース ドメイン コントローラーを追加する、**Cloneable Domain Controllers**グループ。

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>移行元の仮想化ドメイン コントローラーに複製対象となるアクセス許可を付与するには

1.  複製の準備中、ドメイン コントローラーと同じドメイン内のドメイン コントローラー上 (**VirtualDC1**)、開かれている**Active Directory 管理センター** (ADAC) 仮想化ドメイン コントローラーのオブジェクトを見つける (ドメイン コントローラーが下にある通常、**ドメイン コントローラー** ADAC でコンテナー)、右クリックして、選択**グループに追加**し、[**を選択するオブジェクト名を入力**種類**Cloneable Domain Controllers** ] をクリックし、**[OK]**します。

    この手順で実行されるグループ メンバーシップの更新は、複製を実行する前に PDC エミュレーターにレプリケートする必要があります。 場合、**Cloneable Domain Controllers**グループが見つからない場合は、Windows Server 2012 を実行しているドメイン コントローラーで PDC エミュレーターの役割がホストされない可能性があります。

    > [!NOTE]
    > Windows Server 2012 ドメイン コントローラーで ADAC を開くを開き、Windows PowerShell の種類**dsac.exe**します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>手順 2: 実行 Get-ADDCCloningExcludedApplicationList コマンドレット
この手順では、実行、`Get-ADDCCloningExcludedApplicationList`プログラムまたは複製に向けて評価がないサービスを識別するソース仮想化ドメイン コントローラーでコマンドレット。 DCCloneConfig.xml ファイルが作成されますしない場合は、New-ADDCCloneConfigFile コマンドレットは、除外されたアプリケーションを検出するために、New-ADDCCloneConfigFile コマンドレットの前に、Get-ADDCCloningExcludedApplicationList コマンドレットを実行する必要があります。

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>アプリケーションまたは複製が評価されていないソース ドメイン コントローラー上で実行されるサービスを識別するには

1.  ソース ドメイン コントローラーで (**VirtualDC1**)、] をクリックして**サーバー マネージャー**、] をクリックして**ツール**、] をクリックして**Active Directory 用 Windows PowerShell モジュール**し、次のコマンドを入力します。


    Get-ADDCCloningExcludedApplicationList


2.  返されたサービスとインストールされているプログラムの一覧が安全に複製可能かどうかを決定するソフトウェア ベンダーと共に吟味します。 一覧でアプリケーションまたはサービスは、安全に複製することはできません、ソース ドメイン コントローラーから削除する必要がありますか、複製は失敗します。

3.  一連のサービスと安全に複製できると判断したプログラムがインストールされている、実行、コマンドをもう一度、**"GenerateXML**これらをプロビジョニングするスイッチは、サービスし、プログラム、**CustomDCCloneAllowList.xml**ファイル。


    Get-ADDCCloningExcludedApplicationList GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>手順 3: New-ADDCCloneConfigFile を実行します。
ソース ドメイン コントローラーで New-ADDCCloneConfigFile を実行し、必要に応じて、名、IP アドレス、DNS リゾルバーなど、複製ドメイン コントローラーの構成設定を指定します。

たとえば、静的な IPv4 アドレスして VirtualDC2 という複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> 複製ドメイン コントローラーは、別のサイトが DCCloneConfig.xml ファイルに指定されていない場合、ソース ドメイン コントローラーと同じサイトに格納されます。 IP アドレスに基づいて複製ドメイン コントローラーの DCCloneConfig.xml ファイルに適切なサイトを指定することをお勧めします。

コンピューター名は省略可能です。 いずれかを指定しない場合、次のアルゴリズムに基づいて一意の名前が生成されます。

-   プレフィックスは、ソース ドメイン コントローラーのコンピューター名の最初の 8 文字です。 たとえば、ソース コンピューター名 sourcecomputer はプレフィックス文字列 sourceco に切り捨てられます。

-   形式の一意の名前サフィックス""CL*nnnn*"プレフィックス文字列に追加場所*nnnn*が現在使用されていないと PDC が判断 0001-9999 から [次へ] の使用可能な値です。 たとえば、0047 が許容範囲で次の利用可能な番号の場合は、コンピューター名のプレフィックス SourceCo、前の例を使用して複製コンピューター用に使用する派生名として設定されます SourceCo CL0047 します。

> [!NOTE]
> グローバル カタログ (GC) サーバーは、New-ADDCCloneConfigFile コマンドレットを正常に実行する必要があります。 ソース ドメイン コントローラーのメンバーシップ、**Cloneable Domain Controllers**グループは、GC に反映する必要があります。 GC は PDC エミュレーターと同じドメイン コントローラーである必要はありませんが、可能であれば、同じサイト内にする必要があります。 GC が使用できない場合、コマンドが失敗し、エラー「サーバーが機能していない」 詳細については、次を参照してください。[仮想化ドメイン コントローラーのトラブルシューティング](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)します。

静的な IPv4 設定で Clone1 という名前の複製ドメイン コントローラーを作成し、優先と代替 WINS サーバーを指定する、次のように入力します。


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> WINS サーバーを指定する場合、両方を指定する必要があります**"PreferredWINSServer**と**"AlternateWINSServer**します。 のみこれらの引数を指定する場合は複製 dcpromo.log にエラー コード 0x80041005 が表示されるで失敗します。

動的な IPv4 設定で Clone2 という名前の複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> この場合、必要があります、DHCP サーバー環、複製が到達し、IP アドレスとその他の関連するネットワーク設定を取得することができます。

動的な IPv4 設定で Clone2 という名前の複製ドメイン コントローラーを作成し、優先と代替 WINS サーバーを指定する、次のように入力します。


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


動的な IPv6 設定で複製ドメイン コントローラーを作成するに次のように入力します。


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


静的な IPv6 設定で複製ドメイン コントローラーを作成するに次のように入力します。


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> 唯一の違い、静的および動的な設定を含めることは、IPv6 設定を指定するときに**-静的**切り替えます。 信頼、**-静的**スイッチにより、少なくとも 1 つを指定する必須**IPv6DNSResolver**します。静的な IPv6 アドレスが割り当てられているルーター プレフィックスとステートレス アドレス自動構成 (SLAAC) を介して設定すると想定されます。 動的な ipv6 設定、DNS リゾルバー オプションですが、複製が IPv6 アドレスと DNS 構成情報を取得するサブネット上の IPv6 対応の DHCP サーバーに到達できることを想定しています。

#### <a name="BKMK_OfflineMode"></a>オフライン モードで New-ADDCCloneConfigFile を実行しています。
(つまり、ソース ドメイン コントローラーが複製の承認されている、Get-ADDCCloningExcludedApplicationList コマンドレットがされて、実行など) の複製の準備したソース ドメイン コントローラー メディアの複数のコピーがあり、各メディアのコピーのさまざまな設定を指定する場合は、オフライン モードで New-ADDCCloneConfigFile を実行することができます。 各コピーをインポートすることによって、各 VM を個々 に準備するよりも効率的を指定できます。

この場合は、ドメイン管理者はオフライン ディスクをマウントし、Windows Server 2012 に含まれる新しい Windows PowerShell オプションを使用して工場出荷時のような自動化を可能にする XML ファイルを追加するために、-offline 引数で New-ADDCCloneConfigFile コマンドレットを実行するリモート サーバー管理ツール (RSAT) を使用できます。 オフライン モードで New-ADDCCloneConfigFile コマンドレットを実行するためにオフライン ディスクをマウントする方法の詳細については、次を参照してください。[オフライン システム ディスクを追加する XML](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline)します。

その前提条件チェックに合格することを確認する元のメディアのローカルで最初にコマンドレットを実行する必要があります。 できない可能性がある同じドメインまたはドメインに参加しているコンピューターから、マシンから、コマンドレットを実行することがあるために、前提条件のチェックはオフライン モードで実行されません。 コマンドレットをローカルで実行した後、DCCloneConfig.xml ファイルが作成されます。 続いてオフライン モードを使用する予定の場合、ローカルで作成される DCCloneConfig.xml を削除することがあります。

複製ドメイン コントローラーを作成するには、という CloneDC1 REDMOND と呼ばれるサイトでのオフライン モードで"の静的 IPv4 アドレスの種類。


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


オフライン モード静的な IPv4 設定と静的な IPv6 設定で Clone2 という名前の複製ドメイン コントローラーを作成します。


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


静的な IPv4 設定と動的な IPv6 設定を使用して、オフライン モードで複製ドメイン コントローラーを作成して、複数の DNS サーバー、DNS リゾルバー設定の指定、次のように入力します。


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


オフライン モード動的な IPv4 設定と静的な IPv6 設定で Clone1 という名前の複製ドメイン コントローラーを作成します。


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


オフライン モード動的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーを作成するに次のように入力します。


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>手順 4: エクスポートし、ソース ドメイン コントローラーの仮想マシンをインポート
この手順では、ソース仮想化ドメイン コントローラーの仮想マシンをエクスポートし、仮想マシンをインポートします。 この操作は、ドメインに複製仮想化ドメイン コントローラーを作成します。

各 Hyper-V ホスト上のローカルの Administrators グループのメンバーある必要があります。 サーバーごとに異なる資格情報を使用する場合は、エクスポートして別の Windows PowerShell セッションで VM をインポートする Windows PowerShell コマンドレットを実行します。

ソース ドメイン コントローラーでスナップショットがある場合は、VM がインポートを行わない場合は、スナップショットがあるターゲットの hyper-v ホストと互換性がないプロセッサ設定のために、ソース ドメイン コントローラーをエクスポートする前に、削除してください。 プロセッサの設定がソースとターゲットの hyper-v ホスト間で互換性のある場合は、エクスポートして、事前にスナップショットを削除することがなく、ソースをコピーすることがあります。 インポートの後ただし、スナップショットから削除しなければなりません複製 VM を開始する前にします。

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>仮想ドメイン コントローラーをコピー、エクスポートして、仮想化ソース ドメイン コントローラーをインポートするには

1.  **HyperV1**、ソース ドメイン コントローラーのシャット ダウン (**VirtualDC1**)。

    ![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

    Stop-VM-VirtualDC1-computername HyperV1 の名前


2.  **HyperV1**のスナップショットを削除、および、ソース ドメイン コントローラー (VirtualDC1) を c:\CloneDCs ディレクトリにエクスポートします。

> [!NOTE]
> スナップショットが作成されるたびに新しい AVHD ファイルが作成されるため差分ディスクとして機能するには、関連付けられているすべてのスナップショットを削除してください。 これにより、チェーンに影響が作成されます。 スナップショットを取得するいるし、DCCLoneConfig.xml ファイルを VHD に挿入すると、古い DIT バージョンから複製が作成または不適切な VHD ファイルへの構成ファイルの挿入を終了する可能性があります。 基本 VHD これらすべての AVHDs にマージ、スナップショットを削除します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  フォルダーをコピー **virtualdc1**の c:\Import ディレクトリに**HyperV2**します。

4.  **HyperV2**を利用して**Hyper-V マネージャー**、仮想マシンのインポート (を使用して、**仮想マシンのインポート**でウィザード**Hyper-V マネージャー**) フォルダーから**c:\Import\virtualdc1**と関連付けられているすべて削除**スナップショット**します。

使用して、**仮想マシンをコピー (新しい一意の ID を作成)**オプション、バーチャル マシンをインポートするときにします。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


同じソース ドメイン コントローラーから複数の複製ドメイン コントローラーを作成します。

  -   : Ui**仮想マシンのインポート**ウィザード、新しい場所を指定**仮想マシンの構成] フォルダー**、**スナップショット ストア**、**スマート ページング フォルダー**、や、さまざまな**場所**のバーチャル マシンの仮想ハード_ディスク。

  -   Windows PowerShell: 次のパラメーターを使用して、バーチャル マシン用の新しい場所を指定する、`Import-VM`コマンドレット。

        $path Get-ChildItem「C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual マシン」= Import-VM-パス $path.fullname-コピー - GenerateNewId-computername HyperV2 - VhdDestinationPath"path"- SnapshotFilePath"path"- SmartPagingFilePath"path"- VirtualMachinePath「パス」


> [!NOTE]
> 複数の複製ドメイン コントローラーを同時に作成する推奨されるバッチ サイズは 10 です。 最大数は、既定では、分散ファイル システム レプリケーション (DFSR) の 16 と 10 ファイル レプリケーション サービス (FRS) で、出力方向のレプリケーション接続の最大数に制限されます。 デプロイしないで複製ドメイン コントローラーの推奨される数よりも多く同時に、環境の数を十分にテストがある場合を除き、します。

5.  **HyperV1**、ソース ドメイン コントローラーを再起動 (**(VirtualDC1**) をオンライン状態に戻します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  **HyperV2**、仮想マシンの起動 (**VirtualDC2**) をオンラインに複製ドメイン コントローラーとして、ドメインにします。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> PDC エミュレーターは、複製を正常に実行されている必要があります。 シャット ダウンされている場合、開始されたことを確認し、PDC エミュレーターの役割を保持するので、認識されている初期同期を実行します。 詳細については、Microsoft を参照してください。[サポート技術情報の記事 305476](https://support.microsoft.com/kb/305476)します。

複製が完了したら、複製操作を確実に複製コンピューターの名前が成功したことを確認します。 VM がディレクトリ サービス復元モード (DSRM) でを起動しなかったことを確認します。 ログオンし、使用できるログオン サーバーがないことを示すエラーが発生すると、ログオンを試してください DSRM でします。 DC が正常に複製されず、DSRM で起動されている場合は、イベント ビューアーのログを確認し、%systemroot%/debug フォルダー内の dcpromo ログします。

複製されたドメイン コントローラーのメンバーであるが、**Cloneable Domain Controllers**ソース ドメイン コントローラーのメンバーシップをコピーするためにグループ化します。 ベスト プラクティスとして、おく必要があります、**Cloneable Domain Controllers**グループを空まで、複製操作を実行する準備ができたら、複製操作が完了した後は、メンバーを削除する必要があります。

ソース ドメイン コントローラーは、バックアップ メディアを保存する場合、複製されたドメイン コントローラーもバックアップ メディアを保存します。 行うことができます`wbadmin get versions`複製ドメイン コントローラーのバックアップ メディアを表示します。 Domain Admins グループのメンバーを誤って復元されるを防ぐために、複製されたドメイン コントローラー上のバックアップ メディアを削除する必要があります。 Wbadmin.exe を使用してシステム状態バックアップを削除する方法の詳細については、次を参照してください。[Wbadmin の削除 systemstatebackup](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx)します。

## <a name="troubleshooting"></a>トラブルシューティング
場合、複製ドメイン コントローラー (**VirtualDC2**) ディレクトリ サービス復元モード (DSRM) で起動するは返しません標準モードに自身で、[次への再起動時にします。 DSRM で起動しているドメイン コントローラーにログオンするには、使用**. \Administrator**し、DSRM パスワードを指定します。

複製に失敗した原因を正しし、dcpromo.log 示されていないことの複製再試行できないことを確認します。 複製を再試行することはできない場合、メディアを安全に破棄します。 複製を再試行できる場合、は、複製をもう一度試すために DS 復元モード ブート フラグを削除する必要があります。

1.  (右 Windows Server 2012] をクリックし、管理者として実行] を選択)、管理者特権のコマンドと入力し、Windows Server 2012 を開いている**msconfig**します。

2.  **ブート**] タブの [**ブート オプション**クリア、**セーフ ブート**(オプションで既に選択されている**有効になっている Active Directory 修復**)。

3.  をクリックして**OK**が表示されたら再起動します。

仮想化ドメイン コントローラーのトラブルシューティングの詳細については、次を参照してください。[仮想化ドメイン コントローラーのトラブルシューティング](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)します。


