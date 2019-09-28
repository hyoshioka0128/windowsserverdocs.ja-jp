---
title: Linux のシールドされた VM テンプレートディスクを作成する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: d0e1d4fb-97fc-4389-9421-c869ba532944
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 66d5f70f747a6209f2856afde58b6f486ea597f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386708"
---
# <a name="create-a-linux-shielded-vm-template-disk"></a>Linux のシールドされた VM テンプレートディスクを作成する

> 適用先:Windows Server 2019、Windows Server (半期チャネル)、 

このトピックでは、1つまたは複数のテナント Vm のインスタンス化に使用できる Linux のシールドされた Vm のテンプレートディスクを準備する方法について説明します。

## <a name="prerequisites"></a>前提条件

Linux のシールドされた VM を準備してテストするには、次のリソースを使用できる必要があります。

- Windows Server バージョン1709以降を実行している仮想化機能を備えたサーバー
- 実行中の VM のコンソールに接続するために Hyper-v マネージャーを実行できる2台目のコンピューター (Windows 10 または Windows Server 2016)
- サポートされている Linux シールドされた VM Os の1つの ISO イメージ:
    - 4\.4 カーネルを使用した Ubuntu 16.04 LTS
    - Red Hat Enterprise Linux 7.3
    - SUSE Linux Enterprise Server 12 Service Pack 2
- Lsvmtools パッケージと OS の更新プログラムをダウンロードするためのインターネットアクセス

> [!IMPORTANT]
> 上記の Linux Os の新しいバージョンには、既知の TPM ドライバーのバグが含まれている可能性があります。これにより、シールドされた Vm として正常にプロビジョニングできなくなります。
> 修正プログラムが利用可能になるまで、テンプレートまたはシールドされた Vm を新しいリリースに更新することはお勧めしません。
> サポートされている Os の一覧は、更新プログラムが公開されるときに更新されます。

## <a name="prepare-a-linux-vm"></a>Linux VM を準備する

シールドされた Vm は、セキュリティで保護されたテンプレートディスクから作成されます。
テンプレートディスクには、VM のオペレーティングシステムとメタデータが含まれます。これには、コア OS コンポーネントがデプロイ前に変更されないように、/boot パーティションと/root パーティションのデジタル署名が含まれます。

テンプレートディスクを作成するには、最初に、今後のシールドされた Vm の基本イメージとして準備する通常の (シールドされていない) VM を作成する必要があります。
この VM に対してインストールしたソフトウェアと構成の変更は、このテンプレートディスクから作成されたすべてのシールドされた Vm に適用されます。
以下の手順では、Linux VM を templatization 用に準備するための最小限の要件について説明します。

> [!NOTE]
> Linux ディスク暗号化は、ディスクがパーティション分割されるときに構成されます。
> これは、Linux のシールドされた VM テンプレートディスクを作成するために、dm-crypt を使用して事前に暗号化された新しい VM を作成する必要があることを意味します。


1.  仮想化サーバーで、管理者特権の PowerShell コンソールで次のコマンドを実行して、Hyper-v と Host Guardian Hyper-v サポート機能がインストールされていることを確認します。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2.  信頼できるソースから ISO イメージをダウンロードし、仮想化サーバーに保存するか、仮想化サーバーからアクセスできるファイル共有に保存します。

3.  Windows Server バージョン1709を実行している管理コンピューターで、次のコマンドを実行して、シールドされた VM リモートサーバー管理ツールをインストールします。

    ```powershell
    Install-WindowsFeature RSAT-Shielded-VM-Tools
    ```

4.  管理コンピューターで**Hyper-v マネージャー**を開き、仮想化サーバーに接続します。
    これを行うには、[サーバーへの接続...] をクリックします。[操作] ウィンドウで、または Hyper-v マネージャーを右クリックして、[サーバーへの接続...] を選択します。Hyper-v サーバーの DNS 名と、必要に応じて、接続に必要な資格情報を指定します。

5.  Hyper-v マネージャーを使用して、仮想化サーバーで[外部スイッチを構成](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/create-a-virtual-switch-for-hyper-v-virtual-machines)し、Linux VM がインターネットにアクセスして更新プログラムを取得できるようにします。

6.  次に、Linux OS をインストールするための新しい仮想マシンを作成します。
    [操作] ウィンドウで、[**新規** > **バーチャルマシン**] をクリックしてウィザードを起動します。
    "テンプレート化 Linux" などの VM のフレンドリ名を入力し、 **[次へ]** をクリックします。

7.  ウィザードの2ページ目で、 **[第2世代]** を選択して、VM が UEFI ベースのファームウェアプロファイルでプロビジョニングされていることを確認します。

