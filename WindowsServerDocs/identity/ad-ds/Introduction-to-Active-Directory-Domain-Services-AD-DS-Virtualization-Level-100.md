---
ms.assetid: 7a3114c8-bda8-49bb-83a8-4e04340ab221
title: Active Directory Domain Services (AD DS) の仮想化 (レベル 100) の概要
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b818ba5a58db38bdb3c0f630a8d9d2daa1494403
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878093"
---
# <a name="introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100"></a>Active Directory Domain Services (AD DS) の仮想化 (レベル 100) の概要

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory ドメイン サービス (AD DS) 環境の仮想化は、過去何年も取り組まれてきました。 Windows Server 2012 以降では、AD DS ドメイン コント ローラーを安全に仮想化できる機能を導入することで仮想化のサポートが強化を提供します。

## <a name="safe-virtualization-of-domain-controllers"></a>ドメイン コントローラーの安全な仮想化

論理クロック ベースのレプリケーション スキーマに依存する分散ワークロードに、仮想環境は特異な課題をもたらします。 AD DS レプリケーションは、たとえば各ドメイン コントローラー上でトランザクションに割り当てられる、単調に増加する値 (USN や Update Sequence Number と呼ばれる) を使用します。 各ドメイン コント ローラーのデータベース インスタンスは、InvocationID と呼ばれる、id とも付けられます。 ドメイン コントローラーの InvocationID と USN が組み合わされて 1 つの一意の識別子となり、この識別子が各ドメイン コントローラー上で実行される各書き込みトランザクションに関連付けられます。この識別子はフォレスト内で一意である必要があります。

AD DS レプリケーションは、各ドメイン コントローラー上の InvocationID と USN を使用し、どの変更を他のドメイン コントローラーにレプリケートする必要があるかを判断します。 その他のドメイン コント ローラーは、更新プログラムを既に受け取っていると思われるために、レプリケーションが収束しない場合は、ドメイン コント ローラーがドメイン コント ローラーに認識外の特定のロールバックされ、まったく異なるトランザクションの USN が再利用、その InvocationID のコンテキストで再使用された USN に関連付けられました。

たとえば、次の図は USN ロールバックが VDC2 で検出された場合に Windows Server 2008 R2 以前のオペレーティング システムで発生する一連のイベントを示しています。VDC2 は、仮想マシンで実行されているレプリケート先ドメイン コントローラーです。 この図で USN ロールバックの検出 VDC2 で検出すると発生レプリケーション パートナー VDC2 が VDC2 のデータベースがロールバックことで時間を示すレプリケーション パートナーがこれまで見てきたが、最新の USN 値を送信します。不適切です。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_Exampleofhowreplicationcanbecomeinconsistent.png)

仮想マシン (VM) 簡単ハイパーバイザー管理者は、ロールバック ドメイン コント ローラーの Usn (その論理クロック) によって、たとえば、ドメイン コント ローラーに認識スナップショットを適用します。 USN と USN ロールバックの詳細については、「 [USN and USN Rollback (USN と USN ロールバック)](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx#usn_and_usn_rollback)」を参照してください (このページには検出されない USN ロールバック インスタンスを示した他の図もあります)。

Windows Server 2012 以降では、VM 生成 ID と呼ばれる識別子を公開するハイパーバイザー プラットフォームでホストされる AD DS 仮想ドメイン コント ローラー検出し、仮想マシンがロールバックされた場合は、AD DS 環境を保護するために必要な安全対策を施すVM スナップショットのアプリケーションでの時間。 VM-GenerationID 設計では、ハイパーバイザー ベンダーに依存しないメカニズムを使用して、ゲスト仮想マシンのアドレス空間でこの識別子を公開します。このため、VM-GenerationID をサポートするあらゆるハイパーバイザーで、安全な仮想化が一貫して実現されます。 仮想マシン内で稼働しているサービスとアプリケーションでこの識別子を抽出することにより、仮想マシンが適時にロールバックされたかを調べることができます。

### <a name="BKMK_HowSafeguardsWork"></a>これらの仮想化セーフガードのしくみ
最初に AD DS はドメイン コント ローラーのインストール時に、(多くの場合、ディレクトリ情報ツリーまたは DIT と呼ばれます)、データベース内のドメイン コント ローラーのコンピューター オブジェクトの Msds-generationid 属性の一部として VM GenerationID 識別子を格納します。 VM GenerationID は、仮想マシン内部の Windows ドライバーによって単独に追跡されます。

管理者が以前のスナップショットから仮想マシンを復元する際には、仮想マシン ドライバー内の VM GenerationID の現在値が DIT 内の値と比較されます。

これら 2 つの値が異なる場合、invocationID がリセットされ、RID プールが破棄されます。この結果、USN の再使用が防止されます。 値が同じ場合、トランザクションは通常どおりコミットされます。

AD DS は、ドメイン コントローラーが再起動されるときにも毎回仮想マシンの VM GenerationID の現在値と DIT 内の値を比較します。それらの値が異なると、invocationID をリセットして RID プールを破棄し、新しい値を使用して DIT を更新します。 AD DS は、安全に復元する対策として、SYSVOL フォルダーの権限のない同期も実行します。 この結果、シャットダウンされた VM 上のスナップショットのアプリケーションまでセーフガードの範囲が広がります。 Windows Server 2012 で導入されたこれらのセーフガードには、展開と管理仮想化環境内のドメイン コント ローラーの独自のメリットを享受する AD DS 管理者が有効にします。

次の図は、Vm-generationid をサポートするハイパーバイザー上で Windows Server 2012 を実行する仮想化ドメイン コント ローラーの同一の USN ロールバックが検出されたときに仮想化セーフガードを適用する方法を示します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/ADDS_VDC_Exampleofhowsafeguardswork.gif)

この場合、ハイパーバイザーが VM-GenerationID 値の変化を検知した時点で仮想化セーフガードがトリガーされます。この結果、仮想化 DC の InvocationID がリセットされる (上の例では A から B にリセットされる) と共に、ハイパーバイザーによって保存された新しい値 (G2) と一致するように VM 上に保存されている VM-GenerationID 値が更新されます。 これらのセーフガードにより、レプリケーション時には両方のドメイン コントローラーが確実に収束されます。

