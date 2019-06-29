---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: オンプレミスに VM と保護されたファブリックに移動してテナント - 新しいを作成するためのシールドされた Vm のシールドされました。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9601145048b8798cfb102757384da49bed16a538
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469624"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>オンプレミスに VM と保護されたファブリックに移動してテナント - 新しいを作成するためのシールドされた Vm のシールドされました。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、HYPER-V のみ; を使用して、シールドされた VM を作成する手順を説明しますつまり、Virtual Machine Manager、テンプレート ディスク、またはシールド データ ファイルのないです。 ホスティング環境では、ほとんどのパブリック クラウドの一般的ではないシナリオは、これが、保護されたファブリックをテストするときに便利な場合があります、または企業内に部門別のファブリックから VM の移動先のシナリオが IT インフラストラクチャを共有し、移行する前に暗号化する必要があります。

このトピックがシールドされた Vm の展開の全体的なプロセスがどのように適合するしくみを理解するのを参照してください。[保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしている](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)します。

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>テナント、HYPER-V サーバー上のガーディアンの構成をインポートします。

1.  プロシージャを開始する前に、HYPER-V ホストが次の役割と機能がインストールされている Windows Server 2016 を実行しているいることを確認します。

    - ロール

        - Hyper-V

    - 機能

        - リモート サーバー管理ツール\\機能管理ツール\\のシールドされた VM ツール

    > [!NOTE]
    > ここで使用されるホストにする必要があります*いない*で保護されたファブリック ホストであります。 これは、個別のホストが保護されたファブリックに移動して Vm を準備する場所です。

2.  シールドされた VM を実行するにはこのコンピューターで、前に仮想化ベースのセキュリティが有効で実行されていることを確認する必要があります。 Host Guardian HYPER-V サポート機能をインストールする管理者特権の Windows PowerShell ウィンドウで、次のコマンドを実行します。 シールドされた Vm を実行できるマシン上のすべての必要な設定に設定されます。

        Install-WindowsFeature HostGuardian

3.  VM が実行される場所、保護されたファブリックのガーディアン メタデータを取得する必要があります。 このメタデータは、シールドされた VM を実行するには、そのファブリックを承認するために使用されます。 この情報を取得する方法は、ホスティング サービス プロバイダーまたはエンタープライズごとに異なるになります。 ホスト側 (またはする保護されたファブリック ネットワークにアクセスできる場合) は、次の Windows PowerShell コマンドを実行してこの情報を入手できます。

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    上記の例では"hgs"は、HGS クラスターの分散ネットワーク名と"bastion.local"は、HGS ドメインの名前です。

4.  これ以降の手順で必要になります、ガーディアン キーをインポートするには、次のコマンドを実行します。

    &lt;パス&gt;&lt;Filename&gt;ファイル、XML のファイル名やパスに置き換えてくださいたとえば前の手順で保存します。**C:\\temp\\GuardianKey.xml**

    &lt;GuardianName&gt;、ホスティング プロバイダーまたはエンタープライズ データ センターの名前を指定する例: **HostingProvider1**します。 次の手順の名前を記録します。

    含める **- AllowUntrustedRoot** HGS サーバーは、自己署名証明書を使用して設定された場合にのみです。 (これらの証明書で HGS キー保護サービスの一部です)。

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>ホスト上の新しいシールドされた仮想マシンの作成します。

この手順では、HYPER-V ホストでは、仮想マシンを作成し、ホスティング プロバイダーやデータ センター管理者は、保護されたホストで実行できますへのエクスポート用に準備します。

手順の一環として、2 つの重要な要素を含むキー プロテクターを作成します。

-   **所有者**:または多くの場合、証明書などのセキュリティ要素を共有するで作業するグループ、キー プロテクターでは、VM の「所有者」として識別されます。 所有者として自分の id は、自己署名証明書として示すように、コマンドを実行する場合に生成される証明書によって表されます。 必要に応じて、代わりに、PKI インフラストラクチャによって証明書を使用して省略、 **- AllowUntrustedRoot**コマンドのパラメーター。

