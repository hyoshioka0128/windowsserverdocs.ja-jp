---
title: certreq
description: Certreq コマンドの参照記事。証明機関 (CA) から証明書を要求し、CA からの以前の要求への応答を取得し、.inf ファイルから新しい要求を作成し、要求に対する応答を受け入れてインストールし、既存の CA 証明書または要求からのクロス証明または限定従属の要求を作成し、クロス証明または限定従属の要求
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d51cc178ee5b689071336b0dabd1e8d3565bcd2
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955364"
---
# <a name="certreq"></a>certreq

Certreq コマンドを使用して、証明機関 (CA) から証明書を要求することができます。 CA からの要求に対する応答を取得するには、.inf ファイルから新しい要求を作成し、要求への応答を受け入れてインストールするには、既存の CA 証明書または要求からクロス証明または限定従属の要求を構築するには、クロス証明または限定従属の要求に署名します。

> [!IMPORTANT]
> 以前のバージョンの certreq コマンドでは、ここで説明するすべてのオプションが提供されない場合があります。 特定のバージョンの certreq に基づいてサポートされているオプションを確認するには、コマンドラインヘルプオプションのを実行し `certreq -v -?` ます。
>
> Certreq コマンドでは、CEP/CES 環境でのキーの構成証明テンプレートに基づく新しい証明書要求の作成はサポートされていません。

> [!WARNING]
> このトピックの内容は、Windows Server の既定の設定に基づいています。たとえば、キーの長さを2048に設定し、Microsoft ソフトウェアキー記憶域プロバイダーを CSP として選択し、セキュアハッシュアルゴリズム 1 (SHA1) を使用します。 これらの選択は、会社のセキュリティポリシーの要件に照らして評価します。

## <a name="syntax"></a>構文