Windows Server 2012 では、AD DS は Vm-generationid を認識するハイパーバイザーでホストされている仮想ドメイン コント ローラーにセーフガードを適用およびのスナップショットまたは他のようなハイパーバイザー対応メカニズム仮想ロールバックの可能性のある、偶発的なアプリケーションを確実マシンの状態が (USN バブルなどのレプリケーションの問題の防止や残留オブジェクト) を AD DS 環境を妨害しません。 ただし、ドメイン コントローラーのバックアップに代わる手段として、仮想マシン スナップショットの適用によってドメイン コントローラーを復元するという方法はお勧めできません。 引き続き Windows Server バックアップまたは他の VSS ライター ベース バックアップ ソリューションを使用することをお勧めします。

> [!CAUTION]
> 運用環境でドメイン コント ローラーは、スナップショットに戻す、誤って場合は、アプリケーション、およびガイダンスについては後にこれらのプログラムの状態を検証する場合にその仮想マシンでホストされるサービスの仕入先を参照することをお勧めスナップショットの復元。

詳細については、「[仮想化ドメイン コントローラーの安全な復元アーキテクチャ](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)」を参照してください。

## <a name="virtualized_dc_cloning"></a>仮想化ドメイン コント ローラーの複製
Windows Server 2012 以降では、管理者は簡単かつ安全に展開レプリカ ドメイン コント ローラーを既存の仮想ドメイン コント ローラーをコピーすることで。 仮想環境では、管理者は sysprep.exe を使って準備したサーバー イメージを何度も展開し、サーバーをドメイン コントローラーに昇格して、それから各レプリカ ドメイン コントローラーの展開のため他の構成要件を満たすという方法で作業を行う必要がありません。

> [!NOTE]
> sysprep.exe などを使って従来の手順で最初のドメイン コントローラーをドメインに展開してサーバーの仮想ハード ディスク (VHD) を用意し、その後で他の構成要件を満たすだけで済みます。 障害復旧シナリオにおいては、最新のサーバー バックアップを使用してドメイン内の最初のドメイン コントローラーを復元します。

### <a name="scenarios-that-benefit-from-virtual-domain-controller-cloning"></a>仮想ドメイン コントローラーの複製の利点

-   新しいドメインへの追加ドメイン コントローラーの迅速な展開。

-   複製によりドメイン コントローラーを迅速に展開することで AD DS 容量を復元し、障害復旧中のビジネス継続性を迅速に回復させる。

-   ドメイン コントローラーの柔軟なプロビジョニングを利用して、増大したスケール要件に対応することにより、プライベート クラウド展開を最適化する。

-   運用環境へのロールアウト前に新しい機能の展開とテストを行うことができるテスト環境の迅速なプロビジョニング。

-   ブランチ オフィス内の既存のドメイン コントローラーを複製することによって、ブランチ オフィス内の高まる容量ニーズに迅速に対応する。

多数のドメイン コントローラーを迅速に展開するときは、インストールの完了後、従来の手順で各ドメイン コントローラーの正常性を確認してください。 各インストール バッチが完了した後で正常性を確認できるように、適度なサイズのバッチでドメイン コントローラーを展開してください。 バッチ サイズは 10 をお勧めします。 詳細については、「 [Steps for deploying a clone virtualized domain controller](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)」を参照してください。

### <a name="clear-separation-of-responsibilities"></a>明確な責任分担
仮想化ドメイン コントローラーの複製の承認は、AD DS 管理者の制御下に置かれます。 ハイパーバイザー管理者が仮想ドメイン コントローラーをコピーすることで追加のドメイン コントローラーを展開できるようにするには、AD DS 管理者がドメイン コントローラーを選択して承認し、準備手順を実行してそのドメイン コントローラーを複製のソースとして有効化する必要があります。

仮想マシンのプロビジョニングが一般にハイパーバイザー管理者に管理されるようになると、ハイパーバイザー管理者は、AD DS 管理者により複製が承認され、その準備が行われる仮想化ドメイン コントローラーをコピーすることでレプリカ ドメイン コントローラーの仮想マシンをプロビジョニングできます。

> [!WARNING]
> 仮想ドメイン コントローラーをホストするハイパーバイザーの管理を許可される人物は、その環境で十分に信頼され、監査されている必要があります。

### <a name="how-does-virtual-domain-controller-cloning-work"></a>仮想ドメイン コントローラーの複製のしくみ
複製のプロセスでは、既存の仮想ドメイン コント ローラーの VHD の (またはより複雑な構成では、ドメイン コント ローラー VM) のコピーを作成するでは認証を行い、AD DS 内のクローンを作成および複製構成ファイルを作成します。 この結果、反復的な展開タスクが除外されるため、レプリカ仮想ドメイン コントローラーの展開にかかるステップの数が減り、時間が短縮されます。

複製ドメイン コントローラーは、次の条件を使用して、それ自体が他のドメイン コントローラーのコピーであることを検知します。

1.  仮想マシンによって提供される VM 生成 ID の値が、DIT に格納されている VM 生成 ID の値と異なる。

    > [!NOTE]
    > ハイパーバイザー プラットフォームが VM 生成 ID をサポートする必要があります (Windows Server 2012 の HYPER-V では、VM 生成 ID をサポートします)。

2.  次に示す場所のどれかに DCCloneConfig.xml というファイルが存在する。

    -   DIT が存在するディレクトリ

    -   %windir%\NTDS

    -   リムーバブル メディア ドライブのルート

これらの条件が満たされると、それ自体をレプリカ ドメイン コントローラーとしてプロビジョニングするために複製プロセスに進みます。

複製ドメイン コント ローラーは、ソース ドメイン コント ローラー (ドメイン コント ローラーのコピーを表します) のセキュリティ コンテキストを使用して (別名、Windows Server 2012 プライマリ ドメイン コント ローラー (PDC) エミュレーター操作マスターの役割所有者にお問い合わせくださいフレキシブル シングル マスター操作または FSMO)。 Windows Server 2012、PDC エミュレーターを実行する必要がありますが、ハイパーバイザー上で実行されていることはありません。

