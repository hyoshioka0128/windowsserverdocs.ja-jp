---
title: SQL Server で Always Encrypted のホスト ガーディアン サービスの設定
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/03/2018
ms.openlocfilehash: 2f800dfa01077287f8200dd8abea0be899776683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866693"
---
# <a name="setting-up-the-host-guardian-service-for-always-encrypted-with-secure-enclaves-in-sql-server"></a>SQL Server のセキュリティで保護された enclaves での Always Encrypted のホスト ガーディアン サービスの設定 

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、SQL Server 2019 プレビュー
 
[セキュリティで保護された enclaves で always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves)プレビューはデータベースに格納されている機密データの機密情報の計算を有効にするように設計機能で SQL Server 2019 です。 ホスト ガーディアン サービス (HGS) は、Always encrypted の構成、セキュリティで保護されたエンクレーブが仮想化ベースのセキュリティ (VBS) のメモリ エンクレーブにデータを安全に保つための重要な役割を果たします。 VBS メモリのエンクレーブのセキュリティは、Windows ハイパーバイザーのセキュリティより広い意味で、SQL Server をホストするコンピューターのセキュリティに依存します。 

そのため、データベースのクライアント アプリケーションでは、Always Encrypted の機密データに対して計算を実行するために使用する VBS メモリ エンクレーブを許可する前にアプリケーションが信頼された HGS を証明する必要があります。 構成証明書は、エンクレーブを含む、適切な状態で、信頼できる SQL Server をホストするコンピューターを証明します。 このトピックの残りの部分として、ホスト コンピューターでは単に SQL Server をホストするコンピューターに言及します。

2 つは、相互に排他的な方法とアプリケーション。 

- ホスト キーの構成証明はホストを承認証明既知または信頼された秘密キーを所有しています。 ホスト キーの構成証明と、物理ホスト コンピューターまたは SQL Server を実行する第 2 世代仮想マシンは、実稼働前環境をお勧めします。
- TPM 構成証明は、ホスト、適切なバイナリとセキュリティ ポリシーの実行を確認するハードウェアの測定値を検証します。 TPM 構成証明と SQL Server を実行している物理ホスト コンピューター (仮想マシンではなく) は、運用環境ではお勧めします。

ホスト ガーディアン サービスと測定できる内容の詳細については、次を参照してください。[保護され、fabric と、Vm の概要をシールドされた](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)します。 ドキュメントは、シールドされた Vm について説明、ですが、同じ保護機能、アーキテクチャとベスト プラクティスに適用される SQL Server 使用して Always Encrypted VBS enclaves に注意してください。 

この記事では推奨される構成では、HGS をセットアップできます。 

## <a name="prerequisites"></a>前提条件 

このセクションでは、HGS とホスト マシンの前提条件について説明します。 

### <a name="hgs-servers"></a>HGS サーバー