```
certreq [-submit] [options] [requestfilein [certfileout [certchainfileout [fullresponsefileOut]]]]
certreq -retrieve [options] requestid [certfileout [certchainfileout [fullresponsefileOut]]]
certreq -new [options] [policyfilein [requestfileout]]
certreq -accept [options] [certchainfilein | fullresponsefilein | certfilein]
certreq -sign [options] [requestfilein [requestfileout]]
certreq –enroll [options] templatename
certreq –enroll –cert certId [options] renew [reusekeys]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------- | ----------- |
| -submit | 証明機関に要求を送信します。 |
| -取得`<requestid>` | 証明機関からの前の要求に対する応答を取得します。 |
| -新規 | .Inf ファイルから新しい要求を作成します。 |
| -accept | 証明書要求に対する応答を受け入れてインストールします。 |
| -ポリシー | 要求のポリシーを設定します。 |
| -sign | クロス証明または限定従属の要求に署名します。 |
| -登録 | 証明書を登録または更新します。 |
| -? | Certreq 構文、オプション、および説明の一覧を表示します。 |
| `<parameter>` -? | 指定されたパラメーターのヘルプを表示します。 |
| -v-? | Certreq 構文、オプション、および説明の詳細リストを表示します。 |

## <a name="examples"></a>例

### <a name="certreq--submit"></a>certreq-送信

単純な証明書要求を送信するには、次のようにします。

```
certreq –submit certrequest.req certnew.cer certnew.pfx
```

#### <a name="remarks"></a>注釈

- これは、既定の certreq.exe パラメーターです。 コマンドラインプロンプトでオプションが指定されていない場合、certreq.exe は証明機関に証明書要求を送信しようとします。 **– Submit**オプションを使用する場合は、証明書の要求ファイルを指定する必要があります。 このパラメーターを省略すると、一般的な [**ファイルを開く**] ウィンドウが表示され、適切な証明書要求ファイルを選択できます。

- SAN 属性を指定して証明書を要求するには、マイクロソフトサポート技術情報の記事931351「[セキュリティで保護された LDAP 証明書にサブジェクトの別名を追加する方法](https://support.microsoft.com/kb/931351)」の「 *certreq.exe ユーティリティを使用して証明書の要求を作成および送信する方法*」セクションを参照してください。

### <a name="certreq--retrieve"></a>certreq-取得

証明書 ID 20 を取得し、 *Mycertificate*という名前の証明書ファイル (.cer) を作成するには、次のようにします。

```
certreq -retrieve 20 MyCertificate.cer
```

#### <a name="remarks"></a>注釈

- 証明機関によって発行された証明書を取得するには、certreq- *requestid*を使用します。 *Requestid* pkc は、0x プレフィックスを持つ10進数または16進数にすることができ、プレフィックスなしの証明書のシリアル番号にすることができます。 また、証明書の要求が保留中であるかどうかにかかわらず、証明機関によって発行された証明書 (失効または期限切れの証明書を含む) を取得するために使用することもできます。

- 証明機関に要求を送信する場合、証明機関のポリシーモジュールは要求を保留状態のままにし、 *requestid*を表示のために certreq 呼び出し元に返します。 最終的には、証明機関の管理者が証明書を発行するか、要求を拒否します。

### <a name="certreq--new"></a>certreq-新規

新しい要求を作成するには:

```
[newrequest]
; At least one value must be set in this section
subject = CN=W2K8-BO-DC.contoso2.com
```

次に、INF ファイルに追加される可能性のあるいくつかのセクションを示します。

#### <a name="newrequest"></a>[newrequest]

INF ファイルのこの領域は、新しい証明書要求テンプレートでは必須です。値を持つパラメーターを少なくとも1つ含める必要があります。

| キー<sup>1</sup> | 説明 | 値<sup>2</sup> | 例 |
| --- | ---------- | ----- | ------- |
| サブジェクト | いくつかのアプリは、証明書のサブジェクト情報に依存しています。 このキーの値を指定することをお勧めします。 サブジェクトがここで設定されていない場合は、サブジェクトの別名証明書の拡張機能の一部としてサブジェクト名を含めることをお勧めします。 | 相対識別名の文字列値 | Subject = CN = computer1 Subject = CN = John Smith, CN = Users, DC = Contoso, DC = com |
| Exportable | TRUE に設定すると、秘密キーを証明書と共にエクスポートできます。 高いレベルのセキュリティを確保するため、秘密キーをエクスポートすることはできません。ただし、場合によっては、複数のコンピューターまたはユーザーが同じ秘密キーを共有する必要がある場合に必要になることがあります。 | `true | false` | `Exportable = TRUE`. CNG キーは、この形式のエクスポート可能なプレーンテキストを区別できます。 CAPI1 キーを使うことはできません。 |
| ExportableEncrypted | 秘密キーをエクスポート可能にするように設定する必要があるかどうかを指定します。 | `true | false` | `ExportableEncrypted = true`<p>**ヒント:** すべての公開キーのサイズとアルゴリズムがすべてのハッシュアルゴリズムで動作するわけではありません。 指定された CSP は、指定されたハッシュアルゴリズムもサポートする必要があります。 サポートされているハッシュアルゴリズムの一覧を表示するには、次のコマンドを実行します。`certutil -oid 1 | findstr pwszCNGAlgid | findstr /v CryptOIDInfo` |
| HashAlgorithm | この要求に使用するハッシュアルゴリズム。 | `Sha256, sha384, sha512, sha1, md5, md4, md2` | `HashAlgorithm = sha1`. サポートされているハッシュアルゴリズムの一覧については、「certutil-oid 1」を参照してください。 | findstr pwszCNGAlgid | findstr/v CryptOIDInfo|
| KeyAlgorithm| サービスプロバイダーが公開キーと秘密キーのペアを生成するために使用するアルゴリズム。| `RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521` | `KeyAlgorithm = RSA` |
| KeyContainer | 新しいキーマテリアルが生成される新しい要求に対しては、このパラメーターを設定しないことをお勧めします。 キーコンテナーは、システムによって自動的に生成され、維持されます。<p>既存のキーマテリアルを使用する必要がある要求の場合、この値は既存のキーのキーコンテナー名に設定できます。 コマンドを使用して、 `certutil –key` マシンコンテキストで使用可能なキーコンテナーの一覧を表示します。 現在の `certutil –key –user` ユーザーのコンテキストに対してコマンドを使用します。| ランダムな文字列値<p>**ヒント:** Inf 解析の問題の可能性を回避するには、空白または特殊文字を含む INF キー値を二重引用符で囲んでください。 | `KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}` |
| Keylength | 公開キーと秘密キーの長さを定義します。 キーの長さは、証明書のセキュリティレベルに影響します。 キーの長さが多いほど、通常は高いセキュリティレベルになります。ただし、一部のアプリケーションでは、キーの長さに関する制限が適用される場合があります。 | 暗号化サービスプロバイダーでサポートされている任意の有効なキーの長さ。 | `KeyLength = 2048` |
| KeySpec | キーを署名、Exchange (暗号化)、またはその両方に使用できるかどうかを決定します。 | `AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE` | `KeySpec = AT_KEYEXCHANGE` |
| KeyUsage | 証明書キーを使用する必要があるかどうかを定義します。 | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> | `KeyUsage = CERT_DIGITAL_SIGNATURE_KEY_USAGE | CERT_KEY_ENCIPHERMENT_KEY_USAGE`<p>**ヒント:** 複数の値がパイプを使用しています (|) 記号の区切り記号。 複数の値を使用する場合は、INF 解析の問題を回避するために二重引用符を使用してください。 表示される値は、各ビット定義の16進数 (10 進数) 値です。 以前の構文も使用できます。シンボリック表現ではなく、複数のビットが設定された単一の16進値です。 たとえば、「 `KeyUsage = 0xa0` 」のように入力します。 |
| Keyのプロパティ | 秘密キーを使用できる特定の目的を識別する値を取得します。 | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> | `KeyUsageProperty = NCRYPT_ALLOW_DECRYPT_FLAG | NCRYPT_ALLOW_SIGNING_FLAG` |
| MachineKeySet | このキーは、ユーザーではなく、コンピューターによって所有されている証明書を作成する必要がある場合に重要です。 生成されるキーマテリアルは、要求を作成したセキュリティプリンシパル (ユーザーまたはコンピューターアカウント) のセキュリティコンテキストで保持されます。 管理者がコンピューターの代わりに証明書要求を作成する場合、キーマテリアルは、管理者のセキュリティコンテキストではなく、コンピューターのセキュリティコンテキストで作成する必要があります。 そうしないと、管理者のセキュリティコンテキストにあるため、コンピューターは秘密キーにアクセスできませんでした。 | `true | false`. 既定値は false です。 | `MachineKeySet = true` |
| NotBefore | 要求を発行できない日付または日付と時刻を指定します。 `NotBefore`およびと共に使用でき `ValidityPeriod` `ValidityPeriodUnits` ます。 | 日付または日付と時刻 | `NotBefore = 7/24/2012 10:31 AM`<p>**ヒント:** `NotBefore`および `NotAfter` は R `equestType=cert` 専用です。 日付の解析は、ロケールを区別するように試行されます。 月の名前を使用すると、すべてのロケールで明確になり、機能します。 |
| NotAfter | 要求を発行できない日付または日付と時刻を指定します。 `NotAfter`またはと共に使用することはできません `ValidityPeriod` `ValidityPeriodUnits` 。 | 日付または日付と時刻 | `NotAfter = 9/23/2014 10:31 AM`<p>**ヒント:** `NotBefore`と `NotAfter` は、のみを対象としてい `RequestType=cert` ます。 日付の解析は、ロケールを区別するように試行されます。 月の名前を使用すると、すべてのロケールで明確になり、機能します。 |
| PrivateKeyArchive | PrivateKeyArchive 設定は、対応する RequestType が CMC に設定されている場合にのみ機能します。これは、証明書管理メッセージ (CMC) の要求形式のみが、キーのアーカイブのために要求元の秘密キーを CA に安全に転送できるためです。 | `true | false` | `PrivateKeyArchive = true` |
| [EncryptionAlgorithm] | 使用する暗号化アルゴリズム。 | 使用可能なオプションは、オペレーティングシステムのバージョンとインストールされている暗号化サービスプロバイダーのセットによって異なります。 使用可能なアルゴリズムの一覧を表示するには、コマンドを実行します `certutil -oid 2 | findstr pwszCNGAlgid` 。 使用する指定された CSP は、指定された対称暗号化アルゴリズムと長さもサポートする必要があります。 | `EncryptionAlgorithm = 3des` |
| EncryptionLength | 使用する暗号化アルゴリズムの長さ。 | 指定した EncryptionAlgorithm で許可されている任意の長さ。 | `EncryptionLength = 128` |
| ProviderName | プロバイダー名は、CSP の表示名です。 | 使用している CSP のプロバイダー名がわからない場合は、 `certutil –csplist` コマンドラインからを実行します。 このコマンドは、ローカルシステムで使用可能なすべての Csp の名前を表示します。 | `ProviderName = Microsoft RSA SChannel Cryptographic Provider` |
| ProviderType | プロバイダーの種類は、RSA Full などの特定のアルゴリズム機能に基づいて特定のプロバイダーを選択するために使用されます。 | 使用している CSP のプロバイダーの種類がわからない場合は、 `certutil –csplist` コマンドラインプロンプトからを実行します。 このコマンドは、ローカルシステムで使用可能なすべての Csp のプロバイダーの種類を表示します。 | `ProviderType = 1` |
| RenewalCert | 証明書の要求が生成されたシステム上に存在する証明書を更新する必要がある場合は、その証明書のハッシュをこのキーの値として指定する必要があります。 | 証明書要求が作成されたコンピューターで使用可能な証明書の証明書ハッシュ。 証明書のハッシュがわからない場合は、証明書 MMC スナップインを使用して、更新する必要がある証明書を確認します。 証明書のプロパティを開き、 `Thumbprint` 証明書の属性を確認します。 証明書の更新に `PKCS#7` は、またはのいずれかの要求形式が必要です `CMC` 。 | `RenewalCert = 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D` |
| RequesterName | 別のユーザー要求の代理として登録するように要求を作成します。また、登録エージェント証明書を使用して要求に署名する必要があります。これを行わないと、CA は要求を拒否します。 オプションを使用して、 `-cert` 登録エージェントの証明書を指定します。 `RequestType`がまたはに設定されている場合、証明書の要求に対して要求者名を指定でき `PKCS#7` `CMC` ます。 がに設定されている場合 `RequestType` `PKCS#10` 、このキーは無視されます。 は、 `Requestername` 要求の一部としてのみ設定できます。 保留中の要求でを操作することはできません `Requestername` 。 | `Domain\User` | `Requestername = Contoso\BSmith` |
| RequestType | 証明書要求を生成して送信するために使用される標準を決定します。 | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul>**ヒント:** このオプションは、自己署名または自己発行の証明書を示します。 要求を生成するのではなく、新しい証明書を作成してから、証明書をインストールします。 "自己署名" は既定値です。 – Cert オプションを使用して署名証明書を指定し、自己署名されていない自己発行の証明書を作成します。 | `RequestType = CMC` |
| SecurityDescriptor | セキュリティ保護可能なオブジェクトに関連付けられたセキュリティ情報を格納します。 ほとんどのセキュリティ保護可能なオブジェクトでは、オブジェクトを作成する関数呼び出しでオブジェクトのセキュリティ記述子を指定できます。[セキュリティ記述子定義言語](/windows/win32/secauthz/security-descriptor-definition-language)に基づく文字列。<p>**ヒント:** これは、コンピューターコンテキストのスマートカード以外のキーにのみ関連します。 | `SecurityDescriptor = D:P(A;;GA;;;SY)(A;;GA;;;BA)` |
| AlternateSignatureAlgorithm | PKCS # 10 要求または証明書署名の署名アルゴリズムオブジェクト識別子 (OID) が不連続であるか結合されているかを示すブール値を指定して取得します。 | `true | false` | `AlternateSignatureAlgorithm = false`<p>RSA 署名の場合、 `false` はを示しますが、は `Pkcs1 v1.5` `true` シグネチャを示し `v2.1` ます。 |
| サイレント | 既定では、このオプションを使用すると、ユーザーの対話型デスクトップにアクセスしたり、スマートカードの PIN などの情報を要求したりすることができます。 このキーが TRUE に設定されている場合、CSP はデスクトップと対話する必要がなく、ユーザーインターフェイスの表示がブロックされます。 | `true | false` | `Silent = true` |
| S | このパラメーターが TRUE に設定されている場合、オブジェクト識別子の値1.2.840.113549.1.9.15 を持つ拡張機能が要求に追加されます。 オブジェクト識別子の数は、インストールされているオペレーティングシステムのバージョンと CSP の機能によって異なります。これは、Outlook などの Secure Multipurpose Internet Mail Extensions (S/MIME) アプリケーションで使用される対称暗号化アルゴリズムを指します。 | `true | false` | `SMIME = true` |
| UseExistingKeySet | このパラメーターは、既存のキーペアを証明書要求の作成に使用することを指定するために使用されます。 このキーが TRUE に設定されている場合は、RenewalCert キーまたは KeyContainer 名の値も指定する必要があります。 既存のキーのプロパティを変更することはできないため、エクスポート可能なキーは設定しないでください。 この場合、証明書の要求の作成時にキーマテリアルは生成されません。 | `true | false` | `UseExistingKeySet = true` |
| KeyProtection | 秘密キーを使用する前に保護する方法を示す値を指定します。 | <ul><li>`XCN_NCRYPT_UI_NO_PROTCTION_FLAG -- 0`</li><li>`XCN_NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> | `KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG` |
| SuppressDefaults | 既定の拡張機能と属性が要求に含まれるかどうかを示すブール値を指定します。 既定値は、オブジェクト識別子 (Oid) によって表されます。 | `true | false` | `SuppressDefaults = true` |
| FriendlyName | 新しい証明書のフレンドリ名。 | Text | `FriendlyName = Server1` |
| ValidityPeriodUnits | ValidityPeriod で使用する単位の数を指定します。 注: これは、がの場合にのみ使用され `request type=cert` ます。 | 数値 | `ValidityPeriodUnits = 3` |
| ValidityPeriod | ValidityPeriod は米国英語の複数形の期間である必要があります。 注: これは、要求の種類が cert の場合にのみ使用されます。 | `Years |  Months | Weeks | Days | Hours | Minutes | Seconds` | `ValidityPeriod = Years` |

<sup>1</sup>等号 (=) の左側のパラメーター

<sup>2</sup>等号 (=) の右側のパラメーター

#### <a name="extensions"></a>補助

このセクションは省略可能です。

| 拡張 OID | 定義 | 例 |
| ------------- | ---------- | ----- | ------- |
| 2.5.29.17 | | 2.5.29.17 = {text} |
| *continue* | | `continue = UPN=User@Domain.com&` |
| *continue* | | `continue = EMail=User@Domain.com&` |
| *continue* | | `continue = DNS=host.domain.com&` |
| *continue* | | `continue = DirectoryName=CN=Name,DC=Domain,DC=com&` |
| *continue* | | `continue = URL=<http://host.domain.com/default.html&>` |
| *continue* | | `continue = IPAddress=10.0.0.1&` |
| *continue* | | `continue = RegisteredId=1.2.3.4.5&` |
| *continue* | | `continue = 1.2.3.4.6.1={utf8}String&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}AAECAwQFBgc=&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07&` |
| *continue* | | `continue = 1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&` |
| *continue* | | `continue = 1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07` |
| 2.5.29.37 | | `2.5.29.37={text}` |
| *continue* | | `continue = 1.3.6.1.5.5.7` |
| *continue* | | `continue = 1.3.6.1.5.5.7.3.1` |
| 2.5.29.19 | | `{text}ca=0pathlength=3` |
| 重要 | | `Critical=2.5.29.19` |
| KeySpec | | <ul><li>`AT_NONE -- 0`</li><li>`AT_SIGNATURE -- 2`</li><li>`AT_KEYEXCHANGE -- 1`</ul></li> |
| RequestType | | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul> |
| KeyUsage | | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> |
| Keyのプロパティ | | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> |
| KeyProtection | | <ul><li>`NCRYPT_UI_NO_PROTECTION_FLAG -- 0`</li><li>`NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> |
| SubjectNameFlags | template | <ul><li>`CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME -- 40000000 (1073741824)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH -- 80000000 (2147483648)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN -- 10000000 (268435456)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_EMAIL -- 20000000 (536870912)`</li><li>`CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME -- 8`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID -- 1000000 (16777216)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DNS -- 8000000 (134217728)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS -- 400000 (4194304)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL -- 4000000 (67108864)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_SPN -- 800000 (8388608)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_UPN -- 2000000 (33554432)`</li></ul> |
| 「X500nameflags | | <ul><li>`CERT_NAME_STR_NONE -- 0`</li><li>`CERT_OID_NAME_STR -- 2`</li><li>`CERT_X500_NAME_STR -- 3`</li><li>`CERT_NAME_STR_SEMICOLON_FLAG -- 40000000 (1073741824)`</li><li>`CERT_NAME_STR_NO_PLUS_FLAG -- 20000000 (536870912)`</li><li>`CERT_NAME_STR_NO_QUOTING_FLAG -- 10000000 (268435456)`</li><li>`CERT_NAME_STR_CRLF_FLAG -- 8000000 (134217728)`</li><li>`CERT_NAME_STR_COMMA_FLAG -- 4000000 (67108864)`</li><li>`CERT_NAME_STR_REVERSE_FLAG -- 2000000 (33554432)`</li><li>`CERT_NAME_STR_FORWARD_FLAG -- 1000000 (16777216)`</li><li>`CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG -- 10000 (65536)`</li><li>`CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG -- 20000 (131072)`</li><li>`CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG -- 40000 (262144)`</li><li>`CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG -- 80000 (524288)`</li><li>`CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG -- 100000 (1048576)`</li><li>`CERT_NAME_STR_ENABLE_PUNYCODE_FLAG -- 200000 (2097152)`</li></ul> |

