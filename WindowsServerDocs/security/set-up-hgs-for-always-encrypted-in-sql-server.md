---
title: SQL Server の Always Encrypted のホストガーディアンサービスの設定
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 5d1396f609a425adcd87a41d3469f3aa55774851
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402278"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>SQL Server で secure enclaves を使用して Always Encrypted のホストガーディアンサービスを設定する 

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、SQL Server 2019 preview
 
SQL Server 2019 preview での[secure enclaves による Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves)は、データベースに格納されている機密データに対して機密計算を行うことができるように設計された機能です。 ホストガーディアンサービス (HGS) は、Always Encrypted 用に構成されたセキュリティ保護されたエンクレーブが、仮想化ベースのセキュリティ (VBS) メモリエンクレーブである場合に、データの安全性を維持するうえで重要な役割を果たします。 VBS メモリエンクレーブのセキュリティは、Windows ハイパーバイザーのセキュリティ、および SQL Server をホストしているコンピューターのセキュリティに大きく依存します。 

そのため、データベースクライアントアプリケーションで、Always Encrypted に使用される VBS メモリエンクレーブが機微なデータに対して計算を実行することを許可する前に、アプリケーションは信頼された HGS で証明する必要があります。 構成証明は、エンクレーブを含む SQL Server をホストするマシンが正しい状態であり、信頼できることを証明します。 このトピックの残りの部分では、ホストコンピューターとして SQL Server をホストしているコンピューターを参照します。

アプリケーションでは、次の2つの相互排他的な方法で証明することができます。 

- ホストキーの構成証明は、既知の信頼された秘密キーを所有していることを証明することで、ホストを承認します。 運用前環境では、ホストキーの構成証明と、SQL Server を実行している第2世代仮想マシンのどちらかを使用することをお勧めします。
- TPM 構成証明は、ホストが正しいバイナリとセキュリティポリシーのみを実行するように、ハードウェアの測定を検証します。 運用環境では、TPM 構成証明と、SQL Server を実行する物理ホストコンピューター (仮想マシンではない) を使用することをお勧めします。

ホストガーディアンサービスとその使用方法の詳細については、「保護された[ファブリックとシールド](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)された vm の概要」を参照してください。 ドキュメントではシールドされた Vm について説明していますが、VBS enclaves を使用して Always Encrypted SQL Server には、同じ保護、アーキテクチャ、およびベストプラクティスが適用されることに注意してください。 

この記事では、推奨される構成で HGS を設定する方法について説明します。 

## <a name="prerequisites"></a>前提条件 

このセクションでは、HGS とホストコンピューターの前提条件について説明します。 

### <a name="hgs-servers"></a>HGS サーバー

