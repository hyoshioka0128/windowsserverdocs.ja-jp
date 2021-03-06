---
title: サーバー マネージャー
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d996ef40-8bcc-42b0-b6ae-806b828223f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3f3abeec3d4ecbe5e80d08a99a00b43a408c4ac
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811286"
---
# <a name="server-manager"></a>サーバー マネージャー

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー マネージャーは、IT プロフェッショナルのプロビジョニングを支援し、サーバーへの物理アクセスまたはリモート デスクトップを有効にする必要のいずれかを必要とせず、自分のデスクトップからローカルとリモートの両方の Windows ベースのサーバーを管理する Windows server 管理コンソール各サーバーにプロトコル (rdP) 接続します。 サーバー マネージャーは、Windows Server 2008 R2 および Windows Server 2008 で使用できますが、サーバー マネージャーがリモートのマルチ サーバー管理をサポートし、管理者が管理できるサーバーの数を高めるために Windows Server 2012 で更新されました。

テストの結果では、サーバーが実行されているワークロードに応じて、最大 100 台のサーバーを管理する Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 のサーバー マネージャーを使用できます。 1 つのサーバー マネージャー コンソールを使用して管理できるサーバーの数は、サーバー マネージャーを実行するコンピューターの管理対象サーバーと使用可能なハードウェアとネットワーク リソースを要求するデータの量によって異なることがあります。 表示するデータの量がコンピューターのリソースの上限に近づくと、サーバー マネージャーからの応答が遅くなり、更新が完了するまでに時間がかかることがあります。 サーバー マネージャーで管理できるサーバーの数を増やすには、 **[イベント データの構成]** ダイアログ ボックスの設定を使用して、管理対象サーバーからサーバー マネージャーが受け取るイベント データを制限することをお勧めします。 [イベント データの構成] は、 **[イベント]** タイルの **[タスク]** メニューから開くことができます。 組織内でエンタープライズ レベルのサーバーを管理する必要がある場合は、[Microsoft System Center スイート](https://go.microsoft.com/fwlink/p/?LinkId=239437)製品の検討をお勧めします。

このトピックとサブトピックは、サーバー マネージャー コンソールで機能を使用する方法に関する情報を提供します。 このトピックは次のセクションで構成されます。

-   [検討事項とシステム要件](#review-initial-considerations-and-system-requirements)

-   [サーバー マネージャーでを実行できるタスク](#tasks-that-you-can-perform-in-server-manager)

-   [サーバー マネージャーを起動します。](#start-server-manager)

-   [リモート サーバーを再起動します。](#restart-remote-servers)

-   [他のコンピューターにサーバー マネージャーの設定をエクスポートします。](#export-server-manager-settings-to-other-computers)

## <a name="review-initial-considerations-and-system-requirements"></a>考慮事項とシステム要件を確認する
次のセクションでは、初期およびサーバー マネージャー用のハードウェアおよびソフトウェア要件を確認する必要がある事項を一覧表示します。

### <a name="hardware-requirements"></a>ハードウェア要件
Windows Server 2016 のすべてのエディションで既定では、サーバー マネージャーをインストールします。 サーバー マネージャーの追加のハードウェア要件が存在します。

### <a name="software-and-configuration-requirements"></a>ソフトウェアと構成の要件
Windows Server 2016 のすべてのエディションで既定では、サーバー マネージャーをインストールします。 Windows Server 2016 でサーバー マネージャーを使用して管理できる [Server Core インストール オプション](https://go.microsoft.com/fwlink/p/?LinkID=241573) Windows Server 2016、Windows Server 2012、および Windows Server 2008 R2 のリモート コンピューターで実行されているのです。 サーバー マネージャーは Windows Server 2016 の Server Core インストール オプションでは実行されます。

最小サーバー グラフィック インターフェイスでサーバー マネージャーの実行します。サーバー グラフィック シェル機能がインストールされていない場合は、です。 Windows Server 2016 では既定では、サーバー グラフィック シェル機能がインストールされていません。 実行されていないサーバー グラフィック シェル、サーバー マネージャー コンソールを実行するが、一部のアプリケーションやコンソールから使用できるツールは使用できません。 HTML ヘルプ (、mmc の F1 ヘルプ、たとえば) を開くことができないなどせず、サーバー グラフィック シェル、その web ページおよびアプリケーションのインターネット ブラウザーを実行できません。 サーバー グラフィック シェルがインストールされていない場合は、Windows 自動更新とフィードバックを構成するためのダイアログ ボックスを開くことができません。サーバー マネージャー コンソールでこれらのダイアログ ボックスを開くコマンドがリダイレクトされ、 **sconfig.cmd**します。

Windows Server 2016 より古い Windows Server リリースを実行しているサーバーを管理するには、次のソフトウェアと Windows Server 2016 でサーバー マネージャーを使用して、Windows Server の以前のリリースを管理しやすく更新プログラムをインストールします。

|オペレーティング システム|必要なソフトウェア|
|----------|-----------|
| Windows Server 2012 R2 または Windows Server 2012 |-   [.NET framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058)します。 Windows Management Framework 5.0 ダウンロード パッケージは、Windows Server 2012 R2 および Windows Server 2012 上の Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 の管理の容易性の状態である更新プログラムが適用されるまで **アクセス不可**します。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) は Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 では必要なくなりました。|
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)します。 Windows Management Framework 4.0 ダウンロード パッケージは、Windows Server 2008 R2 で Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2008 R2 を実行しているサーバーの管理状態である更新プログラムが適用されるまで**アクセス不可**します。<br />-パフォーマンスの更新プログラムに関連付けられている[サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 R2 からパフォーマンス データを収集します。|
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) 。 Windows Management Framework 3.0 ダウンロード パッケージは、Windows Server 2008 で Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2008 を実行しているサーバーの管理状態である更新プログラムが適用されるまで**アクセス不可 - 以前のバージョンの Windows Management Framework 3.0 を実行することを確認**します。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 からパフォーマンス データを収集します。|

#### <a name="manage-remote-computers-from-a-client-computer"></a>リモート コンピューターをクライアント コンピューターから管理する
サーバー マネージャー コンソールは付属 [リモート サーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=404281) Windows 10 用です。 リモート サーバー管理ツールがクライアント コンピューターにインストールされている場合は管理できないという、ローカル コンピューター サーバー マネージャーを使用して、注意してください。コンピューターまたは Windows クライアント オペレーティング システムを実行しているデバイスを管理する、サーバー マネージャーを使用できません。 サーバー マネージャーは、Windows ベースのサーバーの管理にのみ使用できます。

|サーバー マネージャーのソースのオペレーティング システム|対象が Windows Server 2016|Windows Server 2012 R2 を対象としました。 |Windows Server 2012 を対象としました。 |Windows Server 2008 R2 または Windows Server 2008 を対象としました。 |対象が Windows Server 2003 の場合|
|-------------------------------|--------------------------------------------|---------------------------------------|------------------------------------|-----------------------------------------------------------------------|------------------|
|Windows 10 または Windows Server 2016|フル サポート|フル サポート|フル サポート|「 [ソフトウェアと構成の要件](#software-and-configuration-requirements) 」を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|サポートされていません|
|Windows 8.1 または Windows Server 2012 R2 |サポートされていません|フル サポート|フル サポート|「 [ソフトウェアと構成の要件](#software-and-configuration-requirements) 」を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|限定的なサポート、オンラインとオフラインの状態のみ|
|Windows 8 または Windows Server 2012 |サポートされていません|サポートされていません|フル サポート|「 [ソフトウェアと構成の要件](#software-and-configuration-requirements) 」を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|限定的なサポート、オンラインとオフラインの状態のみ|

###### <a name="to-start-server-manager-on-a-client-computer"></a>クライアント コンピューターでサーバー マネージャーを起動するには

1.  指示に従って [リモート サーバー管理ツール](../../remote/remote-server-administration-tools.md) をリモート サーバー管理ツールの Windows 10 をインストールします。

2.  **開始**画面で、**サーバー マネージャー**します。 リモート サーバー管理ツールをインストールすると、 **[サーバー マネージャー]** タイルが使用できるようになります。

3.  どちらの場合、**管理ツール**も**サーバー マネージャー**にタイルが表示されます、**開始**リモート サーバー管理ツールでは、インストール後に画面とサーバー マネージャー用の検索、**開始**画面に結果が表示されないことを確認します、**管理ツールを表示する**設定を有効にします。 この設定を表示するには、右上隅にマウス カーソルを移動、**開始**、画面をクリックして**設定**します。 **[管理ツールを表示]** が無効になっている場合、この設定を有効にすると、リモート サーバー管理ツールの一部としてインストールされたツールが表示されます。

リモート サーバー管理ツールの Windows 10 をリモート サーバー管理を実行する方法の詳細については、次を参照してください。[リモート サーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=221055)、TechNet Wiki にします。

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>管理対象のサーバーでリモート管理を構成する

> [!IMPORTANT]
> 既定では、Windows Server 2016 でサーバー マネージャーおよび Windows PowerShell のリモート管理が有効にします。

サーバー マネージャーを使用して、リモート サーバーで管理タスクを行うには、サーバー マネージャーと Windows PowerShell を使用してリモート管理を許可するように管理するリモート サーバーを構成する必要があります。 Windows Server 2012 R2 または Windows Server 2012 では、リモート管理が無効になっている、再度有効にする場合は、次の手順を実行します。

##### <a name="to-configure-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-the-windows-interface"></a>Windows インターフェイスを使用して、Windows Server 2012 R2 または Windows Server 2012 サーバー マネージャーのリモート管理を構成するには

1.  > [!NOTE]
    > 設定によって制御されている、**リモート管理を構成する**ダイアログ ボックスで部分サーバー マネージャーのリモート通信に DCOM を使用するには影響しません。

    既に開かれていない場合は、サーバー マネージャーを開くには、次のいずれかの操作を行います。

    -   Windows タスク バーで、サーバー マネージャ ボタンをクリックします。

    -   **開始**画面で、**サーバー マネージャー**します。

2.  **プロパティ**の領域、**ローカル サーバー**  ページで、ハイパーリンクが設定された値をクリックして、**リモート管理**プロパティ。

3.  次のいずれかの操作を行い、 **[OK]** をクリックします。

    -   このコンピューターがサーバー マネージャー (または Windows PowerShell がインストールされている場合) を使用してリモートで管理されていることを防ぐためには、オフ、**他のコンピューターからこのサーバーのリモート管理を有効にする**チェック ボックスをオンします。

    -   このコンピューターをサーバー マネージャーまたは Windows PowerShell を使用してリモートで管理できるように、次のように選択します。**他のコンピューターからこのサーバーのリモート管理を有効にする**します。

##### <a name="to-enable-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-windows-powershell"></a>Windows PowerShell を使用して Windows Server 2012 R2 または Windows Server 2012 サーバー マネージャーのリモート管理を有効にするには

1.  次のいずれかを実行します。

    -   管理者として Windows PowerShell を実行する、**開始**画面で、右クリックし、 **Windows PowerShell**タイルをクリックして**管理者として実行**します。

    -   デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックしてタスク バーで、 **管理者として実行**します。

2.  、次を入力し、キーを押します**Enter**必要なファイアウォール規則の例外をすべて有効にします。

    **Configure-SMremoting.exe -Enable**

    > [!NOTE]
    > このコマンドは、管理者特権 (管理者として実行) を使用して開いたコマンド プロンプトでも実行できます。

    リモート管理を有効にすると失敗した場合を参照してください。 [about_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) Microsoft technet のトラブルシューティングのヒントやベスト プラクティスです。

###### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>以前のオペレーティング システムでサーバー マネージャーおよび Windows PowerShell のリモート管理を有効にするには

-   次のいずれかを実行します。

    -   Windows Server 2008 R2 を実行しているサーバーでリモート管理を有効にするのを参照してください。[サーバー マネージャーによるリモート管理](https://go.microsoft.com/fwlink/?LinkID=137378)、Windows Server 2008 R2 ヘルプ。

    -   Windows Server 2008 を実行しているサーバーでリモート管理を有効にするのを参照してください。[を有効にすると、Windows PowerShell のリモート コマンドを使用して](https://go.microsoft.com/fwlink/p/?LinkId=242565)します。

## <a name="tasks-that-you-can-perform-in-server-manager"></a>サーバー マネージャーで実行できるタスク
サーバー マネージャーでは、管理者は 1 つのツールを使用して、次の表のタスクを実行することによりより効率的にサーバーの管理できるようにします。 Windows Server 2012 R2 および Windows Server 2012 では、サーバーの標準のユーザーと Administrators グループのメンバーの両方を実行できますサーバー マネージャーでの管理タスクが既定では、標準ユーザーはできません、一部のタスクを実行するように、次の表にします。

管理者は、2 つの Windows PowerShell コマンドレットを使用して、サーバー マネージャー コマンドレット モジュールで[Enable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205470.aspx)と[Disable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205468.aspx)をさらにいくつか追加のデータを標準ユーザーのアクセスを制御します。 **Enable-servermanagerstandarduserremoting**コマンドレットは、イベント、サービス、パフォーマンス カウンター、およびよび役割と機能インベントリ データを 1 つまたは複数の標準的な管理者以外のユーザー アクセスを提供できます。

> [!IMPORTANT]
> Windows Server オペレーティング システムのそれ以降のリリースを管理する、サーバー マネージャーを使用できません。 Windows Server 2012 R2 を実行しているサーバーを管理する Windows Server 2012 または Windows 8 で実行されているサーバー マネージャーを使用できません。

|タスクの説明|管理者 (ビルトイン Administrator アカウントを含む)|サーバーの標準ユーザー|
|----------|----------------------------------|-------------|
|リモート サーバーを追加する可能性のあるサーバー マネージャー サーバー プールを管理するために使用します。|〇|X|
|作成し、特定の地理的な場所にまたは特定の目的で使用されるサーバーなどのサーバーのカスタム グループを編集します。|〇|〇|
|インストールまたは役割、役割サービス、および Windows Server 2012 R2 を実行しているリモート サーバーまたは Windows Server 2012 またはローカルでの機能をアンインストールします。 役割、役割サービス、および機能の定義は、次を参照してください。[役割、役割サービス、および機能](https://go.microsoft.com/fwlink/p/?LinkId=239558)します。|〇|X|
|ローカル サーバーまたはリモート サーバーにインストールされているサーバーの役割や機能を表示または変更できます。 **注:** サーバー マネージャーで、役割と機能のデータは、システムの既定の GUI 言語またはオペレーティング システムのインストール時に選択した言語とも呼ばれる、システムの基本言語で表示されます。|〇|標準ユーザーは、役割や機能の表示と管理が可能で、役割イベントの表示などのタスクを実行できますが、役割サービスを追加したり削除したりすることはできません。|
|Windows PowerShell または mmc スナップインなどの管理ツールを起動します。リモート サーバーでサーバーを右クリックする対象とする Windows PowerShell セッションを開始することができます、**サーバー**タイルをクリックして**Windows PowerShell**します。 Mmc スナップインからを起動することができます、**ツール**ポイントし、mmc のスナップインで後にリモート コンピューターに、サーバー マネージャーのコンソールのメニューが開きます。|〇|〇|
|別の資格情報でリモート サーバーを管理できます。これを行うには、 **[サーバー]** タイルでサーバーを右クリックし、 **[管理に使用する資格情報]** をクリックします。 **[管理に使用する資格情報]** は、一般的なサーバー管理タスクとファイル サービスおよび記憶域サービスの管理タスクに使用できます。|〇|X|
|開始やサービスの停止などのサーバーの運用ライフ サイクルに関連付けられている管理タスクを実行します。サーバーのネットワーク設定、ユーザーとグループ、およびリモート デスクトップ接続を構成するための他のツールを起動します。|〇|標準ユーザーは、サービスを開始したり停止したりすることはできません。 これらは、ローカル サーバーの名前、workgroup、またはドメインのメンバーシップ、およびリモート デスクトップの設定を変更できますが、これらのタスクを完了する前に、管理者の資格情報を提供するユーザー アカウント制御によって求められます。 リモート管理の設定を変更することはできません。|
|ベスト プラクティスに準拠するための役割のスキャンなど、サーバーにインストールされている役割の運用ライフサイクルに関連する管理タスクを実行できます。|〇|標準ユーザーは、ベスト プラクティス アナライザー スキャンを実行できません。|
|サーバーの状態を調べ、重要なイベントを識別し、構成に関する問題や失敗の分析とトラブルシューティングを実行できます。|〇|〇|
|イベント、パフォーマンス データ、サービス、およびサーバー マネージャー ダッシュ ボードに警告を表示するベスト プラクティス アナライザーの結果をカスタマイズします。|〇|〇|
|サーバーを再起動できます。|〇|X|
|管理対象サーバーについて、サーバー マネージャー コンソールに表示されるデータを更新します。|〇|X|

> [!NOTE]
> Windows Server 2008 R2 を実行しているサーバーまたは Windows Server 2008 に役割と機能を追加する、サーバー マネージャーを使用できません。

## <a name="start-server-manager"></a>サーバー マネージャーを起動します。
サーバー マネージャーは、Windows Server 2016 ログオン サーバー管理者グループのメンバーを実行しているサーバーでは既定で自動的に開始します。 サーバー マネージャを終了する場合は、次の方法のいずれかで再起動します。 このセクションでは、既定の動作を変更して、サーバー マネージャーが自動的に起動するを防ぐのための手順も含まれています。

#### <a name="to-start-server-manager-from-the-start-screen"></a>スタート画面からサーバー マネージャーを起動するには

-   Windows で**開始**画面で、、**サーバー マネージャー**を並べて表示します。

#### <a name="to-start-server-manager-from-the-windows-desktop"></a>Windows デスクトップからサーバー マネージャーを起動するには

-   Windows タスク バーで **[サーバー マネージャー]** をクリックします。

#### <a name="to-prevent-server-manager-from-starting-automatically"></a>サーバー マネージャーが自動的に起動されないようにするには

1.  サーバー マネージャー コンソールで、**管理** メニューのをクリックして**サーバー マネージャーのプロパティ**します。

2.  **[サーバー マネージャーのプロパティ]** ダイアログ ボックスで、 **[ログオン時にサーバー マネージャーを自動的に起動しない]** チェック ボックスをオンにします。 **[OK]** をクリックします。

3.  または、サーバー マネージャーを防ぐため、グループ ポリシー設定を有効にすると自動的に起動されないことができます**自動的に起動しないサーバー マネージャーのログオン時**します。 ローカル グループ ポリシー エディター コンソールで、このポリシー設定へのパスとは、コンピューター構成 \ 管理用 Templates\System\Server マネージャーです。

## <a name="restart-remote-servers"></a>リモート サーバーを再起動する
リモート サーバーを再起動することができます、**サーバー**役割またはグループのページでサーバー マネージャーのタイル。

> [!IMPORTANT]
> リモート サーバーを再起動すると、そのリモート サーバーにユーザーがログオンしている場合や、開いているプログラムのデータが保存されていない場合でも、サーバーが強制的に再起動されます。 ローカル コンピューターをシャットダウンしたり再起動したりする場合と異なり、保存されていないプログラムのデータを保存するかどうかや、ログオンしているユーザーを強制的にログオフするかどうかを確認するメッセージは表示されません。 そのため、他のユーザーをリモート サーバーから強制的にログオフしたり、リモート サーバーで実行中のプログラムの保存されていないデータを破棄しても問題がないことを確認してください。
> 
> 自動更新では、管理対象サーバーがシャット ダウンと再起動、更新および管理容易性の状態が完了するまで、サーバー マネージャーがリモート サーバーに接続できないため、管理対象のサーバーのエラーが発生することが中にサーバー マネージャーでが発生した場合再起動しています。

#### <a name="to-restart-remote-servers-in-server-manager"></a>サーバー マネージャーでリモート サーバーを再起動するには

1.  サーバー マネージャーで、役割またはサーバー グループのホーム ページを開きます。

2.  サーバー マネージャーを追加した 1 つまたは複数のリモート サーバーを選択します。 **Ctrl** キーを押しながらクリックすると、複数のサーバーを一度に選択できます。 サーバー マネージャー サーバー プールにサーバーを追加する方法の詳細については、次を参照してください。[サーバーを追加するには、サーバー マネージャーに](add-servers-to-server-manager.md)します。

3.  選択したサーバーを右クリックし、 **[サーバーの再起動]** をクリックします。

## <a name="export-server-manager-settings-to-other-computers"></a>サーバー マネージャーの設定を他のコンピューターにエクスポートする
サーバー マネージャーでは、管理対象サーバーの一覧は、サーバー マネージャー コンソールの設定を変更し、作成したカスタムのグループは次の 2 つのファイルに格納します。 サーバー マネージャー (またはリモート サーバー管理ツールがインストールされている Windows 10) の同じリリースを実行している他のコンピューターでこれらの設定を再利用することができます。 リモート サーバー管理ツールは、これらのコンピューターにサーバー マネージャーの設定をエクスポートする Windows クライアント ベース コンピューター上で実行されている必要があります。

-   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

-   %*appdata*%\Local\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

> [!NOTE]
> -   サーバー プールのサーバーに対して [管理に使用する資格情報] で別の資格情報を指定した場合、その資格情報は移動プロファイルに格納されません。 それらの資格情報については、管理元の各コンピューターで サーバー マネージャー ユーザーがそれぞれ追加する必要があります。
> -   ネットワーク共有の移動プロファイルは、ユーザーがネットワークに初めてログオンしてログオフした後に作成されます。 このときに **Serverlist.xml** ファイルが作成されます。

サーバー マネージャーの設定をエクスポート、移植可能で、サーバー マネージャーの設定を行う、または次の 2 つの方法のいずれかで他のコンピューターで使用できます。

-   別のドメインに参加しているコンピューターへの設定をエクスポートするには、サーバー マネージャーのユーザーがそのユーザーの active directory で、移動プロファイルとコンピューターを構成します。 ユーザーのプロパティを active directory ユーザーとコンピューターを変更するドメイン管理者があります。

-   ワークグループ内の別のコンピューターへの設定をエクスポートするには、サーバー マネージャーを使用して管理するコンピューター上の同じ場所に、上記の 2 つのファイルをコピーします。

#### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>ドメインに参加している他のコンピューターにサーバー マネージャーの設定をエクスポートするには

1.  Active directory ユーザーとコンピューター で開く、**プロパティ**サーバー マネージャー ユーザーのダイアログ ボックス。

2.  **プロファイル** タブで、ユーザーのプロファイルを格納するネットワーク共有にパスを追加します。

3.  次のいずれかを実行します。

    -   米国英語 (en-ご) を作成、変更、 **Serverlist.xml**ファイルは、プロファイルに自動的に保存します。 次の手順に進みます。

    -   それ以外のビルドでは、ユーザーの移動プロファイルの一部であるネットワーク共有にサーバー マネージャーを実行しているコンピューターから次の 2 つのファイルをコピーします。

        -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config

4.  **[OK]** をクリックして変更を保存し、 **[プロパティ]** ダイアログ ボックスを閉じます。

#### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>ワークグループ内のコンピューターにサーバー マネージャーの設定をエクスポートするには

-   リモート サーバーを管理するコンピューターで、サーバー マネージャーを実行し、目的の設定を持つ別のコンピューターから同じファイルで次の 2 つのファイルを上書きします。

    -   %*appdata*%\Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*localappdata*%\Microsoft_Corporation\ServerManager.exe_StrongName_*GUID*\6.2.0.0\user.config