> [!NOTE]
> `SubjectNameFlags`現在のユーザーまたは現在のコンピューターのプロパティ (DNS 名、UPN など) に基づいて、certreq によって自動的に設定される**サブジェクト**と**SubjectAltName**の拡張フィールドを INF ファイルで指定できるようにします。 Literal テンプレートを使用することは、代わりにテンプレート名フラグが使用されることを意味します。 これにより、1つの INF ファイルを複数のコンテキストで使用して、コンテキスト固有のサブジェクト情報を含む要求を生成できます。
>
> `X500NameFlags``CertStrToName`値が asn.1 エンコードされた `Subject INF keys` 識別**名**に変換されるときに、API に直接渡されるフラグを指定します。

#### <a name="example"></a>例

ポリシーファイル (.inf) をメモ帳で作成し、 *requestconfig .inf*として保存するには、次のようにします。

```
[NewRequest]
Subject = CN=<FQDN of computer you are creating the certificate>
Exportable = TRUE
KeyLength = 2048
KeySpec = 1
KeyUsage = 0xf0
MachineKeySet = TRUE
[RequestAttributes]
CertificateTemplate=WebServer
[Extensions]
OID = 1.3.6.1.5.5.7.3.1
OID = 1.3.6.1.5.5.7.3.2
```

