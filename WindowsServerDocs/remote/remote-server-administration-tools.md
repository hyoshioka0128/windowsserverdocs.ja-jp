---
title: リモート サーバー管理ツール
description: リモート サーバー管理ツールに関するトップ レベル トピック
ms.prod: windows-server
ms.technology: manage-rsat
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 510ad2cb1449f161658684eeceec4dbbb7ce6699
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857095"
---
# <a name="remote-server-administration-tools"></a>リモート サーバー管理ツール

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows 10 用のリモート サーバー管理ツールについて説明します。

> [!IMPORTANT]
> Windows 10 October 2018 Update 以降では、RSAT は Windows 10 自体の**オンデマンド機能**のセットとして含まれています。 インストールの方法については、後の「**どのようなときに RSAT のどのバージョンを使用するか**」をご覧ください。

RSAT を使用すると、IT 管理者は Windows 10 PC から Windows Server の役割と機能を管理できます。

リモート サーバー管理ツールには、サーバー マネージャー、Microsoft 管理コンソール (MMC) のスナップイン、コンソール、Windows PowerShell のコマンドレットとプロバイダー、Windows Server で実行される役割と機能を管理するためのコマンド ライン ツールが含まれています。

リモート サーバー管理ツールには、リモート サーバーで実行されている役割と機能の管理に利用できる Windows PowerShell コマンドレット モジュールが含まれています。 Windows PowerShell のリモート管理は、Windows Server 2016 では既定で有効になっていますが、Windows 10 では、既定で無効になっています。 リモート サーバー管理ツールに含まれるコマンドレットをリモート サーバーに対して実行するには、リモート サーバー管理ツールをインストールした後、Windows クライアント コンピューターで、管理者特権で開いた (つまり、管理者として実行した) Windows PowerShell セッションで、`Enable-PSremoting` を実行します。

## <a name="remote-server-administration-tools-for-windows-10"></a><a name="BKMK_Thresh"></a>Windows 10 用のリモート サーバー管理ツール
Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、および制限付きで Windows Server 2012 または Windows Server 2008 R2 が実行されているコンピューターで特定のテクノロジを管理するには、Windows 10 用のリモート サーバー管理ツールを使用します。

リモート サーバー管理ツールの Windows 10 には、Server Core インストール オプションまたは最小サーバー インターフェイス構成の Windows Server 2016、Windows Server 2012 R2、および場合によって、Windows Server 2012 の Server Core インストール オプションを実行しているコンピューターのリモート管理のサポートが含まれています。 ただし、リモート サーバー管理ツールの Windows 10 は、任意のバージョンの Windows Server オペレーティング システムにインストールできません。

