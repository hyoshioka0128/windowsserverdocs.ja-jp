---
title: Windows Server で HYPER-V の役割をインストールします。
description: サーバーマネージャーまたは Windows PowerShell を使用して Hyper-v をインストールする手順について説明します。
manager: dongill
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: kbdazure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 32632e7af3db0c3b390606bc784b929e76b2892f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997594"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Windows Server で HYPER-V の役割をインストールします。

>適用先:Windows Server 2019、Windows Server 2016

仮想マシンを作成して実行するには、windows PowerShell でサーバーマネージャーまたは**Install add-windowsfeature**コマンドレットを使用して、windows Server に hyper-v の役割をインストールします。
Windows 10 を参照してください。 [インストールにインストールされた Hyper-v Windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)します。

Hyper-v の詳細については、「 [Hyper-v テクノロジの概要](../Hyper-V-Technology-Overview.md)」を参照してください。 Windows Server 2019 を試用するには、評価版のダウンロードとインストールを行うことができます。 [評価センター](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)を参照してください。

Windows Server をインストールする前、または Hyper-v の役割を追加する前に、次のことを確認してください。
- コンピューターのハードウェアに互換性があります。 詳細については、「windows [server のシステム要件](../../../get-started/System-Requirements.md)」および「 [Windows server の hyper-v のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。
- Hyper-v が必要とするのと同じプロセッサ機能に依存するサードパーティの仮想化アプリを使用する予定はありません。 例としては、VMWare Workstation や VirtualBox などがあります。 これらの他のアプリをアンインストールせずに、Hyper-v をインストールすることができます。 ただし、Hyper-v ハイパーバイザーの実行中に仮想マシンを管理するために使用しようとすると、仮想マシンが起動しないか、確実に動作しない可能性があります。 これらのアプリのいずれかを使用する必要がある場合は、Hyper-v ハイパーバイザーを無効にするための詳細および手順については、「[仮想化アプリケーションが hyper-v、Device guard、および Credential guard と連携](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g)して動作しない」を参照してください。

Hyper-v マネージャーなどの管理ツールのみをインストールする場合は、「hyper-v[マネージャーを使用して hyper-v ホストをリモートで管理](../Manage/Remotely-manage-Hyper-V-hosts.md)する」を参照してください。

## <a name="install-hyper-v-by-using-server-manager"></a>サーバーマネージャーを使用した Hyper-v のインストール

1. **サーバー マネージャー**で、**[管理]** メニューの **[役割と機能の追加]** をクリックします。

2. **[開始する前に]** ページで、インストールする役割と機能のために、対象サーバーとネットワーク環境の準備が整っていることを確認してください。 **[次へ]** をクリックします。

3. **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** を選択し、**[次へ]** をクリックします。

4. **[対象サーバーの選択]** ページで、サーバー プールからサーバーを選択し、**[次へ]** をクリックします。

5. **[サーバーの役割の選択]** ページで **[Hyper-V]** を選択します。

6. 仮想マシンの作成と管理に使うツールを追加するには、**[機能の追加]** をクリックします。 [機能] ページで、**[次へ]** をクリックします。

7. **[仮想スイッチの作成]** ページ、**[仮想マシンの移行]** ページ、および **[既定の保存場所]** ページで、適切なオプションを選択します。

8. **[インストール オプションの確認]** ページで、**[必要に応じて対象サーバーを自動的に再起動する]** をオンにし、**[インストール]** をクリックします。

9. インストールが完了したら、HYPER-V が正しくインストールされていることを確認します。 開いている、 **のすべてのサーバー** ] ページでサーバー マネージャーと HYPER-V がインストールされているサーバーを選択します。 チェック、 **役割と機能の** タイルを選択したサーバーのページです。

## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>Install-Add-windowsfeature コマンドレットを使用して Hyper-v をインストールする

1. Windows デスクトップで [スタート] ボタンをクリックし、名前の一部を入力 **Windows PowerShell**します。

2. [Windows PowerShell] を右クリックし、[**管理者として実行**] を選択します。

3. リモートで接続しているサーバーで HYPER-V をインストールするには、次のコマンドを実行し、置換 `<computer_name>` サーバーの名前に置き換えます。

    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
    ```

    サーバーにローカルに接続している場合は、なしのコマンドを実行 `-ComputerName <computer_name>`します。

4. サーバーが再起動した後、Hyper-v の役割がインストールされていることを確認し、次のコマンドを実行して他の役割と機能がインストールされていることを確認できます。

    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>
    ```

    サーバーにローカルに接続している場合は、なしのコマンドを実行 `-ComputerName <computer_name>`します。

> [!NOTE]
> Windows Server 2016 の Server Core インストールオプションを実行しているサーバーにこの役割をインストールし、パラメーターを使用する場合は、 `-IncludeManagementTools` Windows PowerShell 用の Hyper-v モジュールのみがインストールされます。 Server Core インストールで実行される HYPER-V ホストをリモートで管理する別のコンピューターで、HYPER-V マネージャーの GUI 管理ツールを使用することができます。 リモート接続の手順については、「 [Hyper-v マネージャーを使用して hyper-v ホストをリモートで管理](../Manage/Remotely-manage-Hyper-V-hosts.md)する」を参照してください。

## <a name="additional-references"></a>その他の参照情報

- [Install-windowsfeature](/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)