証明書を要求しているコンピューターで、次のようにします。

```
certreq –new requestconfig.inf certrequest.req
```

Oid に [Strings] セクション構文を使用し、その他の方法でデータを解釈する場合。 EKU 拡張の新しい {text} 構文例では、Oid のコンマ区切りリストを使用しています。

```
[Version]
Signature=$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = 2.5.29.37
szOID_PKIX_KP_SERVER_AUTH = 1.3.6.1.5.5.7.3.1
szOID_PKIX_KP_CLIENT_AUTH = 1.3.6.1.5.5.7.3.2

[NewRequest]
Subject = CN=TestSelfSignedCert
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%={text}%szOID_PKIX_KP_SERVER_AUTH%,
_continue_ = %szOID_PKIX_KP_CLIENT_AUTH%
```

### <a name="certreq--accept"></a>certreq-accept

パラメーターは、 `–accept` 以前に生成された秘密キーを発行済みの証明書とリンクし、要求が要求されたシステムから保留中の証明書要求を削除します。

証明書を手動で受け入れるには:

```
certreq -accept certnew.cer
```

> [!WARNING]
> パラメーターを `-accept` オプションおよびオプションと共に使用する `-user` と、 `–machine` **ユーザー**または**コンピューター**のコンテキストにインストールする証明書をインストールする必要があるかどうかが示されます。 インストールされている公開キーに一致するいずれかのコンテキストで未処理の要求がある場合、これらのオプションは必要ありません。 未処理の要求がない場合は、これらのいずれかを指定する必要があります。

