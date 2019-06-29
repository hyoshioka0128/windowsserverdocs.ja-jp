---
title: シールドされた Vm のテナントでシールドされた VM を定義するシールド データの作成
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 49f4e84d-c1f7-45e5-9143-e7ebbb2ef052
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/30/2019
ms.openlocfilehash: d1d269ecdbfd4803c51da4817b62caf01d2091ae
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469623"
---
# <a name="shielded-vms-for-tenants---creating-shielding-data-to-define-a-shielded-vm"></a>シールドされた Vm のテナントでシールドされた VM を定義するシールド データの作成

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

シールド データ ファイル (別名プロビジョニング データ ファイルまたは PDK ファイル) は、管理者のパスワード、RDP やその他の ID 関連証明書、ドメイン参加の資格情報など、重要な VM 構成情報を保護するために、テナントまたは VM 所有者が作成する暗号化されたファイルです。 このトピックでは、シールド データ ファイルを作成する方法についての情報を提供します。 ファイルを作成する前にする必要があります、ホスティング サービス プロバイダーからテンプレート ディスクを取得またはのいずれかの説明に従ってテンプレート ディスクを作成[テナント - (省略可能) テンプレート ディスクを作成するためのシールドされた Vm](guarded-fabric-tenant-creates-template-disk.md)します。

シールド データ ファイルの内容を次の図と一覧については、次を参照してください。[シールド データを使用するものが、なぜ必要ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)します。

> [!IMPORTANT]
> Windows Server 2016 を実行しているテナント マシンでのこのセクションの手順を完了する必要があります。 そのマシンは保護されたファブリックの一部をすることはできません (つまりは構成しません HGS クラスターを使用する)。

シールド データ ファイルを作成する準備をするには、次の手順を実行します。

