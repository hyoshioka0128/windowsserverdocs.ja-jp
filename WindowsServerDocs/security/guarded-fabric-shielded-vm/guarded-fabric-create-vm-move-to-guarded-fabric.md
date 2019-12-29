---
redirect_url: guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md
title: テナント用のシールドされた Vm-オンプレミスで新しいシールドされた VM を作成し、保護されたファブリックに移動する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 0ca1efa0-01f9-4b6f-87d4-c66db00d7d70
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: a4b5ff2942c8485a4c10770a4374d56734f7f3c9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402382"
---
# <a name="shielded-vms-for-tenants---creating-a-new-shielded-vm-on-premises-and-moving-it-to-a-guarded-fabric"></a>テナント用のシールドされた Vm-オンプレミスで新しいシールドされた VM を作成し、保護されたファブリックに移動する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Hyper-v のみを使用してシールドされた VM を作成する手順について説明します。つまり、Virtual Machine Manager、テンプレートディスク、またはシールドデータファイルがありません。 これは、ほとんどのパブリッククラウドホスティング環境では一般的ではありませんが、保護されたファブリックをテストする場合や、VM が部門ファブリックから共有 IT インフラストラクチャに移動され、移行の前に暗号化する必要がある場合に便利です。

このトピックがシールドされた Vm のデプロイプロセス全体にどのように適合するかを理解するには、「保護された[ホストとシールドされた vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)」を参照してください。

## <a name="import-the-guardian-configuration-on-the-tenant-hyper-v-server"></a>テナント Hyper-v サーバーでガーディアン構成をインポートする

1.  手順を開始する前に、次の役割と機能がインストールされた Windows Server 2016 を実行している Hyper-v ホストを使用していることを確認してください。

    - ロール

        - Hyper-V

    - 機能

        - シールドされた VM ツール\\\\機能管理ツールリモートサーバー管理ツール

    > [!NOTE]
    > ここで使用するホストは、保護されたファブリック内のホストにすることはでき*ません*。 これは、保護されたファブリックに移行する前に Vm を準備する独立したホストです。

2.  このマシンでシールドされた VM を実行する前に、仮想化ベースのセキュリティを有効にして実行する必要があります。 管理者特権の Windows PowerShell ウィンドウで次のコマンドを実行して、Host Guardian Hyper-v サポート機能をインストールします。 これにより、シールドされた Vm を実行できるように、コンピューターで必要なすべての設定が構成されます。

        Install-WindowsFeature HostGuardian

3.  VM が実行される保護されたファブリックのガーディアンメタデータを取得する必要があります。 このメタデータを使用して、シールドされた VM を実行するようにファブリックを承認します。 この情報の取得方法は、ホスティングサービスプロバイダーまたはエンタープライズごとに異なります。 ホスト (または、保護されたファブリックネットワークにアクセスできる場合) は、次の Windows PowerShell コマンドを実行して、この情報を取得できます。

        Invoke-WebRequest 'http://hgs.bastion.local/KeyProtection/service/metadata/2014-07/metadata.xml' -OutFile .\RelecloudGuardian.xml

    上記の例では、"hgs" は HGS クラスターの分散ネットワーク名、"要塞. local" は HGS ドメインの名前です。

4.  後の手順で必要になるガーディアンキーをインポートするには、次のコマンドを実行します。

    &lt;パス&gt;&lt;Filename&gt;には、前の手順で保存した XML ファイルのパスとファイル名を置き換えます。例: **C:\\temp\\GuardianKey**

    &lt;GuardianName&gt;には、ホスティングプロバイダーまたはエンタープライズデータセンターの名前を指定します。たとえば、「 **HostingProvider1**」と指定します。 次の手順の名前を記録します。

    **-Allowuntrustedroot**は、HGS サーバーが自己署名証明書を使用して設定されている場合にのみ含めます。 (これらの証明書は、HGS のキー保護サービスの一部です)。

        Import-HgsGuardian -Path '<Path><Filename>' -Name '<GuardianName>' -AllowUntrustedRoot

## <a name="create-a-new-shielded-virtual-machine-on-the-host"></a>新しいシールドされたバーチャルマシンをホスト上に作成します

この手順では、Hyper-v ホスト上に仮想マシンを作成し、ホストプロバイダーまたはデータセンター管理者が保護されたホストで実行できるように、その仮想マシンをエクスポートするための準備を行います。

この手順の一部として、次の2つの重要な要素を含むキープロテクターを作成します。

-   **所有者**: キー保護機能では、証明書などのセキュリティ要素を共有するグループが、VM の "所有者" として識別されます。 所有者としての id は、証明書によって表されます。これは、示されているようにコマンドを実行すると、自己署名証明書として生成されます。 必要に応じて、PKI インフラストラクチャでサポートされている証明書を使用し、コマンドで **-allowuntrustedroot**パラメーターを省略することもできます。

