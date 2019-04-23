---
title: 作成、Linux のシールドされた VM テンプレートのディスク
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e791d18e027e5e3e1c5b9c52659641ff588a96a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858673"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>作成、Linux のシールドされた VM テンプレートのディスク

> 適用先:Windows Server 2019、Windows Server (半期チャネル) 

このトピックでは、Linux のシールドされた Vm を 1 つまたは複数のテナント Vm をインスタンス化に使用できるは、テンプレート ディスクを準備する方法について説明します。

## <a name="prerequisites"></a>前提条件

準備してテストする Linux のシールドされた VM を次のリソースの使用可能な必要になります。

- Windows Server バージョン 1709 以降を実行している仮想化 capababilities を持つサーバー
- 別のコンピューター (Windows 10 または Windows Server 2016)、実行中の VM のコンソールに接続する、HYPER-V マネージャーを実行できます。
- サポートされている Linux のいずれかの ISO イメージのシールドされた VM の Os:
    - 4.4 カーネルと Ubuntu 16.04 LTS
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 Service Pack 2
- インターネット アクセスで、lsvmtools パッケージと OS の更新プログラムをダウンロードするには

> [!IMPORTANT]
> シールドされた Vm を新しいバージョンの前の Linux Os として正常にプロビジョニングを防ぐことが既知の TPM ドライバー バグを含めることができます。
> テンプレートを更新するか、修正プログラムが利用可能になるまで、新しいリリースにシールドされた Vm は推奨されません。
> 更新プログラムがパブリックに加えられたときは、サポートされている Os 上の一覧が更新されます。

## <a name="prepare-a-linux-vm"></a>Linux VM を準備します。

シールドされた Vm は、セキュリティで保護されたテンプレート ディスクから作成されます。
テンプレート ディスクには、コア OS コンポーネントを展開する前に変更されていないことを確認するには、VM と、/boot、/root パーティションのデジタル署名を含むメタデータのオペレーティング システムが含まれます。

テンプレート ディスクを作成するには、まずは将来のシールドされた Vm のベース イメージとして準備する通常の (シールド) VM を作成する必要があります。
ソフトウェアをインストールして、この VM に行う構成の変更は、このテンプレート ディスクから作成されたすべてのシールドされた Vm に適用されます。
次の手順で templatization 用 Linux VM を準備するベアの最小要件を説明します。

> [!NOTE]
> Linux のディスク暗号化は、ディスクをパーティション分割で構成されます。
> つまり、dm crypt を使用して、Linux を作成する事前暗号化された新しい VM を作成する必要がありますのシールドされた VM テンプレートのディスク。


1.  仮想化サーバーで管理者特権の PowerShell コンソールで、次のコマンドを実行して Hyper-v ホストと Host Guardian HYPER-V サポート機能がインストールされていることを確認します。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  信頼できるソースから ISO イメージをダウンロードし、仮想化サーバーまたは仮想化サーバーにアクセスできるファイル共有に格納します。

3.  Windows Server バージョン 1709 を実行している管理コンピューターでは、次のコマンドを実行して、シールドされた VM リモート サーバー管理ツールをインストールします。

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  開いている **、HYPER-V Manager**管理コンピューターに、仮想化サーバーに接続します。
    "サーバー... に接続 をクリックしてこれを行う操作ウィンドウで、または右、HYPER-V マネージャーでクリックし、"サーバーに接続..."HYPER-V サーバーの DNS 名を指定しに資格情報が必要な場合は、必要に応じて、それに接続します。

5.  HYPER-V マネージャーを使用して[外部スイッチを構成する](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines)Linux VM の更新プログラムを取得する、インターネットにアクセスできるように、仮想化サーバーにします。

6.  次に、上に Linux OS をインストールする新しい仮想マシンを作成します。
    [操作] ウィンドウで、次のようにクリックします。**新規** > **仮想マシン**を、ウィザードを起動します。
    "Pre-templatized Linux"など、VM のフレンドリ名を入力し、クリックして**次**します。

7.  ウィザードの 2 番目のページで選択**第 2 世代**を UEFI ベースのファームウェア プロファイルを使用して、VM がプロビジョニングされたことを確認します。

8.  ユーザーの設定に応じて、ウィザードの残りの部分を完了します。
    この VM の差分ディスクを使用しないでください。シールドされた VM テンプレートのディスクが差分ディスクを使用できません。
    最後に、先ほどダウンロードした、バーチャル DVD ドライブをこの VM の OS をインストールできるように、ISO イメージを接続します。

9.  HYPER-V マネージャーで、新しく作成された VM を選択し、クリックして**接続しています.** VM の仮想のコンソールに接続する [操作] ウィンドウでします。
    ウィンドウが表示されたら、次のようにクリックします。**開始**仮想マシンをオンにします。

10. 選択した Linux ディストリビューションのセットアップ プロセスを実行します。
    各 Linux ディストリビューションでは、別のセットアップ ウィザードを使用するときに、シールドされた VM テンプレート ディスクを Linux になる Vm が次の要件を満たす必要があります。

    - GUID パーティション テーブル (GPT) のレイアウトを使用して、ディスクをパーティション分割する必要があります。
    - Dm crypt では、ルート パーティションを暗号化する必要があります。 パスフレーズを設定する必要があります**パスフレーズ**(すべて小文字)。 このパスフレーズをランダム化し、シールドされた VM がプロビジョニングされるときに、パーティションが再暗号化します。
    - ブート パーティションを使用する必要があります、 **ext2**ファイル システム