8.  設定に従って、ウィザードの残りの部分を完了します。
    この VM には差分ディスクを使用しないでください。シールドされた VM テンプレートディスクは差分ディスクを使用できません。
    最後に、OS をインストールできるように、前の手順でダウンロードした ISO イメージをこの VM の仮想 DVD ドライブに接続します。

9.  Hyper-v マネージャーで、新しく作成した VM を選択し、操作 ウィンドウの **接続** をクリックして、vm の仮想コンソールに接続します。
    表示されるウィンドウで、 **[開始]** をクリックして仮想マシンを有効にします。

10. 選択した Linux ディストリビューションのセットアッププロセスを続行します。
    各 Linux ディストリビューションは異なるセットアップウィザードを使用しますが、Linux のシールドされた VM テンプレートディスクになる Vm では、次の要件を満たす必要があります。

    - ディスクは、GUID Paritioning Table (GPT) レイアウトを使用してパーティション分割する必要があります。
    - ルートパーティションは、dm-crypt を使用して暗号化する必要があります。 パスフレーズは、**パスフレーズ**(すべて小文字) に設定する必要があります。 このパスフレーズはランダム化され、シールドされた VM がプロビジョニングされるときにパーティションが再暗号化されます。
    - ブートパーティションは、 **ext2**ファイルシステムを使用する必要があります。

11. Linux OS が完全に起動し、サインインした後、linux 仮想カーネルと関連する Hyper-v integration services パッケージをインストールすることをお勧めします。
    さらに、シールドされた VM にアクセスするには、SSH サーバーまたはその他のリモート管理ツールをインストールする必要があります。

    Ubuntu で、次のコマンドを実行してこれらのコンポーネントをインストールします。

    ```bash
    sudo apt-get install linux-virtual linux-tools-virtual linux-cloud-tools-virtual linux-image-extra-virtual openssh-server
    ```

    RHEL で、代わりに次のコマンドを実行します。

    ```bash
    sudo yum install hyperv-daemons openssh-server
    sudo service sshd start
    ```

    SLES で、次のコマンドを実行します。

    ```bash
    sudo zypper install hyper-v
    sudo chkconfig hv_kvp_daemon on
    sudo systemctl enable sshd
    ```

12. 必要に応じて Linux OS を構成します。
    インストールするすべてのソフトウェア、追加したユーザーアカウント、およびシステム全体の構成の変更は、このテンプレートディスクから作成された今後のすべての Vm に適用されます。
    シークレットや不要なパッケージはディスクに保存しないようにしてください。

