---
title: リモート サーバー管理ツール
description: リモートサーバー管理ツールのトップレベルトピック
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-rsat
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: e8e8206531e0939a1b6d6dfd17f5c5dd59947c81
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259137"
---
# <a name="remote-server-administration-tools"></a>リモート サーバー管理ツール

>適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows 10 のリモートサーバー管理ツールをサポートします。

> [!IMPORTANT]
> Windows 10 10 月 2018 Update 以降では、RSAT は Windows 10 での**オンデマンド機能**のセットとして含まれています。 インストール手順については、次の**RSAT バージョンを使用するタイミング**に関する説明を参照してください。

RSAT を使用すると、IT 管理者は windows 10 PC から Windows Server の役割と機能を管理できます。

リモートサーバー管理ツールには、サーバーマネージャー、Microsoft 管理コンソール (mmc) スナップイン、コンソール、Windows PowerShell のコマンドレットとプロバイダー、および Windows Server で実行される役割と機能を管理するためのコマンドラインツールが含まれています。

リモートサーバー管理ツールには、リモートサーバーで実行されている役割と機能を管理するために使用できる Windows PowerShell コマンドレットモジュールが含まれています。 Windows PowerShell のリモート管理は、Windows Server 2016 では既定で有効になっていますが、Windows 10 では、既定で無効になっています。 リモートサーバーに対してリモートサーバー管理ツールの一部であるコマンドレットを実行するには、リモートサーバー管理ツールのインストール後に Windows クライアントコンピューターで管理者特権で開かれた (つまり、管理者として実行される) Windows PowerShell セッションで `Enable-PSremoting` を実行します。

## <a name="BKMK_Thresh"></a>Windows 10 のリモートサーバー管理ツール
Windows 10 用のリモートサーバー管理ツールを使用して、windows Server 2019、Windows Server 2016、Windows Server 2012 R2 を実行しているコンピューターで特定のテクノロジを管理し、制限付きの場合は windows Server 2012 または Windows Server 2008 R2 を使用します。

リモート サーバー管理ツールの Windows 10 には、Server Core インストール オプションまたは最小サーバー インターフェイス構成の Windows Server 2016、Windows Server 2012 R2、および場合によって、Windows Server 2012 の Server Core インストール オプションを実行しているコンピューターのリモート管理のサポートが含まれています。 ただし、リモート サーバー管理ツールの Windows 10 は、任意のバージョンの Windows Server オペレーティング システムにインストールできません。