11. Linux OS が完全に起動され、サインインして、linux 仮想カーネルと関連付けられている、HYPER-V 統合サービス パッケージをインストールすることをお勧めします。
    さらに、SSH サーバーまたはシールドされていると、VM にアクセスするには、他のリモート管理ツールをインストールするされます。

    Ubuntu では、これらのコンポーネントをインストールするには、次のコマンドを実行します。

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    RHEL の代わりに、次のコマンドを実行します。

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    および sles では、次のコマンドを実行します。

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. 必要に応じて、Linux OS を構成します。
    任意のソフトウェアをインストールするユーザー アカウントを追加して、行ったシステム全体の構成の変更は、このテンプレート ディスクから作成されたすべての将来の Vm に適用されます。
    ディスクに、シークレットや不要なパッケージの保存を避ける必要があります。

13. System Center Virtual Machine Manager を使用して Vm をデプロイしようとしている場合は、VMM VM のプロビジョニング中に、OS が特殊化を有効にする VMM ゲスト エージェントをインストールします。
    特殊化では、別のユーザーと SSH キー、ネットワークの構成、およびカスタム セットアップの手順で安全に設定するには、各 VM をによりします。
    について説明する方法[を入手して、VMM ゲスト エージェントをインストール](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent)VMM ドキュメント。

14. 次に、[パッケージ マネージャーに Microsoft の Linux ソフトウェア リポジトリを追加](../../administration/linux-package-repository-for-microsoft-software.md)します。

15. VM ブートローダー shim は、コンポーネント、およびディスク準備ツールのプロビジョニングをシールドされた Linux を含む、lsvmtools パッケージをインストール、パッケージ マネージャーを使用します。

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. 完了したら、Linux OS をカスタマイズするには、システムに lsvmprep インストール プログラムを参照し、実行します。
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. VM をシャット ダウンします。

16. (Windows 10 Fall Creators Update では、HYPER-V によって作成された自動チェックポイントを含む)、VM のチェックポイントを取得した場合は、続行する前にそれらを削除することを確認します。
    チェックポイントは、テンプレート ディスク ウィザードでサポートされていない差分ディスク (.avhdx) を作成します。
    
    チェックポイントを削除するには、開く **、HYPER-V マネージャー**VM を選択し、チェックポイントのウィンドウで最上位のチェックポイントを右クリックして **チェックポイントのサブツリーを削除**します。

    ![HYPER-V マネージャーで VM テンプレートのすべてのチェックポイントを削除します。](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>テンプレート ディスクを保護します。

Linux のシールドされた VM テンプレート ディスクとして使用する準備がほぼが前のセクションで準備した VM でください。
最後の手順では、テンプレート ディスク ウィザードは、ハッシュ、デジタル署名をルートおよびブート パーティションの現在の状態のディスクを実行します。
テンプレートの作成とデプロイの間の 2 つのパーティションに不正な変更が行われませんことを確認する、シールドされた VM がプロビジョニングされるときに、ハッシュとデジタル署名が検証されます。

### <a name="obtain-a-certificate-to-sign-the-disk"></a>ディスクの署名証明書を取得します。

ディスクの測定値にデジタル署名をするためには、テンプレート ディスク ウィザードを実行するコンピューターの証明書を取得する必要があります。
証明書は、次の要件を満たす必要があります。

証明書のプロパティ | 必要な値
---------------------|---------------
キー アルゴリズム | RSA
最小キー サイズ | 2048 ビット
署名アルゴリズム | SHA256 (推奨)
キー使用法 | デジタル署名

シールド データ ファイルを作成し、により、信頼済みのディスクでは、この証明書の詳細をテナントに表示されます。
したがって、この証明書を取得して、テナントによって相互に信頼された証明機関から重要なは。
ホスト側とテナントの両方がエンタープライズ シナリオでは、エンタープライズ証明機関からこの証明書の発行を検討する可能性があります。
この証明書を慎重に保護するため、新しいテンプレート ディスクが、本物のディスクと同じ信頼されているようにこの証明書を所有しているすべてのユーザーを作成できます。

テスト ラボ環境では、次の PowerShell コマンドで自己署名証明書を作成できます。

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>プロセス テンプレート ディスク ウィザード コマンドレットを使用したディスク

テンプレート ディスクおよび証明書を Windows Server バージョン 1709 を実行しているコンピューターにコピーし、署名プロセスを開始するには、次のコマンドを実行します。
提供する VHDX、`-Path`パラメーターが更新されたテンプレート ディスクを使用して上書きされるため、必ずコマンドを実行する前にコピーを作成します。

> [!IMPORTANT]
> Windows Server 2016 または Windows 10 で利用できるリモート サーバー管理ツールを使用して、Linux のシールドされたを準備することはできません VM テンプレートのディスク。
> のみを使用して、[保護 TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps)シールドされた VM テンプレート ディスクを Linux を準備するには、Windows Server、バージョン 1709 または Windows Server 2019 で使用できるリモート サーバー管理ツールで使用可能なコマンドレットです。

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

テンプレート ディスクは、Linux のシールドされた Vm のプロビジョニングに使用する準備ができました。
System Center Virtual Machine Manager を使用して VM をデプロイする場合、VMM ライブラリに VHDX を今すぐコピーできます。

また、VHDX からボリューム署名カタログを抽出する可能性があります。
このファイルは、ユーザーは、テンプレートを使用する VM の所有者に、署名証明書、ディスクの名前とバージョンに関する情報を提供に使用されます。
これを作成する、署名証明書を所有しているテンプレートの作成者であることを承認するシールド データ ファイル ウィザードにこのファイルをインポートする必要がありますが、将来テンプレートは、それらのディスクします。

ボリューム署名カタログを抽出するには、PowerShell で、次のコマンドを実行します。

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
