---
title: ホストガーディアンサービスのトラブルシューティング
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 424b8090-0692-49a6-9dc4-3c0e77d74b80
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: be817a2c06b13af254b80090b9a7488209d4df0a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403531"
---
# <a name="troubleshooting-the-host-guardian-service"></a>ホストガーディアンサービスのトラブルシューティング

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、保護されたファブリックでホストガーディアンサービス (HGS) サーバーを展開または運用するときに発生する一般的な問題の解決策について説明します。
問題の性質がわからない場合は、まず HGS サーバーと Hyper-v ホストで保護された[ファブリックの診断](guarded-fabric-troubleshoot-diagnostics.md)を実行して、考えられる原因を絞り込みます。

## <a name="certificates"></a>証明書

HGS では、管理者が構成した暗号化と署名証明書だけでなく、HGS 自体によって管理されている構成証明書を含む、動作するために複数の証明書が必要です。
これらの証明書が正しく構成されていない場合、HGS は、シールドされた Vm のキープロテクターを証明またはロック解除する Hyper-v ホストからの要求を処理できません。
以下のセクションでは、HGS で構成された証明書に関連する一般的な問題について説明します。

### <a name="certificate-permissions"></a>証明書のアクセス許可

HGS は、証明書の拇印によって HGS に追加された暗号化証明書と署名証明書の公開キーと秘密キーの両方にアクセスできる必要があります。
具体的には、HGS サービスを実行するグループの管理されたサービスアカウント (gMSA) は、キーへのアクセスを必要とします。
HGS で使用される gMSA を検索するには、HGS サーバーで管理者特権の PowerShell プロンプトで次のコマンドを実行します。

```powershell
(Get-IISAppPool -Name KeyProtection).ProcessModel.UserName
```

秘密キーを使用するように gMSA アカウントアクセス権を付与する方法は、キーが格納されている場所によって異なります。コンピューター上では、ローカル証明書ファイル、ハードウェアセキュリティモジュール (HSM)、またはカスタムサードパーティキー記憶域プロバイダーを使用します。

#### <a name="grant-access-to-software-backed-private-keys"></a>ソフトウェアがサポートする秘密キーへのアクセスを許可する

ハードウェアセキュリティモジュールまたはカスタムキー記憶域プロバイダーに格納されて**いない**証明機関によって発行された自己署名証明書または証明書を使用している場合は、次の手順を実行して、秘密キーのアクセス許可を変更できます。

1. ローカル証明書マネージャー (certlm .msc) を開く
2. [**個人用 > 証明**書] を展開し、更新する署名証明書または暗号化証明書を見つけます。
3. 証明書を右クリックし、[**すべてのタスク] > [秘密キーの管理**] を選択します。
4. 新しいユーザーに certiciate の秘密キーへのアクセスを許可するには、 **[追加]** をクリックします。
5. オブジェクトピッカーで、前に見つかった HGS の gMSA アカウント名を入力し、[ **OK]** をクリックします。
6. GMSA に証明書への**読み取り**アクセス権があることを確認します。
7. [ **OK]** をクリックして、アクセス許可ウィンドウを閉じます。