### <a name="certreq--policy"></a>certreq-ポリシー

ポリシー .inf ファイルは、限定従属が定義されている場合に、CA 証明書に適用される制約を定義する構成ファイルです。

クロス証明書要求を作成するには:

```
certreq -policy certsrv.req policy.inf newcertsrv.req
```

パラメーターを追加せずにを使用すると `certreq -policy` 、ダイアログウィンドウが開き、要求された xfs (. req、cmc、.txt、der、.cer、または .crt) を選択できます。 要求されたファイルを選択して [**開く**] をクリックすると、別のダイアログウィンドウが開き、ポリシー .inf ファイルを選択できるようになります。

#### <a name="examples"></a>例

[Capolicy.inf 構文](../../networking/core-network-guide/cncg/server-certs/prepare-the-capolicy-inf-file.md)でポリシーの .inf ファイルの例を見つけます。

### <a name="certreq--sign"></a>certreq-sign

新しい証明書要求を作成し、署名して送信するには、次のようにします。

```
certreq -new policyfile.inf myrequest.req
certreq -sign myrequest.req myrequest.req
certreq -submit myrequest_sign.req myrequest_cert.cer
```

#### <a name="remarks"></a>注釈

- パラメーターを追加せずにを使用すると、 `certreq -sign` ダイアログウィンドウが開き、要求されたファイル (req、cmc、txt、der、cer、または crt) を選択できます。