- 1-3 HGS を実行するサーバー。 

  > [!NOTE]
  > テスト環境または実稼働前環境には、1つの HGS サーバーのみが必要です。

  これらのサーバーは、セキュリティで保護された enclaves で Always Encrypted を使用して SQL Server インスタンスを実行できるコンピューターを制御するため、慎重に保護する必要があります。 
  異なる管理者が HGS クラスターを管理し、インフラストラクチャの他の部分から分離された物理ハードウェアで HGS を実行することをお勧めします。または、個別の仮想化ファブリックまたは Azure サブスクリプションを使用することをお勧めします。

  - Windows Server 2019 Standard または Datacenter edition。
  - 2 Cpu
  - 8 GB の RAM
  - 100 GB のストレージ

  [長期的なサービスチャネル (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc)または[半期チャネル](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)のいずれかを使用できます。 
  Windows Server Insider Preview を登録してダウンロードするには、「 [Windows Insider プログラム](https://insider.windows.com/for-business-getting-started-server/)の概要」を参照してください。

- ホストガーディアンサービスによって作成された新しい Active Directory フォレストの名前を選択します。 
  HGS を既存の企業ドメインに参加させることはできません。また、別の管理者を管理する必要があります。   

- 次のホストガーディアンサービスノードで受信 HTTP (TCP 80) または HTTPS (TCP 443) トラフィックを許可するファイアウォールとルーティング規則: 

  - を実行しているコンピューター SQL Server
  - データベースクエリを実行し、セキュリティで保護された enclaves で Always Encrypted を使用する、データベースクライアントアプリケーション (web サーバーなど) を実行しているコンピューター。 

### <a name="sql-server-host-machines"></a>ホストマシンの SQL Server

- SQL Server インスタンスは、次の要件を満たすコンピューター上で実行する必要があります。

  - ウィンドウ 
    - Windows 10 Enterprise、バージョン1809  
    - Windows Server 2019 Datacenter (半期チャネル)、バージョン1809
    - Windows Server 2019 Datacenter
  - 運用環境の物理マシン、またはテスト用の第2世代仮想マシン (Azure では第2世代の Vm がサポートされていないことに注意してください)
  - [SQL Server をインストールするためのハードウェアとソフトウェアの要件](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017)に記載されている一般的な要件。   

  [長期的なサービスチャネル (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc)または[半期チャネル](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)のいずれかを使用できます。 
  Windows Server Insider Preview を登録してダウンロードするには、「 [Windows Insider プログラム](https://insider.windows.com/for-business-getting-started-server/)の概要」を参照してください。

- 選択した構成証明モードに固有の要件:
  - **TPM モード**は最も強力な構成証明モードであり、トラステッドプラットフォームモジュール (tpm) を使用して、ホストコンピューターが (各 TPM からの一意の ID を使用して) データセンターで認識されているかどうかを暗号して検証します。(TPM ベースラインを使用した) 構成と、信頼できるカーネルとユーザーモードコードの実行 (Windows Defender Application Control を使用)。 TPM モードを使用するには、次のハードウェアが必要です。 
    - TPM 2.0 モジュールがインストールされ、有効になっている 
    - Microsoft セキュアブートポリシーでセキュアブートが有効になっている (サードパーティ製セキュアブート CA ポリシーまたはカスタムポリシーを有効にしない)
    - 直接メモリアクセス攻撃を防ぐための IOMMU (Intel VT-d または AMD SR-IOV) 

  - **ホストキーモード**は、非対称キーペア (SSH キーと同様) を使用して、SQL Server を実行するホストコンピューターを識別し、承認します。 このモードは簡単にセットアップでき、特定のハードウェア要件はありませんが、ホストコンピューターで実行されているソフトウェアまたはファームウェアは検証されません。  

TPM に互換性があるかどうかを確認するには、Always Encrypted secure enclaves を使用して SQL Server を実行するホストコンピューターで次のコマンドを実行します。 TPM 構成証明を使用するには、サポートされている SpecVersions の一覧に "2.0" が表示されている必要があります。

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>最初の HGS ノードを設定する 

ホストガーディアンサービスは、3ノードクラスターを使用して高可用性構成で動作します。 他のノードを追加する前に、1つのノードを完全に設定することをお勧めします。 

管理者特権の PowerShell セッションで、次のコマンドをすべて実行します。

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   セキュリティで保護された enclaves の Always Encrypted では、SQL Server を実行するホストコンピューターとデータベースクライアントアプリケーションを実行するコンピューターの両方が、構成証明を必要とするホストコンピューターのみが HGS に接続する必要があります。

4. コンピューターが再起動すると、HGS がインストールされ、Active Directory 構成されたドメインコントローラーもサーバーになります。 
   Active Directory 構成では、ローカルコンピューターの管理者アカウントが Domain Admins グループに追加され、このグループのメンバーだけがドメインコントローラーにサインインできます。
   ドメイン管理者アカウント (たとえば、または local\administrator) administrator@bastion.localを使用してサインインするか、別のドメイン管理者アカウントを作成してサインインし、構成証明サービスを構成します。
   TPM またはホストキーの構成証明を選択し、対応するコマンドを実行する必要があります。 
   HgsServiceName には、選択した DNN を指定します。

   TPM モードの場合:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   ホストキーモードの場合:

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. SQL Server を実行するホストコンピューターが、会社の DNS サーバーから新しい HGS ドメインコントローラーにフォワーダーを設定して、新しい HGS ドメインメンバーの DNS 名を解決できることを確認します。 Windows Server DNS を使用している場合は、組織内の DNS サーバーの管理者特権の PowerShell コンソールで次のコマンドを実行して、条件付きフォワーダーを設定できます。 環境に応じて、以下の Windows PowerShell 構文の名前とアドレスを置き換えます。 さらに HGS ノードを追加した後、このコマンドをもう一度実行してマスターサーバーとして追加します。

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>運用環境のデプロイ用に追加の HGS ノードを設定する

クラスターにノードを追加するには、管理者特権の PowerShell セッションで次のコマンドを実行します。 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. HGS ドメイン名を解決できるように、DNS クライアントリゾルバーをプライマリ HGS サーバーをポイントするように設定します。 デスクトップエクスペリエンスを備えたサーバーを使用している場合は、ネットワークと共有センターで行うことができます。 Server Core では、 **sconfig.cmd**ツールまたはオプション8を使用するか、または **-DnsClientServerAddress を設定**して DNS アドレスを設定できます。 

3. 次に、このサーバーをドメインコントローラーに昇格させます。 このタスクを完了するには、ドメイン管理者の資格情報が必要です。コマンドを実行した後、ディレクトリサービス修復モードのパスワードを入力するように求められます。 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>HTTPS 用に HGS を構成する 

既定では、HGS サーバーを初期化すると、IIS web サイトは HTTP 専用通信用に構成されます。

> [!NOTE]
> よく知られている、信頼された HGS サーバー証明書を使用して HTTPS を構成することは、man-in-the-middle 攻撃を防ぐために必要であり、そのため、運用環境での展開にも推奨されます。

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

> [!NOTE]
> Always Encrypted secure enclaves を使用する場合、SSL 証明書は SQL Server を実行する両方のホストコンピューターで信頼されている必要があり、データベースクライアントアプリケーションを実行するコンピューターでは HGS に接続する必要があります。 

## <a name="collect-attestation-info-from-the-host-machines"></a>ホストコンピューターから構成証明情報を収集する

HGS がセットアップされたら、Always Encrypted および VBS secure enclaves を使用して機密計算を実行することを承認する必要があるコンピューターを認識できるように、ホストコンピューターの構成証明情報を使用して構成する必要があります。 これらの手順は、使用する構成証明モードによって異なります。 

### <a name="collect-tpm-attestation-artifacts"></a>TPM 構成証明アイテムの収集 

TPM モードを使用している場合は、各ホストコンピューターの管理者特権の PowerShell セッションで次のコマンドを実行して、構成証明のサポートをインストールし、ホストガーディアンサービスに登録するために必要な情報を収集します。 

1. ホストコンピューターに HGS クライアントをインストールするには、保護されたホスト機能をインストールします。これにより、Hyper-v もインストールされます。 
   このマシンで Vm を実行するのではなく、VBS enclaves を分離する仮想化ベースのセキュリティ機能を有効にするには、ハイパーバイザーが必要です。

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v のインストールを完了するように求められたら、コンピューターを再起動します。 
3. システムで実行できるソフトウェアを制限するコード整合性ポリシーを作成します。 
   すべての Windows Defender Application Control ポリシーで十分です。 
   サーバー上で Microsoft ソフトウェアのみを実行している場合は、次のコマンドを使用すると、ポリシーがすぐに作成されます。 
   ポリシーは監査モードになります。つまり、未承認のコードに関するイベントがログに記録されますが、実行されません。  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Windows Defender Application Control には、さまざまなセキュリティの強化に対応する多くの機能があります。 
   Microsoft 以外のソフトウェアを許可するか、既定のポリシーをカスタマイズする必要がある場合は、 [Windows Defender Application Control 展開ガイド](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)を参照してください。   


4. 次のコマンドを使用して、仮想化ベースのセキュリティがコンピューター上で実行されていることを確認します。 
   デバイスに "HypervisorEnforcedCodeIntegrity" というフィールドがある場合、VBS は実行されていることがわかります。 
   実行されていない場合は、 [Device Guard 準備ツール](https://www.microsoft.com/download/details.aspx?id=53337)をダウンロードし、"DG_Readiness-ENABLE-hvci" を実行して有効にします。  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```

5. TPM 識別子とベースラインを収集します。

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. Xml、tcglog、および bin ファイルを C:\ アーティファクトから HGS サーバーにコピーします。
7. これが HGS サーバーに追加している最初の TPM ホストである場合は、各 HGS サーバーに信頼された TPM ルート証明書をインストールする必要があります。 
   この手順を実行するには[、HGS のドキュメントに](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates)記載されているガイダンスに従ってください。
8. HGS サーバーで、このホストが構成証明を通過することを承認します。 
   次のスクリプトでは、3つのファイルが HGS サーバーの C:\temp にコピーされており、サーバーのコンピューター名が "ServerA" であることを前提としています。 
   実際の環境に合わせてパスと名前を調整します。 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```

9. これで、最初のサーバーを証明する準備ができました。 
   ホストコンピューターで次のコマンドを実行して、証明する場所を確認します (DNS 名は HGS クラスターのものに変更します。通常は hgs サービス名を HGS ドメイン名と組み合わせて使用します)。 
   HostUnreachable 不能なエラーが発生した場合は、HGS サーバーの DNS 名を解決し、ping を実行できることを確認してください。 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. 上記のコマンドの結果は、AttestationStatus = が渡されたことを示しています。 そうでない場合は、エラーの解決方法について、「[構成証明の失敗](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures)」を参照してください。   
11. 各ホストコンピューターに対して手順1-10 を繰り返します。 
    同一のハードウェアを使用している場合は、すべてのコンピューターの新しい基準または CI ポリシーをキャプチャする必要はありません。 
    最初のサーバーのベースラインは、同じように構成されたすべてのコンピューターを対象とします。また、コンピューター上のソフトウェアが Microsoft ソフトウェアだけである限り、CI ポリシーは複数のコンピューターで再利用できます。

### <a name="collecting-host-keys"></a>ホストキーの収集 

> [!NOTE] 
> ホストキーの構成証明は、テスト環境での使用に対してのみ推奨されます。 TPM 構成証明により、SQL Server 上の機密データを処理する VBS enclaves が信頼されたコードを実行していること、および推奨されるセキュリティ設定でコンピューターが構成されていることが、最も強力な保証を提供します 

ホストキーの構成証明モードで HGS を設定することを選択した場合は、各ホストコンピューターからキーを生成して収集し、ホストガーディアンサービスに登録する必要があります。 

1. ホストコンピューターにインストールされている HGS クライアントを取得するには、保護されたホスト機能をインストールします。これにより、Hyper-v もインストールされます。 
   このマシンで Vm を実行するのではなく、Always Encrypted クエリを実行する VBS enclaves を分離する仮想化ベースのセキュリティ機能を有効にするには、ハイパーバイザーが必要です。 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. Hyper-v のインストールを完了するように求められたら、コンピューターを再起動します。
3. 一意のホストキーを生成し、生成された公開キーをファイルにエクスポートします。 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   また、独自の証明書を使用する場合は、拇印を指定することもできます。 
   これは、複数のコンピューターで証明書を共有する場合や、TPM または HSM にバインドされた証明書を使用する場合に便利です。 次に、TPM バインド証明書を作成する例を示します。これにより、秘密キーが盗まれて別のコンピューターで使用され、TPM 1.2 のみが必要になります。

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. ホストキーをホストガーディアンサービスにコピーします。 
5. 環境に関連する名前とパスを使用して、ホストキーを任意の HGS ノードに登録します。 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. これで、最初のサーバーを証明する準備ができました。 
   ホストコンピューターで次のコマンドを実行して、証明する場所を確認します (DNS 名は HGS クラスターのものに変更します。通常は hgs サービス名を HGS ドメイン名と組み合わせて使用します)。 
   HostUnreachable 不能なエラーが発生した場合は、HGS サーバーの DNS 名を解決し、ping を実行できることを確認してください。    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. 上記のコマンドの結果は、AttestationStatus = が渡されたことを示しています。 
   HostUnreachable 不能なエラーが発生した場合は、ホストコンピューターが HGS と通信できないことを意味します。 
   ホストコンピューターと HGS サーバーの間で DNS 解決が設定されていること、およびサーバーに対して ping を実行できることを確認します。 
   UnauthorizedHost エラーは、公開キーが HGS サーバーに登録されていないことを示します。エラーを解決するには、手順4と5を繰り返します。 
   それ以外の場合は、HgsClientHostKey を実行し、手順3-6 を繰り返します。   

8. VBS enclaves を使用して Always Encrypted SQL Server を実行する各サーバーについて、手順1-7 を繰り返します。     