-   **ガーディアン**: キープロテクターでも、ホスティングプロバイダーまたはエンタープライズデータセンター (HGS と保護されたホストを実行) が "ガーディアン" として識別されます。 ガーディアンは、前の手順でインポートしたガーディアンキーによって表され、[テナント hyper-v サーバーでガーディアン構成をインポート](#import-the-guardian-configuration-on-the-tenant-hyper-v-server)します。

シールドデータファイルの要素であるキープロテクターの例については、「[シールドデータとは何ですか?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)」を参照してください。

1. テナント Hyper-v ホストで、新しい第2世代仮想マシンを作成するには、次のコマンドを実行します。

   &lt;ShieldedVMname&gt;の場合は、VM の名前を指定します (例: **ShieldVM1** )。
    
   &lt;VHDPath&gt;では、VM の VHDX を格納する場所を指定します。例: **C:\\VMs\\ShieldVM1\\ShieldVM1**
    
   &lt;nnGB&gt;の場合は、VHDX のサイズを指定します (例: **60GB** )。

       New-VM -Generation 2 -Name "<ShieldedVMname>" -NewVHDPath <VHDPath>.vhdx -NewVHDSizeBytes <nnGB>

2. サポートされているオペレーティングシステム (Windows Server 2012 以降、Windows 8 クライアント以降) を VM にインストールし、リモートデスクトップ接続とそれに対応するファイアウォール規則を有効にします。 VM の IP アドレスまたは DNS 名を記録します。これは、リモート接続に必要です。

3. RDP を使用して VM にリモート接続し、RDP とファイアウォールが正しく構成されていることを確認します。 シールドプロセスの一環として、Hyper-v を介したバーチャルマシンへのコンソールアクセスは無効になります。そのため、ネットワーク経由でシステムをリモートで管理できるようにすることが重要です。

4. 新しいキー保護機能を作成するには (このセクションの冒頭で説明)、次のコマンドを実行します。

   &lt;GuardianName&gt;の場合は、前の手順で指定した名前を使用します。たとえば、「 **HostingProvider1** 」と指定します。

   自己署名証明書を許可するには **、-allowuntrustedroot**を含めます。

       $Guardian = Get-HgsGuardian -Name '<GuardianName>'

       $Owner = New-HgsGuardian -Name 'Owner' -GenerateCertificates

       $KP = New-HgsKeyProtector -Owner $Owner -Guardian $Guardian -AllowUntrustedRoot

   複数のデータセンターでシールドされた VM (ディザスターリカバリーサイトやパブリッククラウドプロバイダーなど) を実行できるようにする場合は、 **-ガーディアン**パラメーターにガーディアンの一覧を指定できます。 詳細については、[HgsKeyProtector] (https://docs.microsoft.com/powershell/module/hgsclient/new-hgskeyprotector?view=win10-psを参照してください。

5. キー保護機能を使用して vTPM を有効にするには、次のコマンドを実行します。 &lt;ShieldedVMname&gt;については、前の手順で使用したのと同じ VM 名を使用してください。

       $VMName="<ShieldedVMname>"

       Stop-VM -Name $VMName -Force

       Set-VMKeyProtector -VMName $VMName -KeyProtector $KP.RawData

       Set-VMSecurityPolicy -VMName $VMName -Shielded $true

       Enable-VMTPM -VMName $VMName

6. VM を起動して、キープロテクターがローカル所有者の証明書を使用して動作していることを確認するには、次のコマンドを実行します。

       Start-VM -Name $VMName

7. Hyper-v コンソールで VM が開始されていることを確認します。

8. RDP を使用して VM にリモート接続し、シールドされた VM に接続されているすべての Vhdx のすべてのパーティションで BitLocker を有効にします。

   > [!IMPORTANT]
   > 次の手順に進む前に、有効にしたすべてのパーティションで BitLocker 暗号化が終了するのを待ちます。

9. 保護されたファブリックに VM を移動する準備ができたら、VM をシャットダウンします。

10. テナント Hyper-v サーバーで、任意のツール (Windows PowerShell または Hyper-v マネージャー) を使用して VM をエクスポートします。 次に、ホスティングプロバイダーまたはエンタープライズデータセンターによって管理されている保護されたホストにコピーするファイルを配置します。

11. **ホスティングプロバイダーまたはエンタープライズデータセンターの場合**:

    Hyper-v マネージャーまたは Windows PowerShell を使用して、シールドされた VM をインポートします。 Vm を起動するには、vm の所有者から vm 構成ファイルをインポートする必要があります。 これは、キープロテクターと VM の仮想 TPM が構成ファイルに格納されているためです。 保護されたファブリック上で実行するように VM が構成されている場合は、正常に起動できる必要があります。

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
