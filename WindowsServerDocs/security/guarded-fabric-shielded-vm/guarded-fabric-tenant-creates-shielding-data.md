---
title: テナント用のシールドされた Vm-シールドされた VM を定義するシールドデータの作成
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: 86047420cb4b1095d5715739d76daa3dba3ff5d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403452"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>テナント用のシールドされた Vm-シールドされた VM を定義するシールドデータの作成

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

シールド データ ファイル (別名プロビジョニング データ ファイルまたは PDK ファイル) は、管理者のパスワード、RDP やその他の ID 関連証明書、ドメイン参加の資格情報など、重要な VM 構成情報を保護するために、テナントまたは VM 所有者が作成する暗号化されたファイルです。 このトピックでは、シールドデータファイルを作成する方法について説明します。 ファイルを作成する前に、ホスティングサービスプロバイダーからテンプレートディスクを取得するか、「[テナント用のシールドされた vm-テンプレートディスクを作成する (省略可能)](guarded-fabric-tenant-creates-template-disk.md)」で説明されているように、テンプレートディスクを作成する必要があります。

シールドデータファイルの一覧および内容の図については、「[シールドデータとは何ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)」を参照してください。

> [!IMPORTANT]
> このセクションの手順は、Windows Server 2016 を実行しているテナントコンピューターで完了している必要があります。 このマシンは、保護されたファブリックの一部にすることはできません (つまり、HGS クラスターを使用するように構成することはできません)。

シールドデータファイルの作成を準備するには、次の手順を実行します。