Server Core で HGS を実行している場合、またはサーバーをリモートで管理している場合は、ローカル証明書マネージャーを使用して秘密キーを管理することはできません。
代わりに、PowerShell でアクセス許可を管理できるように、保護された[ファブリックツールの powershell モジュール](https://www.powershellgallery.com/packages/GuardedFabricTools)をダウンロードする必要があります。

1. Server Core コンピューターで管理者特権の PowerShell コンソールを開くか、HGS に対するローカル管理者のアクセス許可を持つアカウントで PowerShell リモート処理を使用します。
2. 次のコマンドを実行して、保護されたファブリックツールの PowerShell モジュールをインストールし、gMSA アカウントに秘密キーへのアクセス権を付与します。

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

#### <a name="grant-access-to-hsm-or-custom-provider-backed-private-keys"></a>HSM またはカスタムプロバイダーによってサポートされる秘密キーへのアクセスを許可する

証明書の秘密キーがハードウェアセキュリティモジュール (HSM) またはカスタムキー格納プロバイダー (KSP) によってサポートされている場合、アクセス許可モデルは特定のソフトウェアベンダーによって異なります。
最適な結果を得るには、ベンダーのドキュメントまたはサポートサイトで、特定のデバイス/ソフトウェアの秘密キーのアクセス許可をどのように処理するかについて確認してください。

一部のハードウェアセキュリティモジュールは、特定のユーザーアカウントに秘密キーへのアクセス権を付与することをサポートしていません。代わりに、コンピューターアカウントが特定のキーセット内のすべてのキーにアクセスできるようにします。
このようなデバイスでは、通常、コンピューターにキーへのアクセス権を付与するだけで十分です。 HGS はその接続を利用できます。

**Hsm のヒント**

以下は、Microsoft とそのパートナーのエクスペリエンスに基づいて、HGS で HSM でサポートされているキーを正常に使用するための推奨構成オプションです。
これらのヒントは、利便性のために提供されており、読み取り時には正しいとは限りません。また、HSM 製造元によっても保証されていません。
詳細な質問がある場合は、特定のデバイスに関する正確な情報を HSM の製造元に問い合わせてください。

HSM ブランド/シリーズ      | 推奨事項
----------------------|-------------
Gemalto SafeNet       | 証明書要求ファイルのキー使用法プロパティが0xa0 に設定されていることを確認して、署名と暗号化に証明書を使用できるようにします。 さらに、ローカルの証明書マネージャーツールを使用して、gMSA アカウントに秘密キーへの*読み取り*アクセス権を付与する必要があります (上記の手順を参照)。
nCipher nShield        | 各 HGS ノードが、署名キーと暗号化キーを含むセキュリティワールドにアクセスできることを確認します。 GMSA 固有のアクセス許可を構成する必要はありません。
Utimaco CryptoServers | 証明書要求ファイルのキー使用法プロパティが0x13 に設定されていることを確認し、暗号化、復号化、署名に証明書を使用できるようにします。

### <a name="certificate-requests"></a>証明書の要求

公開キー基盤 (PKI) 環境で証明機関を使用して証明書を発行する場合は、証明書の要求に、それらのキーの HGS の使用に必要な最小要件が含まれていることを確認する必要があります。

**署名証明書**

CSR プロパティ | 必須の値
-------------|---------------
アルゴリズム    | RSA
キーサイズ     | 2048ビット以上
キー使用法    | Signature/Sign/Digitalsignature ビット

**暗号化証明書**

CSR プロパティ | 必須の値
-------------|---------------
アルゴリズム    | RSA
キーサイズ     | 2048ビット以上
キー使用法    | 暗号化/暗号化/DataEncipherment

**証明書サービステンプレートの Active Directory**

Active Directory 証明書サービス (ADCS) 証明書テンプレートを使用して証明書を作成する場合は、次の設定でテンプレートを使用することをお勧めします。

ADCS Template プロパティ | 必須の値
-----------------------|---------------
プロバイダーカテゴリ      | キー ストレージ プロバイダー
アルゴリズム名         | RSA
最小キーサイズ       | 2048
目的                | 署名と暗号化
キー使用法の拡張機能    | デジタル署名、キーの暗号化、データの暗号化 ("ユーザーデータの暗号化を許可する")


### <a name="time-drift"></a>時間のずれ

サーバーの時間が、保護されたファブリック内の他の HGS ノードまたは Hyper-v ホストのドリフトを大幅に超過している場合、構成証明者の証明書の有効性に関する問題が発生する可能性があります。
構成証明者の証明書は、HGS のバックグラウンドで作成および更新され、構成証明サービスによって保護されたホストに発行された正常性証明書に署名するために使用されます。

構成証明者の証明書を更新するには、管理者特権の PowerShell プロンプトで次のコマンドを実行します。

```powershell
Start-ScheduledTask -TaskPath \Microsoft\Windows\HGSServer -TaskName 
AttestationSignerCertRenewalTask
```

または、**タスクスケジューラ**(taskHGSServer d .msc) を開き、タスクスケジューラライブラリに移動し **> Microsoft > Windows >** を開き、という名前**のタスクを実行して、スケジュールされたタスクを手動で実行することもできます。AttestationSignerCertRenewalTask**。

## <a name="switching-attestation-modes"></a>構成証明モードの切り替え

[HgsServer](https://technet.microsoft.com/library/mt652180.aspx)コマンドレットを使用して HGS を TPM モードから Active Directory モードに切り替えるか、またはその逆に切り替えると、hgs クラスター内のすべてのノードが新しい構成証明モードの適用を開始するまでに最大10分かかることがあります。
これは通常の動作です。
新しい構成証明モードを使用してすべてのホストが正常に証明されていることを確認するまで、以前の構成証明モードからホストを許可するポリシーは削除しないことをお勧めします。

**TPM から AD モードに切り替えるときの既知の問題**

TPM モードで HGS クラスターを初期化し、後で Active Directory モードに切り替える場合、既知の問題があります。これにより、HGS クラスター内の他のノードが新しい構成証明モードに切り替わるのを防ぐことができます。
すべての HGS サーバーで正しい構成証明モードが適用されていることを確認するには、HGS クラスターの**各ノードで**`Set-HgsServer -TrustActiveDirectory` を実行します。
この問題は、TPM モードから AD モードに切り替える場合には適用されません。また、クラスターが元々 AD モードでセットアップされ*て*いる場合は、この問題は発生しません。

HGS サーバーの構成証明モードは、 [HgsServer](https://technet.microsoft.com/library/mt652162.aspx)を実行して確認できます。

## <a name="memory-dump-encryption-policies"></a>メモリダンプの暗号化ポリシー

メモリダンプの暗号化ポリシーを構成しようとしているときに、既定の HGS ダンプポリシー (hgs @ no__t-0NoDumps、hgs @ no__t-1DumpEncryption と Hgs @ no__t)、またはダンプポリシーのコマンドレット (HgsAttestationDumpPolicy) が表示されない場合は、最新の累積的な更新プログラムがインストールされていない可能性があります。
この問題を解決するには、 [HGS サーバー](guarded-fabric-manage-hgs.md#patching-hgs)を最新の累積 Windows 更新プログラムに更新し、[新しい構成証明ポリシーをアクティブ化](guarded-fabric-manage-hgs.md#updates-requiring-policy-activation)します。
新しい構成証明ポリシーをアクティブ化する前に、Hyper-v ホストを同じ累積的な更新プログラムに更新してください。新しいダンプ暗号化機能がインストールされていないホストは、HGS ポリシーをアクティブ化すると、構成証明に失敗する可能性があります。

## <a name="endorsement-key-certificate-error-messages"></a>保証キー証明書のエラーメッセージ

[HgsAttestationTpmHost](https://docs.microsoft.com/powershell/module/hgsattestation/add-hgsattestationtpmhost)コマンドレットを使用してホストを登録すると、提供されているプラットフォーム識別子ファイルから、保証キー証明書 (EKcert) と公開保証キー (EKpub) の2つの TPM 識別子が抽出されます。
EKcert は TPM の製造元を識別し、TPM が本物であり、通常のサプライチェーンによって製造されていることを保証します。
EKpub は、特定の TPM を一意に識別します。これは、HGS がシールドされた Vm を実行するためのホストアクセスを許可するために使用するメジャーの1つです。

次の2つの条件のいずれかに該当する場合、TPM ホストの登録時にエラーが表示されます。
1. プラットフォーム識別子ファイルに保証キー証明書が含まれて**いません**
2. プラットフォーム識別子ファイルには保証キー証明書が含まれていますが、その証明書はシステムで信頼されて**いません**

特定の TPM 製造元には、EKcerts が Tpm に含まれていません。
TPM でこれが発生していると思われる場合は、Tpm に EKcert がないことを OEM に確認し、`-Force` フラグを使用してホストを HGS に手動で登録してください。
TPM に EKcert が含まれていても、プラットフォーム識別子ファイルに見つからなかった場合は、ホストで[Get PlatformIdentifier](https://docs.microsoft.com/powershell/module/platformidentifier/get-platformidentifier)を実行するときに、管理者 (管理者特権) の PowerShell コンソールを使用していることを確認してください。

EKcert が信頼できないというエラーが表示された場合は、各 HGS サーバーに[信頼できる tpm ルート証明書パッケージがインストールさ](guarded-fabric-install-trusted-tpm-root-certificates.md)れていること、および tpm ベンダーのルート証明書がローカルコンピューターの**trustedtpm @ no__ に存在していることを確認してください。t-2RootCA**ストア。 適用可能な中間証明書は、ローカルコンピューターの**Trustedtpm @ no__t-1IntermediateCA**ストアにもインストールする必要があります。
ルート証明書と中間証明書をインストールすると、@no__t 0 を正常に実行できるようになります。
