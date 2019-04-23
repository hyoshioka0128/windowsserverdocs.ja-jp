---
title: ホスト ガーディアン サービスのトラブルシューティング
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 2dc9a612fa9760a6ca5f05efe1c287fd0872a1d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861253"
---
# <a name="troubleshooting-the-host-guardian-service"></a>ホスト ガーディアン サービスのトラブルシューティング

> 適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、展開すると、保護されたファブリックにホスト ガーディアン サービス (HGS) サーバーの運用に発生する一般的な問題の解決方法について説明します。
最初のコマンドを試してください、問題の性質の不明な場合、[保護され、fabric 診断](guarded-fabric-troubleshoot-diagnostics.md)HGS サーバーおよび可能性を絞り込むために、HYPER-V ホストで発生します。

## <a name="certificates"></a>証明書

HGS は管理者の構成の暗号化などの作動するためにいくつかの証明書を要求し、HGS 自体によって管理される構成証明書と証明書に署名します。
これらの証明書が正しく構成されていません場合、HGS は証明またはシールドされた Vm のキー プロテクターをロック解除を希望される HYPER-V ホストから要求を処理できません。
次のセクションでは、証明書を HGS の構成に関連する一般的な問題について説明します。

### <a name="certificate-permissions"></a>証明書の権限

HGS では、暗号化と署名証明書の拇印によって HGS に追加された証明書のパブリックおよびプライベートのキーにアクセスできる必要があります。
具体的には、グループの管理された HGS サービスを実行するサービス アカウント (gMSA) には、キーへのアクセスが必要があります。
HGS で使用される、gMSA を見つけるには、するには、HGS サーバーで管理者特権の PowerShell プロンプトで次のコマンドを実行します。

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

キーの格納場所によって異なります、秘密キーを使用する、gMSA アカウントのアクセスを付与する方法: ハードウェア セキュリティ モジュール (HSM) またはサード パーティのカスタム キー ストレージ プロバイダーを使用して、ローカルの証明書ファイルとしてコンピューターにします。

#### <a name="grant-access-to-software-backed-private-keys"></a>ソフトウェアを基盤と秘密キーにアクセスを許可

自己署名証明書または証明書機関によって発行された証明書を使用している場合**いない**ハードウェア セキュリティ モジュールまたはカスタム キー格納プロバイダーに格納されていることができますを変更する秘密キーのアクセス許可を実行して、次の手順:

1. ローカルの証明書を open マネージャー (certlm.msc)
2. 展開**個人 > 証明書**および更新する署名または暗号化証明書を検索します。
3. 証明書を右クリックし、選択**すべてのタスク > 秘密キーの管理**します。
4. クリックして**追加**証明書の秘密キーに新しいユーザー アクセス権を付与します。
5. オブジェクト ピッカーでの HGS、前に、gMSA アカウント名を入力し、クリックして**OK**します。
6. GMSA を与えて**読み取り**証明書にアクセスします。
7. クリックして**OK**アクセス許可 ウィンドウを閉じます。

