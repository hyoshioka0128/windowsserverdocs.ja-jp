---
title: デバイス正常性構成証明
H1: N/A
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e7b77a4-1c6a-4c21-8844-0df89b63f68d
author: brianlic-msft
ms.date: 10/12/2016
ms.openlocfilehash: 888992366f8a722c4834f23e08a393c829b47a26
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544629"
---
# <a name="device-health-attestation"></a>デバイス正常性構成証明

>適用先:Windows Server 2016

Windows 10、バージョン 1507 で導入されたデバイス正常性構成証明 (DHA) には、次の特長があります。

-   [Open Mobile Alliance (OMA) 標準](http://openmobilealliance.org/)に合わせて Windows 10 モバイル デバイス管理 (MDM) フレームワークと統合します。

-   ファームウェアまたは個別の形式でトラステッド プラットフォーム モジュール (TPM) がプロビジョニングされたデバイスをサポートします。

-   企業は、運用コストへの影響が最小限またはなしで、ハードウェアの監視、保証されたセキュリティなど、自社組織のセキュリティ水準を引き上げることができます。

Windows Server 2016 以降、DHA サービスをサーバーの役割として組織内で実行できるようになります。 このトピックを使用して、デバイス正常性構成証明のサーバーの役割をインストールして構成する方法についてご確認ください。

## <a name="overview"></a>概要

DHA を使用して、以下のデバイスの正常性を評価することができます。
  
-   TPM 1.2 または 2.0 をサポートする Windows 10 および Windows 10 Mobile のデバイス。  
-   インターネット アクセスのある Active Directory を使用して管理されるオンプレミスのデバイス、インターネット アクセスなしの Active Directory を使用して管理されるデバイス、Azure Active Directory によって管理されるデバイス、または Active Directory と Azure Active Directory の両方を使用するハイブリッド展開。


### <a name="dha-service"></a>DHA サービス

DHA サービスでは、デバイスの TPM と PCR のログを検証してから、DHA レポートを発行します。 Microsoft は、次の 3 つの方法で DHA サービスを提供します。

- **DHA クラウド サービス**: 無料で、地理的に負荷分散され、かつ世界のさまざまな地域からのアクセス用に最適化された、Microsoft によって管理される DHA サービスです。

- **DHA オンプレミス サービス**: Windows Server 2016 で導入された新しいサーバーの役割です。 Windows Server 2016 ライセンスを持つお客様は無料で使用できます。

- **DHA Azure クラウド サービス**: Microsoft Azure の仮想ホストです。 このサービスを実行するには、DHA オンプレミス サービスの仮想ホストとライセンスが必要です。

DHA サービスは MDM ソリューションと統合し、次の機能を提供します。 

-   (既存のデバイス管理通信チャネルを通じて) デバイスから受信した情報を DHA レポートと組み合わせる
-   ハードウェア保証され、保護されたデータに基づいて、より安全かつ信頼できるセキュリティ上の意思決定を下す

DHA を使用して組織の資産のセキュリティ保護の水準を引き上げる方法の例を次に示します。

1. 次のブート構成/属性を確認するポリシーを作成します。
   - セキュア ブート
   - BitLocker
   - ELAM
2. MDM ソリューションはこのポリシーを実施し、DHA レポート データに基づいて修正動作をトリガーします。  たとえば、以下を確認することができます。
   - セキュア ブートが有効になっており、デバイスが正規の信頼されたコードを読み込み、Windows ブート ローダーが改ざんされていないこと。
   - トラスト ブートによって、Windows カーネルと、デバイスの起動中に読み込まれたコンポーネントのデジタル署名が正常に検証されたこと。
   - メジャー ブートによって、リモートで確認できる TPM で保護された監査証跡が作成されたこと。
   - BitLocker が有効であり、デバイスがオフにされたときに、データが保護されていたこと。
   - ELAM がブートの初期段階で有効化され、ランタイムを監視していること。
  
#### <a name="dha-cloud-service"></a>DHA クラウド サービス

DHA クラウド サービスには、次の利点があります。

-   MDM ソリューションで登録されているデバイスから受信する TCG と PCR デバイスのブート ログを確認します。 
-   デバイスの TPM チップによって収集および保護されたデータに基づいて、デバイスが開始した方法を説明する、不正開封防止および、不正開封の跡がわかるレポート (DHA レポート) を作成します。 
-   DHA レポートを要求した MDM サーバーに、保護された通信チャネルでそのレポートを配信します。

#### <a name="dha-on-premises-service"></a>DHA オンプレミス サービス

DHA オンプレミス サービスは、DHA クラウド サービスによって提供されるすべての機能を提供します。  お客様に対して次のことも実現します。

 - 独自のデータ センターで DHA サービスを実行することにより、パフォーマンスを最適化する
 - DHA レポートが確実にネットワークから離れないようにする

#### <a name="dha-azure-cloud-service"></a>DHA Azure クラウド サービス

このサービスは、DHA Azure クラウド サービスが Microsoft Azure の仮想ホストとして実行する点を除いて、DHA オンプレミス サービスと同じ機能を提供します。

### <a name="dha-validation-modes"></a>DHA 検証モード

DHA オンプレミス サービスを、EKCert または AIKCert のいずれかの検証モードで実行するように設定することができます。 DHA サービスでレポートを発行する場合は、AIKCert または EKCert のどちらの検証モードで発行されたかを示します。 AIKCert と EKCert 検証モードは、信頼されている EKCert チェーンが最新である限り、同じセキュリティ保証を提供します。

#### <a name="ekcert-validation-mode"></a>EKCert 検証モード

EKCert 検証モードは、インターネットに接続されていない組織内のデバイスに向けに最適化されています。 EKCert 検証モードで実行されている DHA サービスに接続するデバイスは、インターネットに直接アクセス**できません**。

DHA が EKCert 検証モードで実行されている場合は、随時 (1 年あたり約 5 - 10 回) 更新する必要がある、企業によって管理された信頼済みのチェーンを利用します。 

Microsoft は、承認された TPM 製造元に対して (利用可能になったときに) 信頼されたルートおよび中間 CA の集約されたパッケージを、.cab アーカイブでパブリックにアクセスできるアーカイブとして発行しています。 フィードをダウンロードし、その整合性を検証して、デバイス正常性構成証明を実行しているサーバーにインストールする必要があります。

アーカイブの例と[https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925)しては、があります。

#### <a name="aikcert-validation-mode"></a>AIKCert 検証モード

AIKCert 検証モードは、インターネットにアクセス可能な運用環境向けに最適化されています。 AIKCert 検証モードで実行されている DHA サービスに接続するデバイスは、インターネットに直接アクセスでき、Microsoft から AIK 証明書を取得できる必要があります。 

## <a name="install-and-configure-the-dha-service-on-windows-server-2016"></a>DHA サービスを Windows Server 2016 にインストールして構成する

以下のセクションを使用して、DHA を Windows Server 2016 にインストールして構成します。

### <a name="prerequisites"></a>必須コンポーネント

DHA オンプレミス サービスを設定して検証するには、次のものが必要です。

- Windows Server 2016 を実行するサーバー。
- TPM (1.2 または 2.0) を装備し、最新の Windows Insider ビルドを実行している、クリア/準備完了状態の Windows 10 クライアント デバイス 1 台 (以上)。
- EKCert と AIKCert のいずれの検証モードで実行するかを決定します。
- 次の証明書:
  - **DHA SSL 証明書**: エクスポート可能な秘密キーを持つ、エンタープライズ信頼済みのルートにチェーンされている x.509 SSL 証明書。 この証明書は、サーバー間 (DHA サービスと MDM サーバー) およびサーバーからクライアント間 (DHA サービスと Windows 10 デバイス) の通信を含む、転送中の DHA データ通信を保護します。
  - **DHA 署名証明書**: エクスポート可能な秘密キーを持つ、エンタープライズ信頼済みのルートにチェーンされている x.509 証明書。 DHA サービスは、デジタル署名にこの証明書を使用します。 
  - **DHA 暗号化証明書**: エクスポート可能な秘密キーを持つ、エンタープライズ信頼済みのルートにチェーンされている x.509 証明書。 DHA サービスは、暗号化にもこの証明書を使用します。 


### <a name="install-windows-server-2016"></a>Windows Server 2016 をインストールする

Windows 展開サービスなど、好みのインストール方法を使用するか、起動可能なメディア、USB ドライブ、またはローカル ファイル システムからインストーラーを実行して、Windows Server 2016 をインストールします。 初めて DHA オンプレミス サービスを構成する場合は、**デスクトップ エクスペリエンス** インストール オプションを使用して Windows Server 2016 をインストールする必要があります。

### <a name="add-the-device-health-attestation-server-role"></a>デバイス正常性構成証明のサーバーの役割を追加する

サーバー マネージャーを使用して、デバイス正常性構成証明のサーバーの役割とその依存関係をインストールできます。 

Windows Server 2016 のインストールが完了すると、デバイスが再起動され、サーバー マネージャーが開きます。 サーバー マネージャーが自動的に起動しない場合は、 **[スタート]** をクリックしてから、 **[サーバー マネージャー]** をクリックします。

1.  **[役割と機能の追加]** をクリックします。
2.  **[開始する前に]** ページで、 **[次へ]** をクリックします。
3.  **[インストールの種類の選択]** ページで、 **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。
4.  **[対象サーバーの選択]** ページで、 **[サーバー プールからサーバーを選択]** を選択し、サーバーを選択して、 **[次へ]** をクリックします。
5.  **[サーバーの役割の選択]** ページで、 **[デバイス正常性構成証明]** チェック ボックスをオンにします。
6.  **[機能の追加]** をクリックして必要な他の役割サービスおよび機能をインストールします。
7.  **[次へ]** をクリックします。
8.  **[機能の選択]** ページで **[次へ]** をクリックします。
9.  **[Web サーバーの役割 (IIS)]** ページで、 **[次へ]** をクリックします。
10. **[役割サービスの選択]** ページで、 **[次へ]** をクリックします。
11. **[デバイス正常性構成証明サービス]** ページで [**次へ]** をクリックします。
12. **[インストール オプションの確認]** ページで、 **[インストール]** をクリックします。
13. インストールが完了したら、 **[閉じる]** をクリックします。

### <a name="install-the-signing-and-encryption-certificates"></a>署名証明書および暗号化証明書をインストールする

次の Windows PowerShell スクリプトを使用して、署名証明書および暗号化証明書をインストールします。 サムプリントの詳細については[、「」を参照してください。証明書](https://msdn.microsoft.com/library/ms734695.aspx)の拇印を取得します。

```
$key = Get-ChildItem Cert:\LocalMachine\My | Where-Object {$_.Thumbprint -like "<thumbprint>"}
$keyname = $key.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
$keypath = $env:ProgramData + "\Microsoft\Crypto\RSA\MachineKeys\" + $keyname
icacls $keypath /grant <username>`:R
  
#<thumbprint>: Certificate thumbprint for encryption certificate or signing certificate
#<username>: Username for web service app pool, by default IIS_IUSRS
```

### <a name="install-the-trusted-tpm-roots-certificate-package"></a>信頼済み TPM のルート証明書パッケージをインストールする

信頼済み TPM ルート証明書パッケージをインストールするには、パッケージを展開し、組織で信頼されていない信頼済みチェーンを削除してから setup.cmd を実行します。

#### <a name="download-the-trusted-tpm-roots-certificate-package"></a>信頼済み TPM ルート証明書パッケージをダウンロードする

証明書パッケージをインストールする前に、から[https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925)信頼できる TPM ルートの最新の一覧をダウンロードできます。

> **重要:** パッケージをインストールする前に、Microsoft によってデジタル署名されていることを確認します。

#### <a name="extract-the-trusted-certificate-package"></a>信頼済み証明書パッケージを展開する
次のコマンドを実行して、信頼済み証明書パッケージを展開します。
```
mkdir .\TrustedTpm
expand -F:* .\TrustedTpm.cab .\TrustedTpm
```

#### <a name="remove-the-trust-chains-for-tpm-vendors-that-are-not-trusted-by-your-organization-optional"></a>組織で信頼されて*いない* TPM ベンダーの信頼済みチェーンを削除する (省略可能)

組織によって信頼されていない TPM ベンダーの信頼チェーンのフォルダーを削除します。

> **注:** AIK 証明書モードを使用する場合は、microsoft が発行した AIK 証明書を検証するために Microsoft フォルダーが必要です。

#### <a name="install-the-trusted-certificate-package"></a>信頼済み証明書パッケージをインストールする
.cab ファイルから、セットアップ スクリプトを実行して、信頼済み証明書パッケージをインストールします。

```
.\setup.cmd
```

### <a name="configure-the-device-health-attestation-service"></a>デバイス正常性構成証明を構成する

Windows PowerShell を使用して、DHA オンプレミス サービスを構成することができます。

```
Install-DeviceHealthAttestation -EncryptionCertificateThumbprint <encryption> -SigningCertificateThumbprint <signing> -SslCertificateStoreName My -SslCertificateThumbprint <ssl> -SupportedAuthenticationSchema "<schema>"

#<encryption>: Thumbprint of the encryption certificate
#<signing>: Thumbprint of the signing certificate
#<ssl>: Thumbprint of the SSL certificate
#<schema>: Comma-delimited list of supported schemas including AikCertificate, EkCertificate, and AikPub
```

### <a name="configure-the-certificate-chain-policy"></a>証明書チェーン ポリシーを構成する

次の Windows PowerShell スクリプトを実行して、証明書チェーン ポリシーを構成します。

```
$policy = Get-DHASCertificateChainPolicy
$policy.RevocationMode = "NoCheck"
Set-DHASCertificateChainPolicy -CertificateChainPolicy $policy
```

## <a name="dha-management-commands"></a>DHA 管理コマンド

DHA サービスの管理に役立つ Windows PowerShell の例をいくつか示します。

### <a name="configure-the-dha-service-for-the-first-time"></a>初めて DHA サービスを構成する

```
Install-DeviceHealthAttestation -SigningCertificateThumbprint "<HEX>" -EncryptionCertificateThumbprint "<HEX>" -SslCertificateThumbprint "<HEX>" -Force
```

### <a name="remove-the-dha-service-configuration"></a>DHA サービス構成を削除する

```
Uninstall-DeviceHealthAttestation -RemoveSslBinding -Force
```
### <a name="get-the-active-signing-certificate"></a>アクティブな署名証明書を取得する

```
Get-DHASActiveSigningCertificate
```
### <a name="set-the-active-signing-certificate"></a>アクティブな署名証明書を設定する

```
Set-DHASActiveSigningCertificate -Thumbprint "<hex>" -Force
```

> **注:** この証明書は、 **LocalMachine\My**証明書ストアの DHA サービスを実行しているサーバーに展開する必要があります。 アクティブな署名証明書が設定されている場合、既存のアクティブな署名証明書は非アクティブな署名証明書の一覧に移動します。

### <a name="list-the-inactive-signing-certificates"></a>非アクティブな署名証明書を一覧表示する
```
Get-DHASInactiveSigningCertificates
```

### <a name="remove-any-inactive-signing-certificates"></a>非アクティブな署名証明書を削除する
```
Remove-DHASInactiveSigningCertificates -Force
Remove-DHASInactiveSigningCertificates  -Thumbprint "<hex>" -Force
```

> **注:** サービスには *、非アクティブ*な (任意の種類の) 証明書がいつでも存在する可能性があります。 非アクティブな証明書が必要なくなった場合、一覧から証明書を削除する必要があります。

### <a name="get-the-active-encryption-certificate"></a>アクティブな暗号化証明書を取得する

```
Get-DHASActiveEncryptionCertificate
```

### <a name="set-the-active-encryption-certificate"></a>アクティブな暗号化証明書を設定する

```
Set-DHASActiveEncryptionCertificate -Thumbprint "<hex>" -Force
```

証明書は **LocalMachine\My** 証明書ストア内のデバイスに展開する必要があります。 

アクティブな暗号化証明書が設定されている場合、既存のアクティブな暗号化証明書は、非アクティブな暗号化証明書の一覧に移動します。

### <a name="list-the-inactive-encryption-certificates"></a>非アクティブな暗号化証明書を一覧表示する

```
Get-DHASInactiveEncryptionCertificates
```
### <a name="remove-any-inactive-encryption-certificates"></a>非アクティブな暗号化証明書を削除する

```
Remove-DHASInactiveEncryptionCertificates -Force
Remove-DHASInactiveEncryptionCertificates -Thumbprint "<hex>" -Force 
```

### <a name="get-the-x509chainpolicy-configuration"></a>X509ChainPolicy 構成を取得する 

```
Get-DHASCertificateChainPolicy
```
### <a name="change-the-x509chainpolicy-configuration"></a>X509ChainPolicy 構成を変更する

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
- **400** Bad request。 無効な要求形式、無効な正常性証明書、証明書署名の不一致、無効な正常性構成証明 Blob、または無効な正常性状態 Blob です。 応答には、診断に使用できるエラー コードとエラー メッセージとともに、応答スキーマによって記述されたメッセージも含まれます。
- **500** Internal server error。 これは、サービスによる証明書の発行を妨げている問題がある場合に発生することがあります。
- **503** スロットリングがサーバーの過負荷を防ぐために要求を拒否しています。 