13. System Center Virtual Machine Manager を使用して Vm をデプロイする予定の場合は、vmm ゲストエージェントをインストールして、VMM が VM のプロビジョニング中に OS を特殊化できるようにします。
    特殊化を使用すると、各 VM を、さまざまなユーザーと SSH キー、ネットワーク構成、およびカスタムセットアップ手順で安全にセットアップできます。
    Vmm のドキュメントで[vmm ゲストエージェントを取得してインストール](https://docs.microsoft.com/system-center/vmm/vm-linux#install-the-vmm-guest-agent)する方法について説明します。

14. 次に、 [Microsoft Linux ソフトウェアリポジトリをパッケージマネージャーに追加](../../administration/linux-package-repository-for-microsoft-software.md)します。

15. パッケージマネージャーを使用して、Linux のシールドされた VM ブートローダー shim、プロビジョニングコンポーネント、およびディスク準備ツールを含む lsvmtools パッケージをインストールします。

    ```bash
    # Ubuntu 16.04
    sudo apt-get install lsvmtools

    # SLES 12 SP2
    sudo zypper install lsvmtools

    # RHEL 7.3
    sudo yum install lsvmtools
    ```

14. Linux OS のカスタマイズが完了したら、システムで lsvmprep インストールプログラムを見つけて実行します。
    
    ```bash
    # The path below may change based on the version of lsvmprep installed
    # Run "find /opt -name lsvmprep" to locate the lsvmprep executable
    sudo /opt/lsvmtools-1.0.0-x86-64/lsvmprep
    ```

15. VM をシャットダウンします。

16. VM のチェックポイントを作成した場合 (Hyper-v によって作成された自動チェックポイントと Windows 10 の更新プログラムが含まれている場合など)、続行する前に削除してください。
    チェックポイントは、テンプレートディスクウィザードでサポートされていない差分ディスク (. .avhdx) を作成します。
    
    チェックポイントを削除するには、 **Hyper-v マネージャー**を開き、VM を選択して、チェックポイントペインで最上位のチェックポイントを右クリックし、 **[チェックポイントのサブツリーを削除]** をクリックします。

    ![Hyper-v マネージャーでテンプレート VM のすべてのチェックポイントを削除する](../media/Guarded-Fabric-Shielded-VM/delete-checkpoints-lsvm-template.png)

## <a name="protect-the-template-disk"></a>テンプレートディスクを保護する

前のセクションで準備した VM は、Linux のシールドされた VM テンプレートディスクとして使用する準備がほぼ完了しています。
最後の手順では、テンプレートディスクウィザードを使用してディスクを実行します。これにより、ルートとブートパーティションの現在の状態がハッシュされ、デジタル署名が行われます。
ハッシュとデジタル署名は、シールドされた VM がプロビジョニングされるときに検証され、テンプレートの作成とデプロイの間で2つのパーティションに対して承認されていない変更が行われないようにします。

### <a name="obtain-a-certificate-to-sign-the-disk"></a>ディスクに署名するための証明書を取得する

ディスクの測定値にデジタル署名するには、テンプレートディスクウィザードを実行するコンピューターで証明書を取得する必要があります。
証明書は次の要件を満たしている必要があります。

Certificate プロパティ | 必須の値
---------------------|---------------
キーアルゴリズム | RSA
最小キーサイズ | 2048ビット
署名アルゴリズム | SHA256 (推奨)
キー使用法 | デジタル署名

この証明書の詳細は、テナントがシールドデータファイルを作成し、信頼するディスクを承認しているときに、テナントに表示されます。
そのため、この証明書は、自分とテナントが相互に信頼している証明機関から取得することが重要です。
ホストとテナントの両方であるエンタープライズシナリオでは、エンタープライズ証明機関からこの証明書を発行することを検討できます。
この証明書を所有するすべてのユーザーが、正規のディスクと同じように信頼された新しいテンプレートディスクを作成できるため、この証明書は慎重に保護してください。

テストラボ環境では、次の PowerShell コマンドを使用して自己署名証明書を作成できます。

```powershell
New-SelfSignedCertificate -Subject "CN=Linux Shielded VM Template Disk Signing Certificate"
```

### <a name="process-the-disk-with-the-template-disk-wizard-cmdlet"></a>テンプレートディスクウィザードのコマンドレットを使用してディスクを処理する

Windows Server バージョン1709を実行しているコンピューターにテンプレートディスクと証明書をコピーし、次のコマンドを実行して署名プロセスを開始します。
@No__t-0 パラメーターに指定した VHDX は、更新されたテンプレートディスクで上書きされます。そのため、コマンドを実行する前にコピーを作成してください。

> [!IMPORTANT]
> Windows Server 2016 または Windows 10 で利用可能なリモートサーバー管理ツールは、Linux のシールドされた VM テンプレートディスクの準備には使用できません。
> Linux のシールドされた VM テンプレートディスクを準備するには、windows Server バージョン1709または Windows Server 2019 で使用可能なリモートサーバー管理ツールで利用可能な[保護-TemplateDisk](https://docs.microsoft.com/powershell/module/shieldedvmtemplate/protect-templatedisk?view=win10-ps)コマンドレットを使用してください。

```powershell
# Replace "THUMBPRINT" with the thumbprint of your template disk signing certificate in the line below
$certificate = Get-Item Cert:\LocalMachine\My\THUMBPRINT

Protect-TemplateDisk -Path 'C:\temp\MyLinuxTemplate.vhdx' -TemplateName 'Ubuntu 16.04' -Version 1.0.0.0 -Certificate $certificate -ProtectedTemplateTargetDiskType PreprocessedLinux
```

これで、テンプレートディスクを使用して、Linux のシールドされた Vm をプロビジョニングする準備ができました。
System Center Virtual Machine Manager を使用して VM をデプロイしている場合は、VHDX を VMM ライブラリにコピーできるようになりました。

また、VHDX からボリューム署名カタログを抽出することもできます。
このファイルは、テンプレートを使用する VM 所有者に、署名証明書、ディスク名、およびバージョンに関する情報を提供するために使用されます。
このファイルを承認するには、このファイルをシールドデータファイルウィザードにインポートして、署名証明書を所有しているテンプレートの作成者に対して、このファイル用のテンプレートディスクを作成する必要があります。

ボリューム署名カタログを抽出するには、PowerShell で次のコマンドを実行します。

```powershell
Save-VolumeSignatureCatalog -TemplateDiskPath 'C:\temp\MyLinuxTemplate.vhdx' -VolumeSignatureCatalogPath 'C:\temp\MyLinuxTemplate.vsc'
```