### <a name="tools-available-in-this-release"></a>このリリースで使用できるツール
Windows 10 用のリモート サーバー管理ツールで使用できるツールの一覧については、「[Windows オペレーティング システムのリモート サーバー管理ツール (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)」の表を参照してください。

### <a name="system-requirements"></a>システム要件
リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールできます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

Windows 10 用のリモート サーバー管理ツールは、Windows 10 の x86 ベースと x64 ベースの両方のエディションで実行できます。

> [!IMPORTANT]
> Windows 10 用のリモート サーバー管理ツールは、Windows 8.1、Windows 8、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003、または Windows 2000 Server 用の管理ツール パックが実行されているコンピューターにはインストールしないでください。 Windows 10 用のリモート サーバー管理ツールをインストールする前に、以前のプレリリース バージョンや異なる言語またはロケール用のリリースも含めて、管理ツール パックまたはリモート サーバー管理ツールの古いバージョンをすべてコンピューターから削除してください。

このリリースのサーバー マネージャーを使用して、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 が実行されているリモート サーバーにアクセスし、管理するには、サーバー マネージャーを使用して以前のバージョンの Windows Server オペレーティング システムを管理できるように、いくつかの更新プログラムをインストールする必要があります。 Windows 10 用のリモート サーバー管理ツールのサーバー マネージャーを使用して、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 を管理できるように準備する方法については、「[サーバー マネージャーを使用して複数のリモート サーバーを管理する](https://technet.microsoft.com/library/hh831456.aspx)」を参照してください。
        
Windows PowerShell およびサーバー マネージャーのリモート管理は、リモート サーバー管理ツールの Windows 10 に含まれているツールを使用してそれらを管理するリモート サーバーで有効にする必要があります。 Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 が実行されているサーバーでは、リモート管理が既定で有効になります。 リモート管理が無効になっている場合に有効にする方法の詳細については、「 [サーバー マネージャーを使用して複数のリモート サーバーを管理する](https://go.microsoft.com/fwlink/p/?LinkId=241358)」を参照してください。
        
## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>RSAT ツールをインストール、アンインストール、オン/オフする        

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-----r-l----ter"></a>オンデマンド機能 (FoD) を使用して Windows 10 October 2018 Update 以降に特定の RSAT ツールをインストールする

Windows 10 October 2018 Update 以降では、RSAT は Windows 10 の**オンデマンド機能**のセットとして含まれています。 RSAT パッケージをダウンロードするのではなく、 **[設定]** の **[オプション機能の管理]** に移動し、 **[機能の追加]** をクリックして、使用可能な RSAT ツールの一覧を表示します。 必要な特定の RSAT ツールを選択してインストールします。 インストールの進行状況を見るには、 **[戻る]** ボタンをクリックして、 **[オプション機能の管理]** ページで状態を表示します。
        
[**オンデマンド機能**で利用可能な RSAT ツールの一覧](https://docs.microsoft.co    /wi    dows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)を参照してください。 グラフィカルな**設定**アプリでインストールするだけでなく、[**DISM /Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods) を使用してコマンド ラインまたはオートメーションで特定の RSAT ツールをインストールすることもできます。

オンデマンド機能の利点の 1 つは、インストールした機能は Windows 10 のバージョンをアップグレードしても保持されることです。        
        
#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>Windows 10 October 2018 Update 以降で特定の RSAT ツールをアンインストールするには (FoD を使用してインストールした後)        

Windows 10 で、**設定**アプリを開き、 **[オプション機能の管理]** に移動し、削除する RSAT ツールを選択してアンインストールします。 場合によっては、依存関係を手動でアンインストールする必要があることに注意してください。 具体的には、RSAT ツール A が RSAT ツール B で必要な場合、RSAT ツール B がまだインストールされていると、RSAT ツール A のアンインストールを選択しても失敗します。 この場合は、最初に RSAT ツール B をアンインストールしてから、RSAT ツール A をアンインストールします。また、ツールがまだインストールされていても、RSAT ツールのアンインストールが正常に行われたように表示される場合があることに注意してください。 この場合は、PC を再起動すると、ツールの削除が完了します。

[依存関係を含む RSAT ツールのリスト](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat)を参照してください。 グラフィカルな設定アプリでアンインストールするだけでなく、[**DISM /Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods) を使用してコマンド ラインまたはオートメーションで特定の RSAT ツールをアンインストールすることもできます。

### <a name="when-to-use-which-rsat-version"></a>どのようなときに RSAT のどのバージョンを使用するか

October 2018 Update (1809) より前のバージョンの Windows 10 を使用している場合は、**オンデマンド機能**を使用できません。 RSAT パッケージをダウンロードしてインストールする必要があります。

- **上記の説明に従って、Windows 10 から直接 RSAT FOD をインストールする**: Windows Server 2019 またはそれ以前のバージョンを管理するために、Windows 10 October 2018 Update (1809) 以降にインストールする場合。

- **下記の説明に従って、WS_1803 RSAT パッケージをダウンロードしてインストールする**: Windows Server バージョン 1803 または Windows Server バージョン 1709 を管理するために、Windows 10 April 2018 Update (1803) 以前にインストールする場合。

- **下記の説明に従って、WS2016 RSAT パッケージをダウンロードしてインストールする**: Windows Server 2016 またはそれ以前のバージョンを管理するために、Windows 10 April 2018 Update (1803) 以前にインストールする場合。

#### <a name="download-the-rsat-package-to-install-remote-server-administration-tools-for-windows-10"></a><a name="BKMK_installthresh"></a>RSAT パッケージをダウンロードして、Windows 10 用のリモート サーバー管理ツールをインストールする

1.  リモート サーバー管理ツールの Windows 10 のパッケージをダウンロード、 [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=404281)します。 ダウンロード センターの Web サイトからインストーラーを実行するか、ダウンロード パッケージをローカル コンピューターまたは共有に保存します。

    > [!IMPORTANT]
    > リモート サーバー管理ツールの Windows 10 は、Windows 10 を実行しているコンピューターにのみインストールすることができます。 リモート サーバー管理ツールは、Windows RT 8.1、またはその他のシステムを搭載デバイスを実行しているコンピューターにインストールできません。

2.  ダウンロード パッケージをローカル コンピューターまたは共有に保存した場合は、ツールをインストールするコンピューターのアーキテクチャに応じて、インストーラー プログラム **WindowsTH-KB2693643-x64.msu** または **WindowsTH-KB2693643-x86.msu**をダブルクリックします。

3.  **[Windows Update スタンドアロン インストーラー]** ダイアログ ボックスで、更新をインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

4.  ライセンス条項を読んで内容に同意します。 **[同意する]** をクリックします。

5.  インストールの完了には数分かかります。    
        
##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-----aft----r-rsat-package-install"></a>Windows 10 用のリモート サーバー管理ツールをアンインストールするには (RSAT パッケージのインストール後)
        
1. デスクトップで、 **[スタート]** 、 **[すべてのアプリ]** 、 **[Windows システム]** 、 **[コントロール パネル]** の順にクリックします。

2. **[プログラム]** の **[プログラムのアンインストール]** をクリックします。

3. **[インストールされた更新プログラムを表示]** をクリックします。

4. **[Microsoft Windows (KB2693643) の更新プログラム]** を右クリックし、 **[アンインストール]** をクリックします。

5. 更新プログラムをアンインストールするかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。
   S
   ##### <a name="to-turn----off-specific-tools-after-rsat-package-in----tall"></a>特定のツールを無効にするには (RSAT パッケージのインストール後)
        
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

Windows 10 用のリモート サーバー管理ツールの一部としてインストールされるツールは、ローカル環境のクライアント コンピューターの管理には使用できません。 実行するツールに関係なく、ツールを実行する 1 つまたは複数のリモート サーバーを指定する必要があります。 ツールを使用して、サーバーを管理する前にサーバー マネージャー サーバー プールを管理するリモート サーバーを追加するほとんどのツールには、サーバー マネージャーでは統合されているので、 **ツール** メニュー。 サーバーをサーバー プールに追加する方法およびサーバーのカスタム グループを作成する方法の詳細については、「 [サーバー マネージャーへのサーバーの追加](https://go.microsoft.com/fwlink/p/?LinkId=241353) 」および「 [サーバー グループの作成と管理](https://go.microsoft.com/fwlink/?LinkId=247328)」を参照してください。

Windows 10 用のリモート サーバー管理ツールでは、MMC のスナップインやダイアログ ボックスなど、すべての GUI ベースのサーバー管理ツールに、サーバー マネージャー コンソールの **[ツール]** メニューからアクセスします。 リモート サーバー管理ツールの Windows 10 を実行しているコンピューターでは、クライアント ベースのオペレーティング システムを実行ツールをインストールした後、既定では、クライアント コンピューターでリモート サーバー管理ツールの Windows 10 に含まれている、サーバー マネージャーが自動的に開きます。 いるのでない **ローカル サーバー** クライアント コンピューターで実行されるサーバー マネージャー コンソール ページでします。

##### <a name="to-start-server-manager-on-a-clien-----co----puter"></a>クライアント コンピューターでサーバー マネージャーを起動するには

1.  **[スタート]** メニューで **[すべてのアプリ]** 、 **[管理ツール]** の順にクリックします。

2.  **[管理ツール]** フォルダーで、 **[サーバー マネージャー]** をクリックします。

サーバー マネージャー コンソールの **[ツール]** メニューには表示されませんが、リモート サーバー管理ツールの一部である役割および機能に対して、Windows PowerShell のコマンドレットおよびコマンド プロンプト管理ツールもインストールされます。 たとえば、管理者特権 ([管理者として実行]) を使って Windows PowerShell セッションを開き、コマンドレット `Get-Command -Module RDManagement` を実行した場合、結果には、リモート サーバー管理ツールのインストール後にローカル コンピューターで実行できるようになっている、リモート デスクトップ サービスのコマンドレットの一覧が含まれます。ただし、これらのコマンドレットの対象が、リモート デスクトップ サービスの役割の全部または一部を実行しているリモート サーバーである場合に限ります。

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>管理者特権を使用して Windows PowerShell を起動するには (管理者として実行)

1.  **[スタート]** メニューで、 **[すべてのアプリ]** 、 **[Windows システム]** 、 **[Windows PowerShell]** の順にクリックします。

2.  デスクトップから管理者として Windows PowerShell を実行を右クリックし、 **Windows PowerShell** ショートカットをクリックして **管理者として実行**します。

> [!NOTE]
> 役割またはグループのページでは、サーバー マネージャーで、管理対象のサーバーを右クリックし、特定のサーバーで対象となる Windows PowerShell セッションを開始することもできます。 **Windows PowerShell**します。
        

## <a name="known-issues"></a>既知の問題

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**問題**: RSAT FOD のインストールがエラー コード 0x800f0954 で失敗する

> **影響**: WSUS/Configuration Manager 環境の Windows 10 1809 (October 2018 Update) 上の RSAT FOD
> 
> **解決方法**: WSUS または Configuration Manager を通して更新プログラムを受け取る、ドメインに参加している PC に FOD をインストールするには、Windows Update またはローカル共有から直接 FOD をダウンロードできるように、グループ ポリシーの設定を変更する必要があります。 その設定を変更する方法の詳細と手順については、「[WSUS/SCCM を使用しているときにオンデマンド機能と言語パックを使用できるようにする方法](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)」をご覧ください。

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**問題**: 設定アプリを使用した RSAT FOD のインストールで状態と進行状況が表示されない

> **影響**: Windows 10 1809 (October 2018 Update) 上の RSAT FOD
> 
> **解決方法**: インストールの進行状況を見るには、 **[戻る]** ボタンをクリックして、 **[オプション機能の管理]** ページで状態を表示します。

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**問題**: 設定アプリを使用した RSAT FOD のアンインストールが失敗することがある

> **影響**: Windows 10 1809 (October 2018 Update) 上の RSAT FOD
> 
> **解決方法**: 場合によっては、依存関係を手動でアンインストールする必要があるために、アンインストールが失敗します。 具体的には、RSAT ツール A が RSAT ツール B で必要な場合、RSAT ツール B がまだインストールされていると、RSAT ツール A のアンインストールを選択しても失敗します。 この場合は、最初に RSAT ツール B をアンインストールしてから、RSAT ツール A をアンインストールします。依存関係を含む RSAT FOD の一覧を参照してください。

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**問題**: RSAT のアンインストールは成功したように見えるが、ツールがまだインストールされている

> **影響**: Windows 10 1809 (October 2018 Update) 上の RSAT FOD
> 
> **解決方法**: PC を再起動すると、ツールの削除が完了します。

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**問題**: Windows 10 のアップグレード後に RSAT が見つからない

> **影響**: RSAT .MSU パッケージのインストール (RSAT FOD の前) が自動的に再インストールされない
> 
> **解決方法**: RSAT .MSU が Windows Update パッケージとして提供されるため、OS をアップグレードしたときに RSAT のインストールを維持できません。 Windows 10 をアップグレード後、RSAT をもう一度インストールしてください。 この制限は、Windows 10 1809 以降に FOD に移行した理由の 1 つです。 インストールされている RSAT FOD は、今後の Windows 10 バージョンのアップグレードでも保持されます。

## <a name="see-also"></a>参照
>- [Windows 10 用のリモート サーバー管理ツール](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Windows Vista、Windows 7、Windows 8、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 用のリモート サーバー管理ツール (RSAT)](https://go.microsoft.com/fwlink/p/?LinkID=221055)                                                                                                                                                                                                                                                                                                                                                                                    