- 限定従属の要求に署名するには、**エンタープライズ管理者**の資格情報が必要になることがあります。 これは、限定従属の署名証明書を発行するためのベストプラクティスです。

- 限定従属要求に署名するために使用される証明書は、限定従属テンプレートを使用します。 エンタープライズ管理者は、要求に署名するか、証明書に署名する個人にユーザーのアクセス許可を付与する必要があります。

- その後、追加の担当者に CMC 要求の署名が必要になる場合があります。 これは、限定従属に関連付けられている保証レベルによって異なります。

- インストールする限定された下位 CA の親 CA がオフラインの場合は、オフラインの親から限定された下位 CA の CA 証明書を取得する必要があります。 親 CA がオンラインの場合は、**証明書サービスのインストール**ウィザードで、限定された下位 CA の ca 証明書を指定します。

### <a name="certreq--enroll"></a>certreq-登録

このコメントを使用して、証明書を登録または更新することができます。

#### <a name="examples"></a>例

証明書を登録するには、 *web*サーバーテンプレートを使用し、U/I を使用してポリシーサーバーを選択します。

```
certreq -enroll –machine –policyserver * WebServer
```

シリアル番号を使用して証明書を更新するには、次のようにします。

```
certreq –enroll -machine –cert 61 2d 3c fe 00 00 00 00 00 05 renew
```

