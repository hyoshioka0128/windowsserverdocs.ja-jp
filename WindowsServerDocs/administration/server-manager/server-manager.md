---
title: サーバー マネージャー
description: サーバー マネージャー
ms.prod: windows-server
ms.technology: manage-server-manager
ms.topic: article
ms.assetid: d996ef40-8bcc-42b0-b6ae-806b828223f6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41d9227dd5472fc55858d75fa25e728dc69c2c7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851475"
---
# <a name="server-manager"></a>サーバー マネージャー

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーマネージャーは、Windows Server の管理コンソールです。これにより、IT 担当者は、サーバーに物理的にアクセスしたり、各サーバーへのリモートデスクトッププロトコル (rdP) 接続を有効にしなくても、デスクトップからローカルとリモートの両方の Windows ベースのサーバーをプロビジョニングして管理することができます。 サーバー マネージャーは、Windows Server 2008 R2 および Windows Server 2008 で使用できますが、サーバー マネージャーがリモートのマルチ サーバー管理をサポートし、管理者が管理できるサーバーの数を高めるために Windows Server 2012 で更新されました。

テストの結果では、サーバーが実行されているワークロードに応じて、最大 100 台のサーバーを管理する Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 のサーバー マネージャーを使用できます。 1 つのサーバー マネージャー コンソールを使用して管理できるサーバーの数は、サーバー マネージャーを実行するコンピューターの管理対象サーバーと使用可能なハードウェアとネットワーク リソースを要求するデータの量によって異なることがあります。 表示するデータの量がコンピューターのリソースの上限に近づくと、サーバー マネージャーからの応答が遅くなり、更新が完了するまでに時間がかかることがあります。 サーバー マネージャーで管理できるサーバーの数を増やすには、 **[イベント データの構成]** ダイアログ ボックスの設定を使用して、管理対象サーバーからサーバー マネージャーが受け取るイベント データを制限することをお勧めします。 [イベント データの構成] は、 **[イベント]** タイルの **[タスク]** メニューから開くことができます。 組織内でエンタープライズ レベルのサーバーを管理する必要がある場合は、[Microsoft System Center スイート](https://go.microsoft.com/fwlink/p/?LinkId=239437)製品の検討をお勧めします。

このトピックとサブトピックでは、サーバーマネージャーコンソールで機能を使用する方法について説明します。 このトピックの内容は次のとおりです。

-   [最初の考慮事項とシステム要件を確認する](#review-initial-considerations-and-system-requirements)

-   [サーバーマネージャーで実行できるタスク](#tasks-that-you-can-perform-in-server-manager)

-   [サーバーマネージャーの開始](#start-server-manager)

-   [リモートサーバーの再起動](#restart-remote-servers)

-   [サーバーマネージャーの設定を他のコンピューターにエクスポートする](#export-server-manager-settings-to-other-computers)

## <a name="review-initial-considerations-and-system-requirements"></a>考慮事項とシステム要件を確認する
以下のセクションでは、サーバーマネージャーのハードウェアとソフトウェアの要件に加えて、確認する必要がある最初の考慮事項について説明します。

### <a name="hardware-requirements"></a>ハードウェア要件
Windows Server 2016 のすべてのエディションで既定では、サーバー マネージャーをインストールします。 サーバー マネージャーの追加のハードウェア要件が存在します。

### <a name="software-and-configuration-requirements"></a>ソフトウェアと構成の要件
Windows Server 2016 のすべてのエディションで既定では、サーバー マネージャーをインストールします。 Windows Server 2016 でサーバー マネージャーを使用して管理できる [Server Core インストール オプション](https://go.microsoft.com/fwlink/p/?LinkID=241573) Windows Server 2016、Windows Server 2012、および Windows Server 2008 R2 のリモート コンピューターで実行されているのです。 サーバー マネージャーは Windows Server 2016 の Server Core インストール オプションでは実行されます。

最小サーバー グラフィック インターフェイスでサーバー マネージャーの実行します。サーバー グラフィック シェル機能がインストールされていない場合は、です。 Windows Server 2016 では既定では、サーバー グラフィック シェル機能がインストールされていません。 実行されていないサーバー グラフィック シェル、サーバー マネージャー コンソールを実行するが、一部のアプリケーションやコンソールから使用できるツールは使用できません。 サーバーグラフィックシェルを使用せずにインターネットブラウザーを実行することはできないので、HTML ヘルプなどの web ページやアプリケーション (たとえば、mmc の F1 ヘルプなど) を開くことはできません。 サーバー グラフィック シェルがインストールされていない場合は、Windows 自動更新とフィードバックを構成するためのダイアログ ボックスを開くことができません。サーバー マネージャー コンソールでこれらのダイアログ ボックスを開くコマンドがリダイレクトされ、 **sconfig.cmd**します。

Windows Server 2016 より古い Windows Server リリースを実行しているサーバーを管理するには、次のソフトウェアと Windows Server 2016 でサーバー マネージャーを使用して、Windows Server の以前のリリースを管理しやすく更新プログラムをインストールします。

|オペレーティング システム|必要なソフトウェア|
|----------|-----------|
| Windows Server 2012 R2 または Windows Server 2012 |-   [.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />[Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058)を -   します。 Windows Management Framework 5.0 ダウンロード パッケージは、Windows Server 2012 R2 および Windows Server 2012 上の Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 の管理の容易性の状態である更新プログラムが適用されるまで **アクセス不可**します。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) は Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 では必要なくなりました。|
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />[Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)を -   します。 Windows Management Framework 4.0 ダウンロードパッケージは、Windows Server 2008 R2 の Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 更新が適用されるまで、Windows Server 2008 R2 を実行しているサーバーの管理状態は、 **[アクセス不可]** になります。<br />-[サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487)に関連付けられているパフォーマンスの更新プログラムを使用すると、Windows Server 2008 R2 からパフォーマンスデータを収集サーバーマネージャーことができます。|
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />windows [Management framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) -   Windows management framework 3.0 ダウンロードパッケージは、windows Server 2008 で WINDOWS MANAGEMENT INSTRUMENTATION (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 更新が適用されるまで、Windows Server 2008 を実行しているサーバーの管理状態は、[アクセス不可] になります。以前のバージョンでは、 **Windows Management Framework 3.0 が実行**されます。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 からパフォーマンス データを収集します。|

#### <a name="manage-remote-computers-from-a-client-computer"></a>リモート コンピューターをクライアント コンピューターから管理する
サーバー マネージャー コンソールは付属 [リモート サーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=404281) Windows 10 用です。 リモート サーバー管理ツールがクライアント コンピューターにインストールされている場合は管理できないという、ローカル コンピューター サーバー マネージャーを使用して、注意してください。コンピューターまたは Windows クライアント オペレーティング システムを実行しているデバイスを管理する、サーバー マネージャーを使用できません。 サーバー マネージャーは、Windows ベースのサーバーの管理にのみ使用できます。

|サーバー マネージャーのソースのオペレーティング システム|対象が Windows Server 2016|Windows Server 2012 R2 を対象としました。 |対象 (Windows Server 2012) |対象 (Windows Server 2008 R2 または Windows Server 2008) |対象が Windows Server 2003 の場合|
|-------------------------------|--------------------------------------------|---------------------------------------|------------------------------------|-----------------------------------------------------------------------|------------------|
|Windows 10 または Windows Server 2016|フル サポート|フル サポート|フル サポート|[ソフトウェアと構成の要件](#software-and-configuration-requirements)を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|サポートされない|
|Windows 8.1 または Windows Server 2012 R2 |サポートされない|フル サポート|フル サポート|[ソフトウェアと構成の要件](#software-and-configuration-requirements)を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|限定的なサポート、オンラインとオフラインの状態のみ|
|Windows 8 または Windows Server 2012 |サポートされない|サポートされない|フル サポート|[ソフトウェアと構成の要件](#software-and-configuration-requirements)を満たしていれば、役割や機能のインストールとアンインストールを除く、ほとんどの管理タスクを実行可能|限定的なサポート、オンラインとオフラインの状態のみ|

###### <a name="to-start-server-manager-on-a-client-computer"></a>クライアント コンピューターでサーバー マネージャーを起動するには

1.  指示に従って [リモート サーバー管理ツール](../../remote/remote-server-administration-tools.md) をリモート サーバー管理ツールの Windows 10 をインストールします。

2.  **[スタート]** 画面で、 **[サーバーマネージャー]** をクリックします。 リモート サーバー管理ツールをインストールすると、 **[サーバー マネージャー]** タイルが使用できるようになります。

3.  リモートサーバー管理ツールをインストールした後に、**スタート**画面に **[管理ツール]** と **[サーバーマネージャー]** タイルのどちらも表示されない場合、 **[スタート]** 画面でサーバーマネージャーを検索しても結果が表示されない場合は、[**管理ツールを表示する]** の設定がオンになっていることを確認します。 この設定を表示するには、**スタート**画面の右上隅にマウスカーソルを置き、 **[設定]** をクリックします。 **[管理ツールを表示]** が無効になっている場合、この設定を有効にすると、リモート サーバー管理ツールの一部としてインストールされたツールが表示されます。

Windows 10 のリモートサーバー管理ツールを実行してリモートサーバーを管理する方法の詳細については、TechNet Wiki の「[リモートサーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=221055)」を参照してください。

#### <a name="configure-remote-management-on-servers-that-you-want-to-manage"></a>管理対象のサーバーでリモート管理を構成する

> [!IMPORTANT]
> 既定では、Windows Server 2016 でサーバー マネージャーおよび Windows PowerShell のリモート管理が有効にします。

サーバー マネージャーを使用して、リモート サーバーで管理タスクを行うには、サーバー マネージャーと Windows PowerShell を使用してリモート管理を許可するように管理するリモート サーバーを構成する必要があります。 Windows Server 2012 R2 または Windows Server 2012 でリモート管理が無効になっていて、もう一度有効にする場合は、次の手順を実行します。

##### <a name="to-configure-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-the-windows-interface"></a>Windows インターフェイスを使用して Windows Server 2012 R2 または Windows Server 2012 でサーバーマネージャーリモート管理を構成するには

1.  > [!NOTE]
    > **[リモート管理の構成]** ダイアログボックスで制御される設定は、リモート通信に DCOM を使用するサーバーマネージャーの一部には影響しません。

    既に開かれていない場合は、サーバー マネージャーを開くには、次のいずれかの操作を行います。

    -   Windows タスク バーで、サーバー マネージャ ボタンをクリックします。

    -   **[スタート]** 画面で、 **[サーバーマネージャー]** をクリックします。

2.  **[ローカルサーバー]** ページの **[プロパティ]** 領域で、 **[リモート管理]** プロパティのハイパーリンクされた値をクリックします。

3.  次のいずれかの操作を行い、 **[OK]** をクリックします。

    -   サーバーマネージャー (または Windows PowerShell がインストールされている場合は Windows PowerShell) を使用してこのコンピューターがリモートで管理されないようにするには、[**他のコンピューターからのこのサーバーのリモート管理を有効**にする] チェックボックスをオフにします。

    -   サーバーマネージャーまたは Windows PowerShell を使用してこのコンピューターをリモートで管理できるようにするには、[**他のコンピューターからのこのサーバーのリモート管理を有効**にする] を選択します。

##### <a name="to-enable-server-manager-remote-management-on--windows-server-2012-r2--or--windows-server-2012--by-using-windows-powershell"></a>Windows PowerShell を使用して Windows Server 2012 R2 または Windows Server 2012 でサーバーマネージャーリモート管理を有効にするには

1.  次のいずれかの操作を行います。

    -   Windows PowerShell を**スタート**画面から管理者として実行するには、 **[windows powershell]** タイルを右クリックし、 **[管理者として実行]** をクリックします。

    -   デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックしてタスク バーで、 **管理者として実行**します。

2.  次のように入力し、 **enter キーを押して、** 必要なすべてのファイアウォール規則の例外を有効にします。

    **Configure-smremoting.exe-Enable**

    > [!NOTE]
    > このコマンドは、管理者特権 (管理者として実行) を使用して開いたコマンド プロンプトでも実行できます。

    リモート管理を有効にできない場合は、Microsoft TechNet の「 [about_remote_Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkID=135188) 」を参照して、トラブルシューティングのヒントとベストプラクティスを確認してください。

###### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-older-operating-systems"></a>以前のオペレーティング システムでサーバー マネージャーおよび Windows PowerShell のリモート管理を有効にするには

-   次のいずれかの操作を行います。

    -   Windows Server 2008 R2 を実行しているサーバーでリモート管理を有効にするには、Windows Server 2008 R2 ヘルプの「[サーバーマネージャーによるリモート管理](https://go.microsoft.com/fwlink/?LinkID=137378)」を参照してください。

    -   Windows Server 2008 を実行しているサーバーでリモート管理を有効にするには、「 [Windows PowerShell でのリモートコマンドの有効化と使用](https://go.microsoft.com/fwlink/p/?LinkId=242565)」を参照してください。

## <a name="tasks-that-you-can-perform-in-server-manager"></a>サーバー マネージャーで実行できるタスク
サーバーマネージャーを使用すると、管理者は次の表のタスクを1つのツールで実行できるようになり、サーバーの管理効率が向上します。 Windows Server 2012 R2 および Windows Server 2012 では、サーバーの標準ユーザーと Administrators グループのメンバーの両方がサーバーマネージャーで管理タスクを実行できますが、既定では、次の表に示すように、標準ユーザーは一部のタスクを実行できません。

管理者は、サーバーマネージャーコマンドレットモジュール ( [enable-servermanagerstandarduserremoting と disable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205470.aspx)と[enable-servermanagerstandarduserremoting と disable-servermanagerstandarduserremoting](https://technet.microsoft.com/library/jj205468.aspx)) の2つの Windows PowerShell コマンドレットを使用して、いくつかの追加データへの標準ユーザーアクセスをさらに制御できます。 **Enable-servermanagerstandarduserremoting と disable-servermanagerstandarduserremoting**コマンドレットは、1人以上の管理者以外のユーザーに、イベント、サービス、パフォーマンスカウンター、および役割と機能インベントリデータへのアクセスを提供することができます。

> [!IMPORTANT]
> Windows Server オペレーティング システムのそれ以降のリリースを管理する、サーバー マネージャーを使用できません。 Windows server 2012 または Windows 8 で実行されているサーバーマネージャーは、Windows Server 2012 R2 を実行しているサーバーの管理には使用できません。

|タスクの説明|管理者 (ビルトイン Administrator アカウントを含む)|サーバーの標準ユーザー|
|----------|----------------------------------|-------------|
|を管理するために使用できるサーバーマネージャーサーバーのプールにリモートサーバーを追加します。|はい|いいえ|
|特定の地理的な場所にあるサーバーや特定の目的に使用するサーバーなど、サーバーのカスタムグループを作成および編集します。|はい|はい|
|Windows Server 2012 R2 または Windows Server 2012 を実行しているローカルサーバーまたはリモートサーバーで、役割、役割サービス、および機能をインストールまたはアンインストールします。 役割、役割サービス、および機能の定義については、「[役割、役割サービス、および](https://go.microsoft.com/fwlink/p/?LinkId=239558)機能」を参照してください。|はい|いいえ|
|ローカル サーバーまたはリモート サーバーにインストールされているサーバーの役割や機能を表示または変更できます。 **注:** サーバーマネージャーでは、役割と機能のデータは、システムの基本言語 (システムの既定の GUI 言語とも呼ばれます)、またはオペレーティングシステムのインストール時に選択された言語で表示されます。|はい|標準ユーザーは、役割や機能の表示と管理が可能で、役割イベントの表示などのタスクを実行できますが、役割サービスを追加したり削除したりすることはできません。|
|Windows PowerShell または mmc スナップインなどの管理ツールを起動します。リモートサーバーを対象とする Windows PowerShell セッションを開始するには、 **[サーバー]** タイルでサーバーを右クリックし、 **[windows powershell]** をクリックします。 Mmc スナップインはサーバーマネージャーコンソールの **[ツール]** メニューから起動して、スナップインが開いた後に mmc をリモートコンピューターに対してポイントすることができます。|はい|はい|
|別の資格情報でリモート サーバーを管理できます。これを行うには、 **[サーバー]** タイルでサーバーを右クリックし、 **[管理に使用する資格情報]** をクリックします。 **[管理に使用する資格情報]** は、一般的なサーバー管理タスクとファイル サービスおよび記憶域サービスの管理タスクに使用できます。|はい|いいえ|
|サービスの開始や停止など、サーバーの運用ライフサイクルに関連する管理タスクを実行します。また、サーバーのネットワーク設定、ユーザーとグループ、およびリモートデスクトップ接続を構成できるその他のツールを開始します。|はい|標準ユーザーは、サービスを開始したり停止したりすることはできません。 ローカルサーバーの名前、ワークグループ、ドメインメンバーシップ、およびリモートデスクトップの設定を変更できますが、これらのタスクを完了するには、ユーザーアカウント制御によって管理者の資格情報を提供するように求められます。 リモート管理の設定を変更することはできません。|
|ベスト プラクティスに準拠するための役割のスキャンなど、サーバーにインストールされている役割の運用ライフサイクルに関連する管理タスクを実行できます。|はい|標準ユーザーはベストプラクティスアナライザースキャンを実行できません。|
|サーバーの状態を調べ、重要なイベントを識別し、構成に関する問題や失敗の分析とトラブルシューティングを実行できます。|はい|はい|
|サーバーマネージャーダッシュボードで警告を表示するイベント、パフォーマンスデータ、サービス、およびベストプラクティスアナライザーの結果をカスタマイズします。|はい|はい|
|サーバーを再起動できます。|はい|いいえ|
|サーバーマネージャーコンソールに表示される管理対象サーバーに関するデータを更新します。|はい|いいえ|

> [!NOTE]
> Windows Server 2008 R2 を実行しているサーバーまたは Windows Server 2008 に役割と機能を追加する、サーバー マネージャーを使用できません。

## <a name="start-server-manager"></a>サーバーマネージャーの開始
サーバー マネージャーは、Windows Server 2016 ログオン サーバー管理者グループのメンバーを実行しているサーバーでは既定で自動的に開始します。 サーバー マネージャを終了する場合は、次の方法のいずれかで再起動します。 また、既定の動作を変更し、サーバーマネージャーが自動的に開始されないようにする手順についても説明します。

#### <a name="to-start-server-manager-from-the-start-screen"></a>スタート画面からサーバーマネージャーを開始するには

-   Windows の**スタート**画面で、 **[サーバーマネージャー]** タイルをクリックします。

#### <a name="to-start-server-manager-from-the-windows-desktop"></a>Windows デスクトップからサーバー マネージャーを起動するには

-   Windows タスク バーで **[サーバー マネージャー]** をクリックします。

#### <a name="to-prevent-server-manager-from-starting-automatically"></a>サーバー マネージャーが自動的に起動されないようにするには

1.  サーバーマネージャーコンソールの **[管理]** メニューで、 **[サーバーマネージャーのプロパティ]** をクリックします。

2.  **[サーバー マネージャーのプロパティ]** ダイアログ ボックスで、 **[ログオン時にサーバー マネージャーを自動的に起動しない]** チェック ボックスをオンにします。 **[OK]** をクリックすると、

3.  または、[グループポリシー] 設定を有効にしてサーバーマネージャーが自動的に開始されないようにすることもできます。**ログオン時に自動的にサーバーマネージャーを開始**しないようにします。 ローカルのグループポリシーエディターコンソールで、このポリシー設定へのパスは、コンピューターの構成 \ 管理用テンプレート \ システム \ サーバーマネージャーです。

## <a name="restart-remote-servers"></a>リモート サーバーを再起動する
リモートサーバーを再起動するには、サーバーマネージャーの役割またはグループのページの **[サーバー]** タイルを使用します。

> [!IMPORTANT]
> リモート サーバーを再起動すると、そのリモート サーバーにユーザーがログオンしている場合や、開いているプログラムのデータが保存されていない場合でも、サーバーが強制的に再起動されます。 ローカル コンピューターをシャットダウンしたり再起動したりする場合と異なり、保存されていないプログラムのデータを保存するかどうかや、ログオンしているユーザーを強制的にログオフするかどうかを確認するメッセージは表示されません。 そのため、他のユーザーをリモート サーバーから強制的にログオフしたり、リモート サーバーで実行中のプログラムの保存されていないデータを破棄しても問題がないことを確認してください。
> 
> 管理対象サーバーのシャットダウン中や再起動中にサーバーマネージャーで自動更新が行われた場合、管理対象サーバーで更新と管理の状態エラーが発生する可能性があります。これは、サーバーマネージャーが再起動を完了するまでリモートサーバーに接続できないためです。

#### <a name="to-restart-remote-servers-in-server-manager"></a>サーバー マネージャーでリモート サーバーを再起動するには

1.  サーバーマネージャーで、役割またはサーバーグループのホームページを開きます。

2.  サーバーマネージャーに追加したリモートサーバーを1つ以上選択します。 **Ctrl** キーを押しながらクリックすると、複数のサーバーを一度に選択できます。 サーバーをサーバーマネージャーサーバープールに追加する方法の詳細については、「[サーバーマネージャーへのサーバーの追加](add-servers-to-server-manager.md)」を参照してください。

3.  選択したサーバーを右クリックし、 **[サーバーの再起動]** をクリックします。

## <a name="export-server-manager-settings-to-other-computers"></a>サーバー マネージャーの設定を他のコンピューターにエクスポートする
サーバー マネージャーでは、管理対象サーバーの一覧は、サーバー マネージャー コンソールの設定を変更し、作成したカスタムのグループは次の 2 つのファイルに格納します。 サーバー マネージャー (またはリモート サーバー管理ツールがインストールされている Windows 10) の同じリリースを実行している他のコンピューターでこれらの設定を再利用することができます。 リモート サーバー管理ツールは、これらのコンピューターにサーバー マネージャーの設定をエクスポートする Windows クライアント ベース コンピューター上で実行されている必要があります。

-   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

-   %*appdata*% \ Local \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config

> [!NOTE]
> -   サーバー プールのサーバーに対して [管理に使用する資格情報] で別の資格情報を指定した場合、その資格情報は移動プロファイルに格納されません。 それらの資格情報については、管理元の各コンピューターで サーバー マネージャー ユーザーがそれぞれ追加する必要があります。
> -   ネットワーク共有の移動プロファイルは、ユーザーがネットワークに初めてログオンしてログオフした後に作成されます。 このときに **Serverlist.xml** ファイルが作成されます。

次の2つの方法のいずれかで、サーバーマネージャー設定のエクスポート、サーバーマネージャー設定の移植、または他のコンピューターでの使用を行うことができます。

-   ドメインに参加している別のコンピューターに設定をエクスポートするには、[active directory ユーザーとコンピューター] で移動プロファイルを持つようにサーバーマネージャーユーザーを構成します。 [Active directory ユーザーとコンピューター] でユーザーのプロパティを変更するには、ドメイン管理者である必要があります。

-   ワークグループ内の別のコンピューターに設定をエクスポートするには、前の2つのファイルを、サーバーマネージャーを使用して管理するコンピューターの同じ場所にコピーします。

#### <a name="to-export-server-manager-settings-to-other-domain-joined-computers"></a>ドメインに参加している他のコンピューターにサーバー マネージャーの設定をエクスポートするには

1.  Active directory ユーザーとコンピューター で、サーバーマネージャーユーザーの **プロパティ** ダイアログボックスを開きます。

2.  **[プロファイル]** タブで、ユーザーのプロファイルを保存するネットワーク共有のパスを追加します。

3.  次のいずれかの操作を行います。

    -   米国英語 (en-us) のビルドでは、 **Serverlist**ファイルへの変更が自動的にプロファイルに保存されます。 次の手順に進みます。

    -   他のビルドでは、サーバーマネージャーを実行しているコンピューターから、ユーザーの移動プロファイルに含まれるネットワーク共有に、次の2つのファイルをコピーします。

        -   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

        -   %*localappdata*% \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config

4.  **[OK]** をクリックして変更を保存し、 **[プロパティ]** ダイアログ ボックスを閉じます。

#### <a name="to-export-server-manager-settings-to-computers-in-workgroups"></a>ワークグループ内のコンピューターにサーバー マネージャーの設定をエクスポートするには

-   リモートサーバーを管理するコンピューターで、次の2つのファイルを、サーバーマネージャーを実行している別のコンピューターの同じファイルで上書きし、必要な設定を行います。

    -   %*appdata*% \ Microsoft\Windows\ServerManager\Serverlist.xml

    -   %*localappdata*% \ Microsoft_Corporation \Servermanager. exe_StrongName_*GUID*\6.2.0.0\user.config