### <a name="tools-available-in-this-release"></a>このリリースで使用できるツール
Windows 10 のリモートサーバー管理ツールで使用できるツールの一覧については、「 [windows オペレーティングシステム用のリモートサーバー管理ツール (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)」の表を参照してください。

### <a name="system-requirements"></a>システム要件
リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールできます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

Windows 10 のリモートサーバー管理ツールは、Windows 10 の x86 ベースと x64 ベースの両方のエディションで実行されます。

> [!IMPORTANT]
> Windows 10 のリモートサーバー管理ツールは、Windows 8.1、Windows 8、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003、または Windows 2000 Server 用の管理ツールパックを実行しているコンピューターにはインストールしないでください。 リモートサーバー管理をインストールする前に、以前のプレリリースバージョンを含む管理ツールパックまたはリモートサーバー管理ツールの古いバージョンをすべて削除し、コンピューターから別の言語またはロケール用のツールをリリースします。Windows 10 用のツール。

このリリースのサーバーマネージャーを使用して、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているリモートサーバーにアクセスして管理するには、いくつかの更新プログラムをインストールして、以前の Windows Server オペレーティングシステムを管理者が管理できるようにする必要があります。r Manager。 Windows 10 リモートサーバー管理ツールのサーバーマネージャーを使用した管理のために Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2 を準備する方法の詳細については、「サーバーマネージャーを使用して[複数のリモートサーバーを管理](https://technet.microsoft.com/library/hh831456.aspx)する」を参照してください。

Windows PowerShell およびサーバー マネージャーのリモート管理は、リモート サーバー管理ツールの Windows 10 に含まれているツールを使用してそれらを管理するリモート サーバーで有効にする必要があります。 Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 を実行しているサーバーでは、リモート管理が既定で有効になっています。 リモート管理が無効になっている場合に有効にする方法の詳細については、「 [サーバー マネージャーを使用して複数のリモート サーバーを管理する](https://go.microsoft.com/fwlink/p/?LinkId=241358)」を参照してください。

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>RSAT ツールをインストール、アンインストール、およびオンにする

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>必要に応じて機能を使用して、2018年10月の更新プログラム、またはそれ以降に特定の RSAT ツールをインストールします。

Windows 10 10 月 2018 Update 以降では、RSAT は Windows 10 から**オンデマンドで**一連の機能として含まれています。 RSAT パッケージをダウンロードするのではなく、 **[設定]** の **[オプション機能の管理]** にアクセスして、 **[機能の追加]** をクリックすると、使用可能な RSAT ツールの一覧が表示されます。 必要な特定の RSAT ツールを選択してインストールします。 インストールの進行状況を表示するには、 **[戻る]** ボタンをクリックして、 **[オプション機能の管理]** ページの状態を表示します。

[**オンデマンド機能**を使用して利用できる RSAT ツールの一覧](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)を参照してください。 グラフィカル**設定**アプリを使用してをインストールするだけでなく、 [**DISM/Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)を使用してコマンドラインまたはオートメーションを使用して、特定の RSAT ツールをインストールすることもできます。

オンデマンド機能の利点の1つは、インストールされている機能が Windows 10 のバージョンのアップグレードにわたって保持されることです。

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>Windows 10 10 月2018更新以降で特定の RSAT ツールをアンインストールするには (with を使用してインストールした後)

Windows 10 では、**設定**アプリを開き、 **[オプション機能の管理]** にアクセスして、削除する RSAT ツールを選択してアンインストールします。 場合によっては、依存関係を手動でアンインストールする必要があることに注意してください。 具体的には、rsat ツール a が rsat ツール B で必要な場合、rsat ツール B がまだインストールされていると、RSAT ツール A のアンインストールを選択しても失敗します。 この場合、最初に RSAT ツール B をアンインストールしてから、RSAT ツール A をアンインストールします。また、ツールがまだインストールされている場合でも、RSAT ツールのアンインストールが正常に行われることがあります。 この場合、PC を再起動すると、ツールの削除が完了します。

「[依存関係」を含む RSAT ツールの一覧](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)を参照してください。 グラフィカル設定アプリを使用してをアンインストールするだけでなく、 [**DISM/Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)を使用してコマンドラインまたはオートメーションを使用して特定の RSAT ツールをアンインストールすることもできます。

### <a name="when-to-use-which-rsat-version"></a>RSAT のバージョンを使用する場合

2018年10月の更新プログラム (1809) より前のバージョンの Windows 10 を使用している場合は、**オンデマンド機能**を使用することはできません。 RSAT パッケージをダウンロードしてインストールする必要があります。

- Windows 10 10 月2018更新プログラム (1809) 以降で windows Server 2019 またはそれ以前のバージョンを管理する場合は、**前に説明したように、windows 10 から RSAT を直接インストール**します。

- 次に示すように、 **WS_1803 RSAT パッケージをダウンロードしてインストールし**ます。 Windows 10 年4月2018更新プログラム (1803) をインストールする場合は、windows server、バージョン1803、または windows server のバージョン1709を管理する場合は、「」を参照してください。

- **次に示すように、WS2016 RSAT パッケージをダウンロードしてインストールし**ます。 Windows 10 年4月2018更新プログラム (1803) 以前にインストールした場合は、windows Server 2016 または以前のバージョンを管理します。

#### <a name="BKMK_installthresh"></a>RSAT パッケージをダウンロードして、Windows 10 用のリモートサーバー管理ツールをインストールする

1.  リモート サーバー管理ツールの Windows 10 のパッケージをダウンロード、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=404281)します。 ダウンロード センターの Web サイトからインストーラーを実行するか、ダウンロード パッケージをローカル コンピューターまたは共有に保存します。

    > [!IMPORTANT]
    > リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールすることができます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

2.  ダウンロード パッケージをローカル コンピューターまたは共有に保存した場合は、ツールをインストールするコンピューターのアーキテクチャに応じて、インストーラー プログラム **WindowsTH-KB2693643-x64.msu** または **WindowsTH-KB2693643-x86.msu**をダブルクリックします。

3.  **[Windows Update スタンドアロン インストーラー]** ダイアログ ボックスで、更新をインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

4.  ライセンス条項を読んで内容に同意します。 **[同意する]** をクリックします。

5.  インストールの完了には数分かかります。

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>Windows 10 のリモートサーバー管理ツールをアンインストールするには (RSAT パッケージのインストール後)

1. デスクトップで、 **[スタート]** 、 **[すべてのアプリ]** 、 **[Windows システム]** 、 **[コントロール パネル]** の順にクリックします。

2. **[プログラム]** の **[プログラムのアンインストール]** をクリックします。

3. **[インストールされた更新プログラムを表示]** をクリックします。

4. **[Microsoft Windows (KB2693643) の更新プログラム]** を右クリックし、 **[アンインストール]** をクリックします。

5. 更新プログラムをアンインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。
   S
   ##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>特定のツールを無効にするには (RSAT パッケージのインストール後)

6. デスクトップで、 **[スタート]** 、 **[すべてのアプリ]** 、 **[Windows システム]** 、 **[コントロール パネル]** の順にクリックします。

7. **[プログラム]** をクリックし、 **[プログラムと機能]** の **[Windows の機能の有効化または無効化]** をクリックします。

8. **[Windows の機能]** ダイアログ ボックスで、 **[リモート サーバー管理ツール]** を展開し、 **[役割管理ツール]** または **[機能管理ツール]** を展開します。

9. 無効にするツールのチェック ボックスをオフにします。

   > [!NOTE]
   > サーバー マネージャーをオフにすると、コンピューターを再起動する必要があります、そのからアクセスできたツールを **ツール** からサーバー マネージャーのメニューを開く必要がある、 **管理ツール** フォルダーです。

10. 使用しないツールの無効化が完了したら、 **[OK]** をクリックします。

### <a name="run-remote-server-administration-tools"></a>リモート サーバー管理ツールの実行

> [!NOTE]
> リモート サーバー管理ツールの Windows 10 をインストールした後、 **管理ツール** フォルダーに表示、 **開始** メニュー。 ツールには、次の場所からアクセスできます。
>
> -   **ツール** ] メニューの [サーバー マネージャー コンソールでします。
> -   **[コントロール パネル]\[システムとセキュリティ]\[管理ツール]** 。
> -   **[管理ツール]** フォルダーからデスクトップに保存したショートカット (これを使用するには、 **[コントロール パネル]\[システムとセキュリティ]\[管理ツール]** リンクを右クリックし、 **[ショートカットの作成]** をクリックします)。

Windows 10 のリモートサーバー管理ツールの一部としてインストールされたツールを使用して、ローカルクライアントコンピュータを管理することはできません。 実行するツールに関係なく、ツールを実行するリモートサーバーまたは複数のリモートサーバーを指定する必要があります。 ツールを使用して、サーバーを管理する前にサーバー マネージャー サーバー プールを管理するリモート サーバーを追加するほとんどのツールには、サーバー マネージャーでは統合されているので、 **ツール** メニュー。 サーバーをサーバー プールに追加する方法およびサーバーのカスタム グループを作成する方法の詳細については、「 [サーバー マネージャーへのサーバーの追加](https://go.microsoft.com/fwlink/p/?LinkId=241353) 」および「 [サーバー グループの作成と管理](https://go.microsoft.com/fwlink/?LinkId=247328)」を参照してください。

Windows 10 のリモートサーバー管理ツールでは、mmc スナップインやダイアログボックスなど、すべての GUI ベースのサーバー管理ツールに、サーバーマネージャーコンソールの **[ツール]** メニューからアクセスできます。 リモート サーバー管理ツールの Windows 10 を実行しているコンピューターでは、クライアント ベースのオペレーティング システムを実行ツールをインストールした後、既定では、クライアント コンピューターでリモート サーバー管理ツールの Windows 10 に含まれている、サーバー マネージャーが自動的に開きます。 いるのでない **ローカル サーバー** クライアント コンピューターで実行されるサーバー マネージャー コンソール ページでします。

##### <a name="to-start-server-manager-on-a-client-computer"></a>クライアント コンピューターでサーバー マネージャーを起動するには

1.  **[スタート]** メニューで **[すべてのアプリ]** 、 **[管理ツール]** の順にクリックします。

2.  **[管理ツール]** フォルダーで、 **[サーバー マネージャー]** をクリックします。

サーバーマネージャーコンソールの **[ツール]** メニューには表示されませんが、Windows PowerShell コマンドレットおよびコマンドプロンプト管理ツールもリモートサーバー管理ツールの一部として役割と機能にインストールされます。 たとえば、管理者特権 ([管理者として実行]) を使用して Windows PowerShell セッションを開き、`Get-Command -Module RDManagement`コマンドレットを実行すると、リモートデスクトップサービスの役割のすべてまたは一部を実行しているリモートサーバーでコマンドレットが対象になっている限り、リモートサーバー管理ツールをインストールした後にローカルコンピューターで実行できるようになります。

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>管理者特権を使用して Windows PowerShell を起動するには (管理者として実行)

1.  **[スタート]** メニューで、 **[すべてのアプリ]** 、 **[Windows システム]** 、 **[Windows PowerShell]** の順にクリックします。

2.  デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックして **管理者として実行**します。

> [!NOTE]
> 役割またはグループのページでは、サーバー マネージャーで、管理対象のサーバーを右クリックし、特定のサーバーで対象となる Windows PowerShell セッションを開始することもできます。 **Windows PowerShell**します。


## <a name="known-issues"></a>既知の問題

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**問題**: RSAT のインストールがエラーコード0x800f0954 で失敗する

> **影響**: WSUS/SCCM 環境で Windows 10 1809 (10 2018 月の更新プログラム) に RSAT を実行する
> 
> **解決方法**: WSUS または SCCM から更新プログラムを受信するドメインに参加している PC にインストールするには、グループポリシー設定を変更して、Windows Update またはローカル共有から直接 ds をダウンロードできるようにする必要があります。 この設定を変更する方法の詳細と手順については、「 [WSUS/SCCM を使用しているときに機能をオンデマンドおよび言語パックで使用できるようにする方法](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)」を参照してください。

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**問題**: 設定アプリを使用して RSAT をインストールすると、状態または進行状況が表示されない

> **影響**: Windows 10 1809 (2018 年10月の更新プログラム)
> 
> **解決方法**: インストールの進行状況を確認するには、 **[戻る]** ボタンをクリックして、 **[オプション機能の管理]** ページの状態を表示します。

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**問題**: 設定アプリを使用した RSAT のアンインストールが失敗することがある

> **影響**: Windows 10 1809 (2018 年10月の更新プログラム)
> 
> **解決方法**: アンインストールエラーは、依存関係を手動でアンインストールする必要がある場合があります。 具体的には、rsat ツール a が rsat ツール B で必要な場合、rsat ツール B がまだインストールされていると、RSAT ツール A のアンインストールを選択しても失敗します。 この場合、最初に RSAT ツール B をアンインストールしてから、RSAT ツール A をアンインストールします。依存関係を含む RSAT の一覧を参照してください。

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**問題**: RSAT のアンインストールは成功したように見えますが、ツールがまだインストールされています

> **影響**: Windows 10 1809 (2018 年10月の更新プログラム)
> 
> **解決方法**: PC を再起動すると、ツールの削除が完了します。

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**問題**: Windows 10 のアップグレード後に RSAT が見つからない

> **影響**: RSAT。MSU パッケージのインストール (RSAT に先立って) が自動的に再インストールされない
> 
> **解決方法**: rsat が原因で、rsat のインストールを OS のアップグレード間で永続化することはできません。Windows Update パッケージとして配信される MSU。 Windows 10 のアップグレード後に RSAT をもう一度インストールしてください。 この制限は、Windows 10 1809 以降で Ds に移行した理由の1つです。 インストールされている RSAT Ds は、今後の Windows 10 バージョンのアップグレードでも保持されます。

## <a name="see-also"></a>関連項目
>- [Windows 10 のリモートサーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Windows Vista、Windows 7、Windows 8、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、および Windows Server 2012 R2 用のリモートサーバー管理ツール (RSAT)](https://go.microsoft.com/fwlink/p/?LinkID=221055)
