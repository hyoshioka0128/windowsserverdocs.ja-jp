---
title: "デバイス正常性構成証明"
H1: na
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology:
- techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.date: 10/12/2016
ms.openlocfilehash: d304ee3456f8db1e5b202c1d9221d1374a5251be
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="device-health-attestation"></a>デバイス正常性構成証明

>Windows Server 2016 の適用対象:

Windows 10 バージョン 1507 で導入されたデバイス正常性構成証明 (DHA) には、次します。

-   合わせて Windows 10 Mobile デバイス管理 (MDM) フレームワークと統合されます。[Open Mobile Alliance (OMA) 標準](http://openmobilealliance.org/)します。

-   ファームウェアまたは個別の形式でプロビジョニングされたトラステッド モジュール プラットフォーム (TPM) のデバイスをサポートしています。

-   ハードウェアに自分の組織のセキュリティ レベルを上げるにできるように企業が監視され、最小限でのセキュリティまたは運用コストを損なうことがなく証明されます。

Windows Server 2016 以降では、実行できます DHA サービスは、サーバーの役割として組織内でします。 このトピックを使用して、インストールして、デバイス正常性構成証明のサーバーの役割を構成する方法について説明します。

## <a name="overview"></a>概要

デバイスの正常性を評価するためには、DHA を使用できます。
  
-   TPM 1.2 または 2.0 をサポートする Windows 10 と Windows 10 Mobile のデバイス。  
-   Azure Active Directory、または Active Directory と Azure Active Directory の両方を使用するハイブリッド展開によって管理されるデバイス、インターネット アクセスなしの Active Directory を使用して管理されているデバイスをインターネットにアクセスできる、Active Directory を使用して管理されている内部設置型デバイスです。


### <a name="dha-service"></a>DHA サービス

DHA サービスは、デバイスの TPM と PCR のログを検証し、DHA レポートを発行します。 Microsoft では、次の 3 つの方法で DHA サービスを提供します。

- **DHA クラウド サービス**空き、地理的な-負荷分散、および世界のさまざまな地域からアクセス用に最適化されたの、Microsoft で管理される DHA サービスです。

- **DHA オンプレミス サービス**Windows Server 2016 で導入された新しいサーバーの役割。 Windows Server 2016 のライセンスを持っているユーザーに提供を無料であります。

- **DHA Azure クラウド サービス**Microsoft Azure での仮想ホストです。 これを行うには、DHA オンプレミス サービスの仮想ホストとライセンスを必要です。

DHA サービスは MDM ソリューションと統合し、次を提供します。 

-   DHA レポートと (既存のデバイス管理通信チャネル) を通じてデバイスから受信した情報を組み合わせる
-   決定を行うより安全かつ信頼できるセキュリティに基づくハードウェア保証され、保護されたデータ

DHA を使用して、組織の資産のセキュリティ保護の水準を引き上げる方法を示す例を次に示します。

1. 次のブート構成/属性を確認するポリシーを作成します。
  - セキュア ブート
  - BitLocker
  - ELAM
2. MDM ソリューションでは、このポリシーを強制し、DHA レポート データに基づいて修正動作をトリガーします。  たとえば、次を確認でした。
  - セキュア ブートが有効になっているし、デバイスが本物であり、信頼されたコードを読み込む Windows ブート ローダーが改ざんされていません。
  - ブートは、Windows カーネルとデバイスの起動中に読み込まれたコンポーネントのデジタル署名を正常に検証を信頼します。
  - メジャー ブートには、リモートで確認できる可能性があります TPM で保護された監査証跡が作成されます。
  - BitLocker が有効であり、デバイスが有効にした場合、データを保護してオフです。
  - ELAM がブートの初期段階で有効になったを監視しているランタイムします。
  
#### <a name="dha-cloud-service"></a>DHA クラウド サービス

DHA クラウド サービスには、次の利点があります。

-   MDM ソリューションで登録されているデバイスから受信 TCG と PCR デバイス ブートのログを確認します。 
-   改ざんされにくい、改ざん証明が可能なレポート (DHA レポート、デバイスが収集され、デバイスの TPM チップによって保護されるデータに基づいてを開始する方法を説明する) を作成します。 
-   保護された通信チャネルでレポートを要求した MDM サーバーには、DHA レポートを配信します。

#### <a name="dha-on-premises-service"></a>DHA オンプレミス サービス

DHA オンプレミス サービスは、DHA クラウド サービスによって提供されているすべての機能を提供します。  お客様はこともできます。

 - データ センターで DHA サービスを実行してパフォーマンスを最適化します。
 - DHA レポートに、ネットワークままにしていないことを確認します。

#### <a name="dha-azure-cloud-service"></a>DHA Azure クラウド サービス

このサービスは、Microsoft Azure での仮想ホストとして、DHA Azure クラウド サービスが実行されることを除いて、DHA オンプレミス サービスと同じ機能を提供します。

### <a name="dha-validation-modes"></a>DHA 検証モード

EKCert または AIKCert のいずれかの検証モードで実行する、DHA オンプレミス サービスを設定することができます。 DHA サービス レポートの問題、AIKCert または EKCert 検証モードで発行されたかどうかはこれを示します。 AIKCert と EKCert 検証モードは、信頼の EKCert チェーンが最新の状態と同じセキュリティ保証を提供します。

#### <a name="ekcert-validation-mode"></a>EKCert 検証モード

EKCert 検証モードは、インターネットに接続されていない組織内のデバイスに最適です。 EKCert 検証モードで実行されている DHA サービスに接続するデバイスは**いない**、インターネットに直接アクセスします。

DHA が EKCert 検証モードでを実行している場合は、随時 (約 5 - 1 年あたり 10 回) を更新する必要がある信頼、企業が管理チェーンに依存します。 

(利用可能になる)、Microsoft は信頼されたルートおよび中間 CA の承認された TPM 製造元の集約されたパッケージを公開して .cab アーカイブでパブリックにアクセスできるアーカイブに保存します。 フィードをダウンロードし、その整合性を検証および、デバイス正常性構成証明を実行しているサーバーにインストールする必要があります。

An example archive is [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

#### <a name="aikcert-validation-mode"></a>AIKCert 検証モード

AIKCert 検証モードは、インターネットにアクセスすることは可能な運用環境に最適です。 AIKCert 検証モードで実行されている DHA サービスに接続するデバイスでは、インターネットに直接アクセスする必要があり、Microsoft から AIK 証明書を取得することがします。 

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>インストールして Windows Server 2016 で DHA サービスを構成します。

Dha を Windows Server 2016 にインストールして構成するのにには、次のセクションを使用します。

### <a name="prerequisites"></a>前提条件

設定し、DHA オンプレミス サービスを確認する必要があります。

- Windows Server 2016 を実行しているサーバー。
- TPM (1.2 または 2.0) 内にある最新の Windows Insider を実行している、クリア/準備完了状態で、1 つ (以上) の Windows 10 クライアント デバイスを作成します。
- EKCert または AIKCert 検証モードで実行しようとしているかどうかを決定します。
- 次の証明書:
  - **DHA SSL 証明書**エクスポート可能な秘密キーを使用して、エンタープライズ信頼されたルートにチェーンされている x.509 SSL 証明書。 この証明書は、(DHA サービスと MDM サーバー) サーバーに転送中の DHA データ通信およびサーバー クライアント (DHA サービスと Windows 10 デバイス) の通信を保護します。
  - **署名証明書の DHA**エクスポート可能な秘密キーを使用して、エンタープライズ信頼されたルートにチェーンされている x.509 証明書。 DHA サービスは、デジタル署名のこの証明書を使用します。 
  - **DHA 暗号化証明書**エクスポート可能な秘密キーを使用して、エンタープライズ信頼されたルートにチェーンされている x.509 証明書。 DHA サービスは、暗号化にもこの証明書を使用します。 


### <a name="install-windows-server-2016"></a>Windows Server 2016 をインストールします。

Windows 展開サービスなど、好みのインストール方法を使用して、または起動可能なメディア、USB ドライブ、またはローカル ファイル システムからインストーラーを実行している、Windows Server 2016 をインストールします。 初めて DHA オンプレミス サービスを構成する場合は、Windows Server 2016 を使用してをインストールする必要があります、**デスクトップ エクスペリエンス**インストール オプションです。

### <a name="add-the-device-health-attestation-server-role"></a>Add the Device Health Attestation server role

デバイス正常性構成証明のサーバーの役割とその依存関係をインストールするには、サーバー マネージャーを使用します。 

Windows Server 2016 をインストールした後、デバイスが再起動し、サーバー マネージャーを開きます。 サーバー マネージャーが自動的に起動しない場合はクリックして**開始**、] をクリックし、**サーバー マネージャー**します。

1.  をクリックして**役割と機能の追加**します。
2.  **開始する前に**] ページで [**次**します。
3.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、**[次へ]**します。
4.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**サーバーを選択し、[クリックして**[次へ]**します。
5.  **サーバーの役割の選択**ページで、選択、**デバイス正常性構成証明**チェック ボックスをオンします。
6.  をクリックして**機能の追加**を他をインストールする役割サービスおよび機能が必要です。
7.  をクリックして**次**します。
8.  **機能の選択**] ページで [**次**します。
9.  **Web サーバーの役割 (IIS)** ] ページで [**次**します。
10. **役割サービスの選択**] ページで [**次**します。
11. **デバイス正常性構成証明サービス**] ページで [**次**します。
12. **インストール オプションの確認**] ページで [**インストール**します。
13. インストールが完了したら、クリックして**閉じる**します。

### <a name="install-the-signing-and-encryption-certificates"></a>署名と暗号化の証明書をインストールします。

次の Windows PowerShell スクリプトを使用して、署名と暗号化の証明書をインストールします。 拇印の詳細については、次を参照してください。[方法: 証明書の拇印を取得](https://msdn.microsoft.com/library/ms734695.aspx)します。

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R
  
#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>信頼済み TPM ルート証明書パッケージをインストールします。

信頼済み TPM ルート証明書パッケージをインストールするには必要があります展開、および、組織で信頼されていない信頼済みチェーンを削除する setup.cmd を実行します。

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>信頼済み TPM ルート証明書パッケージをダウンロードします。

Before you install the certificate package, you can download the latest list of trusted TPM roots from [https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab](https://tpmsec.microsoft.com/OnPremisesDHA/TrustedTPM.cab).

> **重要:**、パッケージをインストールする前に Microsoft によってデジタル署名されていることを確認します。

#### <a name="extract-the-trusted-certificate-package"></a>信頼された証明書パッケージを抽出します。
次のコマンドを実行して、信頼された証明書パッケージを抽出します。
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>TPM ベンダーの信頼済みチェーンを削除する*いない*(省略可能)、組織で信頼

組織によって信頼されていない TPM ベンダーの信頼チェーンのフォルダーを削除します。

> **注:** Microsoft フォルダーが Microsoft が AIK 証明書の発行を検証するために必要な AIK 証明書モードを使用する場合。

#### <a name="install-the-trusted-certificate-package"></a>信頼された証明書パッケージをインストールします。
信頼された証明書パッケージをインストールするには、.cab ファイルから、セットアップ スクリプトを実行します。

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>デバイス正常性構成証明サービスを構成します。

Windows PowerShell を使用して、DHA オンプレミス サービスを構成することができます。

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>証明書チェーン ポリシーを構成します。

証明書チェーン ポリシーを構成するには、次の Windows PowerShell スクリプトを実行します。

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA 管理コマンド

DHA サービスの管理に役立ついくつかの Windows PowerShell の例を次に示します。

### <a name="configure-the-dha-service-for-the-first-time"></a>初めて DHA サービスを構成します。

```
Install-DeviceHealthAttestation -SigningCertificateThumbprint "<HEX>" -EncryptionCertificateThumbprint "<HEX>" -SslCertificateThumbprint "<HEX>" -Force
```

### <a name="remove-the-dha-service-configuration"></a>DHA サービス構成を削除します。

```
Uninstall-DeviceHealthAttestation -RemoveSslBinding -Force
```
### <a name="get-the-active-signing-certificate"></a>アクティブな署名証明書を取得します。

```
Get-DHASActiveSigningCertificate
```
### <a name="set-the-active-signing-certificate"></a>アクティブな署名証明書を設定します。

```
Set-DHASActiveSigningCertificate -Thumbprint "<hex>" -Force
```

> **注:** DHA サービスを実行しているサーバーにこの証明書を展開する必要があります、**localmachine \my**証明書ストアです。 アクティブな署名証明書を設定すると、既存のアクティブな署名証明書は非アクティブな署名証明書の一覧に移動します。

### <a name="list-the-inactive-signing-certificates"></a>非アクティブな署名証明書を一覧表示します。
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>非アクティブな署名証明書を削除します。
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **注:**のみ*1 つ*(任意のタイプ) の非アクティブな証明書がサービスにいつでも存在可能性があります。 必要な不要になった後、非アクティブな証明書の一覧から証明書を削除する必要があります。

### <a name="get-the-active-encryption-certificate"></a>アクティブな暗号化証明書を取得します。

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>アクティブな暗号化証明書を設定します。

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

内のデバイスで、証明書を展開する必要があります、**localmachine \my**証明書ストアです。 

アクティブな暗号化証明書を設定すると、既存のアクティブな暗号化証明書は非アクティブな暗号化証明書の一覧に移動します。

### <a name="list-the-inactive-encryption-certificates"></a>非アクティブな暗号化証明書を一覧表示します。

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>非アクティブな暗号化証明書を削除します。

```
Remove-DHASInactiveEncryptionCertificates -Force
Remove-DHASInactiveEncryptionCertificates -Thumbprint "<hex>" -Force 
```

### <a name="get-the-x509chainpolicy-configuration"></a>X509ChainPolicy 構成を取得します。 

```
Get-DHASCertificateChainPolicy
```
### <a name="change-the-x509chainpolicy-configuration"></a>X509ChainPolicy 構成を変更します。

```
$certificateChainPolicy = Get-DHASInactiveEncryptionCertificates
$certificateChainPolicy.RevocationFlag = <X509RevocationFlag>
$certificateChainPolicy.RevocationMode = <X509RevocationMode>
$certificateChainPolicy.VerificationFlags = <X509VerificationFlags>
$certificateChainPolicy.UrlRetrievalTimeout = <TimeSpan>
Set-DHASCertificateChainPolicy = $certificateChainPolicy
```

## <a name="dha-service-reporting"></a>DHA サービス レポート

DHA サービスによって MDM ソリューションに報告されるメッセージの一覧を次に示します。 

- **200** HTTP OK。 証明書が返されます。
- **400**要求が正しくありません。 無効な要求形式、無効な正常性証明書、証明書の署名がないマッチ、無効な正常性構成証明 Blob、または、無効な正常性状態 Blob です。 応答には、エラー コードとエラー メッセージの診断に使用できる応答スキーマによって記述されたメッセージが含まれます。
- **500**内部サーバー エラー。 これは、サービスが証明書を発行する妨げとなる問題がある場合に発生することができます。
- **503**スロットルがサーバーの過負荷を防ぐために要求を拒否しています。 
