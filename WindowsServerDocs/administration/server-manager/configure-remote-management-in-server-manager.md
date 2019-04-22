---
title: サーバー マネージャーでリモート管理を構成します。
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4a66fe7a274756de9bed9f6b14f5b9e491e5b623
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819583"
---
# <a name="configure-remote-management-in-server-manager"></a>サーバー マネージャーでリモート管理を構成します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows server のリモート サーバー管理タスクを実行するのにサーバー マネージャーを使用できます。 リモート管理は、Windows Server 2016 を実行しているサーバーでは、既定で有効です。 サーバー マネージャーを使用してサーバーをリモート管理をするには、サーバー マネージャー サーバー プールにサーバーを追加します。

サーバー マネージャーを使用して、Windows Server の以前のリリースを実行しているリモート サーバーを管理することができますが、これらの古いオペレーティング システムを完全に管理する次の更新プログラムが必要です。

Windows Server 2016 より古い Windows Server リリースを実行しているサーバーを管理するには、次のソフトウェアと Windows Server 2016 でサーバー マネージャーを使用して、Windows Server の以前のリリースを管理しやすく更新プログラムをインストールします。

|オペレーティング システム|必要なソフトウェア|管理状態|
|----------|-----------|---------|
| Windows Server 2012 R2 または Windows Server 2012 |-   [.NET framework 4.6](https://www.microsoft.com/download/details.aspx?id=45497)<br />-   [Windows Management Framework 5.0](https://go.microsoft.com/fwlink/?LinkID=395058)します。 Windows Management Framework 5.0 ダウンロード パッケージは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 で Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているサーバーの管理状態である更新プログラムが適用されるまで**アクセス不可**します。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) は Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 では必要なくなりました。||
| Windows Server 2008 R2 |-   [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)<br />-   [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)します。 Windows Management Framework 4.0 ダウンロード パッケージは、Windows Server 2008 R2 で Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2008 R2 を実行しているサーバーの管理状態である更新プログラムが適用されるまで**アクセス不可**します。<br />-パフォーマンスの更新プログラムに関連付けられている[サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 R2 からパフォーマンス データを収集します。||
| Windows Server 2008 |-   [.NET Framework 4](https://www.microsoft.com/download/en/details.aspx?id=17718)<br />-   [Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019) 。 Windows Management Framework 3.0 ダウンロード パッケージは、Windows Server 2008 で Windows Management Instrumentation (WMI) プロバイダーを更新します。 更新された WMI プロバイダーは、管理対象のサーバーにインストールされている役割と機能に関する情報を収集するサーバー マネージャーを使用できます。 Windows Server 2008 を実行しているサーバーの管理状態である更新プログラムが適用されるまで**アクセス不可 - 以前のバージョンの Windows Management Framework 3.0 を実行することを確認**します。<br />-パフォーマンスの更新プログラムに関連付けられている [サポート技術情報の記事 2682011](https://go.microsoft.com/fwlink/p/?LinkID=245487) Server manager で Windows Server 2008 からパフォーマンス データを収集します。||

ワークグループ内にある管理、またはサーバー マネージャーを実行しているワークグループ コンピューターからリモート サーバーの管理サーバーを追加する方法の詳細については、次を参照してください。[サーバーを追加するには、サーバー マネージャーに](add-servers-to-server-manager.md)します。

## <a name="BKMK_remote"></a>有効化またはリモート管理を無効にします。
Windows Server 2016 では、リモート管理は既定で有効にします。 サーバー マネージャーを使用してリモートで Windows Server 2016 を実行されているコンピューターに接続するには、無効になっている場合、対象のコンピューターでサーバー マネージャーのリモート管理を有効にする必要があります。 このセクションの手順では、リモート管理を無効にする方法、およびリモート管理が無効になっている場合に再度有効にする方法について説明します。 サーバー マネージャー コンソールで、ローカル サーバーのリモート管理の状態が表示される、**プロパティ**の領域、**ローカル サーバー**ページ。

リモート管理が有効になっている場合でも、ビルトイン Administrator アカウント以外のローカル管理者アカウントには、サーバーをリモートで管理するための権限がないことがあります。 リモート ユーザー アカウント制御 (UAC) **LocalAccountTokenFilterPolicy**レジストリ設定は、リモートで管理する組み込みの administrator アカウント以外の Administrators グループのローカル アカウントを許可するように構成する必要があります、サーバー。

Windows Server 2016 では、サーバー マネージャーは、Windows リモート管理 (WinRM) とリモート通信に分散コンポーネント オブジェクト モデル (DCOM) に依存します。 設定によって制御されている、**リモート管理を構成する** ダイアログ ボックスでは、サーバー マネージャーおよび Windows PowerShell のリモート通信に WinRM を使用する部分のみに影響します。 パーツ サーバー マネージャーのリモート通信に DCOM を使用するには影響しません。 たとえば、サーバー マネージャーの Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行しているリモート サーバーとの通信に WinRM を使用して、Windows Server 2008 を実行しているサーバーと Windows Server 2008 R2 との通信に DCOM を使用ない、 [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkId=293881)または[Windows Management Framework 3.0](https://go.microsoft.com/fwlink/p/?LinkID=229019)更新を適用します。 Microsoft 管理コンソール (mmc) とその他の従来の管理ツールは、DCOM を使用します。 これらの設定を変更する方法の詳細については、次を参照してください。 [DCOM を介して mmc またはその他のツールのリモート管理を構成する](#BKMK_dcom)このトピックの「します。

> [!NOTE]
> このセクションの手順は、Windows Server を実行しているコンピューターでのみ実行することができます。 有効にするかはサーバー マネージャーを使用して、クライアント オペレーティング システムを管理することはできませんので、これらの手順を使用して Windows 10 を実行するコンピューターでリモート管理を無効にすることはできません。

-   WinRM のリモート管理を有効にするには、次のいずれかの手順を選択してください。

    -   [Windows インターフェイスを使用してサーバー マネージャーのリモート管理を有効にするには](#BKMK_windows)

    -   [Windows PowerShell を使用してサーバー マネージャーのリモート管理を有効にするには](#BKMK_ps)

    -   [コマンドラインを使用してサーバー マネージャーのリモート管理を有効にするには](#BKMK_cmdline)

    -   [サーバー マネージャーおよび Windows PowerShell リモート管理を以前のリリースの Windows Server を有効にするには](#BKMK_old)

-   WinRM とサーバー マネージャーのリモート管理を無効にするには、次の手順のいずれかを選択します。

    -   [グループ ポリシーを使用してリモート管理を無効にするには](#BKMK_disableGP)

    -   [無人インストール中に、応答ファイルを使用してリモート管理を無効にするには](#BKMK_unattend)

-   DCOM のリモート管理を構成するには、「[DCOM のリモート管理を構成するには](#BKMK_dcom)」を参照してください。

### <a name="BKMK_windows"></a>Windows インターフェイスを使用してサーバー マネージャーのリモート管理を有効にするには

1.  > [!NOTE]
    > 設定によって制御されている、**リモート管理を構成する**ダイアログ ボックスで部分サーバー マネージャーのリモート通信に DCOM を使用するには影響しません。

    をリモートで管理するコンピューターには、が開いていない場合、サーバー マネージャーを開きます。 Windows タスク バーで **[サーバー マネージャー]** をクリックします。 **開始**画面で、、**サーバー マネージャー**を並べて表示します。

2.  **プロパティ**の領域、**ローカル サーバー**  ページで、ハイパーリンクが設定された値をクリックして、**リモート管理**プロパティ。

3.  次のいずれかの操作を行い、 **[OK]** をクリックします。

    -   このコンピューターがサーバー マネージャー (または Windows PowerShell がインストールされている場合) を使用してリモートで管理されていることを防ぐためには、オフ、**他のコンピューターからこのサーバーのリモート管理を有効にする**チェック ボックスをオンします。

    -   このコンピューターをサーバー マネージャーまたは Windows PowerShell を使用してリモートで管理できるように、次のように選択します。**他のコンピューターからこのサーバーのリモート管理を有効にする**します。

### <a name="BKMK_ps"></a>Windows PowerShell を使用してサーバー マネージャーのリモート管理を有効にするには

1.  をリモートで管理するコンピューターには、管理者特権で Windows PowerShell セッションを開くには、次のいずれかを実行します。

    -   Windows デスクトップで、タスク バーの **[Windows PowerShell]** を右クリックし、 **[管理者として実行]** をクリックします。

    -   Windows で**開始**画面を右クリックして**Windows PowerShell**、アプリ バーでをクリック**管理者として実行**します。

2.  、次を入力し、キーを押します**Enter**必要なファイアウォール規則の例外をすべて有効にします。

    **構成 SMremoting.exe-有効にします。**

### <a name="BKMK_cmdline"></a>コマンドラインを使用してサーバー マネージャーのリモート管理を有効にするには

1.  リモート管理対象のコンピューターで、管理者特権でコマンド プロンプト セッションを開きます。 これを実行する、**開始**画面で「 **cmd**、を右クリックし、**コマンド プロンプト**タイルが表示されたら、**アプリ**結果とアプリ バーでクリックして**管理者として実行**します。

2.  次の実行可能ファイルを実行します。

    **%windir%\system32\Configure-SMremoting.exe**

3.  次のいずれかの操作を行います。

    -   リモート管理を無効にするには、次のように入力します。 **SMremoting.exe-を無効にする**、キーを押しますと **」と入力**します。

    -   リモート管理を有効にするには、入力**SMremoting.exe-有効にする**、し、キーを押します **」と入力**します。

    -   現在のリモート管理設定を表示するには、次のように入力します。 **SMremoting.exe-取得**、し、ENTER キーを押します。

### <a name="BKMK_old"></a>サーバー マネージャーおよび Windows PowerShell リモート管理を以前のリリースの Windows Server を有効にするには

-   次のいずれかの操作を行います。

    -   Windows Server 2012 を実行しているサーバーでリモート管理を有効にするのを参照してください。 [Windows インターフェイスを使用してサーバー マネージャーのリモート管理を有効にする](#BKMK_windows)このトピックの「します。

    -   Windows Server 2008 R2 を実行しているサーバーでリモート管理を有効にするのを参照してください。[サーバー マネージャーによるリモート管理](https://go.microsoft.com/fwlink/?LinkID=137378)、Windows Server 2008 R2 ヘルプ。

    -   Windows Server 2008 を実行しているサーバーでリモート管理を有効にするのを参照してください。[を有効にすると、Windows PowerShell のリモート コマンドを使用して](https://go.microsoft.com/fwlink/p/?LinkId=242565)します。

### <a name="BKMK_dcom"></a>DCOM を介して mmc またはその他のツールのリモート管理を構成するには

1.  次のいずれかの操作を行い、セキュリティが強化された Windows ファイアウォール スナップインを開きます。

    -   **プロパティ**の領域、**ローカル サーバー**サーバー マネージャーでのページで、ハイパー テキスト値をクリックして、 **Windows ファイアウォール**プロパティ、およびクリック**詳細設定**します。

    -   **開始**画面で「 **WF.msc**、に表示されるときにスナップイン タイルをクリックしてして、**アプリ**結果。

2.  ツリー ウィンドウで、 **[受信の規則]** を選択します。

3.  次のファイアウォール規則の例外は、有効になっているし、グループ ポリシー設定で無効になっていないことを確認します。 次のいずれかの規則が無効になっている場合は、次の手順に進みます。

    -   COM+ ネットワーク アクセス (DCOM-受信)

    -   リモート イベント ログ管理 (np 受信)

    -   リモート イベント ログ管理 (RPC)

    -   リモート イベント ログ管理 (RPC-EPMAP)

4.  無効になっている規則を右クリックし、ショートカット メニューの **[規則の有効化]** をクリックします。

5.  セキュリティが強化された Windows ファイアウォール スナップインを閉じます。

### <a name="BKMK_disableGP"></a>グループ ポリシーを使用してリモート管理を無効にするには

1.  ローカル グループ ポリシー エディターを開くには、次のいずれかの操作を行います。

    -   実行している Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 でのサーバーで、**開始**画面で「 **gpedit.msc**、 をクリックしてし、 **gpedit**タイルときに表示されます。

    -   実行している Windows Server 2008 R2 または Windows Server 2008 でのサーバーで、**実行**ダイアログ ボックスに「 **gpedit.msc**、し、キーを押します **」と入力**します。

2.  開いている**コンピューター構成 \ 管理用テンプレート \windows コンポーネント \windows リモート管理 (WinRM) \WinRM サービス**します。

3.  コンテンツ ウィンドウで **[WinRM によるリモート サーバー管理を許可する]** をダブルクリックします。

4.  **[WinRM によるリモート サーバー管理を許可する]** ポリシー設定のダイアログ ボックスで、 **[無効]** をクリックしてリモート管理を無効にします。 **[OK]** をクリックして変更内容を保存し、ポリシー設定のダイアログ ボックスを閉じます。

### <a name="BKMK_unattend"></a>無人インストール中に、応答ファイルを使用してリモート管理を無効にするには

1.  Windows システム イメージ マネージャー (Windows SIM) を使用して、Windows Server 2016 のインストール用の無人インストール応答ファイルを作成します。 応答ファイルを作成して、Windows SIM を使用する方法の詳細については、次を参照してください。 [Windows System Image Manager とは何ですか?](https://technet.microsoft.com/library/cc766347.aspx)と[ステップ バイ ステップ。IT プロフェッショナル向けの基本的な Windows 展開](https://technet.microsoft.com/library/dd349348.aspx)します。

2.  応答ファイルで設定を見つけます**microsoft-windows-web-services-for-management-core \enableserverremotemanagement**します。

3.  既定では、応答ファイルを適用するすべてのサーバー上でサーバー マネージャーのリモート管理を無効にする設定**Microsoft-Windows-Web-Services-for-Management-Core \EnableServerremoteManagement**に**False**.

    > [!NOTE]
    > この設定は、オペレーティング システムのセットアップ プロセスの一環としてリモート管理を無効にします。 この設定を構成しても、管理者から、オペレーティング システムのセットアップが完了したら、サーバー上のサーバー マネージャーのリモート管理を有効にします。 管理者は、サーバー マネージャーのリモート管理を使用して、もう一度手順を有効にできます[Windows インターフェイスを使用してサーバー マネージャーのリモート管理を構成する](#BKMK_windows)または[を使用してサーバー マネージャーのリモート管理を有効にするにはWindows PowerShell](#BKMK_ps)このトピックの「します。
    > 
    > 既定では、無人インストールの一環としてリモート管理を無効にしてインストールした後、サーバーでリモート管理を有効にしない場合、サーバー マネージャーを使用して、この応答ファイルを適用するサーバーを完全に管理されてことはできません。 Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 で実行されている (および、既定で無効になっているリモート管理がある) サーバーは、サーバー マネージャーのサーバーに追加された後、サーバー マネージャー コンソールで管理容易性の状態のエラーを生成します。プール。

## <a name="windows-remote-management-winrm-listener-settings"></a>Windows リモート管理 (WinRM) リスナー設定
サーバー マネージャーは、既定の WinRM リスナー設定を管理するリモート サーバー上に依存します。 既定の認証メカニズム、またはリモート サーバー上の WinRM リスナー ポート番号は、既定の設定から変更されましたが場合、は、サーバー マネージャーがリモート サーバーと通信できません。

次の一覧に、サーバー マネージャーを使用して管理するための既定の WinRM リスナー設定を示します。

-   WinRM サービスが実行されています。

-   ポート番号 5985 を介した HTTP 要求を受け入れるための WinRM リスナーが作成されます。

-   WinRM からの要求を許可するために Windows ファイアウォール設定でポート番号 5985 が有効になっています。

-   **Kerberos** 認証と **Negotiate** 認証の両方が有効になっています。

WinRM がリモート コンピューターと通信するために既定のポート番号は 5985 です。

コマンド プロンプトで WinRM リスナー設定を構成する方法の詳細については、入力**winrm ヘルプ config**、し、ENTER キーを押します。

## <a name="see-also"></a>関連項目
[サーバー マネージャーにサーバーの追加](add-servers-to-server-manager.md)
[Windows PowerShell: about_remote_Troubleshooting、Windows Server TechCenter のに関する](https://technet.microsoft.com/library/dd347642.aspx)
[ユーザー アカウント制御の説明](https://support.microsoft.com/kb/951016)