-   **Guardians**:キー プロテクターでは、ホスティング プロバイダーまたはエンタープライズ データ センター (これは、HGS を実行して、保護されたホスト) として識別されます「ガーディアン」 前の手順でインポートしたガーディアン キーによって表されるガーディアン[テナント、HYPER-V サーバー上のガーディアンの構成をインポート](#import-the-guardian-configuration-on-the-tenant-hyper-v-server)します。

シールド データ ファイル内の要素には、キーの保護機能を示す図解は、次を参照してください。[シールド データを使用するものが、なぜ必要ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)します。

1. HYPER-V ホスト、テナントで新しい第 2 世代仮想マシンを作成する次のコマンドを実行します。

   &lt;ShieldedVMname&gt;、たとえば、VM の名前を指定します。**ShieldVM1**
    
   &lt;VHDPath&gt;、たとえば、VM の VHDX を格納する場所を指定します。**C:\\Vm\\ShieldVM1\\ShieldVM1.vhdx**
    
   &lt;NnGB&gt;、たとえば、VHDX のサイズを指定します。**60 GB**

       New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2. サポートされているオペレーティング システムをインストール (Windows Server 2012 以降、Windows 8 クライアント以上)、VM で、リモート デスクトップ接続と対応するファイアウォール規則を有効にするとします。 VM の IP アドレスや DNS 名を記録します。リモート接続に必要になります。

3. RDP を使用して、リモート VM に接続し、RDP とファイアウォールが正しく構成されていることを確認します。 シールドのプロセスの一環として、HYPER-V によって仮想マシンへのコンソール アクセスは無効になります、ため、ネットワーク経由でシステムをリモートで管理できることを確認することが重要です。

4. (このセクションの冒頭に示した) 新しいキー プロテクターを作成するには、次のコマンドを実行します。

   &lt;GuardianName&gt;、たとえば、前の手順で指定した名前を使用します。**HostingProvider1**

   含める **- AllowUntrustedRoot**自己署名証明書を許可します。

       $Guardian = Get-HgsGuardian -Name '<GuardianName>'

       $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

       $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

   1 つ以上のデータ センターのシールドされた VM (たとえば、ディザスター リカバリー サイトおよびパブリック クラウド プロバイダー) を実行できるようにする場合に保護者の一覧を行うことができます、 **-ガーディアン**パラメーター。 詳細については、[新規 HgsKeyProtector] を参照してください (https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-ps します。

5. キーの保護機能を使用して vTPM を有効にするには、次のコマンドを実行します。 &lt;ShieldedVMname&gt;、前の手順で使用される同じ VM 名を使用します。

       $VMName="<ShieldedVMname>"

       Stop-VM -Name $VMName -Force

       Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

       Set-VMSecurityPolicy -VMName $VMName -Shielded $true

       Enable-VMTPM -VMName $VMName

6. ローカルの所有者の証明書とキー保護機能が動作していることを確認するには、次のように VM を開始するには、次のコマンドを実行します。

       Start-VM -Name $VMName

7. VM を HYPER-V コンソールで開始されたことを確認します。

8. リモート VM に接続し、シールドされた VM にアタッチされているすべての Vhdx のすべてのパーティションで BitLocker を有効にするには、RDP を使用します。

   > [!IMPORTANT]
   > 次の手順に進む前に BitLocker 暗号化を有効にした、すべてのパーティションに終了するまで待ちます。

9. 保護されたファブリックに移動する準備ができたら、VM をシャット ダウンします。

10. テナント、HYPER-V サーバーでは、(Windows PowerShell または HYPER-V マネージャー) に好みのツールを使用して VM をエクスポートします。 ホスティング プロバイダーまたはエンタープライズ データ センターによって管理される保護されたホストにコピーするファイルを配置します。

11. **ホスティング プロバイダーまたはエンタープライズ データ センターの**:

    HYPER-V マネージャーまたは Windows PowerShell を使用して、シールドされた VM をインポートします。 VM を起動するには、VM 所有者から VM の構成ファイルをインポートする必要があります。 これは、キー保護機能と、VM の仮想 TPM が構成ファイルに格納されているためにです。 保護されたファブリック上で実行する VM を構成する場合、正常に起動できる必要があります。

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしています。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