Server Core で HGS を実行しているサーバーをリモートで管理するか、ローカルの証明書マネージャーを使用して秘密キーを管理することができなきます。
代わりに、ダウンロードする必要がありますには、[保護されたファブリックのツールの PowerShell モジュール](https://www.powershellgallery.com/packages/GuardedFabricTools)PowerShell でのアクセス許可を管理できるようにします。

1. Server Core コンピューターで管理者特権の PowerShell コンソールを開くか、HGS のローカル管理者権限を持つアカウントを使用して PowerShell リモート処理を使用します。
2. 保護されたファブリックのツールの PowerShell モジュールをインストールし、gMSA アカウントの秘密キーへのアクセスを付与するには、次のコマンドを実行します。

```powershell
$certificateThumbprint = '<ENTER CERTIFICATE THUMBPRINT HERE>'

# Install the Guarded Fabric Tools module, if necessary
Install-Module -Name GuardedFabricTools -Repository PSGallery

# Import the module into the current session
Import-Module -Name GuardedFabricTools

# Get the certificate object
$cert = Get-Item "Cert:\LocalMachine\My\$certificateThumbprint"

# Get the gMSA account name
$gMSA = (Get-IISAppPool -Name KeyProtection).ProcessModel.UserName

# Grant the gMSA read access to the certificate
$cert.Acl = $cert.Acl | Add-AccessRule $gMSA Read Allow
```

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>HSM またはカスタムのプロバイダー サポートの秘密キーにアクセスを許可

証明書の秘密キーをバックアップして、ハードウェア セキュリティ モジュール (HSM) またはカスタム キー格納プロバイダー (KSP) で場合、アクセス許可モデルは、特定のソフトウェア ベンダーによって決まります。
最適な結果を製造元のマニュアルを参照してください。 またはサポートについては、特定のデバイス/ソフトウェアのアクセス許可の処理方法にプライベートのキーにサイト。

一部のハードウェア セキュリティ モジュールは、秘密キーへの特定のユーザー アカウントのアクセス許可をサポートしていません代わりに、特定のキーのセット内のコンピューター アカウントのすべてのキーへのアクセスが許可します。
このようなデバイスでは、通常コンピューター アクセス キーを付与するだけで十分ですし、HGS がその接続を利用できるようになります。

**Hsm に関するヒント**

提案された構成に役立つオプションが正常に使用する HSM バックアップ キーを Microsoft とそのパートナーの経験に基づいて HGS を次に示します。
これらのヒントは、利便性のために提供されが、読み取り時に正しいとは限りません。 また HSM の製造元によって承認されています。
さらに質問がある場合は、特定のデバイスに関連する正確な情報は、HSM の製造元にお問い合わせください。

HSM ブランド/シリーズ      | 推奨事項
----------------------|-------------
Gemalto SafeNet       | 署名と暗号化に使用する証明書を許可する 0xa0 とに、証明書要求ファイルのキー使用法プロパティが設定を確認します。 さらに、gMSA アカウントを付与する必要があります*読み取り*ローカル証明書マネージャー ツールを使用して秘密キーへのアクセス (上記の手順を参照してください)。
Thales nShield        | HGS の各ノードは、署名および暗号化キーを格納しているセキュリティ ワールドにアクセスすることを確認します。 GMSA 固有のアクセス許可を構成する必要はありません。
務めて CryptoServers | 暗号化、復号化、および署名に使用する証明書を許可する 0x13 に証明書要求ファイルのキー使用法プロパティが設定を確認します。

### <a name="certificate-requests"></a>証明書の要求

公開キー基盤 (PKI) 環境で証明書を発行する証明機関を使用する場合は、証明書の要求には、それらのキーの HGS の使用量の最小要件が含まれるようにする必要があります。

**証明書の署名**

CSR プロパティ | 必要な値
-------------|---------------
アルゴリズム    | RSA
キーのサイズ     | 2048 ビット以上
キー使用法    | Digitalsignature ビット署名/サインイン/

**暗号化証明書**

CSR プロパティ | 必要な値
-------------|---------------
アルゴリズム    | RSA
キーのサイズ     | 2048 ビット以上
キー使用法    | 暗号化/暗号化/DataEncipherment

**Active Directory 証明書サービス テンプレート**

作成する Active Directory 証明書サービス (ADCS) の証明書テンプレートを使用している場合、証明書をお勧めするは、次の設定でテンプレートを使用します。

ADCS テンプレートのプロパティ | 必要な値
-----------------------|---------------
プロバイダーのカテゴリ      | キー ストレージ プロバイダー
アルゴリズム名         | RSA
最小キー サイズ       | 2048
目的                | 署名と暗号化
キー使用法の拡張機能    | デジタル署名、キーの暗号化、データの暗号化 ("許可するユーザー データの暗号化")


### <a name="time-drift"></a>時間のずれ

他の HGS ノードや、保護されたファブリックで HYPER-V ホストのサーバーの時刻に大幅にずれていますと構成証明書の署名者証明書の有効性に問題が発生する可能性があります。
構成証明書の署名者証明書が作成され、バック グラウンドで HGS で更新し、構成証明サービスによって保護されたホストに発行される正常性証明書の署名に使用されます。

構成証明書の署名者証明書を更新するには、管理者特権の PowerShell プロンプトで次のコマンドを実行します。

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

開き、スケジュールされたタスクを手動で実行する代わりに、**タスク スケジューラ**(taskschd.msc) に移動する**タスク スケジューラ ライブラリ > Microsoft > Windows > HGSServer**を実行していると、という名前のタスク**AttestationSignerCertRenewalTask**します。

## <a name="switching-attestation-modes"></a>構成証明モードを切り替える

Active Directory モードまたはその逆を使用して TPM モードから HGS を切り替えた場合、[セット HgsServer](https://technet.microsoft.com/library/mt652180.aspx)コマンドレット、かかる場合がありますすべてのノードには、最大で 10 分で、新しい構成証明モードの適用を開始するように HGS クラスター。
これは、通常の動作です。
正常に新しい構成証明モードを使用してすべてのホストを証明することを確認するまでは、前の構成証明モードからホストを許可するすべてのポリシーが削除されないことをお勧めします。

**TPM から AD モードに切り替えるときに既知の問題**

Active Directory モードに TPM モードとそれ以降のスイッチで HGS クラスターを初期化する場合は、既知の問題を新しい構成証明モードに切り替えてから HGS クラスター内の他のノードが行われなくなります。
すべての HGS サーバーが、正しい構成証明モードを適用するためには、次のように実行します。 `Set-HgsServer -TrustActiveDirectory` **の各ノードで**HGS クラスターの。
TPM モードから AD モードに切り替える場合は、この問題は適用されません*と*クラスターがもともと AD モードを設定します。

HGS サーバーの構成証明モードを確認するにを実行して[Get HgsServer](https://technet.microsoft.com/library/mt652162.aspx)します。

## <a name="memory-dump-encryption-policies"></a>メモリ ダンプ暗号化ポリシー

既定 HGS がポリシーをダンプするメモリ ダンプ暗号化ポリシーを構成しようとしているし、表示されない場合 (Hgs\_NoDumps、Hgs\_DumpEncryption と Hgs\_DumpEncryptionKey) またはダンプのポリシーのコマンドレット (Add-HgsAttestationDumpPolicy)、インストールされている最新累積的な更新がないこと可能性があります。
これを修正する[HGS サーバーを更新](guarded-fabric-manage-hgs.md#patching-hgs)最新累積的な Windows update と[構成証明書の新しいポリシーをアクティブ化](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation)します。
新しいダンプ暗号化機能がインストールされていないホスト失敗する可能性が構成証明 HGS ポリシーがアクティブ化されるように、新しい構成証明書ポリシーをアクティブ化する前に、同じ累積更新プログラムを HYPER-V ホストを更新することを確認します。

## <a name="endorsement-key-certificate-error-messages"></a>保証キー証明書のエラー メッセージ

使用してホストを登録するときに、[追加 HgsAttestationTpmHost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost)コマンドレットでは、TPM の 2 つの識別子が指定されたプラットフォーム識別子ファイルから抽出されます。 保証キー証明書 (EKcert) と公開保証キー (EKpub)。
EKcert では、TPM が本物であり、通常のサプライ チェーンによって製造された保証を提供する、TPM の製造元を識別します。
EKpub は一意にその特定の TPM を識別し、HGS を使用してホストにシールドされた Vm を実行するアクセスを許可する手段の 1 つです。

2 つの条件のいずれかに該当する場合は、TPM のホストを登録するときに、エラーが表示されます。
1. プラットフォーム識別子ファイル**しない**保証キー証明書を含む
2. プラットフォーム id のファイルには、保証キー証明書が含まれていますが、その証明書が**信頼されていない**システム

特定の TPM の製造元は、その Tpm で EKcerts を含めないでください。
TPM の場合とであると思われる場合ことを確認、oem、Tpm する必要がありますいない、EKcert があるを使用して、`-Force`フラグを手動でホストを HGS に登録します。
TPM は、EKcert である必要がありますプラットフォーム識別子ファイルのいずれかが見つからなかった場合は、実行するときに、管理者 (特権) の PowerShell コンソールを使用していることを確認[Get PlatformIdentifier](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier)ホスト。

EKcert は信頼されていないエラーを受信する場合があることを確認[信頼済み TPM ルート証明書パッケージをインストール](guarded-fabric-install-trusted-tpm-root-certificates.md)HGS サーバーごとに、TPM ベンダーのルート証明書は、ローカル コンピューターのに存在します。**TrustedTPM\_ルート Ca**を格納します。 適用可能な中間証明書でインストールする必要も、 **TrustedTPM\_IntermediateCA**ローカル コンピューターに格納します。
ルートおよび中間証明書をインストールするを実行することをする必要がある`Add-HgsAttestationTpmHost`正常にします。
