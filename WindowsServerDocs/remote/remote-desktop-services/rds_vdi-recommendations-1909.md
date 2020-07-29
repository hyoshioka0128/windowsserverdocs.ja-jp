---
title: 仮想デスクトップ インフラストラクチャ (VDI) ロール用の Windows 10 バージョン 1909 の最適化
description: VDI イメージとして使用される Windows 10 バージョン 1909 デスクトップのオーバーヘッドを最小限に抑える推奨の設定および構成。
ms.prod: windows-server
ms.reviewer: robsmi
ms.technology: remote-desktop-services
ms.author: helohr
ms.topic: article
author: heidilohr
manager: lizross
ms.date: 02/19/2020
ms.openlocfilehash: 7568db50f09273b398955c314491b903f627d1a9
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182098"
---
# <a name="optimizing-windows-10-version-1909-for-a-virtual-desktop-infrastructure-vdi-role"></a>仮想デスクトップ インフラストラクチャ (VDI) ロール用の Windows 10 バージョン 1909 の最適化

この記事では、仮想デスクトップ インフラストラクチャ (VDI) 環境で最高のパフォーマンスをもたらす Windows 10 バージョン 1909 (ビルド 18363) の設定を選択する方法について説明します。 このガイドのすべての設定は、考慮すべき推奨事項であり、要件では決してありません。

VDI 環境で Windows 10 のパフォーマンスを最適化する主な方法は、アプリのグラフィックスの再描画と、VDI 環境に大きなメリットがないバックグラウンド アクティビティを最小限に抑え、実行中のプロセスを必要最小限まで全般的に低減するというものです。 2 次的な目標は、基本イメージでのディスク領域使用量を必要最低限まで低減することです。 VDI の実装では、可能な最小の基本イメージつまり "ゴールド" イメージのサイズであれば、ハイパーバイザーでのメモリ使用量を少し減らすことができ、デスクトップ イメージをコンシューマーに配信するために必要なネットワーク操作全体も少し削減できます。

> [!NOTE]
> これらの推奨設定は、物理マシンや他の仮想マシン上のものも含め、Windows 10 1909 の他のインストールに適用できます。 この記事の推奨事項はいずれも、Windows 10 1909 のサポート性に影響しません。

## <a name="vdi-optimization-principles"></a>VDI 最適化の原則

VDI 環境は、ネットワーク上のコンピューター ユーザーに、アプリケーションを含む完全なデスクトップ セッションを表示します。 ネットワーク配信手段は、オンプレミス ネットワークでもインターネットでもかまいません。 VDI 環境は "基本" オペレーティング システムのイメージであり、これがその後、ユーザーに提示されるデスクトップの基礎になります。 VDI の実装には、"永続的"、"非永続的"、"デスクトップ セッション" などのバリエーションが存在します。 永続的タイプは、セッション間で VDI デスクトップ OS の変更内容を保持します。 非永続的タイプは、セッション間で VDI デスクトップ OS の変更内容を保持しません。 ユーザーにとっては、このデスクトップは他の仮想または物理デバイスとほとんど違いはありませんが、ネットワーク経由でアクセスされる点が異なります。

最適化設定は、参照デバイス上で行います。 VM は、状態の保存、チェックポイントの作成、バックアップの作成を行えるため、イメージを構築するための理想的な場所になります。 既定の OS インストールは、ベース VM で実行されます。 そのベース VM はその後、不要なアプリの削除、Windows 更新プログラムのインストール、他の更新プログラムのインストール、一時ファイルの削除、設定の適用によって最適化されます。