有効な証明書のみを更新できます。 期限切れの証明書は更新できないため、新しい証明書で置き換える必要があります。

## <a name="options"></a>オプション

| オプション | 説明 |
| ------- | ----------- |
| -任意 | `Force ICertRequest::Submit`エンコードの種類を確認します。|
| -attrib`<attributestring>` | **名前**と**値**の文字列のペアをコロンで区切って指定します。<p>( **Name**例: **Value** `\n` Name1: value1\nName2: value2) を使用して、名前と値の文字列ペアを区切ります。 |
| -バイナリ | 出力ファイルを base64 でエンコードされた形式ではなくバイナリとして書式設定します。 |
| -policyserver`<policyserver>` | ldap`<path>`<br>証明書の登録ポリシー web サービスを実行しているコンピューターの URI または一意の ID を挿入します。<p>参照によって要求ファイルを使用するように指定するには、にマイナス記号 (-) を使用し `<policyserver>` ます。 |
| -config`<ConfigString>` | 構成文字列で指定された CA ( **cahostame caname**) を使用して操作を処理します。 Https: \ 接続の場合は \\ 、登録サーバーの URI を指定します。 ローカルコンピューターストアの CA の場合は、マイナス記号 (-) を使用します。 |
| -匿名 | 証明書の登録 web サービスには匿名の資格情報を使用します。 |
| -kerberos | 証明書の登録 web サービスには、Kerberos (ドメイン) 資格情報を使用します。 |
| -clientcertificate`<ClientCertId>` | は、 `<ClientCertId>` 証明書の拇印、CN、EKU、テンプレート、電子メール、UPN、または新しい構文に置き換えることができ `name=value` ます。 |
| -ユーザー名`<username>` | 証明書の登録 web サービスで使用されます。 を `<username>` SAM 名または**domain\user**の値に置き換えることができます。 このオプションは、オプションと共に使用し `-p` ます。 |
| -p`<password>` | 証明書の登録 web サービスで使用されます。 `<password>`実際のユーザーのパスワードに置き換えます。 このオプションは、オプションと共に使用し `-username` ます。 |
| -ユーザー | `-user`新しい証明書要求のコンテキストを構成するか、証明書の受け入れのコンテキストを指定します。 これは、INF またはテンプレートで何も指定されていない場合の既定のコンテキストです。 |
| -コンピューター | 新しい証明書要求を構成するか、コンピューターコンテキストに対する証明書の受け入れのコンテキストを指定します。 新しい要求の場合、MachineKeyset INF キーとテンプレートコンテキストとの一貫性がある必要があります。 このオプションが指定されておらず、テンプレートでコンテキストが設定されていない場合、既定値はユーザーコンテキストになります。 |
| -crl | によって指定された base64 エンコード PKCS #7 ファイルへの出力に証明書失効リスト (Crl) を含め `certchainfileout` ます。または、によって指定された base64 エンコードファイルにも含め `requestfileout` ます。 |
| -rpc | 分散 COM ではなくリモートプロシージャコール (RPC) サーバー接続を使用するように Active Directory 証明書サービス (AD CS) に指示します。 |
| -adminforcemachine | キーサービスまたは偽装を使用して、ローカルシステムコンテキストから要求を送信します。 このオプションを呼び出しているユーザーは、ローカル管理者のメンバーである必要があります。 |
| -renewonbehalfof | 署名証明書で特定されたサブジェクトに代わって更新を送信します。 [ICertRequest:: Submit メソッド](/windows/win32/api/certcli/nf-certcli-icertrequest-submit)を呼び出すと、CR_IN_ROBO が設定します。 |
| -f | 既存のファイルを強制的に上書きします。 これにより、テンプレートとポリシーのキャッシュも省略されます。 |
| -Q | サイレントモードを使用します。すべての対話型プロンプトを非表示にします。 |
| -unicode | 標準出力がリダイレクトされるか別のコマンドにパイプ処理されるときに、Unicode 出力を書き込みます。これは、Windows PowerShell スクリプトから呼び出すときに役立ちます。 |
| -unicodetext | Base64 テキストでエンコードされたデータ blob をファイルに書き込むときに、Unicode 出力を送信します。 |