> [!NOTE]
> ソース ドメイン コントローラーを参照している属性を持つスキーマ拡張が存在し、複製の作成のためにコピーされるオブジェクト (コンピューター オブジェクト、NTDS 設定オブジェクト) の 1 つにその属性が存在する場合、複製ドメイン コントローラーの参照のためにその属性がコピーまたは更新されることはありません。

要求しているドメイン コントローラーに複製が許可されていることを確認した後、PDC エミュレーターはこのマシンをレプリカ ドメイン コントローラーとして識別する新しいマシン ID を作成 (新しいアカウント、SID、名前、およびパスワードを含めて作成) し、この情報を複製に返送します。 続いて、複製ドメイン コントローラーが、レプリカとして機能する AD DS データベース ファイルを準備すると共に、マシン状態をクリーンアップします。

詳細については、「[仮想化ドメイン コントローラーの複製アーキテクチャ](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)」を参照してください。

### <a name="cloning-components"></a>複製コンポーネント
複製コンポーネントには、Windows PowerShell 用 Active Directory モジュール内の新しいコマンドレット、関連付けられた XML ファイルなどがあります。

-   **New-addccloneconfigfile** "このコマンドレットは、作成し、複製のトリガーに使用できるようにするに適切な場所に DCCloneConfig.xml を配置します。 また、複製が正常に行われるようにするため、前提条件のチェックも行います。 このコマンドレットは、Windows PowerShell 用 Active Directory モジュールに含まれています。 このコマンドレットは、複製の準備が行われている仮想化ドメイン コントローラーでローカルに実行することも、-offline オプションを使用してリモートで実行することもできます。 複製ドメイン コントローラーには、その名前、サイト、IP アドレスなどを設定できます。

    このコマンドレットが実行する前提条件のチェックは次のとおりです。

    > [!NOTE]
    > 前提条件のチェックが実行されるときに、"offline オプションを使用します。 詳細については、「 [Running New-ADDCCloneConfigFile in offline mode](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#BKMK_OfflineMode)」を参照してください。

    -   準備中の DC に複製が承認されている (準備中の DC が **[Cloneable Domain Controllers]** グループのメンバーである)。

    -   PDC エミュレーターは、Windows Server 2012 を実行します。

    -   **Get-ADDCCloningExcludedApplicationList** の実行で表示されるプログラムまたはサービスのどれかが CustomDCCloneAllowList.xml に含まれる (この複製コンポーネント リストの最後に詳細が説明されている)。

