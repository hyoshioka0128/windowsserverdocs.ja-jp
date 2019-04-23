---
title: リモート サーバー管理ツール
description: リモート サーバー管理ツールの最上位レベルのトピック
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-rsat
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: cc4b0eb51b477ec175040b46c9563f81955c0be3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846213"
---
# <a name="remote-server-administration-tools"></a>リモート サーバー管理ツール

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、リモート サーバー管理ツールの Windows 10 をサポートします。

> [!IMPORTANT]
> 以降では Windows 10 年 2018年 10 月 Update、RSAT のセットとして含まれる**オンデマンド機能**自体の Windows 10 でします。 参照してください**RSAT バージョンを使用するときに**以下のインストール手順についてはします。

RSAT には、IT 管理者が Windows 10 PC から Windows Server の役割と機能を管理することができます。

リモート サーバー管理ツールを含むサーバー マネージャー、Microsoft 管理コンソール (mmc) スナップイン、コンソール、Windows PowerShell コマンドレットとプロバイダー、および Windows Server で実行される役割と機能を管理するためのいくつかのコマンド ライン ツール。

リモート サーバー管理ツールには、リモート サーバーで実行されている役割と機能を管理するために使用できる Windows PowerShell コマンドレットのモジュールが含まれています。 Windows PowerShell のリモート管理は、Windows Server 2016 では既定で有効になっていますが、Windows 10 では、既定で無効になっています。 リモート サーバーに対してリモート サーバー管理ツールの一部であるコマンドレットを実行する実行`Enable-PSremoting`後に Windows クライアント コンピューターで管理者特権でのユーザー権限 (つまり、管理者として実行) で開かれた Windows PowerShell セッションでリモート サーバー管理ツールをインストールします。

## <a name="BKMK_Thresh"></a>Windows 10 用のリモート サーバー管理ツール
リモート サーバー管理ツールの Windows 10 を使用すると、特定のテクノロジと制限付きの場合、Windows Server 2012、または Windows Server 2008 R2 で Windows Server 2016、Windows Server 2012 R2 を実行しているコンピューターを管理できます。

リモート サーバー管理ツールの Windows 10 には、Server Core インストール オプションまたは最小サーバー インターフェイス構成の Windows Server 2016、Windows Server 2012 R2、および場合によって、Windows Server 2012 の Server Core インストール オプションを実行しているコンピューターのリモート管理のサポートが含まれています。 ただし、リモート サーバー管理ツールの Windows 10 は、任意のバージョンの Windows Server オペレーティング システムにインストールできません。

