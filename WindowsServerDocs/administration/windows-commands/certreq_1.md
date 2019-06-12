---
title: certreq
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b947a231228d66084bc61146f7347a76cf41406
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434509"
---
# <a name="certreq"></a>certreq



前の要求をそのまま使用して、クロス証明書を作成する、要求への応答をインストールする、.inf ファイルから新しい要求を作成する、CA からの応答を取得する証明機関 (CA) から証明書を要求する Certreq を使用できますか限定従属の要求から既存の CA 証明書または要求、およびクロス証明または限定従属の要求に署名します。

> [!WARNING]
> - Certreq の以前のバージョンではすべてこのドキュメントで説明されているオプションの提供はしません。 Certreq の特定のバージョンでは、構文の表記で示されているコマンドを実行している、すべてのオプションを確認できます。
> - Certreq は CEP/CES 環境でのキー構成証明書テンプレートに基づいて新しい証明書要求の作成をサポートしていません

## <a name="BKMK_Contents"></a>内容

この記事の主要なセクションは次のとおりです。
1.  [動詞](#BKMK_Verbs)
2.  [構文の表記](#BKMK_notation)
3.  [[オプション](#BKMK_Options)]
4.  [書式設定します。](#BKMK_Formats)
5.  [追加の certreq 例](#BKMK_Examples)

## <a name="BKMK_Verbs"></a>動詞

次の表の certreq コマンドで使用できる動詞について説明します

|Switch|説明|
|------|-----------|
|送信します。|CA に要求を送信します。 詳細については、次を参照してください。 [Certreq-送信](#BKMK_Submit)します。|
|-取得*RequestID*|前の要求を CA からの応答を取得します。 詳細については、次を参照してください。 [Certreq-取得](#BKMK_Retrieve)します。|
|-新しい|.Inf ファイルから新しい要求を作成します。 詳細については、次を参照してください。 [Certreq-新しい](#BKMK_New)します。|
|-そのまま使用します。|受け入れるし、証明書の要求に対する応答をインストールします。 詳細については、次を参照してください。 [Certreq-受け入れる](#BKMK_accept)します。|
|-ポリシー|要求のポリシーを設定します。 詳細については、次を参照してください。 [Certreq-ポリシー](#BKMK_policy)します。|
|署名|クロス証明または限定従属の要求に署名します。 詳細については、次を参照してください。 [Certreq-記号](#BKMK_sign)します。|
|登録するには|登録または、証明書を更新します。 詳細については、次を参照してください。 [Certreq-登録](#BKMK_enroll)します。|
|-?|Certreq 構文、オプション、および説明の一覧を表示します。|
|*\<verb>* -?|指定された動詞のヘルプを表示します。|
|-v -?|Certreq 構文、オプション、および説明の詳細な一覧が表示されます。|

戻り[内容](#BKMK_Contents)

## <a name="BKMK_notation"></a>構文の表記

-   基本的なコマンドライン構文は、次のように実行します。 `certreq -?`
-   構文については、特定の動詞を使用して certutil を使用して、実行**certreq** *\<動詞 >* **-でしょうか。**
-   テキスト ファイルに送信する certutil 構文のすべては、するには、次のコマンドを実行します。  
    -   `certreq -v -? > certreqhelp.txt`
    -   `notepad certreqhelp.txt`

次の表では、コマンドラインの構文を示すために使用される表記について説明します。

|表記法|説明|
|--------|-----------|
|角かっこまたは中かっこのないテキスト|項目に示すように入力する必要があります。|
|\<山かっこ内のテキスト >|プレース ホルダーの値を指定する必要があります。|
|[角かっこ内のテキスト]|省略可能な項目|
|{中かっこ内のテキスト}|必要な項目のセットいずれかを選択します。|
|垂直バー (&#124;)|相互に排他的な項目の区切り記号いずれかを選択します。|
|省略記号 (...)|項目を繰り返すことができます。|

戻り[内容](#BKMK_Contents)

## <a name="BKMK_Submit"></a>Certreq -submit

Certreq.exe はオプションが指定されていない場合に明示的にコマンド ライン プロンプトで、既定の certreq.exe パラメーターは、CA に証明書要求を送信する試行します。
```
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]
```
使用する場合は、証明書要求ファイルを指定する必要があります – オプションを送信します。 このパラメーターを省略すると、適切な証明書要求ファイルを選択する一般的なファイルを開くウィンドウが表示されます。

これらの例は、証明書の送信要求を構築するのに開始点として使用できます。

送信するには、は、単純な証明書の要求は、次の例を使用します。
```
certreq –submit certRequest.req certnew.cer certnew.pfx
```
証明書を要求するには、SAN 属性を指定する、マイクロソフト サポート技術情報記事 931351 の詳細な手順を参照してください[セキュリティで保護された LDAP 証明書にサブジェクトの別名を追加する方法](https://support.microsoft.com/kb/931351)に Certreq.exe ユーティリティを使用する方法」。作成して、SAN を含む証明書の要求を送信する」のセクション。

戻り[内容](#BKMK_Contents)

## <a name="BKMK_Retrieve"></a>Certreq -retrieve

```
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]
```
-   -Config CAComputerName\CANamea ダイアログ ボックスで、CAComputerName または ca 名を指定しない場合が表示され、使用可能なすべての Ca の一覧を表示します。
-   -Config --config CAComputerName\CAName ではなくを使用する場合、既定の CA を使用して、操作が処理されます。
-   Certreq を使用することができます-取得*RequestID* CA が発行して実際には、証明書を取得します。 *RequestID*PKC は、10 進数または 0 x プレフィックスとこれを 16 進数は 0 x プレフィックスなしで証明書のシリアル番号を指定できます。 既にかどうか、証明書の要求がかつての保留中の状態に関係なく、失効または期限が切れた証明書を含む、CA によって発行された任意の証明書の取得に使用できます。
-   CA のポリシー モジュールは、可能性があります、保留中の状態と戻り値の要求のままに、CA に対する要求を送信する場合、 *RequestID* Certreq 呼び出し元の表示にします。 最終的には、CA の管理者は証明書を発行または、要求を拒否します。

次のコマンドは、20 証明書の id を取得し、証明書ファイル (.cer) を作成します。
```
certreq -retrieve 20 MyCertificate.cer 
```
戻り[内容](#BKMK_Contents)

## <a name="BKMK_New"></a>Certreq -new

```
certreq -new [Options] [PolicyFileIn [RequestFileOut]]
```
パラメーターとオプションを指定する豊富な一連の INF ファイルなので、管理者がすべての目的で使用する既定のテンプレートを定義する困難です。 そのため、このセクションでは、特定のニーズに合わせて INF ファイルを作成するためのすべてのオプションについて説明します。 次のキーワードを使用して、INF ファイルの構造を記述します。
1.  A*セクション*はキーの論理グループをカバーする INF ファイルの領域です。 セクションは、常に角かっこ、INF ファイル内に表示されます。
2.  A*キー*等号の左側に表示されるパラメーターです。
3.  A*値*等号の右側に表示されるパラメーターです。

たとえば、最小限の INF ファイルは、次のようなになります。
```
[NewRequest] 
; At least one value must be set in this section 
Subject = "CN=W2K8-BO-DC.contoso2.com"
```
INF ファイルに追加できる使用可能なセクションの一部を次に示します。

**[NewRequest]**

このセクションでは、新しい証明書の要求のテンプレートとして機能する INF ファイルの必須です。 このセクションでは、少なくとも 1 つのキー値を持つ必要があります。

|Key|定義|Value|例|
|---|----------|-----|-------|
|サブジェクト|いくつかのアプリケーションは、証明書のサブジェクト情報に依存します。 したがって、このキーの値を指定することをお勧めします。 サブジェクトがここで設定されていない場合は、サブジェクト名がサブジェクト代替名の証明書の拡張機能の一部として含めることをお勧めします。|相対識別名の文字列値|Subject = "CN=computer1.contoso.com" Subject="CN=John Smith,CN=Users,DC=Contoso,DC=com"|
|Exportable|この属性が TRUE に設定されている場合は、証明書に秘密キーをエクスポートできます。 高レベルのセキュリティを確実には、秘密キーしないでエクスポート可能です。ただし、場合によっては、これは秘密キーをエクスポートできるは、いくつかのコンピューターまたはユーザーが同じ秘密キーを共有する必要がありますしている場合に必要なする可能性があります。|true、false|エクスポート可能 = TRUE。 CNG キーをこの間で区別でき、エクスポート可能なプレーン テキスト。 CAPI1 キーことはできません。|
|ExportableEncrypted|秘密キーをエクスポート可能に設定する必要があるかどうかを指定します。|true、false|ExportableEncrypted = true</br>ヒント:すべてのパブリック キーのサイズおよびアルゴリズムについては、すべてのハッシュ アルゴリズムで動作します。 Tamehe では、CSP は、指定したハッシュ アルゴリズムもサポートする必要がありますを指定します。 サポートされているハッシュ アルゴリズムの一覧を表示するには、コマンドを実行することができます。 <code>certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo</code>|
|HashAlgorithm|この要求に使用するハッシュ アルゴリズム。|Sha256, sha384, sha512, sha1, md5, md4, md2|HashAlgorithm sha1 を = です。 使用して、サポートされているハッシュ アルゴリズムの一覧を表示する: certutil oid 1 &#124; findstr pwszCNGAlgid &#124; findstr/v CryptOIDInfo|
|KeyAlgorithm|パブリックとプライベート キーのペアを生成するサービス プロバイダーによって使用されるアルゴリズム。|RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521|KeyAlgorithm RSA を =|
|KeyContainer|新しいキー マテリアルが生成される新しい要求には、このパラメーターを設定するのには推奨されません。 キー コンテナーは自動的に生成され、システムによって維持されます。 要求の既存のキー マテリアルを使用する場合は、既存のキーのキー コンテナー名にこの値を設定できます。 Certutil を使用して、– コンピューターのコンテキストの使用可能なキー コンテナーの一覧を表示するコマンドのキーします。 Certutil を使用して、– キー – 現在のユーザーのコンテキストのユーザー コマンド。|ランダムな文字列値</br>ヒント:空白または INF の潜在的な解析を行って問題を回避するために特殊文字を含む INF キーの値を二重引用符を使用する必要があります。|KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}|
|KeyLength|パブリックおよびプライベート キーの長さを定義します。 キーの長さは、証明書のセキュリティ レベルに影響を与えます。 キーの長さが大きく、通常より高いセキュリティ レベルを提供します。ただし、一部のアプリケーションには、キーの長さに関する制限事項があります。|有効なキーの長さ、暗号化サービス プロバイダーでサポートされています。|KeyLength = 2048|
|KeySpec|署名、交換 (暗号化)、または両方のキーを使用できるかどうかを決定します。|AT_NONE、AT_SIGNATURE、AT_KEYEXCHANGE|KeySpec AT_KEYEXCHANGE を =|
|KeyUsage|使用する証明書のキーを定義します。|CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)</br>ヒント:表示される値では、各ビット定義に対応する 16 進数の (10 進数) 値です。 古い構文も使用できます。 複数の 1 つの 16 進値、シンボリックな表現ではなく、セットのビット。 たとえば、KeyUsage 0xa0 を = です。</br>CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE -- 8</br>CERT_KEY_CERT_SIGN_KEY_USAGE -- 4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2</br>CERT_CRL_SIGN_KEY_USAGE -- 2</br>CERT_ENCIPHER_ONLY_KEY_USAGE -- 1</br>CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)|KeyUsage ="CERT_DIGITAL_SIGNATURE_KEY_USAGE &#124; CERT_KEY_ENCIPHERMENT_KEY_USAGE"</br>ヒント:パイプを使用して、複数の値 (&#124;) 記号の区切り記号。 INF 解析の問題を回避するために複数の値を使用する場合は、二重引用符を使用することを確認します。|
|KeyUsageProperty|秘密キーを使用できる特定の目的を識別する値を取得します。|NCRYPT_ALLOW_DECRYPT_FLAG -- 1</br>NCRYPT_ALLOW_SIGNING_FLAG -- 2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4</br>NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)|KeyUsageProperty = "NCRYPT_ALLOW_DECRYPT_FLAG &#124; NCRYPT_ALLOW_SIGNING_FLAG"|
|MachineKeySet|このキーは、コンピューターとユーザーではなくによって所有されている証明書を作成する必要がある場合に重要です。 セキュリティ コンテキスト セキュリティ プリンシパル (ユーザーまたはコンピューター アカウント) が、要求を作成するには、生成されるキー マテリアルが維持されます。 管理者は、コンピューターの代わりの証明書の要求を作成するとき、マシンのセキュリティ コンテキストで、管理者のセキュリティ コンテキストではなくキー マテリアルを作成する必要があります。 それ以外の場合、管理者のセキュリティ コンテキスト内になるために、コンピューターはその秘密キーをアクセスできませんでした。|true、false|MachineKeySet = true</br>ヒント:既定値は false です。|
|NotBefore|日付または日付と時刻の前に、要求を発行できませんを指定します。 ValidityPeriod と ValidityPeriodUnits NotBefore を使用できます。|日付または日付と時刻|NotBefore ="2012 7 月 24 日 10時 31分 AM"</br>ヒント:RequestType のための NotBefore と NotAfter = 証明書のみです。ロケールに依存する試行の日付を解析します。使用する月名はあいまいさを解消し、すべてのロケールで作業する必要があります。|
|NotAfter|日付または日付と時刻の後、要求を発行できませんを指定します。 ValidityPeriod または ValidityPeriodUnits NotAfter を使用できません。|日付または日付と時刻|NotAfter ="2014 年 9 月 23 日 10時 31分 AM"</br>ヒント:RequestType のための NotBefore と NotAfter = 証明書のみです。ロケールに依存する試行の日付を解析します。使用する月名はあいまいさを解消し、すべてのロケールで作業する必要があります。|
|PrivateKeyArchive|PrivateKeyArchive 設定は、CA キーのアーカイブ用に、要求者の秘密キーを安全に転送するための CMS (CMC) 要求の形式で証明書管理のメッセージのみであるため、対応する RequestType が"CMC"に設定されている場合にのみ機能します。|true、false|PrivateKeyArchive = True|
|EncryptionAlgorithm|使用する暗号化アルゴリズム。|使用可能なオプションは、オペレーティング システムのバージョンとインストールされている暗号化サービス プロバイダーのセットによって異なります。 使用可能なアルゴリズムの一覧については、コマンドを実行<code>certutil -oid 2 &#124; findstr pwszCNGAlgid</code>指定した対称暗号化アルゴリズムと長さ、指定した CSP を使用する必要がありますもサポートします。|EncryptionAlgorithm 3 des を =|
|EncryptionLength|使用する暗号化アルゴリズムの長さ。|指定した EncryptionAlgorithm で許可されている任意の長さ。|EncryptionLength >= 128|
|ProviderName|プロバイダー名は、CSP の表示名は.|使用する CSP のプロバイダー名がわからない場合は、コマンドラインから certutil – csplist を実行します。 コマンドは、ローカル システムで使用できるすべての Csp の名前が表示されます。|ProviderName ="Microsoft RSA SChannel Cryptographic Provider"|
|ProviderType|プロバイダーの種類を使用して、完全"RSA"などの特定のアルゴリズムの機能に基づく特定のプロバイダーを選択します。|使用する CSP のプロバイダーの種類がわからない場合は、コマンド ライン プロンプトから certutil – csplist を実行します。 コマンドは、ローカル システムで使用できるすべての Csp のプロバイダーの種類が表示されます。|プロバイダーの種類 = 1|
|RenewalCert|証明書の要求が生成される場所、システム上に存在する証明書を更新する必要がある場合は、このキーの値としてその証明書ハッシュを指定する必要があります。|証明書の要求が作成されているコンピューターで使用できる任意の証明書の証明書ハッシュ。 証明書ハッシュがわからない場合は、証明書の MMC スナップインを使用し、証明書を更新する必要があます。 証明書のプロパティを開き、証明書の「サムプリント」属性を参照してください。 証明書の更新では、PKCS #7 または CMC 要求の形式のいずれかが必要です。|RenewalCert 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D を =|
|RequesterName</br>注:これにより、別のユーザー要求の代理として登録を要求します。要求は、Enrollment Agent 証明書で署名も必要があります。 または CA は、要求を拒否します。 使用して登録エージェント証明書を指定するには、証明書オプション。|PKCS #7 または CMC RequestType が設定されている場合、証明書の要求の要求元の名前を指定できます。 RequestType を PKCS #10 に設定すると、このキーは無視されます。 Requestername は、要求の一部としてのみ設定できます。 保留中の要求で Requestername を操作することはできません。|ドメイン \ ユーザー|Requestername = "Contoso\BSmith"|
|RequestType|生成し、証明書の要求を送信するために使用する標準を決定します。|PKCS10 - 1</br>PKCS7 -- 2</br>CMC - 3</br>証明書 - 4</br>SCEP--fd00 (64768)</br>ヒント:このオプションでは、自己署名または自己発行の証明書を示します。 要求は新しい証明書ではなく作成せずにし、証明書をインストールします。既定値は、自己署名します。使用して署名証明書の指定が自己署名されていない自己発行の証明書を作成するには証明書オプション。|RequestType = CMC|
|SecurityDescriptor</br>ヒント:これは、機能は、コンピューターのコンテキストで、スマート カード キーに対してのみ適用されます。|セキュリティ保護可能なオブジェクトに関連付けられているセキュリティ情報が含まれてください。 最もセキュリティ保護可能なオブジェクトは、オブジェクトを作成する関数呼び出しで、オブジェクトのセキュリティ記述子を指定できます。|文字列に基づいて[セキュリティ記述子定義言語](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx)します。|SecurityDescriptor = "D:P(A;;GA;;;SY)(A;;GA;;;BA)"|
|AlternateSignatureAlgorithm|指定し、PKCS #10 要求または証明書署名の署名アルゴリズム オブジェクト識別子 (OID) が不連続または結合があるかどうかを示すブール値を取得します。|true、false|AlternateSignatureAlgorithm = false</br>ヒント:RSA 署名では、false は Pkcs1 v1.5 を示します。 True は、バージョン 2.1 以降のシグネチャを示します。|
|Silent|既定では、このオプションは、スマート カード暗証番号 (pin) など、対話型ユーザー デスクトップと要求情報をユーザーからの CSP アクセスできます。 このキーが TRUE に設定されている場合、CSP は、デスクトップと対話する必要があり、任意のユーザー インターフェイスをユーザーに表示がブロックされます。|true、false|サイレント = true|
|SMIME|このパラメーターが TRUE に設定されている場合、オブジェクト識別子値 1.2.840.113549.1.9.15 拡張機能は、要求に追加されます。 オブジェクト識別子の数によって異なります、Outlook などの Secure Multipurpose Internet Mail Extensions (S/MIME) アプリケーションで使用できる対称暗号化アルゴリズムを参照しているオペレーティング システムのバージョンがインストールされていると CSP の機能です。|true、false|SMIME = true|
|UseExistingKeySet|このパラメーターは、既存のキー ペアを証明書の要求の作成に使用することを指定するに使用されます。 このキーが TRUE に設定されている場合も、RenewalCert キーまたは KeyContainer 名の値を指定する必要があります。 既存のキーのプロパティを変更できないために、エクスポート可能なキーを設定する必要がありますできません。 この場合、証明書の要求のビルド時にキー マテリアルは生成されません。|true、false|UseExistingKeySet = true|
|KeyProtection|使用する前に、秘密キーを保護する方法を示す値を指定します。|XCN_NCRYPT_UI_NO_PROTCTION_FLAG -- 0</br>XCN_NCRYPT_UI_PROTECT_KEY_FLAG -- 1</br>XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2|KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG|
|SuppressDefaults|要求で、既定の拡張機能と属性を含めるかどうかを示すブール値を指定します。 既定値は、それらのオブジェクト識別子 (Oid) で表されます。|true、false|SuppressDefaults = true|
|FriendlyName|新しい証明書のフレンドリ名。|Text|FriendlyName ="Server1"|
|ValidityPeriodUnits</br>注:これでのみ使用が、要求が入力すると証明書を = です。|ValidityPeriod で使用されるユニットの数を指定します。|数値|ValidityPeriodUnits 3 を =|
|ValidityPeriod</br>注:これでのみ使用が、要求が入力すると証明書を = です。|VValidityPeriod する必要があります、米国英語に複数形の期間。|年、月、週、日、時間、分、秒|ValidityPeriod 年を =|

戻り[内容](#BKMK_Contents)

**[拡張機能]**

このセクションは省略可能です。


|  拡張機能の OID   | 定義 | Value |                                                                                                                                                                                                                                                                                                                                                                                                                      例                                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------|------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    2.5.29.17     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                2.5.29.17 ="{text}"                                                                                                                                                                                                                                                                                                                                                                                                                |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *引き続き*="UPN =User@Domain.com(& a)"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *引き続き*="電子メール =User@Domain.com(& a)"                                                                                                                                                                                                                                                                                                                                                                                                        |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *continue* = "DNS=host.domain.com&"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                               *continue* = "DirectoryName=CN=Name,DC=Domain,DC=com&"                                                                                                                                                                                                                                                                                                                                                                                               |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                             *引き続き*="URL =<http://host.domain.com/default.html&>"                                                                                                                                                                                                                                                                                                                                                                                              |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                         *continue* = "IPAddress=10.0.0.1&"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *引き続き*="RegisteredId 1.2.3.4.5 という拡張 = (& a)"                                                                                                                                                                                                                                                                                                                                                                                                       |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                      *引き続き*="1.2.3.4.6.1={utf8}String (& a)"                                                                                                                                                                                                                                                                                                                                                                                                      |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                  *引き続き*="1.2.3.4.6.2={octet}AAECAwQFBgc= (& a)"                                                                                                                                                                                                                                                                                                                                                                                                   |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                          *引き続き*="1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07 (& a)"                                                                                                                                                                                                                                                                                                                                                                                           |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                 *continue* = "1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&"                                                                                                                                                                                                                                                                                                                                                                                                  |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                           *continue* = "1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07"                                                                                                                                                                                                                                                                                                                                                                                            |
|    2.5.29.37     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 2.5.29.37="{text}"                                                                                                                                                                                                                                                                                                                                                                                                                 |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                            *引き続き*="1.3.6.1.5.5.7 します。                                                                                                                                                                                                                                                                                                                                                                                                            |
|    *続行*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                          *引き続き*「1.3.6.1.5.5.7.3.1」を =                                                                                                                                                                                                                                                                                                                                                                                                          |
|    2.5.29.19     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                              "{テキスト} ca 0pathlength = 3 ="                                                                                                                                                                                                                                                                                                                                                                                                              |
|     重大     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 重要な 2.5.29.19 を =                                                                                                                                                                                                                                                                                                                                                                                                                 |
|     KeySpec      |            |       |                                                                                                                                                                                                                                                                                                                                                                                             AT_NONE -- 0</br>AT_SIGNATURE - 2</br>AT_KEYEXCHANGE -- 1                                                                                                                                                                                                                                                                                                                                                                                             |
|   RequestType    |            |       |                                                                                                                                                                                                                                                                                                                                                                                   PKCS10 - 1</br>PKCS7 -- 2</br>CMC - 3</br>証明書 - 4</br>SCEP--fd00 (64768)                                                                                                                                                                                                                                                                                                                                                                                   |
|     KeyUsage     |            |       |                                                                                                                                                                                                       CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)</br>CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE -- 8</br>CERT_KEY_CERT_SIGN_KEY_USAGE -- 4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2</br>CERT_CRL_SIGN_KEY_USAGE -- 2</br>CERT_ENCIPHER_ONLY_KEY_USAGE -- 1</br>CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)                                                                                                                                                                                                       |
| KeyUsageProperty |            |       |                                                                                                                                                                                                                                                                                                                                            NCRYPT_ALLOW_DECRYPT_FLAG -- 1</br>NCRYPT_ALLOW_SIGNING_FLAG -- 2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4</br>NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)                                                                                                                                                                                                                                                                                                                                             |
|  KeyProtection   |            |       |                                                                                                                                                                                                                                                                                                                                                                NCRYPT_UI_NO_PROTECTION_FLAG -- 0</br>NCRYPT_UI_PROTECT_KEY_FLAG -- 1</br>NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2                                                                                                                                                                                                                                                                                                                                                                 |
| SubjectNameFlags |  テンプレート  |       |                                                                           CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME -- 40000000 (1073741824)</br>CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH -- 80000000 (2147483648)</br>CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN -- 10000000 (268435456)</br>CT_FLAG_SUBJECT_REQUIRE_EMAIL -- 20000000 (536870912)</br>CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME -- 8</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID -- 1000000 (16777216)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DNS -- 8000000 (134217728)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS -- 400000 (4194304)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL -- 4000000 (67108864)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_SPN -- 800000 (8388608)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_UPN -- 2000000 (33554432)                                                                            |
|  X500NameFlags   |            |       | CERT_NAME_STR_NONE -- 0</br>CERT_OID_NAME_STR -- 2</br>CERT_X500_NAME_STR -- 3</br>CERT_NAME_STR_SEMICOLON_FLAG -- 40000000 (1073741824)</br>CERT_NAME_STR_NO_PLUS_FLAG -- 20000000 (536870912)</br>CERT_NAME_STR_NO_QUOTING_FLAG -- 10000000 (268435456)</br>CERT_NAME_STR_CRLF_FLAG -- 8000000 (134217728)</br>CERT_NAME_STR_COMMA_FLAG -- 4000000 (67108864)</br>CERT_NAME_STR_REVERSE_FLAG -- 2000000 (33554432)</br>CERT_NAME_STR_FORWARD_FLAG -- 1000000 (16777216)</br>CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG -- 10000 (65536)</br>CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG -- 20000 (131072)</br>CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG -- 40000 (262144)</br>CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG -- 80000 (524288)</br>CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG -- 100000 (1048576)</br>CERT_NAME_STR_ENABLE_PUNYCODE_FLAG -- 200000 (2097152) |

戻り[内容](#BKMK_Contents)

> [!NOTE]
> SubjectNameFlags は、INF ファイル件名と SubjectAltName 拡張機能フィールドは、現在のユーザーまたはコンピューターの現在のプロパティに基づいて certreq によって自動的に設定されますをする必要がありますを指定することができます。DNS 名、UPN、およびなど。 "Template"というリテラルを使用して、テンプレート名のフラグを使用して代わりに意味します。 これにより、複数のコンテキストでコンテキストに固有のサブジェクト情報を要求の生成に使用する 1 つの INF ファイルです。
>
> X500NameFlags では、エンコードされた識別名をサブジェクト INF のキー値は ASN.1 に変換するときに、CertStrToName API に直接渡すフラグを指定します。

基づく certreq を使用して証明書を要求する-新しい手順を次の例を使用します。

> [!WARNING]
> このトピックの内容は Windows Server 2008 の AD CS; の既定の設定に基づきますたとえば、2048、CSP、として Microsoft Software Key Storage Provider を選択し、セキュア ハッシュ アルゴリズム 1 (SHA1) を使用するキーの長さを設定します。 これらの選択に対して、会社のセキュリティ ポリシーの要件を評価します。

ポリシー ファイル (.inf) のコピーを作成し、メモ帳で、次の例を保存と RequestConfig.inf を付けて保存。
```
[NewRequest] 
Subject = "CN=<FQDN of computer you are creating the certificate>" 
Exportable = TRUE 
KeyLength = 2048 
KeySpec = 1 
KeyUsage = 0xf0 
MachineKeySet = TRUE 
[RequestAttributes]
CertificateTemplate="WebServer"
[Extensions] 
OID = 1.3.6.1.5.5.7.3.1 
OID = 1.3.6.1.5.5.7.3.2  
```
証明書を要求しているコンピューターでは、次のコマンドを入力します。
```
CertReq –New RequestConfig.inf CertRequest.req 
```
次の例では、Oid とその他の解釈が困難なデータを [文字列] セクションの構文の実装を示します。 EKU 拡張機能の Oid のコンマ区切りリストを使用して新しい {text} 構文の例を示します。
```
[Version]
Signature="$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = "2.5.29.37"
szOID_PKIX_KP_SERVER_AUTH = "1.3.6.1.5.5.7.3.1"
szOID_PKIX_KP_CLIENT_AUTH = "1.3.6.1.5.5.7.3.2"

[NewRequest]
Subject = "CN=TestSelfSignedCert"
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%="{text}%szOID_PKIX_KP_SERVER_AUTH%,"
_continue_ = "%szOID_PKIX_KP_CLIENT_AUTH%"
```
戻り[内容](#BKMK_Contents)

## <a name="BKMK_accept"></a>Certreq-そのまま使用

```
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]
```
– パラメーターは、発行された証明書で以前に生成された秘密キーへのリンクし、保留中の証明書の要求を削除します (一致する要求がある場合)、証明書が要求されているシステムからそのまま使用します。

手動で証明書を受け入れるため、この例を使用できます。
```
certreq -accept certnew.cer 
```

> [!WARNING]
> 動詞を受け入れる、-、ユーザーとコンピューターのオプションは、ユーザーまたはコンピューターのコンテキストでインストールされている証明書をインストールするかどうかを示します。 インストールされている公開キーと一致するいずれかのコンテキストで保留中の要求がある場合は、これらのオプションは必要ありません。 未処理の要求がない場合、これらの 1 つ指定してください。

戻り[内容](#BKMK_Contents)

## <a name="BKMK_policy"></a>Certreq-ポリシー

```
certreq -policy [-attrib AttributeString] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]
```
-   限定従属が定義されている場合、CA 証明書に適用される制約を定義する構成ファイルは、Policy.inf と呼ばれる.
-   Policy.inf ファイルの例を見つけることができます、[付録 A の計画し実装のクロス証明と限定従属](https://technet.microsoft.com/library/cc738878(WS.10).aspx)ホワイト ペーパー。
-   Certreq を入力する場合、ポリシーの追加のパラメーターがない場合、ダイアログのウィンドウが開きます選択できるように、要求されたファイル (req、cmc、txt、der、cer または crt)。 要求されたファイルを選択し、[開く] ボタンをクリックした後、INF ファイルを選択するために別のダイアログ ウィンドウが開きます。

この例を使用して、クロス証明書の要求を構築できます。
```
certreq -policy Certsrv.req Policy.inf newcertsrv.req 
```
戻り[内容](#BKMK_Contents)

## <a name="BKMK_sign"></a>Certreq-サインイン

```
certreq -sign [Options] [RequestFileIn [RequestFileOut]]
```
-   Certreq を入力する場合-記号 (req、cmc、txt、der、cer または crt)、要求されたファイルを選択できるように追加パラメーターを指定しないでダイアログ ウィンドウを開くことができます。
-   限定従属の要求に署名すると、エンタープライズ管理者の資格情報が必要があります。 これは、限定従属の署名証明書を発行することをお勧めします。
-   限定従属のテンプレートを使用して、限定従属の要求の署名に使用される証明書が作成されます。 エンタープライズ管理者は、要求の署名またはユーザーの個人証明書に署名するアクセス許可を付与する必要があります。
-   CMC 要求に署名すると、複数の担当者が限定従属に関連付けられている保証レベルに応じて、この要求に署名する必要があります。
-   修飾下位 CA をインストールするは、親 CA がオフラインの場合は、オフラインの親から修飾下位 CA の CA 証明書を取得する必要があります。 親 CA がオンラインの場合は、証明書サービスのインストール ウィザードの中に、修飾下位 CA の CA 証明書を指定します。

次のコマンドのシーケンスでは、新しい証明書の要求を作成、署名、および送信する方法を示します。
```
certreq -new policyfile.inf MyRequest.req
certreq -sign MyRequest.req MyRequest_Sign.req
certreq -submit MyRequest_Sign.req MyRequest_cert.cer 
```
戻り[内容](#BKMK_Contents)

## <a name="BKMK_enroll"></a>Certreq の登録

証明書に登録するには
```
certreq –enroll [Options] TemplateName
```
既存の証明書を更新するには
```
certreq –enroll –cert CertId [Options] Renew [ReuseKeys]
```
時間の有効な証明書のみ更新できます。 有効期限が切れた証明書は、更新できないし、新しい証明書で置き換える必要があります。

次のシリアル番号を使用して証明書の更新の例に示します。
```
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" Renew
```
U/操作を使用して、ポリシー サーバーを選択するアスタリスク (*) を使用して、web サーバーという証明書テンプレートを登録する際の例
```
certreq -enroll –machine –policyserver * "WebServer"
```
戻り[内容](#BKMK_Contents)

## <a name="BKMK_Options"></a>オプション

|オプション|説明|
|-------|-----------|
|-すべて|エンコードの種類を決定する ICertRequest::Submit を強制します。|
|-attrib \<AttributeString >|名前と値文字列のペアをコロンで区切って指定します。</br>\N (たとえば、Name1:Value1\nName2:Value2) で別個の名前と値の文字列のペアします。|
|-バイナリ|代わりに、base64 でエンコードされたバイナリ形式で出力ファイルの形式。|
|-PolicyServer *\<PolicyServer>*|"ldap: *\<パス >* "</br>URI または証明書登録ポリシー Web サービスを実行しているコンピューターの一意の ID を挿入します。</br>参照して、要求ファイルを使用したいかを指定するに負符号を使用して単に (-) 記号 *\<policyserver >* 。|
|-config \<ConfigString >|これは CAHostName\CAName 構成文字列で指定された CA を使用して、操作を処理します。 Https 接続用には、登録サーバーの URI を指定します。 ローカル コンピューターのストアの CA、マイナス記号を使用して記号 (-)。|
|匿名|証明書の登録 Web サービスには、匿名の資格情報を使用します。|
|-Kerberos|証明書の登録 Web サービス (ドメイン) の Kerberos の資格情報を使用します。|
|-ClientCertificate *\<ClientCertId>*|置き換えることができます、  *\<ClientCertID >* 証明書の拇印、CN、EKU、テンプレート、電子メール、UPN、および新しい名前と値の構文を = です。|
|-UserName *\<UserName>*|証明書の登録 Web サービスで使用します。 代わりに使用することができます *\<ユーザー名 >* SAM 名またはドメイン \ ユーザー。 このオプションは、-p オプションで使用されます。|
|-p *\<Password>*|証明書の登録 Web サービスで使用します。 代替 *\<パスワード >* を実際のユーザーのパスワード。 このオプションでは、-UserName オプションと一緒に使用します。|
|-ユーザー|構成ユーザー コンテキストを指定する新しい証明書の要求のコンテキストを指定または、証明書の承認。 これは、INF またはテンプレートで指定されていない場合の既定のコンテキストです。|
|-コンピューター|新しい証明書の要求を構成します。 または、コンテキストを指定するコンピューターのコンテキストの証明書の承認。 新しい要求 MachineKeyset INF キーとテンプレートのコンテキストで一貫性のある場合があります。 このオプションが指定されていないテンプレートは、コンテキストを設定していない場合、既定値は、ユーザー コンテキストとします。|
|-crl|証明書失効リスト (Crl) を使用または RequestFileOut によって指定された base64 でエンコードされたファイルに CertChainFileOut によって指定された base64 でエンコードされた PKCS #7 ファイルに、出力に含まれています。|
|-rpc|Active Directory 証明書サービス (AD CS) 分散 COM の代わりに、リモート プロシージャ コール (RPC) サーバーの接続を使用するように指示します|
|-AdminForceMachine|キーのサービスまたは権限借用を使用して、ローカル システム コンテキストから要求を送信します。 このオプションを呼び出しているユーザーは、ローカルの Administrators のメンバーである必要があります。|
|-RenewOnBehalfOf|署名証明書で識別されるサブジェクトに代わって更新を送信します。 呼び出すときに設定 CR_IN_ROBO [ICertRequest::Submit](https://technet.microsoft.com/subscriptions/aa385040.aspx)|
|-f|既存のファイルを上書きを強制します。 これもキャッシュのテンプレートおよびポリシーをバイパスします。|
|-q|サイレント モードを使用します。すべての対話型メッセージを非表示します。|
|Unicode|出力を書き込みます Unicode 標準出力のリダイレクトまたは Windows PowerShell® スクリプトから呼び出されたときに、別のコマンドにパイプ処理された場合)。|
|-UnicodeText|ファイルを blob にデータをエンコードされた base64 テキストを書き込むときに、Unicode 出力を送信します。|

戻り[内容](#BKMK_Contents)

## <a name="BKMK_Formats"></a>書式設定します。

|書式設定します。|説明|
|-------|-----------|
|RequestFileIn|Base64 でエンコードされたバイナリ入力名またはファイル名:PKCS #10 証明書の要求、CMS 証明書の要求、PKCS #7 証明書更新要求、クロス証明された X.509 証明書または KeyGen タグ形式の証明書の要求。|
|RequestFileOut|Base64 でエンコードされた出力ファイル名|
|CertFileOut|Base64 でエンコードされた X-509 ファイル名。|
|PKCS10FileOut|使用するため、 [Certreq-ポリシー](#BKMK_policy)動詞のみです。 PKCS10 出力ファイル名の base 64 エンコード形式です。|
|CertChainFileOut|Base64 でエンコードされた PKCS #7 ファイル名。|
|FullResponseFileOut|Base64 でエンコードされた完全な応答ファイルの名前。|
|PolicyFileIn|使用するため、 [Certreq-ポリシー](#BKMK_policy)動詞のみです。 要求を修飾するために使用される拡張機能のテキスト表現を格納している INF ファイルです。|

## <a name="BKMK_Examples"></a>追加の certreq 例

次の記事には、certreq の使用例が含まれます。
-   [カスタムのサブジェクト代替名を持つ証明書を要求する方法](https://technet.microsoft.com/library/ff625722.aspx)
-   [テスト ラボ ガイド:AD CS 2 層 PKI 階層の展開](https://technet.microsoft.com/library/hh831348.aspx)
-   [付録 3:Certreq.exe 構文](https://technet.microsoft.com/library/cc736326.aspx)
-   [Web サーバーの SSL 証明書を手動で作成する方法](http://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)
-   [AMT プロビジョニング証明書を Windows Server 2008 CA を使用して要求します。](https://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)
-   [System Center Operations Manager エージェントの証明書の登録](https://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)
-   [AD CS のステップ バイ ステップ ガイド:2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)
-   [サード パーティの証明機関を使用して SSL 経由で LDAP を有効にする方法](https://support.microsoft.com/kb/321051)

戻り[内容](#BKMK_Contents)