- [リモートデスクトップ接続用の証明書を取得する](#obtain-a-certificate-for-remote-desktop-connection)
- [応答ファイルを作成する](#create-an-answer-file)
- [ボリューム署名カタログファイルを取得する](#get-the-volume-signature-catalog-file)
- [信頼されたファブリックの選択](#select-trusted-fabrics)

次に、シールドデータファイルを作成できます。

- [シールドデータファイルを作成して、ガーディアンを追加する](#create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard)


## <a name="obtain-a-certificate-for-remote-desktop-connection"></a>リモートデスクトップ接続用の証明書を取得する

テナントはリモートデスクトップ接続またはその他のリモート管理ツールを使用してシールドされた Vm にしか接続できないため、テナントが適切なエンドポイントに接続していることを確認できること (つまり、"man-in-the-middle" がないこと) を確認することが重要です。接続を遮断しています。

目的のサーバーに接続していることを確認する方法の1つとして、接続の開始時に提示するリモートデスクトップサービス用の証明書をインストールして構成する方法があります。 サーバーに接続しているクライアントコンピューターは、証明書が信頼されているかどうかを確認し、存在しない場合は警告を表示します。 一般に、接続しているクライアントが証明書を信頼していることを確認するために、RDP 証明書はテナントの PKI から発行されます。 [リモートデスクトップサービスでの証明書の使用](https://technet.microsoft.com/library/dn781533.aspx)の詳細については、TechNet を参照してください。

> [!NOTE]
> シールドデータファイルに含める RDP 証明書を選択する場合は、必ずワイルドカード証明書を使用してください。 1つのシールドデータファイルを使用すると、無制限の数の Vm を作成できます。 各 VM は同じ証明書を共有するので、ワイルドカード証明書によって、VM のホスト名に関係なく証明書が有効であることが確認されます。

シールドされた Vm を評価していて、証明機関からの証明書を要求する準備がまだできていない場合は、次の Windows PowerShell コマンドを実行して、テナントコンピューターに自己署名証明書を作成できます ( *contoso.com*はテナントのドメイン):

``` powershell
$rdpCertificate = New-SelfSignedCertificate -DnsName '\*.contoso.com'
$password = ConvertTo-SecureString -AsPlainText 'Password1' -Force
Export-PfxCertificate -Cert $RdpCertificate -FilePath .\rdpCert.pfx -Password $password
```

## <a name="create-an-answer-file"></a>応答ファイルを作成する

VMM の署名済みテンプレートディスクは一般化されているため、テナントは、プロビジョニングプロセス中に、シールドされた Vm を専門にするための応答ファイルを提供する必要があります。 応答ファイル (多くの場合、無人セットアップファイルと呼ばれます) は、目的のロールに対して VM を構成できます。つまり、Windows の機能をインストールし、前の手順で作成した RDP 証明書を登録して、その他のカスタム操作を実行できます。 また、既定の管理者のパスワードやプロダクトキーなど、Windows セットアップに必要な情報も提供されます。

シールドされた Vm を作成するための応答ファイル (Unattend.xml ファイル) を生成するために**ShieldingDataAnswerFile**関数を使用する方法の詳細については、「 [ShieldingDataAnswerFile 関数を使用した応答ファイルの生成](guarded-fabric-sample-unattend-xml-file.md)」を参照してください。 関数を使用すると、次のような選択肢を反映した応答ファイルをより簡単に生成できます。

- 初期化プロセスの最後に、VM はドメインに参加することを意図していますか?
- ボリュームライセンスまたは特定のプロダクトキーを VM ごとに使用しますか?
- DHCP または静的 IP を使用していますか?
- VM が組織に属していることを証明するために使用されるリモートデスクトッププロトコル (RDP) 証明書を使用しますか。
- 初期化の最後にスクリプトを実行しますか?
- 追加の構成に Desired State Configuration (DSC) サーバーを使用していますか。

シールドデータファイルで使用される応答ファイルは、そのシールドデータファイルを使用して作成されたすべての VM で使用されます。 そのため、VM 固有の情報を応答ファイルにハードコーディングしないようにする必要があります。 VMM では、VM 間で変更される可能性のある特殊化値を処理するために、無人セットアップファイルの一部の代替文字列 (下の表を参照) がサポートされています。 これらを使用する必要はありません。ただし、これらが存在する場合、VMM はそれらの機能を利用します。

シールドされた Vm の unattend.xml ファイルを作成する場合は、次の制限事項に注意してください。

-   無人セットアップファイルを構成した後、VM がオフになるようにする必要があります。 これは、VM がプロビジョニングを完了し、使用できる状態になったことを、VMM がテナントに報告する必要があることを VMM が認識できるようにするためです。 プロビジョニング中に VM がオフになったことを検出すると、VMM によって自動的に VM が電源に入れられます。

-   RDP 証明書を構成して、中間者攻撃用に構成された別のマシンではなく、適切な VM に接続していることを確認することを強くお勧めします。

-   構成した後に VM にアクセスできるように、RDP と対応するファイアウォール規則を必ず有効にしてください。 VMM コンソールを使用してシールドされた Vm にアクセスすることはできないため、VM に接続するには RDP が必要です。 Windows PowerShell リモート処理でシステムを管理する場合は、WinRM が有効になっていることも確認してください。

-   シールドされた VM の無人セットアップファイルでサポートされている代替文字列は次のとおりです。

| 置き換え可能な要素 | 置換文字列 |
|-----------|-----------|
| ComputerName        | @ComputerName@      |
| TimeZone            | @TimeZone@          |
| ProductKey          | @ProductKey@        |
| IPAddr4-1           | @IP4Addr-1@         |
| IPAddr6-1           | @IP6Addr-1@         |
| MACAddr-1           | @MACAddr-1@         |
| Prefix-1-1          | @Prefix-1-1@        |
| NextHop-1-1         | @NextHop-1-1@       |
| Prefix-1-2          | @Prefix-1-2@        |
| NextHop-1-2         | @NextHop-1-2@       |

代替文字列を使用する場合は、VM のプロビジョニング処理中に文字列が設定されるようにすることが重要です。 展開時に @ProductKey @ のような文字列が指定されていない場合は、無人セットアップファイルの 1ProductKey @ no__t ノードを空白の @no__t ままにすると、特殊化プロセスは失敗し、VM に接続できなくなります。

また、テーブルの末尾に向かうネットワーク関連の代替文字列は、VMM 静的 IP アドレスプールを利用している場合にのみ使用されることに注意してください。 これらの置換文字列が必要であるかどうかは、ホスティングサービスプロバイダーから通知されます。 VMM テンプレートでの静的 IP アドレスの詳細については、VMM のドキュメントの次の情報を参照してください。

- [IP アドレスプールに関するガイドライン](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools) 
- [VMM ファブリックでの静的 IP アドレスプールの設定](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

最後に、シールドされた VM の展開プロセスでは、OS ドライブのみが暗号化されることに注意する必要があります。 1つまたは複数のデータドライブを含むシールドされた VM をデプロイする場合は、データドライブを自動的に暗号化するために、無人コマンドまたはグループポリシー設定をテナントドメインに追加することを強くお勧めします。

## <a name="get-the-volume-signature-catalog-file"></a>ボリューム署名カタログファイルを取得する

シールドデータファイルには、テナントが信頼しているテンプレートディスクに関する情報も含まれています。 テナントは、ボリューム署名カタログ (VSC) ファイルの形式で、信頼されたテンプレートディスクからディスク署名を取得します。 これらの署名は、新しい VM のデプロイ時に検証されます。 シールドデータファイル内のどの署名も、VM と共にデプロイしようとしているテンプレートディスクに一致しない場合 (つまり、変更されたか、別の悪意のあるディスクと交換された場合)、プロビジョニングプロセスは失敗します。

> [!IMPORTANT]
> VSC によってディスクが改ざんされていないことが保証されますが、最初にテナントがそのディスクを信頼することが重要になります。 テナントでテンプレートディスクがホスト側によって提供される場合は、そのテンプレートディスクを使用してテスト VM をデプロイし、独自のツール (ウイルス対策、脆弱性スキャナーなど) を実行して、実際には信頼できる状態でディスクを検証します。

テンプレートディスクの VSC を取得するには、次の2つの方法があります。

-  ホスト (またはテナントが VMM にアクセスできる場合) は、VMM PowerShell コマンドレットを使用して、VSC を保存し、テナントに渡します。 これは、VMM コンソールがインストールされ、ホストファブリックの VMM 環境を管理するように構成されている任意のコンピューターで実行できます。 VSC を保存するための PowerShell コマンドレットは次のとおりです。

        $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"
    
        $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk
    
        $vsc.WriteToFile(".\templateDisk.vsc")

-  テナントは、テンプレートディスクファイルにアクセスできます。 これは、ホスティングサービスプロバイダーにアップロードするテンプレートディスクをテナントが作成する場合、またはテナントがホストのテンプレートディスクをダウンロードできる場合に発生する可能性があります。 この場合、図に VMM がないと、テナントは次のコマンドレットを実行します (シールドされた VM ツール機能と共にインストールされ、リモートサーバー管理ツール)。

        Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc

## <a name="select-trusted-fabrics"></a>信頼されたファブリックの選択

シールドデータファイルの最後のコンポーネントは、VM の所有者とガーディアンに関連します。 ガーディアンは、シールドされた VM の所有者と実行を承認された保護されたファブリックの両方を指定するために使用されます。

ホストしているファブリックがシールドされた VM を実行することを承認するには、ホスティングサービスプロバイダーのホストガーディアンサービスからガーディアンメタデータを取得する必要があります。 多くの場合、ホスティングサービスプロバイダーは、管理ツールを通じてこのメタデータを提供します。 エンタープライズシナリオでは、自分でメタデータを取得するための直接アクセスが必要になる場合があります。

ユーザーまたはホスティングサービスプロバイダーは、次のいずれかのアクションを実行して、HGS からガーディアンメタデータを取得できます。

-  次の Windows PowerShell コマンドを実行するか、web サイトを参照して表示されている XML ファイルを保存して、HGS から直接ガーディアンメタデータを取得します。

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

-  Vmm PowerShell コマンドレットを使用して、VMM からガーディアンメタデータを取得します。

        $relecloudmetadata = Get-SCGuardianConfiguration

        $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8

続行する前に、シールドされた Vm の実行を承認する保護されたファブリックごとにガーディアンメタデータファイルを取得します。

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>シールドデータファイルを作成し、シールドデータファイルウィザードを使用してガーディアンを追加する

シールドデータファイルウィザードを実行して、シールドデータ (PDK) ファイルを作成します。 ここでは、RDP 証明書、無人セットアップファイル、ボリューム署名カタログ、所有者ガーディアン、および前の手順で取得したダウンロードしたガーディアンメタデータを追加します。

1.  サーバーマネージャーまたは次の Windows PowerShell コマンドを使用して、 **&gt; @no__t シールド**された VM ツールをコンピューターにインストールリモートサーバー管理ツールます。

        Install-WindowsFeature RSAT-Shielded-VM-Tools

2.  [スタート] メニューの [管理ツール] セクションからシールドデータファイルウィザードを開くか、次の実行可能ファイル**C: \\Windows @ no__t-2System32\\ShieldingDataFileWizard.exe**を実行します。

3.  最初のページで、2番目の [ファイルの選択] ボックスを使用して、シールドデータファイルの場所とファイル名を選択します。 通常、シールドデータファイルには、そのシールドデータを使用して作成された任意の Vm を所有するエンティティ (HR、IT、Finance など) と、実行しているワークロードロール (たとえば、ファイルサーバー、web サーバー、または無人セットアップファイルによって構成されている他のすべてのもの) を所有するエンティティを指定します オプションボタンは、シールドされた**テンプレートのシールドデータ**に設定したままにしておきます。

    > [!NOTE]
    > シールドデータファイルウィザードでは、次の2つのオプションが表示されます。
    >- **シールドされたテンプレートのシールドデータ**
    >- **既存の Vm とシールドされていないテンプレートのシールドデータ**<br>
    > 最初のオプションは、シールドされたテンプレートから新しいシールドされた Vm を作成するときに使用します。 2番目のオプションでは、既存の Vm を変換する場合、またはシールドされていないテンプレートからシールドされた Vm を作成する場合にのみ使用できるシールドデータを作成できます。

    ![シールドデータファイルウィザード、ファイルの選択](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

       また、このシールドデータファイルを使用して作成された Vm を本当にシールドするか、"暗号化がサポートされている" モードで構成するかを選択する必要があります。 これら2つのオプションの詳細については、「[保護されたファブリックが実行できる仮想マシンの種類を教え](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run)てください。」を参照してください。

    > [!IMPORTANT]
    > 次の手順に注意してください。シールドされた Vm の所有者と、シールドされた Vm の実行が許可されるファブリックを定義するためです。<br>後で既存のシールド**され**た VM を**シールド**からサポート、またはその逆に変更するには、**所有者ガーディアン**を所有する必要があります。
    
4.  この手順の目標は2つのフォールドです。

    - VM の所有者として自分を表す所有者ガーディアンを作成または選択します。

    - 前の手順でホスティングプロバイダーの (または独自の) ホストガーディアンサービスからダウンロードしたガーディアンをインポートします。

    既存の所有者ガーディアンを指定するには、ドロップダウンメニューから適切なガーディアンを選択します。 秘密キーが残っているローカルコンピューターにインストールされているガーディアンだけが、この一覧に表示されます。 また、右下隅にある **[ローカルガーディアンの管理]** を選択し、 **[作成]** をクリックしてウィザードを完了することで、独自の所有者ガーディアンを作成することもできます。

    次に、**所有者** ページと ガーディアン ページを使用して、先ほどダウンロードしたガーディアンメタデータをインポートします。 右下隅にある **[ローカルガーディアンの管理]** を選択します。 **インポート**機能を使用して、ガーディアンメタデータファイルをインポートします。 必要なすべてのガーディアンをインポートまたは追加したら、[ **OK]** をクリックします。 ベストプラクティスとして、ホスティングサービスプロバイダーまたはエンタープライズデータセンターの後に、それらが表すガーディアンという名前を付けてください。 最後に、シールドされた VM の実行が許可されているデータセンターを表すすべてのガーディアンを選択します。 所有者ガーディアンを再度選択する必要はありません。 完了したら **[次へ]** をクリックします。

    ![シールドデータファイルウィザード、所有者、およびガーディアン](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5.  ボリューム ID の修飾子 ページで、**追加** をクリックして、シールドデータファイル内の署名済みテンプレートディスクを承認します。 ダイアログボックスで VSC を選択すると、そのディスクの名前、バージョン、および署名に使用された証明書に関する情報が表示されます。 承認するテンプレートディスクごとに、この手順を繰り返します。

6.  **[特殊化値]** ページで、 **[参照]** をクリックして、vm を特殊化するために使用する unattend.xml ファイルを選択します。

    下部にある **[追加]** ボタンを使用して、特殊化プロセス中に必要な追加ファイルを PDK に追加します。 たとえば、無人セットアップファイルが VM に RDP 証明書をインストールする場合 (「 [ShieldingDataAnswerFile 関数を使用して応答ファイルを生成](guarded-fabric-sample-unattend-xml-file.md)する」の説明を参照)、無人セットアップファイルで参照されている RDPCert ファイルをここに追加する必要があります。 ここで指定するファイルは、作成される VM の C: \\temp @ no__t-1 に自動的にコピーされます。 無人セットアップファイルでは、パスによってファイルを参照するときに、ファイルがそのフォルダー内にあることを想定する必要があります。

7.  次のページで選択内容を確認し、 **[生成]** をクリックします。

8.  完了したら、ウィザードを閉じます。

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>PowerShell を使用してシールドデータファイルを作成し、ガーディアンを追加する

シールドデータファイルウィザードの代わりに、 [ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps)を実行してシールドデータファイルを作成することもできます。

シールドされた Vm が保護されたファブリックで実行されることを承認するには、すべてのシールドデータファイルを正しい所有者およびガーディアン証明書で構成する必要があります。
[HgsGuardian](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsguardian?view=win10-ps)を実行すると、ローカルにガーディアンがインストールされているかどうかを確認できます。 所有者のガーディアンには秘密キーがありますが、データセンターのガーディアンでは通常は使用されません。

所有者ガーディアンを作成する必要がある場合は、次のコマンドを実行します。

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

このコマンドは、"シールドされた VM ローカル証明書" フォルダーの下にあるローカルコンピューターの証明書ストアに、署名証明書と暗号化証明書のペアを作成します。
仮想マシンのシールドを解除するには、所有者証明書とそれに対応する秘密キーが必要です。そのため、これらの証明書がバックアップされ、盗難から保護されていることを確認してください。
所有者の証明書にアクセスできる攻撃者は、その証明書を使用して、シールドされた仮想マシンを起動したり、セキュリティの構成を変更したりできます。

仮想マシン (プライマリデータセンター、バックアップデータセンターなど) を実行する保護されたファブリックからガーディアン情報をインポートする必要がある場合は、保護された[ファブリックから取得した各メタデータファイル](#select-trusted-fabrics)に対して次のコマンドを実行します。

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> 自己署名証明書を使用した場合、または HGS に登録されている証明書の有効期限が切れている場合は、HgsGuardian コマンドを使用して、セキュリティチェックを回避するために、`-AllowUntrustedRoot` および/または `-AllowExpired` フラグを使用する必要がある場合があります。

また、このシールドデータファイルと共に使用するテンプレートディスクごとに[ボリューム署名カタログを取得](#get-the-volume-signature-catalog-file)する必要があります。また、オペレーティングシステムが特殊化タスクを自動的に完了できるように、[シールドデータ応答ファイル](#create-an-answer-file)を取得する必要もあります。
最後に、VM を完全にシールドするか、vTPM のみを有効にするかを決定します。
完全にシールドされた VM の場合は `-Policy Shielded`、基本的なコンソール接続と PowerShell Direct を許可する vTPM が有効になっている VM の場合は `-Policy EncryptionSupported` を使用します。

すべての準備ができたら、次のコマンドを実行してシールドデータファイルを作成します。

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

上記のコマンドでは、"Owner" という名前のガーディアン (HgsGuardian から取得) で VM のセキュリティ構成を変更できますが、"米国東部データセンター" では VM を実行できますが、その設定は変更できません。
複数のガーディアンがある場合は、ガーディアンの名前をコンマで区切って `'EAST-US Datacenter', 'EMEA Datacenter'` のようにします。
ボリューム ID 修飾子は、テンプレートディスクまたは将来のバージョン (GreaterThanOrEquals) の正確なバージョン (Equals) のみを信頼するかどうかを指定します。
ディスク名と署名証明書は、展開時に考慮されるバージョン比較と完全に一致している必要があります。
ボリューム ID 修飾子のコンマ区切りリストを `-VolumeIDQualifier` パラメーターに指定することで、複数のテンプレートディスクを信頼できます。
最後に、VM に応答ファイルを添付する必要がある他のファイルがある場合は、`-OtherFile` パラメーターを使用し、コンマ区切りのファイルパスの一覧を指定します。

シールドデータファイルを構成するためのその他の方法については、 [ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps)と[New-VolumeIDQualifier](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps)のコマンドレットのドキュメントを参照してください。

## <a name="see-also"></a>関連項目

- [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