## <a name="formats"></a>形式

| 形式 | 説明 |
| ------- | ----------- |
| requestfilein | Base64 でエンコードされたまたはバイナリ入力ファイル名: PKCS #10 証明書の要求、CMS 証明書の要求、PKCS #7 証明書の更新要求、x.509 証明書をクロス認定にする、または Ssh-keygen タグ形式の証明書要求。 |
| requestfileout | Base64 でエンコードされた出力ファイル名。 |
| certfileout | Base64 でエンコードされた X-509 ファイル名。 |
| PKCS10fileout | パラメーターでのみ使用 `certreq -policy` します。 Base64 でエンコードされた PKCS10 出力ファイル名。 |
| certchainfileout | Base64 でエンコードされた PKCS #7 ファイル名。 |
| fullresponsefileout | Base64 でエンコードされた完全な応答ファイル名。 |
| policyfilein | パラメーターでのみ使用 `certreq -policy` します。 要求を限定するために使用される拡張機能のテキスト表現を含む INF ファイル。 |

## <a name="additional-resources"></a>その他の情報

次の記事には、certreq の使用例が含まれています。

- [セキュリティで保護された LDAP 証明書にサブジェクトの別名を追加する方法](https://support.microsoft.com/help/931351/how-to-add-a-subject-alternative-name-to-a-secure-ldap-certificate)

- [Test Lab Guide: Deploying an AD CS Two-Tier PKI Hierarchy](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831348(v=ws.11))

- [付録 3: Certreq.exe 構文](/previous-versions/windows/it-pro/windows-server-2003/cc736326(v=ws.10))

- [Web サーバーの SSL 証明書を手動で作成する方法](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/how-to-create-a-web-server-ssl-certificate-manually/ba-p/1128529)

- [Windows Server 2008 CA を使用して AMT プロビジョニング証明書を要求する](https://social.technet.microsoft.com/wiki/contents/articles/548.request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)

- [System Center Operations Manager エージェントの証明書の登録](https://social.technet.microsoft.com/wiki/contents/articles/2017.certificate-enrollment-for-system-center-operations-manager-agent.aspx)

- [AD CS のステップバイステップガイド: 2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)

- [サードパーティの証明機関を使用して SSL 経由で LDAP を有効にする方法](https://support.microsoft.com/help/321051/how-to-enable-ldap-over-ssl-with-a-third-party-certification-authority)