- [リモート デスクトップ接続の証明書を取得します。](#obtain-a-certificate-for-remote-desktop-connection)
- [応答ファイルを作成します。](#create-an-answer-file)
- [ボリューム署名カタログ ファイルを取得します。](#get-the-volume-signature-catalog-file)
- [信頼されたファブリックを選択します。](#select-trusted-fabrics)

シールド データ ファイルを作成します。

- [シールド データ ファイルを作成し、保護者を追加](#create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard)


## <a name="obtain-a-certificate-for-remote-desktop-connection"></a>リモート デスクトップ接続の証明書を取得します。

テナントは、リモート デスクトップ接続または他のリモート管理ツールを使用して、シールドされた Vm に接続することは、ことが重要には、適切なエンドポイントに接続するテナントが確認できることを確認します (つまりがない"man in the middle"接続をインターセプト)。

目的のサーバーに接続することを確認する 1 つの方法は、インストールして接続を開始するときに表示するへリモート デスクトップ サービス用の証明書を構成します。 サーバーに接続するクライアント コンピューターでは、そうでない場合、その信頼証明書と、警告を表示するかどうかを確認します。 一般に、接続するクライアント証明書を信頼するためには、RDP 証明書は、テナントの PKI から発行されます。 詳細については[リモート デスクトップ サービスの証明書を使用して](https://technet.microsoft.com/library/dn781533.aspx)TechNet で確認できます。

> [!NOTE]
> シールド データ ファイルに含める、RDP 証明書を選択すると、必ず、ワイルドカード証明書を使用します。 シールド データ ファイルを 1 つは、無制限の数の Vm を作成するために可能性があります。 各 VM は、同じ証明書を共有するためのワイルドカード証明書により、証明書が VM のホスト名に関係なく有効になります。

シールドされた Vm を評価することは、証明機関から証明書を要求する準備ができて、して作成できます自己署名証明書をテナントのコンピューターで、次の Windows PowerShell コマンドを実行している場合 (場所*contoso.com*はテナントのドメインです)。

``` powershell
$rdpCertificate = New-SelfSignedCertificate -DnsName '\*.contoso.com'
$password = ConvertTo-SecureString -AsPlainText 'Password1' -Force
Export-PfxCertificate -Cert $RdpCertificate -FilePath .\rdpCert.pfx -Password $password
```

## <a name="create-an-answer-file"></a>応答ファイルを作成する

VMM での署名付きテンプレート ディスクは汎用化するために、プロビジョニング プロセス中に、シールドされた Vm を特殊な応答ファイルを提供するテナントが必要です。 その目的のロールの VM を構成することができます (多くの場合は、無人セットアップ ファイルと呼ばれます)、応答ファイル - は、Windows の機能をインストール、前の手順で作成された RDP 証明書を登録して他のカスタム アクションを実行します。 また、既定の管理者のパスワードとプロダクト キーを含む、Windows セットアップに必要な情報が供給されます。

取得および使用方法については、 **New-shieldingdataanswerfile** 、シールドされた Vm を作成するための応答ファイル (Unattend.xml ファイル) を生成する関数を参照してください[を使用して応答ファイルを生成します新しい ShieldingDataAnswerFile 関数](guarded-fabric-sample-unattend-xml-file.md)します。 関数を使用して、次の選択肢を反映する応答ファイルをより簡単に生成できます。

- VM は、初期化プロセスの最後に参加しているドメインを意図したでしょうか。
- ボリューム ライセンスまたは VM ごとの特定のプロダクト キーを使用するでしょうか。
- DHCP または静的 ip アドレスを使用していますか。
- VM が、組織に属していることを証明するために使用されるリモート デスクトップ プロトコル (RDP) の証明書を使用するでしょうか。
- 初期化の最後にスクリプトを実行しますか。
- 追加の構成を Desired State Configuration (DSC) サーバーを使っているか

シールド データ ファイルで使用する応答ファイルは、シールド データ ファイルを使用して作成されたすべての VM で使用されます。 そのため、応答ファイルに、VM に固有の情報をハード コーディングしないされませんすることを確認する必要があります。 VMM では、VM から VM に変わる可能性のある値を特殊化を処理する無人セットアップ ファイル (次の表を参照してください) の一部の置換文字列をサポートしています。 これらは; を使用する必要はありません。ただし、存在する場合は、VMM は、それらの利点をかかります。

シールドされた Vm の unattend.xml ファイルを作成するときに、次の制限に注意してください。

-   無人セットアップ ファイルと、VM を構成した後に無効にされている必要があります。 これは、VMM を VM がプロビジョニング完了し、使用できるように、テナントにレポートする必要があるときを把握できるようにします。 プロビジョニング中にオフされたことが検出される VMM に自動的に VM を電源します。

-   適切な VM とで中間者攻撃用に構成されていない別のコンピューターに接続していることを確認して、RDP 証明書を構成することを強くお勧めします。

-   構成した後、VM にアクセスできるように、RDP と対応するファイアウォール規則を有効にすることを確認します。 RDP、VM に接続する必要があります、アクセスのシールドされた Vm に、VMM コンソールを使用することはできません。 Windows PowerShell リモート処理を使用してシステムを管理する場合は、すぎる WinRM が有効になってください。

-   シールドされた VM の無人セットアップ ファイルでサポートされている唯一の代替文字列は次のとおりです。

| 置き換え可能要素 | 置換文字列 |
|-----------|-----------|
| ComputerName        | @ComputerName@      |
| TimeZone            | @TimeZone@          |
| ProductKey          | @ProductKey@        |
| IPAddr4-1           | @IP4Addr-1@         |
| IPAddr6-1           | @IP6Addr-1@         |
| MACAddr 1           | @MACAddr-1@         |
| プレフィックス-1-1          | @Prefix-1-1@        |
| NextHop-1-1         | @NextHop-1-1@       |
| Prefix-1-2          | @Prefix-1-2@        |
| NextHop-1-2         | @NextHop-1-2@       |

代替文字列を使用する場合は、文字列を VM のプロビジョニング プロセス中に設定することを確認する必要があります。 などの文字列の場合@ProductKey@ が指定されていない、配置時に残して、 &lt;ProductKey&gt;ノード、無人セットアップ ファイルが空で、特殊化のプロセスは失敗し、VM に接続できないことができます。

また、VMM 静的 IP アドレス プールを活用している場合のみ、テーブルの末尾に向かってネットワーク関連の置換文字列に使用することに注意してください。 ホスティング サービス プロバイダーはこれらの代替文字列が必要なかどうかに指定することになります。 VMM テンプレートでの静的 IP アドレスの詳細については、VMM のマニュアルでは、次を参照してください。

- [IP アドレス プールに関するガイドライン](https://technet.microsoft.com/system-center-docs/vmm/plan/plan-network#guidelines-for-ip-address-pools) 
- [VMM ファブリックでの静的 IP アドレス プールを設定します。](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-network-static-address-pools)

最後は、シールドされた VM の展開プロセスが OS ドライブの暗号化のみことに注意してください。 1 つまたは複数のデータ ドライブのシールドされた VM をデプロイする場合は、自動的にデータ ドライブを暗号化するテナントのドメインに、unattend コマンドまたはグループ ポリシー設定を追加することを強くお勧めします。

## <a name="get-the-volume-signature-catalog-file"></a>ボリューム署名カタログ ファイルを取得します。

シールド データ ファイルには、テナントが信頼されたテンプレート ディスクについての情報も含まれます。 テナントは、ボリューム シグネチャ カタログ (VSC) ファイルの形式での信頼されたテンプレート ディスクからディスク署名を取得します。 新しい VM をデプロイするときに、これらの署名を検証し、されます。 テンプレート ディスクを一致するシールド データ ファイルの署名がない場合 (つまり変更またはされた可能性のある悪意のある、別のディスクとスワップ)、VM をデプロイしようとして、プロビジョニング プロセスは失敗します。

> [!IMPORTANT]
> VSC は、ディスクが改ざんされていないことを保証されますが、最初にディスクを信頼するテナントのも重要です。 テナントがあり、テスト テンプレート ディスクを使用して VM をデプロイして、ディスクを検証する独自のツール (ウイルス対策や脆弱性スキャナー、) を実行、テンプレートのディスクが、ホスト側によって提供される場合は、実際には、信頼できる状態にします。

テンプレート ディスクの VSC を取得する 2 つの方法はあります。

-  ホスト (またはテナントのテナントに VMM へのアクセスがある場合) は、VMM PowerShell コマンドレットを使用して、VSC を保存して、テナントに提供します。 これは、VMM コンソールをインストールし、ホスティング ファブリックの VMM 環境を管理するように構成とすべてのコンピューターで実行できます。 PowerShell コマンドレットは、保存、VSC は次のとおりです。

        $disk = Get-SCVirtualHardDisk -Name "templateDisk.vhdx"
    
        $vsc = Get-SCVolumeSignatureCatalog -VirtualHardDisk $disk
    
        $vsc.WriteToFile(".\templateDisk.vsc")

-  テナントが、テンプレートのディスク ファイルにアクセスします。 場合は、テナントは、ホスト側のテンプレート ディスクをダウンロードする場合は、テナントは、ホスティング サービス プロバイダーにアップロードするテンプレート ディスクを作成します。 または、大文字と小文字があります。 この場合、VMM の図に、なし、テナントは、(シールドされた VM ツール機能により、リモート サーバー管理ツールの一部がインストールされている) 次のコマンドレットを実行は。

        Save-VolumeSignatureCatalog -TemplateDiskPath templateDisk.vhdx -VolumeSignatureCatalogPath templateDisk.vsc

## <a name="select-trusted-fabrics"></a>信頼されたファブリックを選択します。

シールド データ ファイルの最後のコンポーネントは、所有者および VM の保護者に関連しています。 ガーディアンを使用して、シールドされた VM の保護されたファブリックを実行する権限が、両方の所有者を指定します。

シールドされた VM を実行するためのホスティング ファブリックを承認するために、ホスティング サービス プロバイダーのホスト ガーディアン サービスからガーディアン メタデータを取得する必要があります。 多くの場合、ホスティング サービス プロバイダーが表示されます、管理ツールを使ってこのメタデータを使用します。 エンタープライズ シナリオでは、自分でメタデータの取得に直接アクセスするがあります。

か、ホスティング サービス プロバイダーから入手できますガーディアン メタデータ HGS アクションを次のいずれかを行います。

-  次の Windows PowerShell コマンドを実行して、web サイトを参照または表示される XML ファイルを保存して、HGS から直接ガーディアン メタデータを取得します。

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

-  VMM PowerShell コマンドレットを使用して、VMM からガーディアン メタデータを取得します。

        $relecloudmetadata = Get-SCGuardianConfiguration

        $relecloudmetadata.InnerXml | Out-File .\RelecloudGuardian.xml -Encoding UTF8

シールドされた Vm 上で続行する前に実行を承認する各保護されたファブリックのガーディアン メタデータ ファイルを取得します。

## <a name="create-a-shielding-data-file-and-add-guardians-using-the-shielding-data-file-wizard"></a>シールド データ ファイルを作成し、シールド データ ファイル ウィザードを使用して保護者を追加

シールド データ (PDK) ファイルを作成するシールド データ ファイル ウィザードを実行します。 ここでは、RDP 証明書の追加を無人セットアップ ファイルをボリューム署名カタログでは、所有者のガーディアンをし、ガーディアンをダウンロードしたメタデータは、前の手順で取得します。

1.  インストール**リモート サーバー管理ツール&gt;機能管理ツール&gt;シールドされた VM ツール**サーバー マネージャーまたは Windows PowerShell の次のコマンドを使用してコンピューターに。

        Install-WindowsFeature RSAT-Shielded-VM-Tools

2.  管理者ツール セクションで、スタート メニュー、または次の実行可能ファイルを実行してから、シールド データ ファイル ウィザードを開く**c:\\Windows\\System32\\ShieldingDataFileWizard.exe**します。

3.  最初のページで、2 番目のファイルの選択ボックスを使用して、シールド データ ファイルの場所とファイル名を選択します。 シールド データのすべての Vm を所有するエンティティが作成された後にシールド データ ファイルの名前は通常、(たとえば、人事、財務、IT) と実行 (例、ファイル サーバー、web サーバー、またはその他、無人セットアップ ファイルで構成されている) のワークロードのロール。 設定するオプション ボタンのままに**シールド データのシールドされたテンプレート**します。

    > [!NOTE]
    > シールド データ ファイル ウィザードでは、以下の 2 つのオプションが表示されます。
    >- **シールドされたテンプレートのデータを保護できます。**
    >- **シールド データの既存の Vm とシールドされていないテンプレート**<br>
    > 最初のオプションは、シールドされたテンプレートからシールドされた Vm を新規作成するときに使用されます。 2 番目のオプションを使用して、シールド データを変換する既存の Vm または作成は、シールドされていないテンプレートから Vm をシールドされた場合にのみ使用できますを作成できます。

    ![シールド データ ファイル ウィザードの ファイルの選択](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-01.png)

       さらに、Vm が作成されたかどうかこのシールド データ ファイルの使用が本当にシールドされたまたは「暗号化のサポート」モードで構成を選択してください。 これら 2 つのオプションの詳細については、次を参照してください。 [、保護されたファブリックを実行できる仮想マシンの種類は何ですか?](guarded-fabric-and-shielded-vms.md#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run)します。

    > [!IMPORTANT]
    > シールドされた Vm との所有者を定義するために、次の手順に注意を払うファブリックは、シールドされた Vm の承認で実行します。<br>所有している**所有者ガーディアン**から既存のシールドされた VM を後で変更するために必要なは**シールドされた**に**暗号化がサポートされている**またはその逆。
    
4.  この手順では目標は、2 つです。

    - 作成または VM 所有者として表すする所有者ガーディアン選択

    - ホスティング プロバイダーからダウンロードしたガーディアンのインポート (または独自) 前の手順で、ホスト ガーディアン サービス

    既存の所有者のガーディアンを指定するには、ドロップ ダウン メニューから適切なガーディアンを選択します。 この一覧に、秘密キーがそのままで、ローカル コンピューターにインストールされている guardians のみが表示されます。 選択して、独自の所有者のガーディアンを作成することもできます**管理ローカル Guardians**下で右クリックして**作成**とウィザードの完了します。

    次に、以前にダウンロードしたガーディアン メタデータをインポート使用してもう一度、**所有者と Guardians**ページ。 選択**管理ローカル Guardians**右下隅から。 使用して、**インポート**ガーディアン メタデータ ファイルをインポートする機能。 をクリックして**OK**インポートまたはすべての必要な保護者を追加するとします。 ベスト プラクティスとして、ホスティング サービス プロバイダーまたはエンタープライズ データ センターを表す後 guardians 名前を付けます。 最後に、シールドされた VM による実行が承認されているデータ センターを表すすべてのガーディアンを選択します。 所有者のガーディアンをもう一度選択する必要はありません。 クリックして**次**完了後します。

    ![シールド データ ファイル ウィザード、所有者および guardians](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-wizard-02.png)

5.  ボリュームの ID の修飾子 ページで、次のようにクリックします。**追加**シールド データ ファイルの署名付きテンプレート ディスクを承認します。 ダイアログ ボックスで、VSC を選択するとはそのディスクの名前、バージョン、および署名に使用された証明書に関する情報を表示するが。 各テンプレート ディスクを承認するには、このプロセスを繰り返します。

6.  **特殊化値**] ページで [**参照**の Vm を特殊化に使用される、unattend.xml ファイルを選択します。

    使用して、**追加**特殊化プロセス中に必要な PDK にその他のファイルを追加する下部にあるボタンをクリックします。 たとえば、VM に RDP 証明書のインストールは、無人セットアップ ファイル (」の説明に従って[New-shieldingdataanswerfile 関数を使用して応答ファイルを生成](guarded-fabric-sample-unattend-xml-file.md)) で参照されている RDPCert.pfx ファイルを追加する必要があります、無人セットアップ ファイルをここでします。 ここで指定したすべてのファイルが自動的には注意が c: にコピーする\\temp\\作成される VM にします。 ファイルのパスで参照するときにそのフォルダー内に、無人セットアップ ファイルが予想されます。

7.  次のページで選択内容を確認し、クリックして**生成**します。

8.  これが完了した後は、ウィザードを閉じます。

## <a name="create-a-shielding-data-file-and-add-guardians-using-powershell"></a>シールド データ ファイルを作成し、PowerShell を使用するガーディアンを追加

実行することができます、シールド データ ファイル ウィザードに代わりに、[新規 ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/new-shieldingdatafile?view=win10-ps)シールド データ ファイルを作成します。

すべてのシールド データ ファイルは、保護されたファブリック上で実行する、シールドされた Vm を承認するには、適切な所有者とガーディアンの証明書を構成する必要があります。
実行してローカルにインストールされている任意の保護者があることを確認することができます[Get HgsGuardian](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsguardian?view=win10-ps)します。 所有者 guardians は秘密キーを持つ、データ センターのガーディアン通常はそうではありません。

所有者ガーディアンを作成する必要がある場合は、次のコマンドを実行します。

```powershell
New-HgsGuardian -Name "Owner" -GenerateCertificates
```

このコマンドは、シールドされた VM ローカル証明書 フォルダーの下のローカル コンピューターの証明書ストアに証明書の署名と暗号化のペアを作成します。
所有者の証明書と仮想マシンを unshield、ようにこれらに対応する秘密キーが必要証明書がバックアップされ、盗難から保護します。
所有者の証明書にアクセスできる攻撃者は、それらを使用、シールドされた仮想マシンを起動またはセキュリティの構成を変更できます。

ごとに、次のコマンドを実行する仮想マシン (、プライマリ データ センター、バックアップ データ センターなど) を実行する保護されたファブリックからガーディアンの情報をインポートする必要がある場合[メタデータ ファイルを取得して、保護されたファブリックから](#select-trusted-fabrics).

```powershell
Import-HgsGuardian -Name 'EAST-US Datacenter' -Path '.\EastUSGuardian.xml'
```

> [!TIP]
> 自己署名証明書や登録されている証明書を使用した場合は、HGS が期限切れを使用する必要があります、`-AllowUntrustedRoot`や`-AllowExpired`セキュリティ チェックをバイパスするインポート HgsGuardian コマンドを使用したフラグ。

必要がありますも[ボリューム署名カタログを取得](#get-the-volume-signature-catalog-file)このシールド データ ファイルを使用するテンプレート ディスクごとに、[シールド データファイル応答](#create-an-answer-file)オペレーティング システムが完了するその特殊化は自動的にタスクします。
最後に、VM をシールドされた完全または vTPM が有効なだけするかを決定します。
使用`-Policy Shielded`完全にシールドされた vm または`-Policy EncryptionSupported`vTPM で基本的なコンソールの接続を許可する VM と PowerShell ダイレクトが有効になっています。

すべての準備ができたら、シールド データ ファイルを作成するには、次のコマンドを実行します。

```powershell
$viq = New-VolumeIDQualifier -VolumeSignatureCatalogFilePath 'C:\temp\marketing-ws2016.vsc' -VersionRule Equals
New-ShieldingDataFile -ShieldingDataFilePath "C:\temp\Marketing-LBI.pdk" -Policy EncryptionSupported -Owner 'Owner' -Guardian 'EAST-US Datacenter' -VolumeIDQualifier $viq -AnswerFile 'C:\temp\marketing-ws2016-answerfile.xml'
```

上記のコマンドの「所有者」(Get HgsGuardian から取得した) という名前のガーディアンは '- 米国東部データ センター' は、VM を実行できますが、その設定を変更中に、VM のセキュリティの構成は、今後を変更することになります。
1 つ以上のガーディアンがあれば、別のガーディアンをコンマで名前などの`'EAST-US Datacenter', 'EMEA Datacenter'`します。
ボリュームの ID 修飾子では、正確なバージョンのテンプレート ディスク (等しい) のみまたは今後のバージョン (GreaterThanOrEquals) も信頼するかどうかを指定します。
ディスクの名前と署名証明書は、デプロイ時に考慮するバージョンの比較を正確に一致しなければなりません。
1 つ以上のテンプレート ディスクを信頼するには ID の修飾子をボリュームのコンマ区切りの一覧を提供することで、`-VolumeIDQualifier`パラメーター。
最後に、その他の操作をした場合は、ファイル、VM を使用して、応答ファイルに付随する必要がある、`-OtherFile`パラメーター ファイルのパスのコンマ区切りの一覧を指定します。

コマンドレットのドキュメントを参照して[新規 ShieldingDataFile](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-ShieldingDataFile?view=win10-ps)と[新規 VolumeIDQualifier](https://docs.microsoft.com/powershell/module/shieldedvmdatafile/New-VolumeIDQualifier?view=win10-ps)するシールド データ ファイルを構成するその他の方法について説明します。

## <a name="see-also"></a>関連項目

- [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