VDI には、リモート デスクトップ セッション (RDS) や最近リリースされた [Windows 仮想デスクトップ](https://azure.microsoft.com/services/virtual-desktop/)などの他の種類があります。 これらのテクノロジに関する詳細な説明は、この記事の範囲外です。 この記事では、ホストの最適化など、環境内の他の要因には言及せずに、Windows 基本イメージ設定に焦点を当てます。

セキュリティと安定性は、Microsoft にとって製品とサービスに関する最優先事項です。 企業のお客様は、インターネットの有無にかかわらず機能する一連のサービスである組み込みの Windows セキュリティを利用される場合があります。 インターネットに接続されていない VDI 環境については、Microsoft からシグネチャ更新が 1 日に複数リリースされる可能性があるため、セキュリティ シグネチャを 1 日に複数回ダウンロードできます。 これらのシグニチャは、永続的か非永続的かにかかわらず、VDI VM に提供され、実稼働中にインストールされるようにスケジュールされます。 これにより、VM の保護は可能な限り最新の状態になります。

インターネットに接続されていないため、クラウド対応のセキュリティに参加できない VDI 環境に対しては、適用できないセキュリティ設定がいくつかあります。 "通常の" Windows デバイスでは、クラウド エクスペリエンスや Microsoft Store など、その他の設定も利用できます。 未使用の機能へのアクセスを排除することで、フットプリント、ネットワーク帯域幅、および攻撃対象領域を削減できます。

更新に関しては、Windows 10 は毎月の更新アルゴリズムを利用するため、クライアントが更新を試みる必要はありません。 ほとんどの場合、VDI 管理者は、"マスター" または "ゴールド" のイメージに基づいて VM をシャットダウンするプロセスを通じて更新プロセスを制御し、読み取り専用のイメージの保護を解除し、イメージに修正プログラムを適用した後、再シールして実稼働に戻します。 そのため、VDI VM で Windows Update をチェックする必要はありません。 永続的 VDI VM など、場合によっては、通常の修正プログラムの適用手順が実行されます。 Windows Update または Microsoft Intune を使用することもできます。 System Center Configuration Manager を使用して、更新プログラムおよびその他のパッケージ配信を処理できます。 VDI を更新するための最適な方法は、各組織が決定することになります。

> [!TIP]
> このトピックで説明する最適化を実装するスクリプトは、**LGPO.exe** でインポートできる GPO エクスポート ファイルと同様に、GitHub 上の [TheVDIGuys](https://github.com/TheVDIGuys) で利用できます。

このスクリプトは、ご使用の環境と要件に合わせて設計されています。 メイン コードは PowerShell です。この作業は、入力ファイル (プレーン テキスト) とローカル グループ ポリシー オブジェクト (LGPO) ツールのエクスポート ファイルを使用して行われます。 これらのファイルには、削除するアプリと無効にするサービスの一覧が含まれています。 特定のアプリの削除や特定のサービスの無効化を行いたくない場合は、対応するテキスト ファイルを編集してその項目を削除します。 最後に、お使いのデバイスにインポートできるローカル ポリシー設定があります。 設定の一部は次回の再起動時またはコンポーネントが最初に使用されたときに有効になるため、グループ ポリシーを使用して設定を適用するよりも、基本イメージ内でいくつかの設定を使用することをお勧めします。

### <a name="persistent-vdi"></a>永続的 VDI

永続的 VDI は、基本的なレベルで、再起動間のオペレーティング システムの状態を保存する VM です。 VDI ソリューションの他のソフトウェア レイヤーは、多くの場合シングル サインオン ソリューションによって、割り当てられている VM への簡単でシームレスなアクセスをユーザーにもたらします。

永続的 VDI には複数の異なる実装があります。

- 従来の仮想マシン。この場合、VM は、独自の仮想ディスク ファイルを保有し、通常どおりに起動し、セッション間で変更内容を保存します。 違いは、ユーザーがこの VM にアクセスする方法です。 ユーザーをその 1 つ以上の割り当て済み VDI VM に自動的に誘導する、ユーザーがログインする Web ポータルが存在する可能性があります。

- イメージ ベースの永続的仮想マシン (必要に応じて、個人用の仮想ディスクを使用) この種の実装では、1 つ以上のホスト サーバー上に基本/ゴールド イメージがあります。 VM が作成され、1 つ以上の仮想ディスクが作成され、永続的ストレージ用にこのディスクに割り当てられます。

    - VM が起動すると、基本イメージのコピーがその VM のメモリに読み込まれます。 同時に、永続的仮想ディスクがその VM に割り当てられ、複雑なプロセスを通じて以前のオペレーティング システムの変更内容がマージされます。

    - イベント ログの書き込み、ログの書き込みなどの変更内容は、その VM に割り当てられている読み取り/書き込みの仮想ディスクにリダイレクトされます。

    - このような状況では、オペレーティング システムとアプリ サービスは、Windows Server Update Services やその他の管理テクノロジなどの従来のサービス ソフトウェアを使用して、通常どおり動作する可能性があります。

    - 永続的 VDI マシンと "通常の" 仮想マシンの違いは、マスター/ゴールド イメージとの関係です。 ある時点で、更新プログラムをマスターに適用する必要があります。 これは、ユーザーの永続的な変更をどのように処理するかを実装で決定する場所になります。 場合によっては、変更されたディスクが破棄またはリセットされるため、新しいチェックポイントを設定します。 また、ユーザーが行った変更が毎月の品質更新プログラムを通して保持され、ベースが機能更新プログラム後にリセットされることもあります。

### <a name="non-persistent-vdi"></a>非永続的 VDI

非永続的 VDI 実装がベース イメージまたは "ゴールド" イメージに基づいている場合、最適化はほとんどの場合、ベース イメージで実行され、続いてローカル設定およびローカル ポリシーを通じて実行されます。

イメージ ベースの非永続的 VDI では、基本イメージは読み取り専用です。 非永続的 VM が起動すると、基本イメージのコピーが VM にストリーミングされます。 起動中およびその後次回再起動するまでに発生したアクティビティは、一時的な場所にリダイレクトされます。 ユーザーには通常、データを格納するためのネットワークの場所が用意されています。 場合によっては、ユーザーのプロファイルが標準 VM と結合されて、ユーザーにその設定が提供されます。

単一のイメージに基づく非永続的 VDI の重要な側面の 1 つに、サービスがあります。 オペレーティング システムとコンポーネントの更新は、通常は月に 1 回配信されます。 イメージ ベースの VDI では、イメージに対する更新プログラムを取得するために実行する必要のある一連のプロセスがあります。

- 特定のホストでは、そのホスト上の、ベース イメージから派生したすべての VM をシャット ダウンまたはオフにする必要があります。 つまり、ユーザーは他の VM にリダイレクトされます。

- 続いて基本イメージが開き、起動します。 オペレーティング システムの更新プログラム、.NET の更新プログラム、アプリの更新プログラムなど、すべてのメンテナンス作業が実行します。

- この時点で適用する必要がある新しい設定が適用されます。

- この時点でその他のすべてのメンテナンスが実行されます。

- 続いて基本イメージはシャット ダウンされます。

- 基本イメージは封印され、実稼働環境に戻るように設定されます。

- ユーザーはログオンし直すことができます。

> [!NOTE]
> Windows 10 は、定期的に一連のメンテナンス タスクを自動的に実行します。 既定で毎日午前 3 時に実行するように設定済みのスケジュールされたタスクがあります。 このスケジュールされたタスクは、Windows Update のクリーンアップなどの一連のタスクを実行します。 次の PowerShell コマンドで、自動的に行われるメンテナンスのすべてのカテゴリを表示することができます。
>
>```powershell
>Get-ScheduledTask | ? {$_.Settings.MaintenanceSettings}
>```
>

非永続的 VDI の課題の 1 つは、ユーザーがログオフしたときに、オペレーティング システムのほぼすべてのアクティビティが破棄されるということです。 ユーザーのプロファイルや状態は、集中管理された場所に保存される場合がありますが、仮想マシン自体は、前回の起動以降に行われた変更内容のほぼすべてを破棄します。 したがって、セッション間で状態を保存する、Windows コンピューターを対象にした最適化は、適用できなくなります。

VDI VM の VDI のアーキテクチャによっては、PreFetch や SuperFetch などは、VM の再起動時にすべての最適化が破棄されるので、セッション間には役立ちません。 インデックス作成は、従来のデフラグなどのディスク最適化と同様に、リソースの一部を無駄にする可能性があります。

> [!NOTE]
> 仮想化を使用してイメージを準備し、イメージの作成プロセス中にインターネットに接続している場合は、最初のログオン時に、 **[設定]** 、 **[Windows Update]** の順に移動して、機能更新プログラムを延期する必要があります。

### <a name="to-sysprep-or-not-sysprep"></a>Sysprep の可否

Windows 10 には、[システム準備ツール](/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview) (多くの場合、"Sysprep" と略されます) と呼ばれる組み込み機能があります。 Sysprep ツールは、複製用にカスタマイズされた Windows 10 イメージを準備するために使用されます。 Sysprep プロセスは、最終的なオペレーティング システムが実稼働環境で実行するために適切に一意になっているようにします。

Sysprep を実行したほうがよい理由としないほうがよい理由があります。 VDI の場合、このイメージを使用してログオンする以降のユーザーにとってのプロファイル テンプレートとして使用される既定のユーザー プロファイルをカスタマイズする機能が必要になることがあります。 必要なアプリがインストールされているが、アプリごとの設定を制御できる場合もあります。

代替方法はインストール元の標準の .ISO を使用するというもので、おそらく無人インストール応答ファイルやタスク シーケンスを使用してアプリケーションをインストールしたりアプリケーションを削除したりします。 また、タスク シーケンスを使用して、イメージのローカル ポリシー設定を指定することもできます (たとえば、[ローカル グループ ポリシー オブジェクト ユーティリティ (LGPO) ツール](/archive/blogs/secguide/lgpo-exe-local-group-policy-object-utility-v1-0)を使用)。

### <a name="supportability"></a>サポート

Windows の既定値が変更されるたびに、サポート性に関する疑問点が生じます。 VDI イメージ (VM またはセッション) をカスタマイズしたら、イメージに加えられたすべての変更を変更ログで追跡する必要があります。 トラブルシューティングでは、多くの場合、イメージをプール内で分離し、問題分析用に構成できます。 問題が根本原因まで追跡されると、その変更を最初にテスト環境に展開し、最終的には実稼働ワークロードに展開できます。

このドキュメントでは、セキュリティに影響を与えるシステム サービス、ポリシー、またはタスクに言及することを意図的に避けています。 続いては、Windows サービスです。 メンテナンス期間以外で VDI イメージにサービスを提供する機能は削除されました。これは、"*セキュリティ ソフトウェア更新を除き*"、VDI 環境におけるほとんどのサービス イベントの発生時にメンテナンス期間が存在するためです。 Microsoft では、VDI 環境における Windows セキュリティのガイダンスを公開しています。 詳細については、「[仮想デスクトップ インフラストラクチャ (VDI) 環境への Windows Defender ウイルス対策の展開ガイド](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus)」を参照してください。

既定の Windows 設定を変更する場合は、サポート性を考慮してください。 ハードニング、"ライトニング" などの名のもとに、システム サービス、ポリシー、またはスケジュールされたタスクを変更すると、困難な問題が発生する可能性があります。既定の設定の変更に関する最新の既知の問題については、Microsoft サポート技術情報を参照してください。 このドキュメントのガイダンスと GitHub 上の関連スクリプトは、既知の問題が発生した場合に備えて維持されます。 また、いくつかの方法で Microsoft に問題を報告していただくこともできます。

任意の検索エンジンで “"開始値" site:support.microsoft.com” という語句を検索すると、サービスの既定の開始値に関する既知の問題を表示できます。

このドキュメントと GitHub 上の関連するスクリプトでは、既定のアクセス許可が変更されないことに留意してください。 セキュリティ設定の強化を望まれる場合は、**AaronLocker** として知られているプロジェクトで開始してください。 詳細については、「[発表:"AaronLocker" を使用したアプリケーションのホワイトリスト登録](/archive/blogs/aaron_margosis/announcing-application-whitelisting-with-aaronlocker)」を参照してください。

#### <a name="vdi-optimization-categories"></a>VDI 最適化のカテゴリ

- グローバル オペレーティング システム設定のカテゴリ:

    - UWP アプリのクリーンアップ

    - オプション機能のクリーンアップ

    - ローカル ポリシー設定

    - システム サービス

    - スケジュールされたタスク

    - Windows と他の更新プログラムを適用する

    - Windows の自動トレース

    - イメージの最終処理 (封印) 前のディスク クリーンアップ

    - ユーザー設定

    - ハイパーバイザー/ホスト設定

### <a name="universal-windows-platform-uwp-application-cleanup"></a>ユニバーサル Windows プラットフォーム (UWP) アプリケーションのクリーンアップ

VDI イメージの目標の 1 つは、できるだけ軽量にすることです。 イメージのサイズを減らす 1 つの方法は、その環境で使用されない UWP アプリケーションを削除することです。 UWP アプリでは、ペイロードと呼ばれる、メインのアプリケーション ファイルがあります。 アプリケーション固有の設定に関する、各ユーザーのプロファイルに格納されている少量のデータがあります。 "All Users" のプロファイルにも少量のデータがあります。

UWP アプリのクリーンアップには、接続とタイミングが重要な要素です。 ネットワーク接続のないデバイスに基本イメージを展開する場合、ユーザーがアプリをアンインストールしようとしている間、Windows 10 は Microsoft Store に接続してアプリをダウンロードしてインストールを試みることができません。 これは、時間をかけてイメージをカスタマイズし、イメージ作成プロセスの後の段階で残っているものを更新できるようにするための適切な戦略である可能性があります。

Windows 10 のインストールに使用する基本 .WIM を変更し、インストール前に不要な UWP アプリを .WIM から削除すると、アプリが最初にインストールされず、プロファイルの作成時間が短縮されます。 インストール .WIM ファイルから UWP アプリを削除する方法については、このセクションで後から説明します。

VDI の適切な戦略は、基本イメージで必要なアプリをプロビジョニングしてから、Microsoft Store へのその後のアクセスをブロックすることです。 ストア アプリは、通常のコンピューターでバック グラウンドで定期的に更新されます。 UWP アプリは、他の更新プログラムが適用されると、メンテナンス期間中に更新できます。 詳細については、「[ユニバーサル Windows プラットフォーム アプリ](https://docs.citrix.com/citrix-virtual-apps-desktops/manage-deployment/applications-manage/universal-apps.html)」を参照してください

#### <a name="delete-the-payload-of-uwp-apps"></a>UWP アプリのペイロードを削除する

不要な UWP アプリがまだファイル システムに存在し、少量のディスク領域を消費しています。 決して必要にならないアプリについては、PowerShell コマンドを使用して、不要な UWP アプリのペイロードを基本イメージから削除できます。

実際、このセクションの後から提供するリンクを使用してインストール .WIM ファイルからこれらを削除する場合、UWP アプリの非常に少ない一覧の冒頭から始められる必要があります。

PowerShell からのこの切り詰められた出力例に示すように、次のコマンドを実行して、実行中のオペレーティング システムからプロビジョニング済みの UWP アプリを列挙します。

```powershell

    Get-AppxProvisionedPackage -Online

    DisplayName  : Microsoft.3DBuilder
    Version      : 13.0.10349.0
    Architecture : neutral
    ResourceId   : \~
    PackageName  : Microsoft.3DBuilder_13.0.10349.0_neutral_\~_8wekyb3d8bbwe
    Regions      :
    ...
```

システムにプロビジョニングされている UWP アプリは、タスク シーケンスの一環としてオペレーティング システムのインストール中に、またはオペレーティング システムのインストール後に後から削除することができます。 これは、イメージ モジュラーを作成または維持するプロセス全体を構成するので、推奨の方法になる可能性があります。 スクリプトを開発した後は、以降のビルドで何かが変更された場合に、プロセスを最初から繰り返すのではなく、既存のスクリプトを編集します。 このトピックの情報へのリンクを次に示します。

[タスク シーケンス中の Windows 10 インボックス アプリの削除](/archive/blogs/mniehaus/removing-windows-10-in-box-apps-during-a-task-sequence)

[PowerShell バージョン 1.3 を使用した Windows 10 WIM ファイルからの組み込みアプリの削除](https://gallery.technet.microsoft.com/Removing-Built-in-apps-65dc387b)

[Windows 10 1607:機能更新プログラムの展開時でのアプリの復帰の防止](/archive/blogs/mniehaus/windows-10-1607-keeping-apps-from-coming-back-when-deploying-the-feature-update)

続いて [Remove-AppxProvisionedPackage](/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) PowerShell コマンドを実行して、UWP アプリ ペイロードを削除します。

```powershell
Remove-AppxProvisionedPackage -Online -PackageName
```

それぞれの一意の環境での適用性について各 UWP アプリを評価する必要があります。 Windows 10 1909 の既定のインストール環境をインストールしてから、どのアプリが実行されていてメモリを消費しているかを確認することをお勧めします。 たとえば、自動的に起動するアプリや、 [スタート] メニューに自動的に情報を表示するアプリ (たとえば [天気とニュース] ) など、自分の環境には役に立たないものを削除することを検討できます。

>[!NOTE]
>GitHub のスクリプトを利用すれば、スクリプトを実行する前に、どのアプリを削除するかを簡単に制御できます。 スクリプト ファイルをダウンロードした後、"Win10_1909_AppxPackages.txt" ファイルを見つけて編集し、Microsoft 電卓や Microsoft 付箋など、残しておきたいアプリのエントリを削除します。

### <a name="manage-windows-optional-features-using-powershell"></a>PowerShell を使用して Windows のオプション機能を管理する

PowerShell を使用して Windows のオプション機能を管理できます。 詳細については、[Windows Server の PowerShell のフォーラム](https://docs.microsoft.com/answers/topics/windows-server-powershell.html)をご覧ください。 現在インストールされている Windows の機能を列挙するには、次の PowerShell コマンドを実行します。

```powershell
Get-WindowsOptionalFeature -Online
```

次の例に示すように、特定の Windows オプション機能を有効または無効にできます。

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName "DirectPlay" -All
```

次の例に示すように、VDI イメージの機能を無効にすることができます。

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName “WindowsMediaPlayer”
```

次に、Windows Media Player パッケージを削除することを検討できます。 Windows 10 1909 には、次の 2 つの Windows Media Player パッケージがあります。

```powershell
Get-WindowsPackage -Online -PackageName *media*

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : DISM Package Manager Provider
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1.mum
InstallTime       : 3/19/2019 6:20:22 AM
...

Features         : {}

PackageName       : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449
Applicable        : True
Copyright        : Copyright (c) Microsoft Corporation. All Rights Reserved
Company         :
CreationTime       :
Description       : Play audio and video files on your local device and on the Internet.
InstallClient      : UpdateAgentLCU
InstallPackageName    : Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.449.mum
InstallTime       : 10/29/2019 5:15:17 AM
...
```

Windows Media Player パッケージを削除する場合 (約 60 MB のディスク領域を解放):

```powershell
 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1 -Online

 Remove-WindowsPackage -PackageName Microsoft-Windows-MediaPlayer-Package~31bf3856ad364e35~amd64~~10.0.18362.1 -Online
```

#### <a name="enable-or-disable-windows-features-using-dism"></a>DISM を使用して Windows の機能を有効または無効にする

組み込みの Dism.exe ツールを使用して、Windows オプション機能を列挙および制御できます。 Dism.exe スクリプトは、オペレーティング システムのインストール タスク シーケンス中に開発および実行できます。 関連する Windows テクノロジは、[オンデマンド機能](/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)と呼ばれます。

#### <a name="default-user-settings"></a>既定のユーザー設定

"C:\Users\Default\NTUSER.DAT" という名前の Windows レジストリ ファイルにカスタマイズを行うことができます。 このファイルに対して行われたすべての設定は、このイメージを実行するデバイスから作成された後続のユーザー プロファイルに適用されます。 既定のユーザー プロファイルに適用する設定を制御するには、"Win10_1909_DefaultUserSettings.txt" ファイルを編集します。 注意して検討する必要がある設定の 1 つに、この推奨される設定の繰り返しで新規のものである **TaskbarSmallIcons** という設定があります。 この設定を実装する前に、ユーザー ベースで確認することをお勧めします。 **TaskbarSmallIcons** は、Windows タスク バーを小さくして使用する画面領域を削減し、アイコンをよりコンパクトにして検索インターフェイスを最小化します。これを適用する前と後を次の図に示します。

図 1:通常の Windows 10 バージョン 1909 タスク バー

![標準バージョンの Windows 10 バージョン 1909 タスク バー](media/rds-vdi-recommendations-1909/standard-taskbar.png)

図 2:小さいアイコン設定を使用したタスク バー

![小さいアイコン設定を使用したタスク バー](media/rds-vdi-recommendations-1909/taskbar-sm-icons.png)

また、VDI インフラストラクチャでのイメージの送信を減らすために、既定の Windows 10 イメージの代わりに既定の背景を単色に設定できます。 ログオン画面を単色に設定したり、ログオン時の不透明なぼかし効果をオフにしたりすることもできます。

次の設定は、主にアニメーションを減らすために、既定のユーザー プロファイル レジストリ ハイブに適用されます。 これらの設定の一部またはすべてが不要な場合は、このイメージに基づく新しいユーザー プロファイルに適用しない設定を削除します。 これらの設定の目的は、次の同等の設定を有効にすることです。

図 3:最適化されたシステム プロパティ、パフォーマンス オプション

![最適化されたシステム プロパティ、パフォーマンス オプション](media/rds-vdi-recommendations-1909/performance-options.png)

パフォーマンスを最適化するために、既定のユーザー プロファイル レジストリ ハイブに適用される最適化設定を次に示します。

```
Delete HKLM\Temp\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v OneDriveSetup /f
add "HKLM\Temp\Control Panel\Desktop" /v DragFullWindows /t REG_SZ /d 0 /f
add "HKLM\Temp\Control Panel\Desktop" /v WallPaper /t REG_SZ /d "" /f
add "HKLM\Temp\Control Panel\Desktop\WindowMetrics" /v MinAnimate /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AccentColor /t REG_DWORD /d 4292311040 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v ColorizationColor /t REG_DWORD /d 4292311040 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AlwaysHibernateThumbnails /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v EnableAeroPeek /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\DWM /v AlwaysHibernateThumbnails /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v AutoCheckSelect /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v HideIcons /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ListviewAlphaSelect /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ListViewShadow /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v ShowInfoTip /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v TaskbarAnimations /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced /v TaskbarSmallIcons /t REG_DWORD /d 1 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\People /v PeopleBand /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\AnimateMinMax /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\ComboBoxAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\ControlAnimations /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\DWMAeroPeekEnabled /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\DWMSaveThumbnailEnabled /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\MenuAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\SelectionFade /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\TaskbarAnimations /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects\TooltipAnimation /v DefaultApplied /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SubscribedContent-338388Enabled /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SubscribedContent-338389Enabled /t REG_DWORD /d 0 /f
add HKLM\Temp\Software\Microsoft\Windows\CurrentVersion\ContentDeliveryManager /v SystemPaneSuggestionsEnabled /t REG_DWORD /d 0 /f
```

ローカル ポリシー設定で、VDI の背景のイメージを無効にすることができます。  イメージが必要な場合は、色深度を減らしてカスタムの背景イメージを作成し、イメージ情報の送信に使用するネットワーク帯域幅を制限することができます。 ローカル ポリシーで背景イメージを指定しない場合は、ローカル ポリシーを設定する前に背景色を設定することをお勧めします。ポリシーを設定すると、ユーザーは背景色を変更できなくなるためです。 背景イメージとして "(null)" を指定する方が適切な場合があります。 次のセクションでは、リモート デスクトップ プロトコル セッションで背景を使用しない別のポリシー設定を示します。

### <a name="local-policy-settings"></a>ローカル ポリシー設定

VDI 環境での Windows 10 の多数の最適化は、Windows ポリシーを使用して行うことができます。 このセクションの表に示されている設定は、ベース/ゴール ドイメージにローカルに適用できます。 同等の設定がグループ ポリシーなどの他の方法で指定されていない場合も、この設定が適用されます。

一部の判断は、以下のような環境の詳細に基づく場合があります。

- VDI 環境は、インターネットへのアクセスを許可されているか。

- VDI ソリューションが永続的か非永続的か。

次の設定は、セキュリティに関係する設定と対立したり競合したりしないように選択されています。 これらの設定は、VDI 環境に適用できない可能性がある設定を削除したり、機能を無効にしたりするために選択されました。

| ポリシー設定 | Item | サブ項目 | 考えられる設定とコメント|
| -------------- | ---- | -------- | ---------------------------- |
| ローカル コンピューター ポリシー\\コンピューターの構成\\Windows の設定\\セキュリティの設定 | | | |
| ネットワーク リスト マネージャー ポリシー | すべてのネットワーク プロパティ | ネットワークの場所 | ユーザーは場所を変更できません |
| ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\コントロール パネル | | | |
| *コントロール パネル | オンラインのヒントを許可する | | 無効にします。 設定は、Microsoft コンテンツ サービスに問い合わせて、ヒントやヘルプ コンテンツを取得しません。 |
| *コントロール パネル\個人用設定 | ロック画面を表示しない | 有効にします。 この設定では、ロック画面をユーザーに表示するかどうかを制御します。 このポリシー設定を有効にした場合、サインイン前に Ctrl + Alt + Del キーを押す必要がないユーザーが PC をロックした後、選択したタイルが表示されます。 |
| *コントロール パネル\個人用設定 | 特定の既定のロック画面とログオン イメージを強制する | [![ロック画面へのパスを設定するための UI](media/lock-screen-image-settings.png)](media/lock-screen-image-settings.png) | 有効にします。 この設定では、ユーザーがサイン インしていないときに表示される既定のロック画面およびログオン画像を指定できるようにし、また、指定された画像をすべてのユーザーの既定に設定します (既定の画像を置き換えます)。<p>イメージがレンダリングされるたびにネットワーク経由で送信されるデータが少なくなるように、低解像度の複雑でない画像を使用することをお勧めします。 |
| *コントロール パネル\地域と言語のオプション\手書き認識の個人用設定 | 自動学習機能をオフにする | | 有効にします。 このポリシー設定を有効にした場合、自動学習機能は停止し、格納されたデータはすべて削除されます。 ユーザーは、コントロール パネルでこの設定を構成することはできません。 |
| ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\ネットワーク | | | |
| バックグラウンド インテリジェント転送サービス (BITS) | BITS クライアントでの Windows ブランチ キャッシュの使用を許可しない |  | Enabled |
| バックグラウンド インテリジェント転送サービス (BITS) | コンピューターが BITS のピアキャッシュ クライアントとして動作しないようにする |  | Enabled |
| バックグラウンド インテリジェント転送サービス (BITS) | コンピューターが BITS のピアキャッシュ サーバーとして動作しないようにする |  | Enabled |
| バックグラウンド インテリジェント転送サービス (BITS) | BITS のピアキャッシュを許可する |  | 無効 |
| BranchCache | BranchCache を有効にする |  | 無効 |
| *フォント | フォント プロバイダーを有効にする |  | 無効にします。 Windows は、オンライン フォント プロバイダーに接続せず、ローカルにインストールされているフォントのみを列挙します。 |
| ホットスポット認証 | ホットスポット認証を有効にする |  | 無効 |
| Microsoft ピア ツー ピア ネットワーク サービス | Microsoft ピア ツー ピア ネットワーク サービスをオフにする |  | Enabled |
| ネットワーク接続状態インジケーター | パッシブ ポーリングの指定。 | パッシブ ポーリングを無効にする (チェックボクス) | 有効にします。 分離されたネットワーク上にいる場合、または静的 IP アドレスを使用している場合は、この設定を使用します。 |
| オフライン ファイル | オフライン ファイルの使用を許可または禁止する。 |  | 無効 |
| TCPIP 設定\\IPv6 移行テクノロジ | Teredo 状態を設定する | 無効状態 | 有効にします。 無効状態では、ホストに Teredo インターフェイスは存在しません。 |
| WLAN サービス\\WLAN の設定 | 推奨されるオープン ホットスポット、連絡先によって共有されたネットワーク、有料サービスを提供するホット スポットに Windows が自動的に接続することを許可する。 |  | 無効にします。 **[推奨されたオープン ホットスポットに接続する]** 、 **[連絡先によって共有されたネットワークに接続する]** 、および **[有料サービスを有効にする]** がオフになっていますが、このデバイスのユーザーはこれらを有効にできます。 |
| ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\スタート メニューとタスクバー |  |  |  |
| *通知 | ネットワークを使用した通知をオフにする |  | 有効にします。 この設定を有効にした場合、アプリおよびシステム機能は、WNS からまたは通知ポーリング API を使用したネットワークからの通知を受信できません。 |
| ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\システム |  |  |  |
| デバイスのインストール | デバイスに汎用ドライバーがインストールされている場合、Windows エラー報告を送信しない |  | Enabled |
| デバイスのインストール | 通常は復元ポイントの作成が要求されるデバイス操作の際にシステムの復元ポイントが作成されないようにする。 |  | Enabled |
| デバイスのインストール | デバイス メタデータをインターネットから取得しない |  | Enabled |
| デバイスのインストール | デバイス ドライバーのインストール時に追加のソフトウェアが要求されてもエラー報告が送信されないようにする |  | Enabled |
| デバイスのインストール | デバイスのインストール中の**新しいハードウェアが見つかりましたバルーン**をオフにする。 |  | Enabled |
| ファイル システム\\NTFS | 短い名前の作成オプション | すべてのボリュームで無効 | Enabled |
| *グループポリシー | Configure web-to-app linking with app URL handlers (アプリの URI ハンドラーで Web とアプリのリンクを構成する) |  | 無効にします。 Web とアプリのリンクを無効にし、関連付けられているアプリを開始するのではなく、http(s) の URI を既定のブラウザーで開きます。 |
| *グループポリシー | このデバイスでのエクスペリエンスを続行する。 |  | 無効にします。 Windows デバイスは、他のデバイスから検出されず、クロス デバイス エクスペリエンスに参加できません。 |
| インターネット通信の管理\\インターネット通信の設定 | Windows Update のすべての機能へのアクセスをオフにする |  |有効にします。 このポリシー設定を有効にした場合、Windows Update のすべての機能が削除されます。 このポリシー設定には、[スタート] メニューの Windows Update および Internet Explorer の [ツール] メニューのハイパーリンクからの Windows Update Web サイト (https://windowsupdate.microsoft.com ) へのアクセスのブロックが含まれています。 Windows 自動更新も無効になります。Windows Update からの重要な更新プログラムの通知を受けず、受信もしません。 また、デバイス マネージャーで Windows Update Web サイトからドライバーの更新プログラムを自動的にインストールすることもありません。 |
| インターネット通信の管理\\インターネット通信の設定 | ルート証明書の自動更新をオフにする |  |有効にします。 このポリシー設定を有効にした場合、信頼されていないルート機関から発行された証明書を受信した時に、お使いのコンピューターは、Microsoft がこの機関を信頼された機関の一覧に追加したかどうかを確認するために、Windows Update Web サイトを参照することはしません。 注記:最新の証明書失効リストへの別の方法がある場合のみ、このポリシーを使用します。 |
| インターネット通信の管理\\インターネット通信の設定 | イベント ビューアーの "Events.asp" リンクをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | 手書き認識個人用設定のデータ共有を無効にする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | 手書き認識のエラー報告をオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | ヘルプとサポート センターの「役に立つ情報」の内容表示をしない コンテンツ |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | ヘルプとサポート センター Microsoft サポート技術情報 (KB) の検索をオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | URL 接続が Microsoft.com を参照している場合、インターネット接続ウィザードをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | Web 発行およびオンライン注文ウィザードのインターネット ダウンロードをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | インターネット ファイルの関連付けサービスをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | URL 接続が Microsoft.com を参照している場合、登録をオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | 画像のタスクの "プリントの注文" をオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | ファイルおよびフォルダーの "Web に発行" タスクをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | Windows Messenger カスタマー エクスペリエンス向上プログラムをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | Windows カスタマー エクスペリエンス向上プログラムをオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | Windows ネットワーク接続状態インジケーターのアクティブなテストを無効にする |  | 有効にします。 このポリシー設定では、コンピューターがインターネットに接続しているか、またはより制限されたネットワークに接続しているかを検出するために Windows ネットワーク接続状態インジケーター (NCSI) が実行するアクティブなテストを無効にします。接続レベル検出の一環として、NCSI は 2 つのアクティブなテストのうち 1 つを実行します。つまり、専用の Web サーバーからページをダウンロードするか、または専用のアドレスに DNS 要求を実行します。 このポリシー設定を有効にした場合、NCSI はアクティブな 2 つのテストのどちらも実行しません。 これにより、NCSI および NCSI を使用するその他のコンポーネントは、インターネット アクセスを検出する性能が低下する可能性があります)。注:この機能が必要な場合は、NCSI テストを内部リソースにリダイレクトできるようにするその他のポリシーがあります。 |
| インターネット通信の管理\\インターネット通信の設定 | Windows エラー報告をオフにする |  | Enabled |
| インターネット通信の管理\\インターネット通信の設定 | Windows Update でのデバイス ドライバーの検索をオフにする |  | Enabled |
| ログオン | 初回サインインのアニメーションを表示する |  | 無効 |
| ログオン | ロック画面のアプリ通知をオフにする |  | Enabled |
| ログオン | Windows スタートアップ サウンドをオフにする |  | Enabled |
| 電源管理 | 現在使用されている電源プランを選択する | 高パフォーマンス | Enabled |
| 復元 | システムの既定の状態への復元を許可する |  | 無効 |
| *記憶域の正常性 | Allow downloading updates to the Disk Failure Prediction Model (Disk Failure Prediction Model の更新プログラムのダウンロードを許可する) |  | 無効にします。 Disk Failure Prediction Failure Model の更新プログラムはダウンロードされません。 |
| *Windows タイム サービス\\タイム プロバイダー | Windows NTP クライアントを有効にする |  | 無効にします。 このポリシー設定を無効にするか、未構成にした場合、ローカル コンピューター時計の時刻は NTP サーバーと同期されません。 注記:この設定は慎重に検討してください。 ドメインに参加している Windows デバイスでは **NT5DS** を使用する必要があります。 DC から親ドメインの DC へは NTP を使用できます。 PDCe ロールは NTP を使用できます。 仮想マシンは、"機能強化" または "統合サービス"を使用することがあります。 |
| トラブルシューティングと診断\\定期メンテナンス | スケジュールされたメンテナンス動作の構成 |   | 無効 |
| トラブルシューティングと診断\\Windows ブート パフォーマンスの診断 | シナリオ実行レベルを構成する |   | 無効 |
| トラブルシューティングと診断\\Windows メモリ リークの診断 | シナリオ実行レベルを構成する |   | 無効 |
| トラブルシューティングと診断\\Windows リソース消費検出と解決 | シナリオ実行レベルを構成する |   | 無効 |
| トラブルシューティングと診断\\Windows シャットダウン パフォーマンスの診断 | シナリオ実行レベルを構成する |   | 無効 |
| トラブルシューティングと診断\\Windows スタンバイ/再開 パフォーマンスの診断 | シナリオ実行レベルを構成する |   | 無効 |
| トラブルシューティングと診断\\Windows システム応答性パフォーマンスの診断 | シナリオ実行レベルを構成する |   | 無効 |
| *ユーザー プロファイル | 広告 ID を無効にする |   | 有効にします。 このポリシー設定を有効にすると、広告 ID は無効になります。 アプリは、アプリ全体のエクスペリエンスに ID を使用できません。 |
| ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\Windows コンポーネント |  |  |  |
| Windows 10 への機能の追加 | このウィザードが実行されないようにしてください |  | Enabled |
| *アプリのプライバシー | このウィザードが実行されないようにしてください |  | Enabled |
| *アプリのプライバシー | Let Windows apps access account information (Windows アプリからアカウント情報にアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはアカウント情報へのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリで通話履歴にアクセスする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは通話履歴へのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access contacts (Windows アプリから連絡先にアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは連絡先へのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリから他のアプリに関する診断情報にアクセスできるようにする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 このポリシー設定を無効にするか、未構成にした場合、組織の従業員は、デバイスで [設定] > [プライバシー] を使用して、Windows アプリが他のアプリに関する診断情報を取得できるかどうかを決定できます。 |
| *アプリのプライバシー | Windows アプリでメールにアクセスする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは電子メールへのアクセスを許可され、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access location (Windows アプリから場所にアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは場所へのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access messaging (Windows アプリからメッセージングにアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはメッセージングへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリでモーションにアクセスする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはモーション データへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリで通知にアクセスする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは通知へのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリでタスクにアクセスする | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはタスクへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access the calendar (Windows アプリからカレンダーにアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはカレンダーへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access the camera (Windows アプリからカメラにアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはカメラへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access the microphone (Windows アプリからマイクにアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはマイクへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access trusted devices (Windows アプリから信頼済みデバイスにアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは信頼済みデバイスへのアクセスを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps communicate with unpaired devices (Windows アプリでペアリングされていないデバイスと通信する) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはペアリングされていないワイヤレス デバイスとの通信を許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Let Windows apps access radios (Windows アプリで無線にアクセスする) | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは無線を制御するためのアクセス権を持たず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリが電話をかけることを許可する | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリは電話をかけることを許可されず、組織の従業員はこれを変更できません。 |
| *アプリのプライバシー | Windows アプリのバックグラウンド実行を許可する | すべてのアプリの既定値:強制的に拒否 | 有効にします。 **[強制的に拒否]** オプションを選択した場合、Windows アプリはバックグラウンドでの実行を許可されず、組織の従業員はこれを変更できません。 |
| 自動再生のポリシー | 自動実行の既定の動作を設定する | 自動実行コマンドを実行しない | Enabled |
| *自動再生のポリシー | 自動再生機能をオフにする |   | 有効にします。 このポリシー設定を有効にした場合、CD-ROM およびリムーバブル メディア ドライブの自動再生を無効にするか、すべてのドライブの自動再生を無効にすることができます。 |
| *クラウド コンテンツ | Windows のヒントを表示しない | 有効にします。 このポリシー設定は、Windows のヒントがユーザーに表示されないようにします。 |
| *クラウド コンテンツ | Microsoft コンシューマー エクスペリエンスを無効にする | 有効にします。 このポリシー設定を有効にした場合、ユーザーには、Microsoft からの個人用に設定された推奨事項や、Microsoft アカウントに関する通知が表示されなくなります。 |
| *データ収集とプレビュー ビルド | 利用統計情報を許可する | 0 - セキュリティ [Enterprise のみ] | 有効にします。 値 0 の設定は、Enterprise、Education、IoT、または Windows Server のエディションを実行しているデバイスにのみ適用されます。 |
| *データ収集とプレビュー ビルド | フィードバックの通知を表示しない |  | Enabled |
| *データ収集とプレビュー ビルド | Insider ビルドに関するユーザー コントロールの切り替え  |  | 無効 |
| 配信の最適化 | ダウンロード モード | ダウンロード モード:シンプル (99) | 99 = ピアリングなしの簡易なダウンロード モードです。 配信の最適化は、HTTP のみを使用してダウンロードし、配信の最適化クラウド サービスに接続しようとしません。 |
| デスクトップ ウィンドウ マネージャー |  フリップ 3D の起動を許可しない |  | Enabled |
| デスクトップ ウィンドウ マネージャー |  ウィンドウのアニメーションを許可しない |  | Enabled |
| デスクトップ ウィンドウ マネージャー |  スタート画面の背景に単色を使用する |  | Enabled |
| 画面の端の UI |  エッジ スワイプを許可する |  | 無効 |
| 画面の端の UI |  ヘルプ ヒントを無効にする |  | Enabled |
| 画面の端の UI | アプリの使用状況の追跡をオフにする |  | Enabled |
| *エクスプローラー |  Windows Defender SmartScreen の構成 |  | 無効にします。 SmartScreen はすべてのユーザーに対してオフになります。 ユーザーは、インターネットから疑わしいアプリを実行しようとしたときに、警告されません。 注記:インターネットに接続されていない場合、これにより、コンピューターは、SmartScreen の情報について Microsoft への問い合わせを試みることができなくなります。 |
| エクスプローラー |  **新しいアプリケーションがインストールされました** の通知を表示しない |  | Enabled |
| *デバイスの検索 |  デバイスの検索をオン/オフにする |  | 無効にします。 [デバイスの検索] をオフにした場合、デバイスとその場所は登録されず、[デバイスの検索] 機能は動作しません。 ユーザーは、デバイス上でアクティブなデジタイザーを最後に使用した場所を確認することもできません。 |
| エクスプローラー | 縮小表示の画像のキャッシュをオフにする |  | Enabled |
| エクスプローラー | エクスプローラーの検索ボックスで最近検索したエントリの表示を無効にする |  | Enabled |
| エクスプローラー | 非表示の thumbs.db ファイルで縮小表示のキャッシュを無効にする |  | Enabled |
| ゲーム エクスプローラー | ゲーム情報のダウンロードを無効にする |  | Enabled |
| ゲーム エクスプローラー | ゲームの更新プログラムをオフにする |  | Enabled |
| ゲーム エクスプローラー | ゲーム フォルダー内のゲームを最後にプレイした日時を追跡しない |  | Enabled |
| ホームグループ | コンピューターがホームグループに参加できないようにする |  | Enabled |
| *Internet Explorer | ユーザーがアドレス バーに入力した文字に合わせて検索候補の拡張表示を提供することを Microsoft サービスに許可する |  | 無効にします。 アドレス バーに入力したときに、ユーザーには検索候補の拡張表示が提供されません。 また、ユーザーは [候補] 設定を変更できません。 |
| Internet Explorer | Internet Explorer ソフトウェアの更新の周期的なチェックを許可しない |  | Enabled |
| Internet Explorer | スプラッシュ画面を表示しない |  | Enabled |
| Internet Explorer | 最新バージョンの Internet Explorer を自動的にインストールする |  | 無効 |
| Internet Explorer | カスタマー エクスペリエンス向上プログラムに参加できないようにする |  | Enabled |
| Internet Explorer | 初回実行ウィザードを実行しないようにする | ホーム ページに直接移動する | Enabled |
| Internet Explorer | タブ プロセスの増加率を設定 | 低 | Enabled |
| Internet Explorer | 新規タブの既定動作を指定 | 新規タブ ページ | Enabled |
| Internet Explorer | アドオンのパフォーマンスの通知を無効にする |  | Enabled |
| *Internet Explorer | Web アドレスのオートコンプリート機能を無効にする |  | 有効にします。 このポリシー設定を有効にすると、ユーザーが入力しようとしている Web アドレスに一致する候補は表示されません。 ユーザーは、Web アドレスの設定のオートコンプリートを変更できません。 |
| *Internet Explorer | ブラウザーの地理位置情報を無効にする |  | 有効にします。 このポリシー設定を有効にすると、ブラウザーの地理位置情報のサポートは無効になります。 |
| *Internet Explorer | 最終閲覧セッションを再度開くを無効にする |  | Enabled |
| Internet Explorer | 最終閲覧セッションを再度開くを無効にする |  | Enabled |
| *Internet Explorer | おすすめサイトを有効にする |  | 無効にします。 このポリシー設定を無効にすると、この機能に関連するエントリ ポイントと機能は無効になります。 |
| *Internet Explorer\\互換表示 | 互換表示を無効にする |  | 有効にします。 このポリシー設定を有効にすると、ユーザーは [互換表示] ボタンを使用できなくなり、互換表示サイト一覧を管理できなくなります。 |
| *Internet Explorer\\インターネット コントロール パネル\\[詳細設定] ページ | Web ページでアニメーションを再生する |  | 無効 |
| *Internet Explorer\\インターネット コントロール パネル\\[詳細設定] ページ | Web ページでビデオを再生する |  | 無効 |
| *Internet Explorer\\インターネット コントロール パネル\\[詳細設定] ページ | Turn off the flip ahead with page prediction features (ページ予測付きページ フリップ機能を無効にする) |  | 有効にします。 Microsoft では、ページ予測付きページ フリップの改善に役立てるために閲覧履歴を収集します。 この機能は、デスクトップ用 Internet Explorer では利用できません。 このポリシー設定を有効にすると、ページ予測付きページ フリップは無効になり、次の Web ページはバックグラウンドに読み込まれません。 |
| Internet Explorer\\インターネット設定\\詳細設定\\ブラウズ | 電話番号の検出を無効にする |  | Enabled |
| *場所とセンサー | 場所を無効にする |  | 有効にします。 このポリシー設定を有効にすると、場所の機能が無効になり、このコンピューターのすべてのプログラムで場所の機能から場所の情報を使用できなくなります。 |
| 場所とセンサー | センサーを無効にする |  | Enabled |
| 場所とセンサー\\Windows 位置情報取得機能 | Windows 位置情報取得機能を無効にする |  | Enabled |
| *マップ | Turn off Automatic Download and Update of Map Data (マップ データの自動によるダウンロードおよび更新をオフにする) |  | 有効にします。 この設定を有効にした場合、マップ データの自動ダウンロードおよび更新はオフになります。 |
| *マップ | [オフライン マップ] 設定ページ上で要請されていないネットワーク トラフィックを無効にする |  | 有効にします。 このポリシー設定を有効にした場合、[オフライン マップ] 設定ページでネットワーク トラフィックを生成する機能がオフになります。 注: これにより、設定ページ全体がオフになることがあります。 |
| *メッセージング | Allow Message Service Cloud Sync (メッセージ サービス クラウドの同期を許可する) |  | 無効にします。 このポリシー設定によって、携帯電話のテキスト メッセージを Microsoft のクラウド サービスにバックアップおよび復元することができます。 |
| *Microsoft Edge | アドレス バーのドロップダウン リスト候補を許可する |  | 無効 |
| *Microsoft Edge | Allow configuration updates for the Books Library (書籍ライブラリの構成の更新を許可する) |  | 無効にします。 Microsoft Edge での互換性一覧を無効にします。 |
| *Microsoft Edge | Microsoft 互換性一覧を許可 |  | 無効にします。 この設定を無効にした場合、Microsoft 互換性一覧はブラウザーのナビゲーション時に使用されません。 |
| *Microsoft Edge | [新しいタブ] ページでの Web コンテンツの許可 |  | 無効にします。 新しいタブが開いたときに、空白の内容で開くように Edge に指示します。 |
| *Microsoft Edge | オートフィルの構成 |  | 無効にします。 アドレス バーでオートフィルを無効にします。 |
| *Microsoft Edge | トラッキング拒否の構成 |  | 有効にします。 この設定を有効にした場合、トラッキング拒否要求はトラッキング情報を要求する Web サイトに常に送信されます。 |
| *Microsoft Edge | パスワード マネージャーの構成 |  | 無効にします。 この設定を無効にした場合、従業員はパスワード マネージャーを使ってパスワードをローカルに保存できません。 |
| *Microsoft Edge | アドレス バーの検索候補の構成 |  | 無効にします。 ユーザーは Microsoft Edge のアドレス バーで検索候補を確認できません。 |
| *Microsoft Edge | スタート ページを構成する |  | 有効にします。 この設定を有効にした場合、1 つまたは複数のスタート ページを構成できます。 この設定を有効にした場合、ページの URL も含める必要があり、<support.contoso.com><support.microsoft.com> の形式の山かっこを使って複数のページを区切ります。Windows 10 バージョン 1703 以降:Microsoft にトラフィックを送信したくない場合は、<about:blank> 値を使用できます。これは、構成されている URL が 1 つしかない場合に、ドメインに参加しているかどうかにかからずデバイスに対して有効になります。 |
| *Microsoft Edge | Windows Defender SmartScreen の構成 |  | 無効にします。 Windows Defender SmartScreen が無効になります。従業員はこれを有効にすることはできません。 注記:環境内でこの設定を検討してください。 インターネットに接続されていない場合、これにより、コンピューターは、SmartScreen の情報について Microsoft への問い合わせを試みることができなくなります。 |
| *Microsoft Edge | Prevent the First Run web page from opening on Microsoft Edge (Microsoft Edge で初回実行時の Web ページを開かない) |  | 有効にします。 ユーザーが最初に Microsoft Edge を開くときに、初回実行時のページは表示されません。 |
| OneDrive | Prevent OneDrive from generating network traffic until the user signs in to OneDrive (ユーザーが OneDrive にサインインするまで OneDrive がネットワーク トラフィックを生成できないようにする) |  | 有効にします。 この設定を有効にすると、ユーザーが OneDrive にサインインするまで、またはローカル コンピューターとのファイルの同期を開始するまで、OneDrive 同期クライアント (OneDrive.exe) がネットワーク トラフィック (更新プログラムの確認など) を生成できなくなります。 |
| *OneDrive | OneDrive をファイル記憶域として使用できないようにする |  | 有効にします。 ただし、OneDrive がオンプレミスまたはオフプレミスで使用されている場合を除く。 |
| OneDrive | ドキュメントを既定で OneDrive に保存する |  | 無効にします。 ただし、OneDrive がオンプレミスまたはオフプレミスで使用されている場合を除く。 |
| RSS フィード | フィードと Web スライスの自動検出を禁止する |  | Enabled |
|*RSS フィード | フィードと Web スライスのバックグラウンド同期を無効にする |  | 有効にします。 このポリシー設定を有効にすると、バックグラウンドでフィードと Web スライスを同期する機能が無効になります。 |
|*検索 | Cortana を許可する |  | 無効にします。 Cortana をオフにしても、ユーザーは引き続き検索を使用して、デバイス上の情報を検索できます。 |
|検索 | ロック画面で Cortana を許可する |   | 無効 |
|*検索 | 検索と Cortana による位置情報の使用を許可する |  | 無効 |
|検索 | Web 検索を許可しない |   | Enabled |
|*検索 | Web を検索したり [検索] に Web の検索結果を表示したりしない |  | 有効にします。 このポリシー設定を有効にした場合、ユーザーが [検索] でクエリを実行しても、クエリは Web に対して実行されず、Web の検索結果は表示されません。 |
|検索 | コントロール パネルからインデックスに UNC の場所を追加することを禁止する |  | Enabled |
|検索 | オフライン ファイル キャッシュのファイルのインデックス作成を禁止する |  | Enabled |
|*検索 | [検索] (匿名情報) で共有する情報を設定する |  | 有効にします。 使用情報は共有しますが、検索履歴、Microsoft アカウント情報、または特定の位置情報を共有しません。 |
|*ソフトウェア保護プラットフォーム | Turn off KMS Client Online AVC Validation (KMS クライアントオンライン AVC 検証をオフにする) | 有効にします。 この設定を有効にすると、このコンピューターはライセンス認証の状態に関するデータを Microsoft に送信しなくなります。 |
|*音声認識 | 音声認識データの自動更新を許可する |  | 無効にします。 音声モデルの更新を定期的に確認しません。 |
|*ストア | 更新プログラムの自動ダウンロードおよび自動インストールをオフにする |  | 有効にします。 この設定を有効にした場合、アプリの更新プログラムの自動ダウンロードおよび自動インストールはオフになります。 |
|*ストア | Turn off Automatic Download of updates on Win8 devices (Windows 8 デバイスでの更新プログラムの自動ダウンロードをオフにする) | 有効にします。 この設定を有効にした場合、アプリの更新プログラムの自動ダウンロードはオフになります。 |
| ストア | 最新バージョンの Windows への更新プログラム提供をオフにする |  | Enabled |
|*設定の同期 | 同期しない | ユーザーが同期をオンにできるようにします (未選択) | 有効にします。 このポリシー設定を有効にすると、[設定の同期] はオフになり、[設定の同期] グループはこのデバイス上で同期されなくなります。 |
| テキスト入力 | Improve inking and typing recognition (手描き入力およびタイピングの認識) |  | 無効 |
| Windows Defender ウイルス対策\\MAPS | Microsoft MAPS に参加する |  | 無効にします。 この設定を無効にした場合、または構成しなかった場合、Microsoft MAPS に参加しません。 |
| Windows Defender ウイルス対策\\MAPS | 詳細な分析が必要な場合はファイルのサンプルを送信する | 送信しない | 有効にします。 MAPS 診断データについてオプトインされていない場合のみ。 |
| Windows Defender ウイルス対策\\レポート | 拡張通知をオフにする |  | 有効にします。 この設定を有効にした場合、Windows Defender ウイルス対策拡張通知はクライアントで表示されません。 |
| Windows Defender ウイルス対策\\署名の更新 | 定義の更新をダウンロードするための更新元の順序を定義する | FileShares | 有効にします。 この設定を有効にした場合、指定の順序で定義の更新元に接続します。 指定した更新元の 1 つから定義の更新を適切にダウンロードできたら、その他の更新元には接続しません。 |
| Windows エラー報告 | Automatically send memory dumps for operating system-generated error reports (オペレーティング システムが生成するエラー報告のためにメモリ ダンプを自動送信する) |  | 無効 |
| Windows エラー報告 | Windows エラー報告を無効にする |  | Enabled |
| Windows のゲーム録画とブロードキャスト | Windows のゲーム録画とブロードキャストを有効または無効にする | | 無効 |
| Windows インストーラー | ベースライン ファイル キャッシュの最大サイズを制御する | 5 | Enabled |
| Windows インストーラー | システムの復元のチェックポイントの作成をオフにする |  | Enabled |
| Windows メール | Turn off the communities feature (コミュニティ機能をオフにする) |  | Enabled |
| Windows Media Player | 初期設定ダイアログ ボックスを表示しない |  | Enabled |
| Windows Media Player | メディアを共有できないようにする |  | Enabled |
| Windows モビリティ センター | Windows モビリティ センターをオフにする |  | Enabled |
| Windows 信頼性分析 | 信頼性の WMI プロバイダーを構成する |  | 無効 |
| Windows Update | 自動更新を直ちにインストールすることを許可する |  | Enabled |
| Windows Update | インターネット上の Windows Update に接続しない |  | 有効にします。 このポリシーを有効にすると、その機能は無効になり、Microsoft Store など公開されているサービスへの接続が動作しなくなる可能性があります。 注記:このポリシーは、[イントラネットの Microsoft 更新サービスの場所を指定する] ポリシーを使用してイントラネットの更新サービスに接続するようにこのデバイスが構成されているときにのみ適用されます)。 |
| Windows Update | Remove access to all Windows Update features (Windows Update のすべての機能へのアクセスを削除する) |   | Enabled |
| *Windows Update\\Windows Update for Business | Manage preview builds (プレビュー ビルドを管理する) | プレビュー ビルドを受信するための動作を設定します: | 有効にします。 [Disable preview builds]\(プレビュー ビルドを無効にする\) を選択すると、プレビュー ビルドをデバイスにインストールできなくなります。 これにより、ユーザーは、[設定] -> [更新とセキュリティ] から Windows Insider Program にオプトインできなくなります。<br>無効にします。 プレビュー ビルドを無効にします。 |
| *Windows Update\\Windows Update for Business | Select when Preview Builds and Feature Updates are received (プレビュー ビルドや機能更新プログラムをいつ受信するかを選択する) | 半期チャネル<br>延期:365 日<br>一時停止を開始: yyyy-mm-dd。 | 有効にします。 プレビュー ビルドまたは機能更新プログラムを受信するレベルといつ受信するかを指定するには、このポリシーを有効にします。 |
| Windows Update\\Windows Update for Business | 品質更新プログラムをいつ受信するかを選択してください | 1. 30 日<br>2.品質更新プログラムの一時停止を開始しています: yyyy-mm-dd | Enabled |
| Windows Restricted Traffic Custom Policy Settings | Prevent OneDrive from generating network traffic until the user signs in to OneDrive (ユーザーが OneDrive にサインインするまで OneDrive がネットワーク トラフィックを生成できないようにする) |  | 有効にします。 ユーザーが OneDrive にサインインするまで、またはローカル コンピューターとのファイルの同期を開始するまで、OneDrive 同期クライアント (OneDrive.exe) がネットワーク トラフィック (更新プログラムの確認など) を生成できないようにさせる場合に、この設定を有効にします。 |
| Windows Restricted Traffic Custom Policy Settings | Turn off Windows Defender Notifications (Windows Defender の通知をオフにする) |  | 有効にします。 このポリシー設定を有効にすると、Windows Defender は、デバイスの正常性とセキュリティに関する重要な情報を含む通知を送信しません。 |
| ローカル コンピューター ポリシー\\ユーザーの構成\\管理用テンプレート  |  |  |
|コントロール パネル\\地域と言語のオプション | [入力時に予測入力を表示する] をオフにする |  | Enabled |
| デスクトップ | [ネットワークの場所] に最近使ったファイルの共有を追加しない |  | Enabled |
| デスクトップ | Aero Shake のウィンドウ最小化のマウス ジェスチャをオフにする |  | Enabled |
| デスクトップ\\Active Directory | Active Directory 検索の最大サイズ | 2500 | Enabled |
| タスク バーと [スタート] メニュー | タスク バーへのストア アプリの固定を許可しません |  | Enabled |
| タスク バーと [スタート] メニュー | ジャンプ リストで遠隔地からの項目は表示および追跡しない |  | Enabled |
| タスク バーと [スタート] メニュー | シェルのショートカットの解決に検索ベースのメソッドを使用しない |  | 有効にします。 システムでドライブの包括的な検索は行われません。 ファイルが見つからないという内容のメッセージが表示されるだけです。 |
| タスク バーと [スタート] メニュー | Remove the People Bar from the taskbar (タスク バーから People バーを削除する) |  | 有効にします。 人のアイコンがタスク バーから削除され、対応する設定のトグルがタスク バー設定ページから削除され、ユーザーはタスク バーに人をピン留めできなくなります。 |
| タスク バーと [スタート] メニュー | 機能の広告バルーン通知を無効にする |  | 有効にします。 ユーザーはタスク バーに Store アプリをピン留めできません。 既に Store アプリがタスク バーにピン留めされている場合、次回のサインイン時にのタスク バーから削除されます。 |
| タスク バーと [スタート] メニュー | ユーザーの追跡をオフにする |  | Enabled |
| タスク バーと [スタート] メニュー\\通知 | トースト通知をオフにする |  | Enabled |
| Windows コンポーネント\\クラウド コンテンツ | すべての Windows スポットライト機能をオフにする |  | Enabled |

### <a name="notes-about-network-connectivity-status-indicator"></a>ネットワーク接続状態インジケーターに関する注意事項

上記のグループ ポリシー設定には、システムがインターネットに接続されているかどうかの確認をオフにする設定が含まれています。 お使いの環境がインターネットに完全に接続していないか、間接的に接続している場合は、タスク バーから [ネットワーク] アイコンを削除するようにグループ ポリシー設定を指定できます。 タスク バーから [ネットワーク] アイコンを削除する理由は、インターネット接続チェックをオフにした場合、ネットワークが正常に機能していても [ネットワーク] アイコンに黄色のフラグが表示されるからです。 グループ ポリシー設定として [ネットワーク] アイコンを削除したい場合は、次の場所で見つけられます。

| ポリシー設定 | Item | サブ項目 | 考えられる設定とコメント|
| -------------- | ---- | -------- | ---------------------------- |
| Windows Update または Windows Update for Business | 品質更新プログラムをいつ受信するかを選択してください | 1. 30 日<br>2.品質更新プログラムの一時停止を開始しています: yyyy-mm-dd | Enabled |
| ローカル コンピューター ポリシー\\ユーザーの構成\\管理用テンプレート |  |  |  |
| タスク バーと [スタート] メニュー | ネットワーク アイコンを削除する |  | 有効にします。 システム通知領域にネットワーク アイコンが表示されません。 |

ネットワーク接続状態インジケーター (NCSI) の詳細については、[「Windows 10 Enterprise Version 1903 の接続エンドポイントの管理](/windows/privacy/manage-windows-1903-endpoints)」および[「Windows 10 オペレーティング システムのコンポーネントから Microsoft サービスへの接続を管理する」](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services)をご覧ください。

### <a name="system-services"></a>システム サービス

リソースを節約するためにシステム サービスの無効化を検討している場合は、検討しているサービスが他のサービスのコンポーネントになっていないことに十分注意してください。 一部のサービスは、サポートされている方法で無効にできないため、一覧に含まれていないことに注意してください。

これらの推奨事項のほとんどは、「[デスクトップ エクスペリエンス搭載 Windows Server 2016 上のシステム サービスを無効にする場合のガイダンス](../../security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server.md)」にある、デスクトップ エクスペリエンスとともにインストールされた Windows Server 2016 の推奨事項を反映しています。

無効にする候補として適しているように思われるサービスの多くは、手動サービス開始の種類に設定されています。 つまり、プロセスまたはイベントが、無効化を検討しているサービスへの要求をトリガーしない限り、サービスは自動的に開始することも、開始されることもありません。 既に手動開始の種類に設定されているサービスは通常、ここには表示されません。

> [!NOTE]
> この PowerShell サンプル コードを使用して、実行中のサービスを列挙し、サービスの短い名前のみを出力することができます。

```powershell
 Get-Service | Where-Object {$_.Status -eq "Running"} | select -ExpandProperty Name
 ```

| Windows サービス | Item | 備考|
| -------------- | ---- | ---------------------------- |
| CDPUserService | このユーザー サービスは、Connected Devices Platform のシナリオに使用されます | これはユーザーごとのサービスであり、そのため、*テンプレート サービス*を無効にする必要があります。 |
| Connected User Experiences and Telemetry (接続ユーザーのエクスペリエンスと利用統計情報) | アプリケーション内および接続ユーザーのエクスペリエンスをサポートする機能を有効にします。 さらに、このサービスは、[フィードバックと診断] で診断と使用のプライバシー オプション設定が有効な場合に、(Windows プラットフォームのエクスペリエンスと品質の向上に使用される) 診断および使用情報のイベント駆動型の収集と送信を管理します。 | 切断されたネットワークの場合は無効化を検討してください。 |
| 連絡先データ | 高速な連絡先検索のために連絡先データのインデックスを作成します。 このサービスを停止または無効にすると、連絡先が検索結果に表示されなくなる可能性があります。 | これはユーザーごとのサービスであり、そのため、*テンプレート サービス*を無効にする必要があります。 |
| 診断ポリシー サービス | Windows コンポーネントの問題検出、トラブルシューティング、および解決を可能にします。 このサービスを停止すると、診断は機能しなくなります。 | |
| ダウンロード地図マネージャー | ダウンロードした地図にアプリケーションでアクセスするための Windows サービス。 このサービスは、ダウンロードした地図にアクセスするアプリケーションによってオンデマンドで開始されます。 このサービスを無効にすると、アプリが地図にアクセスできなくなります。 | |
| 位置情報サービス | システムの現在の場所を監視し、ジオフェンスを管理します | |
| GameDVR およびブロードキャスト ユーザー サービス | このユーザー サービスは、ゲームの録画とライブ ブロードキャストに使用されます | これはユーザーごとのサービスであり、そのため、テンプレート サービスを無効にする必要があります。 |
| MessagingService | テキスト メッセージングと関連機能をサポートするサービス。 | これはユーザーごとのサービスであり、そのため、*テンプレート サービス*を無効にする必要があります。 |
| ドライブの最適化 | 記憶域ドライブのファイルを最適化すると、コンピューターがより効率的に動作します。 | VDI ソリューションは通常、ディスクの最適化からメリットを受けることはありません。 これらの "ドライブ" は従来のドライブではなく、多くの場合、一時記憶域割り当てに過ぎません。 |
| Superfetch | システム パフォーマンスを維持し、徐々に改善します。 | 一般に、オペレーティング システムの状態が再起動ごとに破棄される場合、VDI (特に非永続的) でのパフォーマンスは向上しません。 |
| タッチ キーボードおよび手書きパネル サービス | タッチ キーボードおよび手書きパネルのペンおよびインク機能を有効にします | |
| Windows エラー報告 | プログラムが動作や応答を停止するときにエラーを報告できるようにし、既存のソリューションを配信できるようにします。 また、診断および修復サービス用にログを生成できるようにします。 このサービスが停止している場合は、エラー報告は正しく機能せず、診断サービスと修復の結果が表示されないことがあります。 | VDI では、診断は、多くの場合、メインストリームの運用シナリオではなく、オフライン シナリオで実行されます。 さらに、どうしても WER を無効にする顧客が存在します。 WER は、デバイスのインストールの失敗や更新プログラムのインストールの失敗など、さまざまな多くの事項について少量のリソースがかかります。 |
| Windows Media Player ネットワーク共有サービス | ユニバーサル プラグ アンド プレイを使用して、他のネットワーク接続したプレイヤーとメディア デバイスと Windows Media Player ライブラリを共有します | 顧客がネットワーク上で WMP ライブラリを共有している場合以外は必要ありません。 |
| Windows Mobile Hotspot Service | 別のデバイスと携帯データ ネットワーク接続を共有する機能を提供します。 | |
| Windows Search | ファイル、電子メール、およびその他のコンテンツに、コンテンツのインデックス処理、プロパティ キャッシュ、および検索結果を提供します。                                                                    | おそらく非永続的 VDI では特に必要ありません |

#### <a name="per-user-services-in-windows"></a>Windows のユーザーごとのサービス

ユーザーごとのサービスは、ユーザーが Windows または Windows Server にサインインするときに作成され、ユーザーがサインアウトすると停止され削除されるサービスです。これらのサービスは、ユーザー アカウントのセキュリティ コンテキストで実行します。これにより、事前構成されたアカウントに関連付けられたり、タスクとして、エクスプローラーでこれらの種類のサービスを実行していた以前のアプローチよりも適切なリソース管理が得られます。

[Windows 10 および Windows Server のユーザーごとのサービス](/windows/application-management/per-user-services-in-windows)

サービス開始値を変更する場合は、管理者特権での .cmd プロンプトを開き、サービス コントロール マネージャー ツール "Sc.exe" を実行する方法をお勧めします。 "Sc.exe" の使用方法の詳細については、「[Sc](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754599(v=ws.11))」を参照してください。

### <a name="scheduled-tasks"></a>スケジュールされたタスク

Windows での他の項目と同様に、項目を無効にすることを検討する前に、それが不要であることを確認してください。

次のタスクの一覧は、再起動後も状態を維持するコンピューター上で最適化またはデータ コレクションを実行するタスクを示しています。 VDI VM タスクが再起動し、前回の起動以降のすべての変更内容を破棄する場合、物理コンピューターを対象とした最適化は役に立たなくなります。

次の PowerShell コードで、現在のスケジュールされたすべてのタスクを説明とともに取得できます。

```powershell
 Get-ScheduledTask | Select-Object -Property TaskPath,TaskName,State,Description
```

>[!NOTE]
> 管理者特権で実行している場合でも、スクリプトを使用して無効にできないタスクがいくつかあります。 スクリプトを使用して無効にできないタスクは無効にしないことをお勧めします。

スケジュールされたタスク名:

- 移動体通信
- Consolidator
- 診断
- FamilySafetyMonitor
- FamilySafetyRefreshTask
- MaintenanceTasks
- MapsToastTask
- 互換性
- Microsoft-Windows-DiskDiagnosticDataCollector
- MNO
- NotificationTask
- PerformRemediation
- ProactiveScan
- ProcessMemoryDiagnosticEvents
- ProgramDataUpdater
- Proxy (プロキシ)
- QueueReporting
- RecommendedTroubleshootingScanner
- ReconcileFeatures
- ReconcileLanguageResources
- RefreshCache
- RegIdleBackup
- ResPriStaticDbSync
- RunFullMemoryDiagnostic
- ScanForUpdates
- ScanForUpdatesAsUser
- スケジュール
- ScheduledDefrag
- sihpostreboot
- SilentCleanup
- SmartRetry
- SpaceAgentTask
- SpaceManagerTask
- SpeechModelDownloadTask
- Sqm-Tasks
- SR
- StartComponentCleanup
- StartupAppTask
- StorageSense
- SyspartRepair
- Sysprep
- UninstallDeviceTask
- UpdateLibrary
- UpdateModelTask
- UsbCeip
- Usb-Notifications
- USO_UxBroker
- WiFi
- WIM-Hash-Management
- WindowsActionDialog
- WinSAT
- フォルダー
- WsSwapAssessmentTask
- XblGameSaveTask

### <a name="apply-windows-and-other-updates"></a>Windows と他の更新プログラムを適用する

Microsoft Update からか、内部リソースからかにかかわらず、Windows Defender のシグネチャを含む使用可能な更新プログラムを適用します。 ここで、Microsoft Office (インストールされている場合) やその他のソフトウェア更新プログラムなど、利用可能なその他の更新プログラムを適用することをお勧めします。 PowerShell がイメージに残る場合は、コマンド [Update-Help](/powershell/module/microsoft.powershell.core/update-help?view=powershell-7) を実行して、PowerShell で使用可能な最新のヘルプをダウンロードできます。

#### <a name="servicing-the-operating-system-and-apps"></a>オペレーティング システムやアプリへのサービス提供

イメージ最適化プロセス中のある時点で、使用可能な Windows 更新プログラムを適用する必要があります。 Windows 10 Update の設定には、追加の更新プログラムを提供する設定があります。

![追加の更新プログラム](media/rds-vdi-recommendations-1909/servicing.png)

これは、Microsoft Office などの Microsoft アプリケーションを基本イメージにインストールしようとしている場合に、適切な設定になります。 そうすれば、イメージが稼働すると Office は最新の状態になります。 .NET の更新プログラムや、Windows Update を通じて更新プログラムを入手できる Adobe などの特定のサードパーティ製のコンポーネントもあります。

非永続的 VDI VM の非常に重要な考慮事項の 1 つが、セキュリティ ソフトウェア定義ファイルを含むセキュリティ更新プログラムです。 これらの更新プログラムは、1 日に 1 回以上リリースされることがあります。 Windows Defender やサードパーティ製のコンポーネントなど、これらの更新プログラムを保持する方法が存在する場合があります。

Windows Defender の場合、非永続的 VDI でも更新プログラムを実行できるようにすることが最善であることがあります。 更新プログラムは、ほぼすべてのログオン セッションを適用しますが、更新プログラムは小さく、問題になることはありません。 さらに、使用できる最新の更新プログラムのみが適用されるため、VM の更新が遅れることはありません。 同じことが、サードパーティの定義ファイルに当てはまることがあります。

> [!NOTE]
> Windows ストアからアプリ (UWP アプリ) の更新プログラムを格納します。 Office 365 などの最新バージョンの Office は、インターネットに直接接続しているときには独自のメカニズムを通じて、そうでないときには管理テクノロジを介して更新します。

### <a name="windows-system-startup-event-traces"></a>Windows システム スタートアップ イベント トレース

Windows は既定で、限られた診断データを収集し保存するように構成されています。 その目的は、診断を有効にすること、またはさらにトラブルシューティングが必要な場合にデータを記録することです。 自動システム トレースは、次の図に示す場所にあります。

![システム トレース](media/rds-vdi-recommendations-1909/system-traces.png)

**[イベント トレース セッション]** と **[スタートアップ イベント トレース セッション]** の下に表示されるトレースの中には、停止できないものや停止すべきでないものがあります。 "WiFiSession" などの他のトレースは停止できます。 実行中のトレースを停止するには、 **[イベント トレース セッション]** の下でそのトレースを右クリックし [停止] をクリックします。 起動時にトレースが自動的に起動しないようにするには、次の手順を実行します。

1. **[スタートアップ イベント トレース セッション]** フォルダーをクリックします。

2. 関心のあるトレースを見つけて、そのトレースをダブルクリックします。

3. **[トレース セッション]** タブをクリックします。

4. **[有効]** というラベルのボックスをクリックして、チェックマークを外します。

5. **[OK]** をクリックします。

VDI の使用を無効にすることを検討する必要があるシステム トレースを次に示します。

| 名前                    | コメント                       |
| ----------------------- | ----------------------------- |
| AppModel | トレースのコレクション。その 1 つは電話 |
| CloudExperienceHostOOBE | |
| DiagLog | |
| NtfsLog | |
| TileStore | |
| UBPM | |
| WiFiDriverIHVSession | WiFi デバイスを使用していない場合 |
| WiFiSession | |
| WinPhoneCritical | |

### <a name="windows-defender-optimization-with-vdi"></a>VDI を使用した Windows Defender の最適化

Microsoft は、VDI 環境での Windows Defender に関する説明書を最近公開しました。 詳細については、「[仮想デスクトップ インフラストラクチャ (VDI) 環境への Windows Defender ウイルス対策の展開ガイド](/windows/security/threat-protection/windows-defender-antivirus/deployment-vdi-windows-defender-antivirus)」を参照してください。

上記の記事には、"ゴールド" の VDI イメージを提供する手順と、実行している状態に VDI クライアントを維持する方法が含まれています。 VDI コンピューターが Windows Defender シグネチャを更新する必要があるときにネットワーク帯域幅を減らすには、再起動の時間をずらし、可能な場合は業務時間外に再起動をスケジュールします。 Windows Defender シグネチャ更新プログラムは、ファイル共有の内部に収容でき、可能であれば、VDI 仮想マシンと同じまたは近接したネットワーク セグメントにこれらのファイル共有を持つことができます。

### <a name="client-network-performance-tuning-by-registry-settings"></a>レジストリ設定によるクライアント ネットワーク パフォーマンスのチューニング

ネットワークのパフォーマンスを向上させるレジストリ設定がいくつかあります。 これは、VDI またはコンピューターに、主にネットワーク ベースであるワークロードがある環境では特に重要です。 このセクションの設定は、ディレクトリ エントリなどに対する追加バッファーおよびキャッシュ処理を設定することにより、パフォーマンスをネットワークに偏らせるために推奨されます。

>[!NOTE]
> このセクションの一部の設定はレジストリのみに基づいており、実稼働環境での使用のためにイメージを展開する前に基本イメージに組み込む必要があります。

次の設定は、Windows Product Group により Microsoft.com で公開された「[Windows Server 2016 のパフォーマンス チューニング ガイドライン](/windows-server/administration/performance-tuning/)」に記載されています。

#### <a name="disablebandwidththrottling"></a>DisableBandwidthThrottling

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling`

Windows 10 に適用されます。 既定値は **0** です。 既定では、SMB リダイレクターは、ネットワーク関連のタイムアウトを回避するために、待機時間の長いネットワーク接続全体のスループットを調整する場合があります。 このレジストリ値を 1 に設定すると、この調整が無効になり、待機時間の長いネットワーク接続でのファイル転送のスループットがより高くなります。 この値を **1** に設定することを検討してください。

#### <a name="fileinfocacheentriesmax"></a>FileInfoCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax` Windows 10 に適用されます。 既定値は **64** であり、有効範囲は 1 から 65536 です。 この値は、クライアントがキャッシュできるファイル メタデータの量を決定するために使用されます。 この値を増やすと、多数のファイルへのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。 この値を **1024** に増やしてみてください。

#### <a name="directorycacheentriesmax"></a>DirectoryCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax`

Windows 10 に適用されます。 既定値は **16** であり、有効範囲は 1 から 4096 です。 この値は、クライアントがキャッシュできるディレクトリ情報の量を決定するために使用されます。 この値を増やすと、大規模なディレクトリへのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。 この値を **1024** に増やすことを検討してください。

#### <a name="filenotfoundcacheentriesmax"></a>FileNotFoundCacheEntriesMax

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax`

Windows 10 に適用されます。 既定値は **128** であり、有効範囲は 1 から 65536 です。 この値は、クライアントがキャッシュできるファイル名情報の量を決定するために使用されます。 この値を増やすと、多数のファイル名へのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。 この値を **2048** に増やすことを検討してください。

#### <a name="dormantfilelimit"></a>DormantFileLimit

`HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit`

Windows 10 に適用されます。 既定値は **1023** です。 このパラメーターでは、アプリケーションがファイルを閉じた後に共有リソース上で開いたままにする必要があるファイルの最大数を指定します。 数千ものクライアントが SMB サーバーに接続している場合、この値を **256** に減らすことを検討してください。

Windows PowerShell コマンドレットの [Set-SmbClientConfiguration](/powershell/module/smbshare/set-smbclientconfiguration?view=win10-ps) および [Set-SmbServerConfiguration](/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps) を使用して、これらの SMB 設定の多くを構成できます。 レジストリのみの設定は、次の例のように Windows PowerShell を使用して構成することもできます。

```powershell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```

Windows Restricted Traffic Limited Functionality Baseline ガイダンスからの追加設定。Microsoft は、インターネットに直接接続していないか、Microsoft や他のサービスに送信されるデータを軽減したい環境に対して、[Windows セキュリティ ベースライン](/powershell/module/smbshare/set-smbserverconfiguration?view=win10-ps)と同じ手順を使用して作成されたベースラインをリリースしました。

[Windows Restricted Traffic Limited Functionality Baseline](/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services) 設定は、グループ ポリシーの表でアスタリスクのマーク付きで示されます。

#### <a name="disk-cleanup-including-using-the-disk-cleanup-wizard"></a>ディスク クリーンアップ (ディスク クリーンアップ ウィザードの使用を含む)

ディスク クリーンアップは、ゴールド/マスター イメージの VDI 実装で特に役立ちます。 イメージの準備、更新、および構成が完了したら、最後に実行するタスクの 1 つがディスク クリーンアップです。 "ディスク クリーンアップ ウィザード" と呼ばれる組み込みツールが用意されており、これを使用すると、ディスク領域の節約につながる可能性のある領域の大部分をクリーンアップできます。 インストールされたものがほとんどないが、パッチが完全に適用されている VM では、通常、ディスク クリーンアップを実行すると約 4 GB のディスク領域が解放されます。

さまざまなディスク クリーンアップ タスクの推奨事項を次に示します。 これらはすべて、実装する前にテストする必要があります。

1. すべての更新プログラムを適用した後に、(管理者特権での) ディスク クリーンアップ ウィザードを実行します。 "配信の最適化" と "Windows 更新プログラムのクリーンアップ" のカテゴリを含めます。 このプロセスは、コマンド ライン `Cleanmgr.exe` を `/SAGESET:11` オプションとともに使用して自動化できます。 `/SAGESET` オプションは、ディスク クリーンアップ ウィザードで使用可能なすべてのオプションを使用する、ディスク クリーンアップを自動化するために後から使用できるレジストリ値を設定します。

    1. テスト VM で、クリーン インストールから、`Cleanmgr.exe /SAGESET:11` を実行すると、既定で有効になった自動ディスク クリーンアップ オプションが 2 つだけがあることがわかります。

        - ダウンロードされたプログラム ファイル

        - インターネット一時ファイル

    2. その他のオプション、またはすべてのオプションを設定する場合、これらのオプションは、前のコマンド (`Cleanmgr.exe /SAGESET:11`) で指定された**インデックス**値に従って、レジストリに記録されます。 この例では、後続の自動ディスク クリーンアップ手順については、値 `11` をインデックスとして使用します。

    3. `Cleanmgr.exe /SAGESET:11` の実行後、ディスク クリーンアップ オプションのカテゴリがいくつか表示されます。 すべてのオプションをオンにし、 **[OK]** を選択できます。 ディスク クリーンアップ ウィザードが閉じ、設定がレジストリに保存されます。

2. ボリューム シャドウ コピーの記憶域が使用されている場合は、それをクリーンアップします。

    - 管理者特権でのコマンド プロンプトを開き、`vssadmin list shadows` コマンドを実行してから、`vssadmin list shadowstorage` コマンドを実行します。

        これらのコマンドからの出力が「**クエリを満たす項目が何もありませんでした**」である場合、使用中の VSS 記憶域はありません。

3. 一時ファイルおよびログをクリーンアップします。 管理者特権でのコマンド プロンプトで、`Del C:\*.tmp /s` コマンド、`Del C:\Windows\Temp\.` コマンド、および `Del %temp%\.` コマンドを実行します。

4. `wmic path win32_UserProfile where LocalPath="c:\users\<user>" Delete` を実行して、システム上の使用されていないプロファイルをすべて削除します。

### <a name="remove-onedrive-components"></a>OneDrive コンポーネントを削除する

OneDrive の削除では、パッケージの削除、アンインストール、および *.lnk ファイルの削除が行われます。 次の PowerShell のサンプル コードは、イメージから OneDrive を削除するのに役立ち、GitHub VDI 最適化スクリプトに含まれています。

```azurecli

Taskkill.exe /F /IM "OneDrive.exe"
Taskkill.exe /F /IM "Explorer.exe"`
    if (Test-Path "C:\\Windows\\System32\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\System32\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
    if (Test-Path "C:\\Windows\\SysWOW64\\OneDriveSetup.exe")`
     { Start-Process "C:\\Windows\\SysWOW64\\OneDriveSetup.exe"`
         -ArgumentList "/uninstall"`
         -Wait }
Remove-Item -Path
"C:\\Windows\\ServiceProfiles\\LocalService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force
Remove-Item -Path "C:\\Windows\\ServiceProfiles\\NetworkService\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\OneDrive.lnk" -Force \# Remove the automatic start item for OneDrive from the default user profile registry hive
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Load HKLM\\Temp C:\\Users\\Default\\NTUSER.DAT" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Delete HKLM\\Temp\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run /v OneDriveSetup /f" -Wait
Start-Process C:\\Windows\\System32\\Reg.exe -ArgumentList "Unload HKLM\\Temp" -Wait Start-Process -FilePath C:\\Windows\\Explorer.exe -Wait
```

ここでの情報に関する質問または問題については、Microsoft アカウント チームに問い合わせるか、Microsoft VDI のブログを調べるか Microsoft フォーラムにメッセージを投稿するか、または質問や問題について Microsoft にお問い合わせください。

## <a name="turn-windows-update-back-on"></a>Windows Update を再度有効にする

永続的 VDI の場合と同様に、Windows Update を再度有効にするには、次の手順に従います。

- これらのグループ ポリシー設定を再度有効にします。

    - ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\システム\\インターネット通信の管理\\インターネット通信の設定

        - Windows Update のすべての機能へのアクセスをオフにする ( **[有効]** から **[未構成]** に変更)

    - ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Windows Update

        - Windows Update のすべての機能へのアクセスを削除する ( **[有効]** から **[未構成]** に変更)

        - インターネット上の Windows Update に接続しない ( **[有効]** から **[未構成]** に変更)

    - ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Windows Update\\Windows Update for Business

        - 品質更新プログラムをいつ受信するかを選択してください ([有効] から [未構成] に変更)

    -   ローカル コンピューター ポリシー\\コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Windows Update\\Windows Update for Business

        - プレビュー ビルドや機能更新プログラムをいつ受信するかを選択してください ( **[有効]** から **[未構成]** に変更)

-  サービスを再度有効にする

    - Orchestrator サービスを更新する( **[無効]** から **[自動 (遅延開始)]** に変更)

    - 次の Windows レジストリ設定を編集します。

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\PolicyState

            - DeferQualityUpdates ( **[1]** から **[0]** に変更)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UpdatePolicy\Settings

            - PausedQualityDate (既存の値をすべて削除)

        - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\WAU

            - 無効

-  スケジュールされたタスクを再度有効にする

    - タスク スケジューラ ライブラリ\\Microsoft\\Windows\\InstallService\\ScanForUpdates

    - タスク スケジューラ ライブラリ\\Microsoft\\Windows\\InstallService\\ScanForUpdatesAsUser

これらの設定をすべて有効にするには、デバイスを再起動します。 このデバイスに機能の更新プログラムを提供したくない場合は、[設定]\\[Windows Update]\\[詳細オプション]\\[更新プログラムをいつインストールするかを選択する] に移動し、オプションを手動で設定します。**機能の更新プログラムには、新機能と機能強化が含まれています。これは、180、365 などの 0 以外の値の日数まで延期できます。**

### <a name="references"></a>参考資料

- [VDI (仮想デスクトップ インフラストラクチャ) とは](https://www.citrix.com/glossary/vdi.html)

- [組み込みの Windows イメージを含む Microsoft Store アプリを削除または更新した後で sysprep が失敗する](https://support.microsoft.com/help/2769827/sysprep-fails-after-you-remove-or-update-windows-store-apps-that-inclu)。
