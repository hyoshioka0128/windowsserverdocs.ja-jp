---
title: Windows Server で HYPER-V の役割をインストールします。
description: HYPER-V をインストールする手順については、サーバー マネージャーまたは Windows PowerShell を使用します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: KBDAzure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 80154c569701608ad190fb76eb3737578895d187
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812379"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Windows Server で HYPER-V の役割をインストールします。

>適用先:Windows Server 2016、Windows Server 2019
  
を作成して仮想マシンを実行する、HYPER-V の役割をインストール Windows Server でサーバー マネージャーを使用して、または**Install-windowsfeature**で Windows PowerShell コマンドレット。 Windows 10 を参照してください。 [インストールにインストールされた Hyper-v Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)します。

HYPER-V の詳細については、次を参照してください。、 [Hyper-v テクノロジの概要](../Hyper-V-Technology-Overview.md)します。 Windows Server 2019 を試すにはダウンロードして評価版をインストールします。 参照してください、 [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)します。

Windows Server をインストールまたは HYPER-V の役割を追加する前にことを確認します。
- コンピューターのハードウェアが互換性のあります。 詳細については、次を参照してください。 [Windows Server のシステム要件の](../../../get-started/System-Requirements.md)と[Windows server、Hyper-v のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)します。
- HYPER-V を必要とする同じプロセッサの機能に依存するサード パーティ製の仮想化アプリを使用する予定がないです。 例には、VMWare ワークステーションと VirtualBox が含まれます。 これらの他のアプリをアンインストールすることがなく、HYPER-V をインストールできます。 ただし、HYPER-V ハイパーバイザーを実行するときに仮想マシンの管理に使用しようとする場合、仮想マシンが開始されないまたは含んで実行可能性があります。 詳細およびこれらのアプリのいずれかを使用する必要がある場合、HYPER-V ハイパーバイザー無効にするための手順では、次を参照してください。[仮想化アプリケーションは、Hyper-v、Device Guard、Credential Guard とは動作しません](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g)します。

Hyper-v マネージャーなどの管理ツールのみをインストールする場合は、「 [、HYPER-V マネージャーと Hyper-v ホストをリモートで管理](../Manage/Remotely-manage-Hyper-V-hosts.md)します。
  
## <a name="install-hyper-v-by-using-server-manager"></a>サーバー マネージャーを使用して、HYPER-V をインストールします。  
  
1. **サーバー マネージャー**で、 **[管理]** メニューの **[役割と機能の追加]** をクリックします。  
  
2. **[開始する前に]** ページで、インストールする役割と機能のために、対象サーバーとネットワーク環境の準備が整っていることを確認してください。 **[次へ]** をクリックします。  
  
3. **インストールの種類を選択**  ページで選択 **役割ベースまたは機能ベースのインストール**  をクリックし、 **次**します。  
  
4. **対象サーバーの選択**  ページで、サーバー プールからサーバーを選択してクリックして **次**します。  
  
5. **[サーバーの役割の選択]** ページで **[Hyper-V]** を選択します。  
  
6. 作成し、仮想マシンを管理するために使用するツールを追加するには、クリックして **機能の追加**します。 [機能] ページで、クリックして **次**します。  
  
7. **仮想スイッチの作成**  ページで、 **バーチャル マシンの移行**  ページで、および **既定の保存場所**  ページで、適切なオプションを選択します。  
  
8. **[インストール オプションの確認]** ページで、 **[必要に応じて対象サーバーを自動的に再起動する]** をオンにし、 **[インストール]** をクリックします。  
  
9. インストールが完了したら、HYPER-V が正しくインストールされていることを確認します。 開いている、 **のすべてのサーバー**  ページでサーバー マネージャーと HYPER-V がインストールされているサーバーを選択します。 チェック、 **役割と機能の** タイルを選択したサーバーのページです。  
  
## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>Install-windowsfeature コマンドレットを使用して、HYPER-V をインストールします。  
  
1. Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。  
  
2. Windows PowerShell を右クリックして **管理者として実行**します。  
  
3. リモートで接続しているサーバーで HYPER-V をインストールするには、次のコマンドを実行し、置換 `<computer_name>` サーバーの名前に置き換えます。  
  
    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart  
    ```  
  
    サーバーにローカルに接続している場合は、なしのコマンドを実行 `-ComputerName <computer_name>`します。  
  
4. サーバーの再起動後に確認できます、Hyper-v の役割がインストールされているし、その他の役割と機能は何を参照してください、次のコマンドを実行してインストールします。  
  
    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>  
    ```  
  
    サーバーにローカルに接続している場合は、なしのコマンドを実行 `-ComputerName <computer_name>`します。  
  
> [!NOTE]  
> Windows Server 2016 の Server Core インストール オプションを実行しているサーバーにこの役割をインストールして、パラメーターを使用するかどうかは`-IncludeManagementTools`、のみ、HYPER-V の Windows PowerShell モジュールがインストールされています。 Server Core インストールで実行される HYPER-V ホストをリモートで管理する別のコンピューターで、HYPER-V マネージャーの GUI 管理ツールを使用することができます。 リモートで接続する方法の詳細については、次を参照してください。 [、Hyper-v マネージャーと Hyper-v ホストをリモートで管理](../Manage/Remotely-manage-Hyper-V-hosts.md)します。  
  
## <a name="see-also"></a>関連項目  
  
- [Install-windowsfeature](https://docs.microsoft.com/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)  