-   **DCCloneConfig.xml** "仮想化ドメイン コント ローラーを正常に複製するには、このファイルは、DIT が存在するディレクトリに存在する必要があります *%windir%\NTDS*、またはリムーバブル メディア ドライブのルート。 複製の検出と開始のためのトリガーの 1 つとして使用される他に、複製ドメイン コントローラーの構成設定を指定する手段にもなります。

    スキーマと、DCCloneConfig.xml ファイルのファイルの例は、のすべての Windows Server 2012 コンピューターに格納されます。

    -   %windir%\system32\DCCloneConfigSchema.xsd

    -   %windir%\system32\SampleDCCloneConfig.xml

    DCCloneConfig.xml ファイルは、New-ADDCCloneConfigFile コマンドレットを使用して作成することをお勧めします。 このファイルは、XML 対応のエディターを利用しスキーマ ファイルを使用することでも作成できますが、ファイルを手動で編集するとエラーを引き起こす可能性が高まります。 このファイルを編集する場合は、Visual Studio や [XML Notepad](https://www.microsoft.com/download/details.aspx?displaylang=en&id=7973)などの XML 対応エディターを使用するか、またはサードパーティ アプリケーションを使用する (メモ帳は使用しない) ことによって行う必要があります。

-   **Get-addccloningexcludedapplicationlist** "でこのコマンドレットは、実行、ソース ドメイン コント ローラー サービスまたはインストールされているプログラム上にない、サポートされている既定の一覧を確認する複製のプロセスを開始する前にDefaultDCCloneAllowList.xml、またはユーザー定義の包含名前付きの CustomDCCloneAllowList.xml ファイルを一覧表示し、それによって評価されていない複製の影響します。

    このコマンドレットは、ソース ドメイン コントローラーを検索し、サービス コントロール マネージャー内のサービスと、既定のリスト (DefaultDCCloneAllowList.xml) または、提供されている場合は、ユーザー定義の包含リスト (CustomDCCloneAllowList.xml ファイル) に指定されていない **HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall** 内に表示されるインストール済みプログラムを確認します。 このコマンドレットの実行で返されるアプリケーションとサービスのリストには、DefaultDCCloneAllowList.xml または CustomDCCloneAllowList.xml ファイルに既に含まれている項目と実行時に構築されるリストの項目のうち、ソース DC にインストールされているアプリケーションとサービスについて相違が示されます。 Get-ADDCCloningExcludedApplicationList から出力されるサービスとプログラムは、それらが安全に複製できると判断できる場合には、CustomDCCloneAllowList.xml ファイルに追加できます。 サービスまたはインストール済みプログラムが安全に複製可能かどうかを判断するには、次の条件を評価します。

    -   サービスまたはインストール済みプログラムは、マシン ID (名前、SID、パスワードなど) によって影響を受けるか。

    -   サービスまたはインストール済みプログラムは、複製において機能に影響する可能性があるコンピューター上に、いずれかの状態をローカルに保存するか。

    サービスまたはプログラムを安全に複製できるかどうかは、アプリケーションのソフトウェア ベンダーと協力して判断する必要があります。

    > [!NOTE]
    > CustomDCCloneAllowList.xml ファイル内の追加サービスまたは追加プログラムをプロビジョニングする場合は、プロビジョニング前にその仮想マシンに含まれるソフトウェアをコピーするために必要なライセンスを所有しているかどうかを確認してください。

    アプリケーションが複製不可能な場合は、複製メディアを作成する前にソース ドメイン コントローラーから複製できないアプリケーションを削除してください。 コマンドレットの出力にアプリケーションが示されるが、CustomDCCloneAllowList.xml ファイルには存在しないという場合、複製は失敗します。 コマンドの出力にサービスまたはプログラムが表示される場合、複製は成功しません。 つまり、アプリケーションは CustomDCCloneAllowList.xml ファイルに存在するか、ソース ドメイン コントローラーから削除されている必要があります。

    次に、Get-ADDCCloningExcludedApplicationList を実行するためのオプションを示します。

    |||
    |-|-|
    |引数|説明|
    |*<no argument specified>*|複製対象にされていない、コンソール上のサービスまたはプログラムの一覧が表示されます。 許容される場所のどこかに CustomDCCloneAllowList.XML が既に存在する場合、そのファイルが使用されて残りのサービスとプログラムが表示されます (リストが同じであれば何も残っていない可能性があります)。|
    |-GenerateXml|コンソールに表示されるサービスとプログラムが設定された CustomDCCloneAllowList.XML ファイルが作成されます。|
    |-Force|既存の CustomDCCloneAllowList.XML ファイルを上書きします。|
    |-Path|CustomDCCloneAllowList.XML を作成するフォルダー パス。|

-   **DefaultDCCloneAllowList.xml** "このファイルは存在に既定ですべての Windows Server 2012 ドメイン コント ローラーで、 *%windir%\system32*。 このファイルには、既定で安全に複製できるサービスとインストール済みプログラムが表示されています。 このファイルの場所と内容は変更しないでください。変更すると複製は失敗します。

-   **CustomDCCloneAllowList.xml** "サービスまたはインストール済みのプログラム ソース ドメイン コント ローラー上に存在する、DefaultDCCloneAllowList.xml ファイルに示されている外にある場合は、それらのサービスとプログラム含める必要があるこのファイルです。 DefaultDCCloneAllowList.xml ファイルに表示されていないサービスまたはインストール済みプログラムを見つけるには、 **Get-ADDCCloningExcludedApplicationList** コマンドレットを実行してください。 使用する必要があります、 **"GenerateXml** XML ファイルを生成する引数。

    複製プロセスでは、他のフォルダーのコンテンツに関係なく、次の場所を順にチェックしてこのファイルが存在しないかどうかを確認し、見つかった最初の XML ファイルを使用します。

    1.  次のレジストリ キー:

        ```
        HKey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters
        AllowListFolder (REG_SZ)
        ```

    2.  DSA 作業ディレクトリ

    3.  %systemroot%\NTDS

    4.  読み取り/書き込み対応リムーバブル メディア (ドライブのルートがドライブ文字の順に検索される)

### <a name="deployment-scenarios"></a>展開シナリオ
仮想ドメイン コントローラー複製では、次の展開シナリオがサポートされます。

-   ソース ドメイン コント ローラーの仮想ハード_ディスク (vhd) ファイルをコピーするには、複製ドメイン コント ローラーをデプロイします。

-   ハイパーバイザーによって公開されるエクスポート/インポート セマンティクスを使用してソース ドメイン コントローラーの仮想マシンをコピーすることによって複製ドメイン コントローラーを展開する。

> [!NOTE]
> セクションの手順[複製仮想化ドメイン コント ローラーを展開する手順](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#steps_deploy_vdc)の Windows Server 2012 HYPER-V のエクスポート/インポート機能を使用して仮想マシンをコピーするかを示します。

## <a name="steps_deploy_vdc"></a>複製の仮想化ドメイン コント ローラーを展開する手順

-   [前提条件](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#prerequisites)

-   [ステップ 1: ソース仮想ドメイン コント ローラーの複製を作成するアクセス許可を付与します。](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk4_grant_source)

-   [手順 2:Get-addccloningexcludedapplicationlist コマンドレットを実行します。](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet)

-   [手順 3:New-addccloneconfigfile を実行します。](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk5_create_insert_dccloneconfig)

-   [手順 4:エクスポートし、ソース ドメイン コント ローラーの仮想マシンをインポート](../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md#bkmk7_export_import_vm_sourcedc)

### <a name="prerequisites"></a>前提条件

-   次の手順を実行するには、Domain Admins グループのメンバーであるか、またはこのグループに割り当てられているものと同等のアクセス許可を持っている必要があります。

-   このガイドで使用される Windows PowerShell コマンドは、管理者特権のコマンド プロンプトから実行する必要があります。 これを行うには、右クリックして、 **Windows PowerShell**アイコン、およびクリック**管理者として実行**します。

-   HYPER-V サーバーの役割がインストールされた Windows Server 2012 サーバー (**HyperV1**)。

-   HYPER-V サーバーの役割がインストールされた 2 つ目の Windows Server 2012 サーバー (**HyperV2**)。

    > [!NOTE]
    > -   他のハイパーバイザーを使用している場合は、そのハイパーバイザーのベンダーに問い合わせ、そのハイパーバイザーが VM 生成 ID をサポートするかどうかを確認する必要があります。 ハイパーバイザーが VM 生成 ID をサポートしない場合に DCCloneConfig.xml を提供すると、新しい VM がディレクトリ サービス復元モード (DSRM) で起動します。
    > -   AD DS サービスの可用性を向上させる手段として、このガイドでは 2 台の Hyper-V ホストの利用を推奨し、その方法を説明しています。Hyper-V ホストを 2 台使用すると、単一障害点の発生を防ぎやすくなります。 仮想ドメイン コントローラーの複製に 2 台の Hyper-V ホストが必須というわけではありません。
    > -   各 Hyper-V サーバー (**HyperV1** と **HyperV2**) のローカル Administrators グループのメンバーである必要があります。
    > -   Hyper-V を使用して VHD ファイルのインポートとエクスポートを確実に行うためには、両方の Hyper-V ホストの仮想ネットワーク スイッチに同じ名前が付いていなければなりません。 たとえば、 **HyperV1** 上に VNet という名前の仮想ネットワーク スイッチが存在する場合には、 **HyperV2** にも VNet という名前の仮想ネットワーク スイッチが必要です。
    > -   2 台の Hyper-V ホスト (**HyperV1** と **HyperV2**) に異なるプロセッサが搭載されている場合は、エクスポートする仮想マシン (**VirtualDC1**) を停止して、VM を右クリックして、**[設定]**、**[プロセッサ]** の順にクリックし、**[プロセッサの互換性]** で **[プロセッサ バージョンが異なる物理コンピューターへ移行する]** をクリックして **[OK]** をクリックします。

-   デプロイされた Windows Server 2012 ドメイン コント ローラー (仮想または物理)、PDC エミュレーターの役割をホストする (**DC1**)。 Windows Server 2012 ドメイン コント ローラーで PDC エミュレーターの役割がホストされているかどうかを確認するには、次の Windows PowerShell コマンドを実行します。

    ```
    Get-ADComputer (Get-ADDomainController "Discover "Service "PrimaryDC").name "Property operatingsystemversion | fl
    ```

    OperatingSystemVersion 値はバージョン 6.2 と返る必要があります。 必要に応じて、Windows Server 2012 を実行するドメイン コント ローラーに PDC エミュレーターの役割を転送できます。 詳細については、「 [Ntdsutil.exe を使用してドメイン コントローラーに FSMO の役割を強制または転送する](https://support.microsoft.com/kb/255504)」を参照してください。

-   デプロイされた Windows Server 2012 ゲスト仮想ドメイン コント ローラー (**VirtualDC1**)、PDC エミュレーターの役割をホストしている Windows Server 2012 ドメイン コント ローラーと同じドメイン内にある (**DC1**)。 これは、複製に使用するソース ドメイン コントローラーとなります。 ゲスト仮想ドメイン コント ローラーが Windows Server 2012 の HYPER-V サーバーでホストされる (**HyperV1**)。

    > [!NOTE]
    > -   複製を確実に行う都合上、ソース VHD メディアの作成以降に降格された DC をソース ドメイン コントローラーとして複製の作成に使用することはできません。
    > -   VM またはその VHD を複製する前に、ソース ドメイン コントローラーを停止してください。
    > -   VHD またはスナップショットが廃棄 (Tombstone) の有効期間値 (Active Directory のごみ箱が有効になっている場合は削除されたオブジェクトの有効期間値) よりも古い場合、複製 (VHD) または復元 (スナップショット) を行ってはなりません。 既存のドメイン コントローラーの VHD をコピーする場合は、VHD ファイルが廃棄 (Tombstone) の有効期間値 (既定は 60 日) よりも古くないことを確認してください。 実行中のドメイン コントローラーの VHD をコピーして複製メディアを作成してはなりません。

    ソース DC に仮想フロッピー ドライブ (VFD) が存在する場合は、それらを取り出してください。 取り出さないと、新しい VM をインポートする際に共有問題が発生することがあります。

    Windows Server 2012 ドメイン コント ローラーのみ、Vm-generationid ハイパーバイザー上でホストされているは、複製のソースとして使用できます。 クローンを作成するために使用するソース Windows Server 2012 ドメイン コント ローラーは、正常な状態でなければなりません。 ソース ドメイン コントローラーの状態は、 [dcdiag](https://technet.microsoft.com/library/cc731968(WS.10).aspx)を実行して確認できます。 Dcdiag が返す出力の理解を深めるためには、次を参照してください[DCDIAG を実際に動作しています。でしょうか。](http://blogs.technet.com/b/askds/archive/2011/03/22/what-does-dcdiag-actually-do.aspx).

    ソース ドメイン コントローラーが DNS サーバーであれば、複製されたドメイン コントローラーも DNS サーバーになります。 Active Directory 統合ゾーンだけをホストする DNS サーバーを選択する必要があります。

    DNS クライアント設定は複製されませんが、代わりに DCCloneConfig.xml ファイルに指定されています。 指定されていない場合、既定で、複製されたドメイン コントローラーは優先 DNS サーバーとしてそれ自体を指し示します。 複製されたドメイン コントローラーに DNS 委任はありません。 親 DNS ゾーンの管理者は、必要に応じ、複製されたドメイン コントローラーの DNS 委任を更新する必要があります。

    > [!WARNING]
    > 仮想化セーフガードは、Active Directory ライトウェイト ディレクトリ サービス (AD LDS) には適用されません。 このため、AD LDS インスタンスを CustomDCCloneAllowList.xml に追加するという方法で、AD LDS インスタンスをホストする AD DS ドメイン コントローラーを複製してはなりません。 AD LDS は VM 生成 ID を認識ではないため、AD LDS ではドメイン コント ローラーの複製可能性があります USN ロールバックによる相違では、その AD LDS 構成セット。

    次に示すサーバーの役割は複製にはサポートされません。

    -   動的ホスト構成プロトコル (DHCP)

    -   Active Directory 証明書サービス (AD CS)

    -   Active Directory ライトウェイト ディレクトリ サービス (AD LDS)

### <a name="bkmk4_grant_source"></a>手順 1:ソース仮想ドメイン コントローラーに複製対象となる許可を与える
この手順では、**Active Directory 管理センター**でソース ドメイン コントローラーを **[Cloneable Domain Controllers]** グループに追加することで、ソース ドメイン コントローラーに複製の対象となる許可を与えます。

##### <a name="to-grant-the-source-virtualized-domain-controller-the-permission-to-be-cloned"></a>ソース仮想ドメイン コントローラーに複製対象となる許可を与えるには

1.  複製用に準備するドメイン コントローラー (**VirtualDC1**) と同じドメイン内の任意のドメイン コントローラー上で、 **Active Directory 管理センター** (ADAC) を開き、仮想ドメイン コントローラー オブジェクトを見つけ (ドメイン コントローラーは、通常、ADAC の **[Domain Controllers]** コンテナーに入っています)、これを右クリックして、 **[グループに追加]** をクリックし、 **[選択するオブジェクト名を入力してください]** に「 **Cloneable Domain Controllers** 」と入力して **[OK]** をクリックします。

    複製を実行するためには、複製前に、この手順で実行したグループ メンバーシップ更新を PDC エミュレーターにレプリケートする必要があります。 場合、 **Cloneable Domain Controllers**グループが見つからない場合は、Windows Server 2012 を実行するドメイン コント ローラーに PDC エミュレーターの役割をホストしない可能性があります。

    > [!NOTE]
    > Windows Server 2012 ドメイン コント ローラーで ADAC を開くには Windows PowerShell を開いて型**dsac.exe**します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。

次の Windows PowerShell コマンドレットは、前の手順と同じ処理を実行します。


    Add-ADGroupMember "Identity "CN=Cloneable Domain Controllers,CN=Users, DC=Fabrikam,DC=Com" "Member "CN=VirtualDC1,OU=Domain Controllers,DC=Fabrikam,DC=com"


### <a name="bkmk6_run_get-addccloningexcludedapplicationlist_cmdlet"></a>手順 2:Get-ADDCCloningExcludedApplicationList コマンドレットを実行する
この手順では、ソース仮想ドメイン コントローラーで `Get-ADDCCloningExcludedApplicationList` コマンドレットを実行し、複製に向けての評価がなされていないプログラムまたはサービスを見つけます。 Get-ADDCCloningExcludedApplicationList コマンドレットは New-ADDCCloneConfigFile コマンドレットよりも先に実行する必要があります。これは、New-ADDCCloneConfigFile コマンドレットが、除外されたアプリケーションを検出した場合には DCCloneConfig.xml ファイルを作成しないためです。

##### <a name="to-identify-applications-or-services-that-run-on-a-source-domain-controller-which-have-not-been-evaluated-for-cloning"></a>ソース ドメイン コントローラーで実行されるアプリケーションまたはサービスの中で複製に向けて評価が行われていないものを見つけるには

1.  ソース ドメイン コントローラー (**VirtualDC1**) で、**[サーバー マネージャー]**、**[ツール]**、**[Windows PowerShell の Active Directory モジュール]** の順にクリックし、次のコマンドを入力します。


    Get-ADDCCloningExcludedApplicationList


2.  返されたサービスとインストール済みプログラムのリストをソフトウェア ベンダーと共に吟味し、それらが安全に複製可能かどうかを判断します。 リスト内に安全に複製できないアプリケーションまたはサービスがあれば、それらをソース ドメイン コントローラーから削除する必要があります。削除しないと複製は失敗します。

3.  サービスと安全に複製できると判断したプログラムがインストールされているセットの実行コマンドをもう一度、 **"GenerateXML**これらをプロビジョニングするスイッチを選択し、サービスのプログラムで、 **CustomDCCloneAllowList.xml**ファイル。


    Get-ADDCCloningExcludedApplicationList -GenerateXml


### <a name="bkmk5_create_insert_dccloneconfig"></a>手順 3:New-ADDCCloneConfigFile を実行する
ソース ドメイン コントローラーで New-ADDCCloneConfigFile を実行し、必要に応じて複製ドメイン コントローラーの構成設定 (名前、IP アドレス、DNS リゾルバーなど) を指定します。

たとえば、静的な IPv4 アドレスを指定して VirtualDC2 という複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile "Static -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.255.0" -CloneComputerName "VirtualDC2" -IPv4DefaultGateway "10.0.0.3" -SiteName "REDMOND"

> [!NOTE]
> この複製ドメイン コントローラーは、DCCloneConfig.xml ファイルに別のサイトを指定しない限り、ソース ドメイン コントローラーと同じサイトに配置されます。 複製ドメイン コントローラーがその IP アドレスに基づいたものになるように、DCCloneConfig.xml ファイルに妥当なサイトを指定することをお勧めします。

コンピューター名は省略できます。 指定しないと、次のアルゴリズムに基づいて一意の名前が生成されます。

-   プレフィックスは、ソース ドメイン コントローラー コンピューター名の最初の 8 文字です。 たとえば、ソース コンピューター名 SourceComputer はプレフィックス文字列 SourceCo に切り詰められます。

-   形式の一意の名前付けサフィックス""CL*nnnn*"がプレフィックス文字列に追加されます、 *nnnn*現在使用されていないと PDC が判断 0001 ~ 9999 の [次へ] の使用可能な値です。 たとえば、許可されているこの範囲で次に使用可能な数字が 0047 の場合、前のコンピューター名プレフィックスの例 SourceCo を使用すると、複製コンピューター用として生成される名前は SourceCo-CL0047 です。

> [!NOTE]
> New-ADDCCloneConfigFile コマンドレットを正常に実行するには、グローバル カタログ (GC) サーバーが必要です。 ソース ドメイン コント ローラーのメンバーシップ、 **Cloneable Domain Controllers**グループは、GC に反映する必要があります。 GC は PDC エミュレーターと同じドメイン コントローラーである必要はありませんが、できれば同じサイト内であることが望まれます。 GC が使用できない場合、コマンドが失敗し、エラー「サーバーが機能していない」 詳細については、「[仮想化ドメイン コントローラーのトラブルシューティング](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)」を参照してください。

静的な IPv4 設定で Clone1 という名前の複製ドメイン コントローラーを作成し、優先 WINS サーバーと代替 WINS サーバーを指定するには、次のように入力します。


    New-ADDCCloneConfigFile "CloneComputerName "Clone1" "Static -IPv4Address "10.0.0.5" "IPv4DNSResolver "10.0.0.1" "IPv4SubnetMask "255.255.0.0" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


> [!NOTE]
> WINS サーバーを指定する場合、両方を指定する必要があります **"PreferredWINSServer**と **"AlternateWINSServer**します。 これらの引数の一方だけを指定すると、複製が失敗し、dcpromo.log にエラー コード 0x80041005 が記録されます。

動的な IPv4 設定で Clone2 という名前の複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" 


> [!NOTE]
> この場合、複製ドメイン コントローラーが到達して関連するネットワーク設定 (IP アドレスなど) を取得できる DHCP サーバーが環境内に存在している必要があります。

動的な IPv4 設定で Clone2 という名前の複製ドメイン コントローラーを作成し、優先 WINS サーバーと代替 WINS サーバーを指定するには、次のように入力します。


    New-ADDCCloneConfigFile -CloneComputerName "Clone2" -IPv4DNSResolver "10.0.0.1" -SiteName "REDMOND" "PreferredWinsServer "10.0.0.1" "AlternateWinsServer "10.0.0.2"


動的な IPv6 設定で複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


静的な IPv6 設定で複製ドメイン コントローラーを作成するには、次のように入力します。


    New-ADDCCloneConfigFile "Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc"


> [!NOTE]
> 静的および動的な設定の唯一の違いを含めることは、IPv6 設定の指定、 **-静的**スイッチします。 包含、 **-静的**スイッチでは、少なくとも 1 つを指定する必須**IPv6DNSResolver**します。ルーターが割り当てられているプレフィックスを持つステートレス アドレス自動構成 (SLAAC) を介して設定するには、静的な IPv6 アドレスが必要です。 動的な ipv6 設定、DNS リゾルバーは省略できますが、複製が IPv6 アドレスと DNS の構成情報を取得するサブネットで、IPv6 対応の DHCP サーバーに到達できることが必要です。

#### <a name="BKMK_OfflineMode"></a>オフライン モードで New-addccloneconfigfile を実行します。
複製用として準備したソース ドメイン コントローラー メディアのコピーが複数存在し (これはそのソース ドメイン コントローラーに複製対象となる許可が与えられ、Get-ADDCCloningExcludedApplicationList コマンドレットが既に実行されていることなどを意味する)、メディア コピーごとに個別の設定を指定する場合は、New-ADDCCloneConfigFile をオフライン モードで実行できます。 この方法は、コピーごとにインポートするなどの手段で VM を個々に準備する方法よりも効率的です。

ここでは、ドメイン管理者はオフライン ディスクをマウントおよび新しい工場出荷時のような自動化を使用して使用できる XML ファイルを追加するには、New-addccloneconfigfile コマンドレットを実行するオフライン引数でリモート サーバー管理ツール (RSAT) を使用できます。Windows PowerShell の Windows Server 2012 に含まれるオプション。 New-ADDCCloneConfigFile コマンドレットをオフライン モードで実行するためにオフライン ディスクをマウントする方法の詳細については、「 [Adding XML to the Offline System Disk](../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Deployment-and-Configuration.md#BKMK_Offline)」を参照してください。

まずソース メディア上でこのコマンドレットをローカルに実行し、前提条件チェックに合格することを確認する必要があります。 前提条件チェックはオフライン モードでは行われません。これは、同じドメイン内に存在しないマシンまたはドメインに参加しているコンピューターからこのコマンドレットが実行される可能性があるためです。 このコマンドレットをローカルに実行すると、DCCloneConfig.xml ファイルが作成されます。 続いてオフライン モードを使用する場合は、ローカルに作成された DCCloneConfig.xml を削除できます。

複製ドメイン コント ローラーを作成するには、という CloneDC1 という REDMOND サイトでのオフライン モードで"静的 IPv4 アドレス。


    New-ADDCCloneConfigFile -Offline -CloneComputerName CloneDC1 -SiteName REDMOND -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -Static -Path F:\Windows\NTDS


静的な IPv4 設定と静的な IPv6 設定で Clone2 という名前の複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.2" -IPv4DNSResolver "10.0.0.1" -IPv4SubnetMask "255.255.0.0" -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone2" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -Path F:\Windows\NTDS


静的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーをオフライン モードで作成し、DNS リゾルバー設定に複数の DNS サーバーを指定するには、次のように入力します。


    New-ADDCCloneConfigFile -Offline -IPv4Address "10.0.0.10" -IPv4SubnetMask "255.255.0.0" -IPv4DefaultGateway "10.0.0.1" -IPv4DNSResolver @( "10.0.0.1","10.0.0.2" ) -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS 


動的な IPv4 設定と静的な IPv6 設定で Clone1 という名前の複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。


    New-ADDCCloneConfigFile -Offline -Static -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -CloneComputerName "Clone1" -PreferredWINSServer "10.0.0.1" -AlternateWINSServer "10.0.0.3" -SiteName "REDMOND" -Path F:\Windows\NTDS


動的な IPv4 設定と動的な IPv6 設定で複製ドメイン コントローラーをオフライン モードで作成するには、次のように入力します。


    New-ADDCCloneConfigFile -Offline -IPv4DNSResolver "10.0.0.1" -IPv6DNSResolver "2002:4898:e0:31fc:d61:2b0a:c9c9:2ccc" -Path F:\Windows\NTDS


### <a name="bkmk7_export_import_vm_sourcedc"></a>手順 4:ソース ドメイン コントローラーの仮想マシンをエクスポートし、続いてインポートする
この手順では、ソース仮想ドメイン コントローラーの仮想マシンをエクスポートし、続いてその仮想マシンをインポートします。 この操作により、ドメイン内に複製仮想ドメイン コントローラーが作成されます。

この操作を行うには、各 Hyper-V ホスト上のローカル Administrators グループのメンバーである必要があります。 サーバーごとに異なる資格情報を使用する場合は、Windows PowerShell コマンドレットを実行して、別々の Windows PowerShell セッションで VM のエクスポートとインポートを行ってください。

ソース ドメイン コントローラー上にスナップショットが存在する場合は、ソース ドメイン コントローラーをエクスポートする前にそれらのスナップショットを削除する必要があります。これは、ターゲットの Hyper-V ホストと互換性のないプロセッサ設定がスナップショットに含まれていると、VM がインポートを行わないためです。 ソースの Hyper-V ホストとターゲットの Hyper-V ホストとの間でプロセッサ設定の互換性がとれている場合には、最初にスナップショットを削除することなくソースのエクスポートとコピーを行うことができます。 ただし、インポートの後で、複製 VM を起動する前に複製 VM からスナップショットを削除する必要があります。

##### <a name="to-copy-a-virtual-domain-controller-by-exporting-and-then-importing-the-virtualized-source-domain-controller"></a>仮想化ソース ドメイン コントローラーをエクスポートしてインポートすることによって仮想ドメイン コントローラーをコピーするには

1.  **HyperV1** 上で、ソース ドメイン コントローラー (**VirtualDC1**) を停止します。

    ![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。

    STOP-VM-VirtualDC1-computername HyperV1 の名前


2.  **HyperV1**上で、スナップショットを削除して、ソース ドメイン コントローラー (VirtualDC1) を c:\CloneDCs ディレクトリにエクスポートします。

> [!NOTE]
> スナップショットが作成されると、その都度差分ディスクとして機能する新しい AVHD ファイルが作成されるため、関連するすべてのスナップショットを削除する必要があります。 これは連鎖的影響を及ぼします。 スナップショットを作成して DCCLoneConfig.xml ファイルを VHD に挿入した場合は、古い DIT バージョンから複製が作成されたり、構成ファイルが不適切な VHD ファイルに挿入されたりする可能性があります。 スナップショットを削除すると、これらの AVHD がすべて結合されてベース VHD に取り込まれます。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。


    Get-VMSnapshot VirtualDC1 | Remove-VMSnapshot -IncludeAllChildSnapshots
    Export-VM -Name VirtualDC1 -ComputerName HyperV1 -Path c:\CloneDCs\VirtualDC1


3.  フォルダー **virtualdc1** を、 **HyperV2**の c:\Import ディレクトリにコピーします。

4.  **HyperV2** で、**Hyper-V マネージャー**を使用して (**Hyper-V マネージャー**内の**仮想マシンのインポート** ウィザードを使用して) フォルダー **c:\Import\virtualdc1** から仮想マシンをインポートし、関連付けられた**スナップショット**をすべて削除します。

仮想マシンをインポートする際には、 **[仮想マシンをコピーする (新しい一意な ID を作成する)]** オプションを使用します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。

    $path = Get-ChildItem "C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual Machines"
    $vm = Import-VM -Path $path.fullname -Copy -GenerateNewId
    Rename-VM $vm VirtualDC2


同じソース ドメイン コントローラーから複数の複製ドメイン コントローラーを作成するには、次のように行います。

  -   UI: **仮想マシンのインポート** ウィザードで、**[仮想マシンの構成フォルダー]**、**[スナップショット ストア]**、**[スマート ページング フォルダー]** に新しい場所を指定し、仮想マシンの仮想ハード ディスクに別の **[場所]** を指定します。

  -   Windows PowerShell: 次のパラメーターを使用して仮想マシンの新しい場所を指定する、`Import-VM`コマンドレット。

        $path = Get-childitem「C:\CloneDCs\VirtualDC1\VirtualDC1\Virtual マシン」IMPORT-VM-パス $path.fullname - コピー - GenerateNewId-computername HyperV2 VhdDestinationPath-"path"SnapshotFilePath-"path"SmartPagingFilePath-"path"-VirtualMachinePath「パス」


> [!NOTE]
> 複数の複製ドメイン コントローラーを同時に作成する場合に推奨されるバッチ サイズは 10 です。 最大数は、出力方向のレプリケーション接続の最大数 (既定では、分散ファイル システム レプリケーション (DFSR) は 16、ファイル レプリケーション サービス (FRS) は 10) によって制限されます。 環境で数を十分にテストしていない限り、推奨数を超える数の複製ドメイン コントローラーを同時に展開することは避けてください。

5.  **HyperV1** で、ソース ドメイン コントローラー (**VirtualDC1**) を再起動して、オンライン状態に戻します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。

    Start-VM -Name VirtualDC1 -ComputerName HyperV1


6.  **HyperV2**で、仮想マシン (**VirtualDC2**) を起動し、ドメインにおける複製ドメイン コントローラーとしてこの仮想マシンをオンラインに戻します。

![AD DS の概要](../media/Introduction-to-Active-Directory-Domain-Services--AD-DS--Virtualization--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。


    Start-VM -Name VirtualDC2 -ComputerName HyperV2

> [!NOTE]
> 複製を確実に行うには、PDC エミュレーターを実行しておく必要があります。 この仮想マシンが停止された場合は、起動して、初期同期を実行してあることを確認してください。これにより、この仮想マシンは PDC エミュレーターの役割を持っていることを認識します。 詳細については、マイクロソフトのサポート技術情報記事 305476 「 [Windows 2000 Server および Windows Server 2003 における操作マスタの役割を持つサーバーの初期同期の要件](https://support.microsoft.com/kb/305476)」を参照してください。

複製が完了した後で、複製コンピューターの名前を調べ、複製操作が正常に行われたことを確認してください。 VM がディレクトリ サービス復元モード (DSRM) で起動しなかったことを確認してください。 ログオンを試みて、使用できるログオン サーバーが存在しないということを伝えるエラーが表示される場合は、DSRM でのログオンを試してください。 DC が正常に複製されず、DSRM で起動される場合は、イベント ビューアー内のログと %systemroot%/debug フォルダー内の dcpromo ログをチェックしてください。

複製されたドメイン コントローラーは、**[Cloneable Domain Controllers]** グループのメンバーになります。これは、複製されたドメイン コントローラーがソース ドメイン コントローラーのメンバーシップをコピーするためです。 ベスト プラクティスとして、複製操作の準備が整うまでは **[Cloneable Domain Controllers]** グループを空にして、複製操作が完了した時点でメンバーを削除することをお勧めします。

ソース ドメイン コントローラーがバックアップ メディアを保存する場合は、複製されたドメイン コントローラーもバックアップ メディアを保存します。 複製されたドメイン コントローラー上のバックアップ メディアは、 `wbadmin get versions` を実行して表示できます。 Domain Admins グループのメンバーは、複製されたドメイン コントローラー上のバックアップ メディアが誤って復元されることがないように、それらのバックアップ メディアを削除する必要があります。 wbadmin.exe を使用してシステム状態のバックアップを削除する方法の詳細については、「 [Wbadmin delete systemstatebackup (Wbadmin の削除 systemstatebackup)](https://technet.microsoft.com/library/cc742081(v=WS.10).aspx)」を参照してください。

## <a name="troubleshooting"></a>トラブルシューティング
複製ドメイン コントローラー (**VirtualDC2**) がディレクトリ サービス復元モード (DSRM) で起動する場合、次の再起動時にこの複製ドメイン コントローラーがそれ自体で標準モードに戻ることはありません。 DSRM で起動しているドメイン コントローラーにログオンするには、**.\Administrator** を使用して、DSRM パスワードを指定します。

複製が失敗する原因を正し、dcpromo.log に複製を再試行できないということが示されていないことを確認してください。 複製を再試行できない場合は、メディアの安全破棄を行ってください。 複製を再試行できる場合は、複製をもう一度試すためにブート フラグ「DS 復元モード」を削除する必要があります。

1.  管理者特権のコマンド (右は Windows Server 2012 をクリックして管理者として実行 を選択、) と入力し、Windows Server 2012 を開く**msconfig**します。

2.  **[ブート]** タブの **[ブート オプション]** で、**[セーフ ブート]** をオフにします (既に選択されていて、オプションの **[Active Directory 修復]** が有効になっています)。

3.  **[OK]** をクリックして、プロンプトが表示されたら再起動します。

仮想化ドメイン コントローラーのトラブルシューティングにの詳細については、「 [Virtualized Domain Controller Troubleshooting](../ad-ds/manage/virtual-dc/Virtualized-Domain-Controller-Troubleshooting.md)」を参照してください。