### <a name="tools-available-in-this-release"></a>このリリースで使用できるツール
リモート サーバー管理ツールの Windows 10 で使用できるツールの一覧は、内のテーブルを参照してください。 [Windows オペレーティング システムのリモート サーバー管理ツール (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)します。

### <a name="system-requirements"></a>システム要件
リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールできます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

リモート サーバー管理ツールの Windows 10 は、Windows 10 の x86 ベースおよび x64 ベースの両方のエディションで実行されます。

> [!IMPORTANT]
> リモート サーバー管理ツールの Windows 10 は、Windows 8.1、Windows 8、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 または Windows 2000 Server の管理ツール パックを実行しているコンピューターにインストールされていない必要があります。 管理ツール パックまたはリモート サーバー管理をインストールする前に、以前のプレリリース バージョンと、コンピューターから別の言語またはロケール用ツールのリリースを含む、リモート サーバー管理ツールの古いバージョンをすべて削除します。Windows 10 用ツール。

サーバー マネージャーのこのリリースにアクセスして、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているリモート サーバーの管理を使用するには、Se を使用して、以前の Windows Server オペレーティング システムを管理できるようにするいくつかの更新プログラムをインストールする必要があります。した rver マネージャー。 管理用リモート サーバー管理ツールの Windows 10 でサーバー マネージャーを使用して Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 を準備する方法の詳細については、次を参照してください[Manage Multiple, Remote Servers。サーバー マネージャーで](https://technet.microsoft.com/library/hh831456.aspx)します。

Windows PowerShell およびサーバー マネージャーのリモート管理は、リモート サーバー管理ツールの Windows 10 に含まれているツールを使用してそれらを管理するリモート サーバーで有効にする必要があります。 リモート管理は、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行しているサーバーでは、既定で有効です。 リモート管理が無効になっている場合に有効にする方法の詳細については、「 [サーバー マネージャーを使用して複数のリモート サーバーを管理する](https://go.microsoft.com/fwlink/p/?LinkId=241358)」を参照してください。

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>インストール、アンインストール、および RSAT ツールのオン/オフを有効にします。

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>Windows 10 年 2018年 10 月特定の RSAT ツールをインストールするオンデマンド (FoD) 機能を使用して更新、またはそれ以降

以降では Windows 10 年 2018年 10 月 Update、RSAT のセットとして含まれる**オンデマンド機能**から Windows 10。 次に、RSAT のパッケージをダウンロードする代わりに単に移動できます**省略可能な機能を管理する**で**設定** をクリック**機能を追加**使用可能な RSAT ツールの一覧を表示します。 選択し、必要な特定の RSAT ツールをインストールします。 インストールの進行状況を表示するには、をクリックして、**戻る**のステータスを表示するボタン、**省略可能な機能を管理する**ページ。

参照してください、 [RSAT 一連のツールを介して使用できる**オンデマンド機能**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)します。 グラフィックを使用してインストールするだけでなく**設定**アプリ、コマンドラインまたはオートメーションを使用してを使用して特定の RSAT ツールをインストールすることもできます。 [ **DISM/Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)します。

オンデマンド機能の利点の 1 つは、インストールされている機能は、Windows 10 バージョンのアップグレードによって維持です。

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>特定 RSAT をアンインストールする windows 10 年 2018年 10 月の更新ツール以降 (FoD とインストール) した後

Windows 10 で開く、**設定**アプリに移動して**省略可能な機能を管理する**を選択して削除する特定の RSAT ツールをアンインストールします。 場合によってが必要依存関係を手動でアンインストールするに注意してください。 具体的には、RSAT ツール A が B の RSAT ツールで必要な場合 RSAT ツール A のアンインストールを選択しは失敗 RSAT ツール B がまだインストールされている場合。 この場合、最初に、RSAT ツール B をアンインストールし、RSAT ツール A. をアンインストール場合によっては、RSAT ツールをアンインストールすることがありますが表示されることが、ツールがまだインストールされている場合でも成功するにも注意してください。 この場合、PC を再起動するには、ツールの削除が完了します。

参照してください、[依存関係を含む RSAT ツールの一覧](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)します。 アンインストールすると、グラフィカル設定アプリを使用して、だけでなく、コマンドラインまたはオートメーションを使用してを使用して特定の RSAT ツールをアンインストールすることができますも[ **DISM/Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)します。

### <a name="when-to-use-which-rsat-version"></a>RSAT バージョンを使用する場合

使用できません (1809) を更新年 10 月 2018 日より前の Windows 10 のバージョンがあれば、**オンデマンド機能**します。 ダウンロードして、RSAT パッケージをインストールする必要があります。

- **上記で説明したように、Windows 10 から直接 RSAT FODs をインストールする**:Windows 上のインストール時に 10 年 2018年 10 月の更新 (1809) またはそれ以降、Windows Server 2019 または以前のバージョンを管理するためです。

- **ダウンロードして、以下に示すとおり、WS_1803 RSAT のパッケージをインストール**:Windows 上のインストール時に 10 April 2018 Update (1803) Windows Server、バージョン 1803 または Windows Server バージョン 1709 を管理するため、以前のバージョン。

- **以下に示すとおり、WS2016 RSAT パッケージのインストールをダウンロードして**:Windows 上のインストール時に 10 April 2018 Update (1803) Windows Server 2016 または以前のバージョンを管理するため、以前のバージョン。

#### <a name="BKMK_installthresh"></a>リモート サーバー管理ツールの Windows 10 をインストールする RSAT パッケージをダウンロードします。

1.  リモート サーバー管理ツールの Windows 10 のパッケージをダウンロード、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=404281)します。 ダウンロード センターの Web サイトからインストーラーを実行するか、ダウンロード パッケージをローカル コンピューターまたは共有に保存します。

    > [!IMPORTANT]
    > リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールすることができます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

2.  ダウンロード パッケージをローカル コンピューターまたは共有に保存した場合は、ツールをインストールするコンピューターのアーキテクチャに応じて、インストーラー プログラム **WindowsTH-KB2693643-x64.msu** または **WindowsTH-KB2693643-x86.msu**をダブルクリックします。

3.  **[Windows Update スタンドアロン インストーラー]** ダイアログ ボックスで、更新をインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

4.  ライセンス条項を読んで内容に同意します。 **[同意する]** をクリックします。

5.  インストールの完了には数分かかります。

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>(RSAT パッケージのインストール) した後、Windows 10 のリモート サーバー管理ツールをアンインストールするには

1.  デスクトップで、 **[スタート]**、 **[すべてのアプリ]**、 **[Windows システム]**、 **[コントロール パネル]** の順にクリックします。

2.  **[プログラム]** の **[プログラムのアンインストール]** をクリックします。

3.  **[インストールされた更新プログラムを表示]** をクリックします。

4.  **[Microsoft Windows (KB2693643) の更新プログラム]** を右クリックし、 **[アンインストール]** をクリックします。

5.  更新プログラムをアンインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。
S
##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>特定のツールをオフに (後、RSAT のパッケージをインストール)

1.  デスクトップで、 **[スタート]**、 **[すべてのアプリ]**、 **[Windows システム]**、 **[コントロール パネル]** の順にクリックします。

2.  **[プログラム]** をクリックし、 **[プログラムと機能]** の **[Windows の機能の有効化または無効化]** をクリックします。

3.  **[Windows の機能]** ダイアログ ボックスで、**[リモート サーバー管理ツール]** を展開し、**[役割管理ツール]** または **[機能管理ツール]** を展開します。

4.  無効にするツールのチェック ボックスをオフにします。

    > [!NOTE]
    > サーバー マネージャーをオフにすると、コンピューターを再起動する必要があります、そのからアクセスできたツールを **ツール** からサーバー マネージャーのメニューを開く必要がある、 **管理ツール** フォルダーです。

5.  使用しないツールの無効化が完了したら、**[OK]** をクリックします。

### <a name="run-remote-server-administration-tools"></a>リモート サーバー管理ツールの実行

> [!NOTE]
> リモート サーバー管理ツールの Windows 10 をインストールした後、 **管理ツール** フォルダーに表示、 **開始** メニュー。 ツールには、次の場所からアクセスできます。
>
> -   **ツール** ] メニューの [サーバー マネージャー コンソールでします。
> -   **[コントロール パネル]\[システムとセキュリティ]\[管理ツール]**。
> -   **[管理ツール]** フォルダーからデスクトップに保存したショートカット (これを使用するには、 **[コントロール パネル]\[システムとセキュリティ]\[管理ツール]** リンクを右クリックし、 **[ショートカットの作成]** をクリックします)。

ローカル クライアント コンピューターを管理するリモート サーバー管理ツールの Windows 10 の一部としてインストールされているツールを使用できません。 実行するツールに関係なく、リモート サーバーの場合、またはツールを実行する複数のリモート サーバーを指定する必要があります。 ツールを使用して、サーバーを管理する前にサーバー マネージャー サーバー プールを管理するリモート サーバーを追加するほとんどのツールには、サーバー マネージャーでは統合されているので、 **ツール** メニュー。 サーバーをサーバー プールに追加する方法およびサーバーのカスタム グループを作成する方法の詳細については、「 [サーバー マネージャーへのサーバーの追加](https://go.microsoft.com/fwlink/p/?LinkId=241353) 」および「 [サーバー グループの作成と管理](https://go.microsoft.com/fwlink/?LinkId=247328)」を参照してください。

ボックスがからアクセス mmc スナップインやダイアログなどの windows 10 のすべての GUI ベースのサーバー管理ツールのリモート サーバー管理ツールで、**ツール**サーバー マネージャー コンソールのメニュー。 リモート サーバー管理ツールの Windows 10 を実行しているコンピューターでは、クライアント ベースのオペレーティング システムを実行ツールをインストールした後、既定では、クライアント コンピューターでリモート サーバー管理ツールの Windows 10 に含まれている、サーバー マネージャーが自動的に開きます。 いるのでない **ローカル サーバー** クライアント コンピューターで実行されるサーバー マネージャー コンソール ページでします。

##### <a name="to-start-server-manager-on-a-client-computer"></a>クライアント コンピューターでサーバー マネージャーを起動するには

1.  **[スタート]** メニューで **[すべてのアプリ]**、**[管理ツール]** の順にクリックします。

2.  **[管理ツール]** フォルダーで、 **[サーバー マネージャー]** をクリックします。

サーバー マネージャー コンソールでは表示されませんが**ツール**メニューの Windows PowerShell コマンドレットおよびコマンド プロンプト管理ツールもインストール役割と機能のリモート サーバー管理ツールの一部として。 たとえば、管理者特権 (管理者として実行) で Windows PowerShell セッションを開き、コマンドレットを実行すると`Get-Command -Module RDManagement`、結果には、後に、ローカル コンピューター上で実行するには今すぐ利用できるリモート デスクトップ サービス コマンドレットの一覧が含まれます。コマンドレットは、リモート デスクトップ サービス ロールのすべてまたは一部を実行しているリモート サーバーを対象とする限り、リモート サーバー管理ツールをインストールします。

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>管理者特権を使用して Windows PowerShell を起動するには (管理者として実行)

1.  **[スタート]** メニューで、**[すべてのアプリ]**、**[Windows システム]**、**[Windows PowerShell]** の順にクリックします。

2.  デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックして **管理者として実行**します。

> [!NOTE]
> 役割またはグループのページでは、サーバー マネージャーで、管理対象のサーバーを右クリックし、特定のサーバーで対象となる Windows PowerShell セッションを開始することもできます。 **Windows PowerShell**します。


## <a name="known-issues"></a>既知の問題

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**問題**:エラー コード 0x800f0954 RSAT FOD インストールに失敗します。

> **影響**:Windows 10 1809 RSAT FODs (2018 の年 10 月更新) WSUS または SCCM 環境で

> **解像度**:FODs を WSUS または SCCM から更新プログラムを受信するドメインに参加している PC にインストールするには Windows Update またはローカル共有から直接ダウンロード FODs を有効にするグループ ポリシー設定を変更する必要があります。 詳細についての詳細とその設定を変更する方法については、次を参照してください。[機能需要と言語パックで使用できるようにする WSUS または SCCM を使用している方法](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)します。

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**問題**:[設定] アプリを使用して RSAT FOD インストールは状態/の進行状況を表示しません。

> **影響**:Windows 10 1809 (2018 の年 10 月更新) 上で RSAT FODs

> **解像度**:インストールの進行状況を表示するには、をクリックして、**戻る**のステータスを表示するボタン、**省略可能な機能を管理する**ページ。

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**問題**:[設定] アプリを使用して RSAT FOD アンインストールが失敗します。

> **影響**:Windows 10 1809 (2018 の年 10 月更新) 上で RSAT FODs

> **解像度**:場合によっては、アンインストールの失敗の依存関係を手動でアンインストールする必要がある原因です。 具体的には、RSAT ツール A が B の RSAT ツールで必要な場合 RSAT ツール A のアンインストールを選択しは失敗 RSAT ツール B がまだインストールされている場合。 この場合、最初に、RSAT ツール B をアンインストールし、RSAT ツール A. をアンインストール依存関係を含む RSAT FODs の一覧を参照してください。

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**問題**:RSAT FOD アンインストールが失敗するに表示されますが、ツールがまだインストールされています。

> **影響**:Windows 10 1809 (2018 の年 10 月更新) 上で RSAT FODs

> **解像度**:PC を再起動すると、ツールの削除を完了します。

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**問題**:Windows 10 にアップグレードした後に不足している RSAT

> **影響**:任意の RSAT します。自動的に再インストール (より前の RSAT FODs) MSU パッケージのインストール

> **解像度**:RSAT が原因の OS のアップグレードでは、RSAT のインストールを保存できません。MSU Windows 更新プログラム パッケージとして配信されています。 Windows 10 をアップグレードした後、RSAT をインストールしてください。 この制限は、以降では、Windows 10 1809 FODs に移行したした理由のいずれかに注意してください。 インストールされている RSAT FODs は、今後の Windows 10 バージョンのアップグレードの間で保持されます。

## <a name="see-also"></a>関連項目
>- [Windows 10 用のリモート サーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Windows Vista、Windows 7、Windows 8、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、および Windows Server 2012 R2 のリモート サーバー管理ツール (RSAT)](https://go.microsoft.com/fwlink/p/?LinkID=221055)


