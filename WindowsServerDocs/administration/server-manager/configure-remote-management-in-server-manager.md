---
title: サーバーマネージャーでのリモート管理の構成
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 509182ed-c37d-4b81-84bc-aee43d006873
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e1058a5679f73fcd2ceb8586da687158762d10f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383210"
---
# <a name="configure-remote-management-in-server-manager"></a>サーバーマネージャーでのリモート管理の構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server では、サーバーマネージャーを使用してリモートサーバー上で管理タスクを実行できます。 Windows Server 2016 を実行しているサーバーでは、リモート管理が既定で有効になっています。 サーバーマネージャーを使用してサーバーをリモートで管理するには、サーバーをサーバーマネージャーサーバープールに追加します。

サーバーマネージャーを使用すると、以前のリリースの Windows Server を実行しているリモートサーバーを管理できますが、これらの古いオペレーティングシステムを完全に管理するには、次の更新プログラムが必要です。

Windows Server 2016 より古い Windows Server リリースを実行しているサーバーを管理するには、次のソフトウェアと Windows Server 2016 でサーバー マネージャーを使用して、Windows Server の以前のリリースを管理しやすく更新プログラムをインストールします。

|オペレーティング システム|必要なソフトウェア|管理状態|
|----------|-----------|---------|
| Windows Server 2012 R2 または Windows Server 2012 |-   [.NET Framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />[Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058)を -   します。 Windows Management Framework 5.0 ダウンロードパッケージは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 の Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 更新が適用されるまで、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているサーバーの管理状態は、 **[アクセス不可]** になります。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) は Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 では必要なくなりました。||
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />[Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)を -   します。 Windows Management Framework 4.0 ダウンロードパッケージは、Windows Server 2008 R2 の Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 更新が適用されるまで、Windows Server 2008 R2 を実行しているサーバーの管理状態は、 **[アクセス不可]** になります。<br />-[サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487)に関連付けられているパフォーマンスの更新プログラムを使用すると、Windows Server 2008 R2 からパフォーマンスデータを収集サーバーマネージャーことができます。||
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />windows [Management framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) -   Windows management framework 3.0 ダウンロードパッケージは、windows Server 2008 で WINDOWS MANAGEMENT INSTRUMENTATION (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 更新が適用されるまで、Windows Server 2008 を実行しているサーバーの管理状態は、[アクセス不可] になります。以前のバージョンでは、 **Windows Management Framework 3.0 が実行**されます。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 からパフォーマンス データを収集します。||

ワークグループ内のサーバーを追加して管理する方法、またはサーバーマネージャーを実行しているワークグループコンピューターからリモートサーバーを管理する方法の詳細については、「[サーバーマネージャーへのサーバーの追加](add-servers-to-server-manager.md)」を参照してください。

## <a name="enabling-or-disabling-remote-management"></a>リモート管理を有効または無効にする
Windows Server 2016 では、リモート管理が既定で有効になっています。 サーバーマネージャーを使用して Windows Server 2016 を実行しているコンピューターにリモート接続できるようにするには、対象コンピューターが無効になっている場合はサーバーマネージャーリモート管理を有効にする必要があります。 このセクションの手順では、リモート管理を無効にする方法、およびリモート管理が無効になっている場合に再度有効にする方法について説明します。 サーバーマネージャーコンソールの **[ローカルサーバー]** ページの **[プロパティ]** 領域に、ローカルサーバーのリモート管理の状態が表示されます。

リモート管理が有効になっている場合でも、ビルトイン Administrator アカウント以外のローカル管理者アカウントには、サーバーをリモートで管理するための権限がないことがあります。 リモートユーザーアカウント制御 (UAC) の**LocalAccountTokenFilterPolicy**レジストリ設定を構成し、ビルトイン administrator アカウント以外の Administrators グループのローカルアカウントでサーバーをリモートで管理できるようにする必要があります。

Windows Server 2016 では、サーバーマネージャーはリモート通信用に Windows リモート管理 (WinRM) と分散コンポーネントオブジェクトモデル (DCOM) に依存しています。 **[リモート管理の構成]** ダイアログボックスで制御される設定は、リモート通信に WinRM を使用するサーバーマネージャーおよび Windows PowerShell の一部にのみ影響します。 これらは、リモート通信に DCOM を使用するサーバーマネージャーの一部には影響しません。 たとえば、サーバーマネージャーは、windows server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行しているリモートサーバーとの通信には WinRM を使用しますが、windows Server 2008[および Windows server](https://go.microsoft.com/fwlink/p/?LinkID=229019) 2008 r2 を[実行して](https://go.microsoft.com/fwlink/?LinkId=293881)いるサーバーと通信するために DCOM を使用します。 Microsoft 管理コンソール (mmc) およびその他のレガシ管理ツールは、DCOM を使用します。 これらの設定を変更する方法の詳細については、このトピックの「 [DCOM 経由で mmc またはその他のツールのリモート管理を構成するには」を](#to-configure-mmc-or-other-tool-remote-management-over-dcom)参照してください。

> [!NOTE]
> このセクションの手順は、Windows Server を実行しているコンピューターでのみ実行することができます。 これらの手順を使用して、Windows 10 を実行しているコンピューターのリモート管理を有効または無効にすることはできません。これは、サーバーマネージャーを使用してクライアントオペレーティングシステムを管理できないためです。

-   WinRM のリモート管理を有効にするには、次のいずれかの手順を選択してください。

    -   [Windows インターフェイスを使用してサーバーマネージャーのリモート管理を有効にするには](#to-enable-server-manager-remote-management-by-using-the-windows-interface)

    -   [Windows PowerShell を使用してサーバーマネージャーのリモート管理を有効にするには](#to-enable-server-manager-remote-management-by-using-windows-powershell)

    -   [コマンドラインを使用してサーバーマネージャーのリモート管理を有効にするには](#to-enable-server-manager-remote-management-by-using-the-command-line)

    -   [以前のリリースの Windows Server でサーバーマネージャーおよび Windows PowerShell のリモート管理を有効にするには](#to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server)

-   WinRM とサーバーマネージャーのリモート管理を無効にするには、次のいずれかの手順を選択します。

    -   [グループポリシーを使用してリモート管理を無効にするには](#to-disable-remote-management-by-using-group-policy)

    -   [無人インストール中に応答ファイルを使用してリモート管理を無効にするには](#to-disable-remote-management-by-using-an-answer-file-during-unattended-installation)

-   DCOM のリモート管理を構成するには、「[DCOM のリモート管理を構成するには](#to-configure-mmc-or-other-tool-remote-management-over-dcom)」を参照してください。

### <a name="to-enable-server-manager-remote-management-by-using-the-windows-interface"></a>Windows インターフェイスを使用してサーバー マネージャーのリモート管理を構成するには

1.  > [!NOTE]
    > **[リモート管理の構成]** ダイアログボックスで制御される設定は、リモート通信に DCOM を使用するサーバーマネージャーの一部には影響しません。

    リモートで管理するコンピューターで、サーバーマネージャーを開きます (まだ開いていない場合)。 Windows タスク バーで **[サーバー マネージャー]** をクリックします。 **スタート**画面で、 **[サーバーマネージャー]** タイルをクリックします。

2.  **[ローカルサーバー]** ページの **[プロパティ]** 領域で、 **[リモート管理]** プロパティのハイパーリンクされた値をクリックします。

3.  次のいずれかの操作を行い、 **[OK]** をクリックします。

    -   サーバーマネージャー (または Windows PowerShell がインストールされている場合は Windows PowerShell) を使用してこのコンピューターがリモートで管理されないようにするには、[**他のコンピューターからのこのサーバーのリモート管理を有効**にする] チェックボックスをオフにします。

    -   サーバーマネージャーまたは Windows PowerShell を使用してこのコンピューターをリモートで管理できるようにするには、[**他のコンピューターからのこのサーバーのリモート管理を有効**にする] を選択します。

### <a name="to-enable-server-manager-remote-management-by-using-windows-powershell"></a>Windows PowerShell を使用してサーバー マネージャーのリモート管理を有効にするには

1.  リモートで管理するコンピューターで、次のいずれかの操作を行って、管理者特権で Windows PowerShell セッションを開きます。

    -   Windows デスクトップで、タスク バーの **[Windows PowerShell]** を右クリックし、 **[管理者として実行]** をクリックします。

    -   Windows の**スタート**画面で、 **[windows PowerShell]** を右クリックし、アプリバーの **[管理者として実行]** をクリックします。

2.  次のように入力し、 **enter キーを押して、** 必要なすべてのファイアウォール規則の例外を有効にします。

    **Configure-smremoting.exe-enable**

### <a name="to-enable-server-manager-remote-management-by-using-the-command-line"></a>コマンド ラインを使用してサーバー マネージャーのリモート管理を有効にするには

1.  リモート管理対象のコンピューターで、管理者特権でコマンド プロンプト セッションを開きます。 これを行うには、**スタート**画面で「 **cmd**」と入力し、 **[アプリ]** の結果に **[コマンドプロンプト]** タイルが表示されたらそれを右クリックして、アプリバーで **[管理者として実行]** をクリックします。

2.  次の実行可能ファイルを実行します。

    **%windir%\system32\Configure-SMremoting.exe**

3.  次のいずれかの操作を行います。

    -   リモート管理を無効にするには、「 **configure-smremoting.exe-disable**」と**入力し、enter キーを**押します。

    -   リモート管理を有効にするには、「 **configure-smremoting.exe-enable**」と**入力し、enter キーを**押します。

    -   現在のリモート管理設定を表示するには、「 **configure-smremoting.exe-get**」と入力し、enter キーを押します。

### <a name="to-enable-server-manager-and-windows-powershell-remote-management-on-earlier-releases-of-windows-server"></a>Windows Server の以前のリリースでサーバー マネージャーおよび Windows PowerShell のリモート管理を有効にするには

-   次のいずれかの操作を行います。

    -   Windows Server 2012 を実行しているサーバーでリモート管理を有効にするには、このトピックの「 [windows のインターフェイスを使用してサーバーマネージャーのリモート管理を有効にするに](#to-enable-server-manager-remote-management-by-using-the-windows-interface)は」を参照してください。

    -   Windows Server 2008 R2 を実行しているサーバーでリモート管理を有効にするには、Windows Server 2008 R2 ヘルプの「[サーバーマネージャーによるリモート管理](https://go.microsoft.com/fwlink/?LinkID=137378)」を参照してください。

    -   Windows Server 2008 を実行しているサーバーでリモート管理を有効にするには、「 [Windows PowerShell でのリモートコマンドの有効化と使用](https://go.microsoft.com/fwlink/p/?LinkId=242565)」を参照してください。

### <a name="to-configure-mmc-or-other-tool-remote-management-over-dcom"></a>DCOM を介して mmc またはその他のツールのリモート管理を構成するには

1.  次のいずれかの操作を行い、セキュリティが強化された Windows ファイアウォール スナップインを開きます。

    -   サーバーマネージャーの **[ローカルサーバー]** ページの **[プロパティ]** 領域で、 **[Windows ファイアウォール]** プロパティのハイパーテキスト値をクリックし、 **[詳細設定]** をクリックします。

    -   **スタート** 画面で「 **WF**」と入力し、**アプリ** の結果に スナップイン タイルが表示されたら、それをクリックします。

2.  ツリー ウィンドウで、 **[受信の規則]** を選択します。

3.  次のファイアウォール規則の例外が有効になっていて、グループポリシー設定によって無効にされていないことを確認します。 次のいずれかの規則が無効になっている場合は、次の手順に進みます。

    -   COM+ ネットワーク アクセス (DCOM-受信)

    -   リモートイベントログ管理 (NP 受信)

    -   リモートイベントログ管理 (RPC)

    -   リモートイベントログ管理 (rpc-epmap)

4.  無効になっている規則を右クリックし、ショートカット メニューの **[規則の有効化]** をクリックします。

5.  セキュリティが強化された Windows ファイアウォール スナップインを閉じます。

### <a name="to-disable-remote-management-by-using-group-policy"></a>グループ ポリシーを使用してリモート管理を無効にするには

1.  ローカルグループポリシーエディターを開くには、次のいずれかの操作を行います。

    -   Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行しているサーバーで、**スタート**画面で「 **gpedit.msc**」と入力し、 **gpedit**タイルが表示されたらそれをクリックします。

    -   Windows Server 2008 R2 または Windows Server 2008 を実行しているサーバーで、[ファイル名を**指定**して**実行**] ダイアログボックスに「 **gpedit.msc**」と入力し、enter キーを押します。

2.  **コンピューターの構成 \ 管理用テンプレート \Windows コンポーネント \windows リモート管理 (winrm) \ Winrm サービス**を開きます。

3.  コンテンツ ウィンドウで **[WinRM によるリモート サーバー管理を許可する]** をダブルクリックします。

4.  **[WinRM によるリモート サーバー管理を許可する]** ポリシー設定のダイアログ ボックスで、 **[無効]** をクリックしてリモート管理を無効にします。 **[OK]** をクリックして変更内容を保存し、ポリシー設定のダイアログ ボックスを閉じます。

### <a name="to-disable-remote-management-by-using-an-answer-file-during-unattended-installation"></a>応答ファイルを使用して無人インストール中にリモート管理を無効にするには

1.  windows システムイメージマネージャー (Windows SIM) を使用して、Windows Server 2016 インストール用の無人インストール応答ファイルを作成します。 応答ファイルを作成する方法および Windows SIM を使用する方法の詳細については、「 [Windows システム イメージ マネージャーとは](https://technet.microsoft.com/library/cc766347.aspx) 」および「 [ステップ バイ ステップ ガイド: IT プロ用 Windows の基本展開](https://technet.microsoft.com/library/dd349348.aspx)」を参照してください。

2.  応答ファイルで、設定**Microsoft-Windows-Web-Services-for-Management-Core\EnableServerremoteManagement**を見つけます。

3.  応答ファイルの適用先となるすべてのサーバーでサーバーマネージャーリモート管理を既定で無効にするには、 **[microsoft-windows-web-services-for-management-core \enableserverremotemanagement]** を **[False]** に設定します。

    > [!NOTE]
    > この設定は、オペレーティング システムのセットアップ プロセスの一環としてリモート管理を無効にします。 この設定を構成しても、オペレーティングシステムのセットアップが完了した後で、管理者がサーバーでサーバーマネージャーリモート管理を有効にすることはできません。 管理者は、「」の手順に従って[、windows インターフェイスを使用](#to-enable-server-manager-remote-management-by-using-the-windows-interface)してリモート管理をサーバーマネージャー構成するか、このトピックの「 [windows PowerShell を使用](#to-enable-server-manager-remote-management-by-using-windows-powershell)してリモート管理をサーバーマネージャー有効にする」の手順に従って、サーバーマネージャーリモート管理を再び有効にすることができます。
    > 
    > 無人インストールの一部としてリモート管理を既定で無効にし、インストール後にサーバーでリモート管理を再び有効にしない場合、この応答ファイルが適用されるサーバーはサーバーマネージャーを使用して完全に管理することはできません。 Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 (およびリモート管理が既定で無効になっている) を実行しているサーバーは、サーバーマネージャーサーバーに追加された後、サーバーマネージャーコンソールで管理状態エラーを生成します。管理.

## <a name="windows-remote-management-winrm-listener-settings"></a>Windows リモート管理 (WinRM) リスナーの設定
サーバーマネージャーは、管理するリモートサーバー上の既定の WinRM リスナー設定に依存します。 リモートサーバーの既定の認証メカニズムまたは WinRM リスナーのポート番号が既定の設定から変更されている場合、サーバーマネージャーはリモートサーバーと通信できません。

次の一覧は、サーバーマネージャーを使用して管理するための既定の WinRM リスナー設定を示しています。

-   WinRM サービスが実行されています。

-   ポート番号 5985 を介した HTTP 要求を受け入れるための WinRM リスナーが作成されます。

-   WinRM からの要求を許可するために Windows ファイアウォール設定でポート番号 5985 が有効になっています。

-   **Kerberos** 認証と **Negotiate** 認証の両方が有効になっています。

WinRM がリモート コンピューターと通信するために既定のポート番号は 5985 です。

WinRM リスナー設定の構成方法の詳細については、コマンドプロンプトで「 **winrm help config**」と入力し、enter キーを押します。

## <a name="see-also"></a>参照
Windows PowerShell
[サーバーマネージャーにサーバーを追加する](add-servers-to-server-manager.md) [: Windows Server
TechCenter の About_remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx) [ユーザーアカウント制御の説明](https://support.microsoft.com/kb/951016)