- HGS を実行する 1 ~ 3 のサーバー。 

  >[!NOTE]
  >HGS サーバーが 1 つだけでは、テストまたは実稼働前環境必要があります。

  これらのサーバーは、どのコンピューターがセキュリティで保護された enclaves で Always Encrypted を使用して、SQL Server インスタンスを実行を制御するので慎重に保護する必要があります。 
  別の管理者が HGS クラスターを管理し、または別の仮想化ファブリックまたは Azure サブスクリプションでは、インフラストラクチャの残りの部分から分離された物理ハードウェアでは、HGS を実行することをお勧めします。

  - Windows Server 2019 Standard または Datacenter エディションです。
  - 2 つの Cpu
  - 8 GB の RAM
  - 100 GB ストレージ

  いずれかを使用することができます、[長期的なサービス チャネル (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc)または[半期チャネル](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)します。 
  登録を Windows Server Insider プレビューのダウンロードは、次を参照してください。 [Windows Insider Program の概要](https://insider.windows.com/for-business-getting-started-server/)します。

- ホスト ガーディアン サービスによって作成された新しい Active Directory フォレストの名前を選択します。 
  HGS に既存の会社のドメインに参加していない必要があり、それを管理する個別の管理者が必要です。   

- ファイアウォールとホスト ガーディアン サービスのノードで受信 HTTP (TCP 80) または HTTPS (TCP 443) トラフィックを許可するルーティング規則: 

  - SQL Server を実行するコンピューター
  - データベース クエリを発行してセキュリティで保護された enclaves で Always Encrypted を使用する (web サーバーなど) データベースのクライアント アプリケーションを実行するコンピューター。 

### <a name="sql-server-host-machines"></a>SQL Server ホスト マシン

- SQL Server インスタンスは、次の要件を満たしているコンピューターで実行する必要があります。

  - Windows: 
    - Windows 10 Enterprise、バージョンは 1809  
    - Windows Server 2019 Datacenter (半期チャネル) バージョンは 1809
    - Windows Server 2019 Datacenter
  - 運用環境、または (Azure では、第 2 世代 Vm はサポートされていないことに注意してください) をテストするための第 2 世代仮想マシンの物理マシン
  - 一般的な要件が記載[Hardware and Software Requirements for SQL Server のインストール](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017)します。   

  いずれかを使用することができます、[長期的なサービス チャネル (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc)または[半期チャネル](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#semi-annual-channel)します。 
  登録を Windows Server Insider プレビューのダウンロードは、次を参照してください。 [Windows Insider Program の概要](https://insider.windows.com/for-business-getting-started-server/)します。

- 選択した構成証明モードに固有の要件:
  - **TPM モード**最強レベルの構成証明モードと、暗号によって、ホスト マシンが正常で、データ センターを (各 TPM から一意の ID を使用)、信頼されているハードウェアおよびファームウェアを実行していることを検証する信頼されたプラットフォーム モジュール (TPM) を使用構成 (TPM ベースラインを使用)、trustworthy カーネルと (Windows Defender Application Control を使用して) ユーザー モード コードを実行しているとします。 TPM のモードを使用して、次のハードウェアが必要です。 
    - TPM 2.0 モジュールをインストールし、有効になっています。 
    - セキュア ブートと Microsoft セキュア ブートのポリシーが有効 (有効にしないサード パーティ製のセキュア ブートの CA ポリシーやカスタム ポリシー)
    - ほとんどサポート (Intel vt-d や IOV の AMD) ダイレクト メモリ アクセスの攻撃を防ぐこと 

  - **ホスト キー モード**(非常によく似た SSH キー)、非対称キー ペアを使用して、SQL Server を実行するホスト コンピューターの承認を識別します。 このモードが簡単にセットアップして、特定のハードウェア要件はありませんは、ソフトウェアまたはファームウェアのホスト コンピューターで実行されていることを確認できません。  

TPM に互換性があるかを確認するにセキュリティで保護された enclaves で Always Encrypted を使用して SQL Server を実行するホスト コンピューターで、次のコマンドを実行します。 「2.0」TPM 構成証明を使用するためのサポートされている SpecVersions の一覧で表示する必要があります。

```powershell
Get-CimInstance -ClassName Win32_Tpm -Namespace root/cimv2/Security/MicrosoftTpm 
```

## <a name="set-up-the-first-hgs-node"></a>HGS の最初のノードを設定します。 

ホスト ガーディアン サービスは、3 ノード クラスターを使用して高可用性構成では動作します。 設定する 1 つのノード完全に他のノードを追加する前にお勧めします。 

管理者特権の PowerShell セッションでは、すべての次のコマンドを実行します。

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. [!INCLUDE [Install HGS by default](../../includes/install-hgs-default.md)] 

3. [!INCLUDE [Determine a DNN](../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

   セキュリティで保護された enclaves で Always encrypted では、SQL Server とマシンを実行しているホスト コンピューターは、database クライアント アプリケーションがホスト マシンのみが構成証明が必要ですが、HGS にお問い合わせください両方必要がありますを実行します。

4. マシンの再起動後は、HGS がインストールされ、サーバーは構成されている Active Directory とドメイン コント ローラーにもなります。 
   Active Directory の構成中に、ローカル コンピューターの管理者アカウントは、Domain Admins グループに追加され、このグループのメンバーだけがドメイン コント ローラーにサインインできます。
   ドメイン管理者アカウントを使用してサインイン (たとえば、administrator@bastion.localまたは bastion.local\administrator) の別のドメイン管理者アカウントを作成またはサインインし、構成証明サービスを構成します。
   TPM] または [ホスト キーの構成証明を選択し、対応するコマンドを実行する必要があります。 
   HgsServiceName した DNN を指定します。

   TPM のモード。
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustTpm
   ```

   ホスト キーのモード。
   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey 
   ```

5. SQL Server を実行するホスト コンピューターは、企業の DNS サーバーから新しい HGS のドメイン コント ローラーのフォワーダーを設定して、新しい HGS ドメイン メンバーの DNS 名を解決できることを確認します。 Windows Server DNS を使用している場合は、管理者特権で PowerShell コンソールで、組織内の DNS サーバーで、次のコマンドを実行して、条件付きフォワーダーを設定できます。 名前と、環境に応じて以下の Windows PowerShell 構文内のアドレスに置き換えてください。 HGS ノードを追加した後は、マスター サーバーとして追加するには、もう一度このコマンドを実行します。

   ```powershell
   Add-DnsServerConditionalForwarderZone -Name <HGS domain name> -ReplicationScope "Forest" -MasterServers <IP addresses of HGS servers>
   ```

## <a name="set-up-additional-hgs-nodes-for-production-deployments"></a>運用環境のデプロイの追加の HGS ノードを設定します。

クラスターにノードを追加するには、管理者特権の PowerShell セッションで、次のコマンドを実行します。 

1. [!INCLUDE [Install the HGS server role](../../includes/guarded-fabric-install-hgs-server-role.md)]

2. プライマリ HGS サーバーを指す、HGS のドメイン名を解決できるように DNS クライアント リゾルバーを設定します。 デスクトップ エクスペリエンス搭載サーバーを使用する場合は、ネットワークと共有センターでこれを実行できます。 Server Core で使用することができます、 **sconfig.exe**ツールでオプションを 8、または**Set-dnsclientserveraddress** DNS アドレスを設定します。 

3. 次に、このサーバーをドメイン コント ローラーに昇格されます。 このタスクを実行するドメイン管理者の資格情報は必要があり、コマンドを実行した後はディレクトリ サービス復元モード パスワードの入力を求められます。 

   ```powershell
   $HgsDomainName = 'bastion.local' 
   $HgsDomainCredential = Get-Credential 
 
   Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $HgsDomainCredential -Restart 
   ```

4. [!INCLUDE [Initialize HGS](../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="configure-hgs-for-https"></a>HTTPS の HGS を構成します。 

既定では、HGS サーバーを初期化するときに、HTTP のみの通信用の IIS web サイトが構成します。

>[!NOTE]
>よく知られていて、信頼された HGS サーバー証明書を使用して HTTPS を構成して、中間の攻撃を回避する必要が、運用環境のデプロイのためお勧めします。

[!INCLUDE [Configure HTTPS](../../includes/configure-hgs-for-https.md)] 

>[!NOTE]
>セキュリティで保護された enclaves で Always Encrypted、SSL 証明書は、SQL Server を実行する両方のホスト マシンで信頼されている必要があるし、database クライアント アプリケーションを実行するマシンは、HGS を問い合わせる必要があります。 

## <a name="collect-attestation-info-from-the-host-machines"></a>ホスト マシンから構成証明情報を収集します。

HGS を設定すると、セキュリティで保護された enclaves が常に暗号化され、VBS を使用して社外秘の計算を実行するどのコンピューターを承認するを認識できるように、ホスト マシンからの構成証明情報で構成が必要です。 次の手順は、使用する構成証明モードによって異なります。 

### <a name="collect-tpm-attestation-artifacts"></a>TPM 構成証明の成果物を収集します。 

TPM のモードを使用している場合は、構成証明のサポートをインストールし、ホスト ガーディアン サービスを登録する必要な情報を収集するには、各ホスト コンピューターで管理者特権の PowerShell セッションで次のコマンドを実行します。 

1. HGS クライアントは、ホスト コンピューターにインストールするには、HYPER-V をインストールしても、ホストの保護機能をインストールします。 
   このコンピューターでは、Vm は実行されません、中には、VBS enclaves を分離する仮想化ベースのセキュリティ機能を有効にする、ハイパーバイザーが必要です。

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. HYPER-V のインストールを完了するように求められたら、コンピューターを再起動します。 
3. システムで実行できるソフトウェアを制限するコード整合性ポリシーを作成します。 
   任意の Windows Defender Application Control ポリシーで十分です。 
   サーバーでのみ Microsoft ソフトウェアを実行して、次のコマンドはポリシーを作成迅速にします。 
   ポリシーは、監査モードでは、未承認のコードについて、イベントがログ記録が実行を保持しないことを意味になります。  

   ```powershell
   mkdir C:\artifacts
   Copy-Item C:\Windows\Schemas\CodeIntegrity\ExamplePolicies\AllowMicrosoft.xml C:\artifacts\AllowMicrosoft-Audit.xml 
   Set-RuleOption -FilePath C:\artifacts\AllowMicrosoft-Audit.xml -Option 3 
   ConvertFrom-CIPolicy -XmlFilePath C:\artifacts\AllowMicrosoft-Audit.xml -BinaryFilePath C:\artifacts\AllowMicrosoft-Audit.bin 
   Copy-Item C:\artifacts\AllowMicrosoft-Audit.bin C:\Windows\System32\CodeIntegrity\SIPolicy.p7b 
   Restart-Computer 
   ```

   Windows Defender Application Control では、さまざまなセキュリティ姿勢をカバーする多数の機能があります。 
   Microsoft 以外のソフトウェアを許可するか、se、既定のポリシーをカスタマイズする必要がある場合、[展開ガイドの Windows Defender Application Control](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide)します。   


4. 次のコマンドを使用してコンピューター上の仮想化ベースのセキュリティが実行されていることを確認します。 
   DeviceGuardSecurityServicesRunning フィールドがある"HypervisorEnforcedCodeIntegrity"が表示されている場合、VBS が実行されていることがわかります。 
   実行されていない場合は、ダウンロード、[デバイス ガード準備ツール](https://www.microsoft.com/download/details.aspx?id=53337)実行"DG_Readiness.ps1-- HVCI を有効にする"を有効にします。  
   
   ```powershell
   Get-ComputerInfo -Property DeviceGuard* 
   ```
5. TPM の識別子と基準を収集します。

   ```powershell 
   (Get-PlatformIdentifier -Name $env:computername).Save("C:\artifacts\TpmID-$env:computername.xml") 
   Get-HgsAttestationBaselinePolicy -SkipValidation -Path "C:\artifacts\TpmBaseline-$env:computername.tcglog" 
   ```
   
6. C:\artifacts から HGS サーバーに、xml、tcglog、および bin ファイルをコピーします。
7. 最初の TPM ホストは HGS サーバーに追加する場合は、各 HGS サーバーを信頼済み TPM ルート証明書をインストールする必要があります。 
   に従って、 [HGS のドキュメントに関するガイダンス](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-install-trusted-tpm-root-certificates)この手順を完了します。
8. HGS サーバーで証明書を渡すには、このホストを承認します。 
   以下のスクリプトは、HGS サーバーで 3 つのファイルがコピーされた C:\temp とサーバーのコンピューター名が"ServerA"であると仮定します。 
   パスと名前は、独自の環境に合わせて調整します。 

   ```powershell
   Add-HgsAttestationTpmHost -Name ServerA -Path C:\temp\TpmID-ServerA.xml 
   Add-HgsAttestationTpmPolicy -Name ServerA-Baseline -Path C:\temp\TpmBaseline-ServerA.tcglog 
   Add-HgsAttestationCiPolicy -Name AllowMicrosoft-Audit -Path C:\temp\AllowMicrosoft-Audit.bin 
   ```
9. 最初のサーバーは、証言する準備ができました! 
   ホスト コンピューターには、(HGS クラスターの DNS 名、通常は使用 HGS のドメイン名と組み合わせて HGS サービス名の変更) を証明する場所を指示する次のコマンドを実行します。 
   HostUnreachable エラーが発生した場合は、解決し、HGS サーバーの DNS 名に対して ping を実行を確認します。 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://hgs.bastion.local/Attestation -KeyProtectionServerUrl https://hgs.bastion.local/KeyProtection/ 
   ```

10. 上記のコマンドの結果を表示する必要がありますその AttestationStatus = 成功。 そうでない場合は、次を参照してください。[構成証明書エラー](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts#attestation-failures)エラーを解決する方法のガイダンスについて。   
11. 手順 1 ~ 10 の各ホスト コンピューターを繰り返します。 
    同一のハードウェアを使用している場合は、新しい基準またはすべてのコンピューターの CI ポリシーをキャプチャする必要はありません。 
    最初のサーバーからの基準はすべての構成がまったく同じマシンをカバーし、CI ポリシーで再利用する複数のコンピューターで Microsoft ソフトウェアがコンピューターのソフトウェアのみです。

### <a name="collecting-host-keys"></a>ホスト キーの収集 

>[!NOTE] 
>ホスト キーの構成証明はテスト環境での使用のみ推奨されます。 TPM 構成証明は、VBS enclaves が SQL Server で機密データの処理は、信頼されたコードを実行しているし、マシンが、推奨されるセキュリティ設定で構成されていることの最も強力な保証を提供します。 

ホスト キーの構成証明モードでの HGS の設定を選択した場合は、生成およびキーの各ホスト コンピューターから収集し、ホスト ガーディアン サービスに登録する必要があります。 

1. ホスト コンピューターにインストールされている HGS クライアントを取得するには、HYPER-V をインストールしても、ホストの保護機能をインストールします。 
   このコンピューターでは、Vm は実行されません、中には、Always Encrypted のクエリを実行する VBS enclaves を分離する仮想化ベースのセキュリティ機能を有効にする、ハイパーバイザーが必要です。 

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All 
   ```

2. HYPER-V のインストールを完了するように求められたら、コンピューターを再起動します。
3. 一意のホスト キーを生成し、結果の公開キーをファイルにエクスポートします。 

   ```powershell
   Set-HgsClientHostKey 
   mkdir C:\artifacts 
   Get-HgsClientHostKey -Path C:\artifacts\$env:computername.cer 
   ```
   
   または、独自の証明書を使用する場合は、拇印を指定できます。 
   複数のコンピューター証明書を共有したり、TPM または HSM にバインドされている証明書を使用する場合に役立ちます。 ことができます。 次に、TPM バインド証明書 (秘密キーを盗まれ、別のコンピューターで使用できないし、TPM 1.2 のみが必要です) を作成する例を示します。

   ```powershell
   $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
   Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
   ```

4. ホスト ガーディアン サービスをホスト キーをコピーします。 
5. 環境に関連する名前とパスを使用して、HGS のノードとホスト キーを登録します。 

   ```powershell
   Add-HgsAttestationHostKey -Name 'ServerA' -Path C:\temp\ServerA.cer 
   ``` 

6. 最初のサーバーは、証言する準備ができました! 
   ホスト コンピューターには、(HGS クラスターの DNS 名、通常は使用 HGS のドメイン名と組み合わせて HGS サービス名の変更) を証明する場所を指示する次のコマンドを実行します。 
   HostUnreachable エラーが発生した場合は、解決し、HGS サーバーの DNS 名に対して ping を実行を確認します。    

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://hgs.bastion.local/Attestation -KeyProtectionServerUrl http://hgs.bastion.local/KeyProtection/  
   ```

7. 上記のコマンドの結果を表示する必要がありますその AttestationStatus = 成功。 
   HostUnreachable エラーが発生する場合は、ホスト コンピューターは HGS と通信できません。 
   DNS 解決が、ホスト マシンと HGS サーバー間で設定されていると、サーバーを ping できることを確認してください。 
   UnauthorizedHost エラーは、HGS サーバー – 手順 4. と 5. エラーを解決すると、公開キーが登録されていないことを示します。 
   すべてうまくいかなかった場合は、クリア HgsClientHostKey を実行し、手順 3. ~ 6. を繰り返します。   

8. SQL Server Always Encrypted VBS enclaves を使用して実行するサーバーごとに手順 1. ~ 7. を繰り返します。     


