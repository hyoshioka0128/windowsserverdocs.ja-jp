---
title: certreq
description: 'Windows コマンドに関するトピック * * * *- '
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
ms.openlocfilehash: 19b4750b627a86a724b2a0f58ed7f9bde5ea1613
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867110"
---
# <a name="certreq"></a>certreq



Certreq を使用して、証明機関 (CA) からの証明書を要求したり、CA からの以前の要求に対する応答を取得したり、.inf ファイルから新しい要求を作成したり、要求に対する応答を受け入れてインストールしたり、クロス証明を構築したりすることができます。既存の CA 証明書または要求からの限定従属要求、およびクロス証明または限定従属要求への署名。

> [!WARNING]
> - 以前のバージョンの certreq では、このドキュメントで説明されているすべてのオプションが提供されない場合があります。 「構文表記」セクションに示されているコマンドを実行すると、特定のバージョンの certreq によって提供されるすべてのオプションを確認できます。
> - CEP/CES 環境でのキーの構成証明テンプレートに基づく新しい証明書要求の作成は、Certreq ではサポートされていません

## <a name="BKMK_Contents"></a>内容

この記事の主なセクションは次のとおりです。
1.  [助動詞](#BKMK_Verbs)
2.  [構文表記](#BKMK_notation)
3.  [[オプション]](#BKMK_Options)
4.  [83'7d](#BKMK_Formats)
5.  [その他の certreq の例](#BKMK_Examples)

## <a name="BKMK_Verbs"></a>助動詞

次の表では、certreq コマンドで使用できる動詞について説明します。

|Switch|説明|
|------|-----------|
|-Submit|CA に要求を送信します。 詳細については、「 [Certreq-submit](#BKMK_Submit)」を参照してください。|
|\- *RequestID*を取得する|CA からの前の要求に対する応答を取得します。 詳細については、「 [Certreq-取得](#BKMK_Retrieve)」を参照してください。|
|-新規|.Inf ファイルから新しい要求を作成します。 詳細については、「 [Certreq-新規](#BKMK_New)」を参照してください。|
|-Accept|証明書要求に対する応答を受け入れてインストールします。 詳細については、「 [Certreq-accept](#BKMK_accept)」を参照してください。|
|-ポリシー|要求のポリシーを設定します。 詳細については、「 [Certreq-policy](#BKMK_policy)」を参照してください。|
|-Sign|クロス証明または限定従属の要求に署名します。 詳細については、「 [Certreq-sign](#BKMK_sign)」を参照してください。|
|-登録|証明書を登録または更新します。 詳細については、「 [Certreq-登録](#BKMK_enroll)」を参照してください。|
|-?|Certreq 構文、オプション、および説明の一覧を表示します。|
|動詞 >-?  *\<*|指定された動詞のヘルプを表示します。|
|-v-?|Certreq 構文、オプション、および説明の詳細リストを表示します。|

[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_notation"></a>構文表記

-   基本的なコマンドライン構文については、を実行します。`certreq -?`
-   特定の動詞で certutil を使用する構文については、「 **certreq**  *\<動詞 >* -?」を実行して**ください。**
-   すべての certutil 構文をテキストファイルに送信するには、次のコマンドを実行します。  
    -   `certreq -v -? > certreqhelp.txt`
    -   `notepad certreqhelp.txt`

次の表では、コマンドライン構文を示すために使用される表記法について説明します。

|Notation|説明|
|--------|-----------|
|角かっこまたは中かっこを含まないテキスト|表示されるように入力する必要がある項目|
|\<山かっこ内のテキスト >|値を指定する必要があるプレースホルダー|
|[角かっこ内のテキスト]|省略可能な項目|
|{中かっこ内のテキスト}|必須項目のセット1つ選択する|
|縦棒 (&#124;)|相互に排他的な項目の区切り記号1つ選択する|
|省略記号 (...)|繰り返し可能な項目|

[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_Submit"></a>Certreq-送信

これは、既定の certreq パラメーターです。コマンドラインプロンプトで明示的にオプションが指定されていない場合、certreq は証明書の要求を CA に送信しようとします。
```
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]
```
– Submit オプションを使用する場合は、証明書の要求ファイルを指定する必要があります。 このパラメーターを省略すると、一般的な [ファイルを開く] ウィンドウが表示され、適切な証明書要求ファイルを選択できます。

これらの例を開始点として使用して、証明書の送信要求を作成できます。

単純な証明書の要求を送信するには、次の例を使用します。
```
certreq –submit certRequest.req certnew.cer certnew.pfx
```
SAN 属性を指定して証明書を要求する方法については、マイクロソフトサポート技術情報の記事931351「how to use the stsadm.exe utility to create and submit」の「[セキュリティで保護された LDAP 証明書にサブジェクト代替名を追加する方法](https://support.microsoft.com/kb/931351)」を参照してください。SAN "セクションを含む証明書要求。

[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_Retrieve"></a>Certreq-取得

```
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]
```
-   [CAComputerName または CAName in-config CAComputerName\CANamea] ダイアログボックスを指定しない場合は、使用可能なすべての Ca の一覧が表示されます。
-   -Config-CAComputerName\CAName の代わりに-config-を使用すると、既定の CA を使用して操作が処理されます。
-   CA が実際に証明書を発行した後に、その証明書を取得するために、certreq- *RequestID*を使用することができます。 *RequestID*pkc は、0x プレフィックスを持つ10進数または16進数にすることができ、プレフィックスなしの証明書のシリアル番号にすることができます。 また、証明書の要求が保留中であるかどうかに関係なく、CA によって発行された証明書 (失効または期限切れの証明書を含む) を取得するために使用することもできます。
-   CA に要求を送信した場合、CA のポリシーモジュールは要求を保留状態のままにし、 *RequestID*を表示のために Certreq 呼び出し元に返します。 最終的には、CA の管理者が証明書を発行するか、要求を拒否します。

次のコマンドでは、証明書 id 20 を取得し、証明書ファイル (.cer) を作成します。
```
certreq -retrieve 20 MyCertificate.cer 
```
[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_New"></a>Certreq-新規

```
certreq -new [Options] [PolicyFileIn [RequestFileOut]]
```
INF ファイルではパラメーターとオプションの豊富なセットを指定できるため、管理者がすべての目的に使用する既定のテンプレートを定義することは困難です。 そのため、このセクションでは、特定のニーズに合わせてカスタマイズできる INF ファイルを作成するためのすべてのオプションについて説明します。 次のキーワードは、INF ファイルの構造を記述するために使用されます。
1.  *セクション*は、キーの論理グループをカバーする INF ファイル内の領域です。 セクションは、常に INF ファイルに角かっこで囲まれて表示されます。
2.  *キー*は等号の左側にあるパラメーターです。
3.  *値*は、等号の右側にあるパラメーターです。

たとえば、最小の INF ファイルは次のようになります。
```
[NewRequest] 
; At least one value must be set in this section 
Subject = "CN=W2K8-BO-DC.contoso2.com"
```
次に、INF ファイルに追加される可能性のあるいくつかのセクションを示します。

**[NewRequest]**

このセクションは、新しい証明書要求のテンプレートとして機能する INF ファイルに必須です。 このセクションには、値を持つキーが少なくとも1つ必要です。

|キー|定義|値|例|
|---|----------|-----|-------|
|サブジェクト|いくつかのアプリケーションは、証明書のサブジェクト情報に依存しています。 このため、このキーの値を指定することをお勧めします。 サブジェクトがここで設定されていない場合は、サブジェクトの別名証明書の拡張機能の一部としてサブジェクト名を含めることをお勧めします。|相対識別名の文字列値|Subject = "CN = computer1" Subject = "CN = John Smith, CN = Users, DC = Contoso, DC = com"|
|Exportable|この属性が TRUE に設定されている場合、秘密キーを証明書と共にエクスポートできます。 高いレベルのセキュリティを確保するには、秘密キーをエクスポートできないようにする必要があります。ただし、場合によっては、複数のコンピューターまたはユーザーが同じ秘密キーを共有する必要がある場合に、秘密キーをエクスポート可能にする必要があります。|true、false|エクスポート可能 = TRUE。 CNG キーは、この形式のエクスポート可能なプレーンテキストを区別できます。 CAPI1 キーはできません。|
|ExportableEncrypted|秘密キーをエクスポート可能にするように設定する必要があるかどうかを指定します。|true、false|ExportableEncrypted = true</br>ヒント:すべての公開キーのサイズとアルゴリズムがすべてのハッシュアルゴリズムで動作するわけではありません。 指定された CSP は、指定されたハッシュアルゴリズムもサポートする必要があります。 サポートされているハッシュアルゴリズムの一覧を表示するには、コマンドを実行します。<code>certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo</code>|
|HashAlgorithm|この要求に使用するハッシュアルゴリズム。|Sha256、sha384、sha512、sha1、md5、md4、md2|HashAlgorithm = sha1。 サポートされているハッシュアルゴリズムの一覧を表示するには&#124; 、certutil &#124; -oid 1 Findstr PwszCNGAlgid Findstr/v cryptoidinfo を使用します。|
|KeyAlgorithm|サービスプロバイダーが公開キーと秘密キーのペアを生成するために使用するアルゴリズム。|RSA、DH、DSA、ECDH_P256、ECDH_P521、ECDSA_P256、ECDSA_P384、ECDSA_P521|KeyAlgorithm = RSA|
|KeyContainer|新しいキーマテリアルが生成される新しい要求に対しては、このパラメーターを設定しないことをお勧めします。 キーコンテナーは、システムによって自動的に生成され、維持されます。 既存のキーマテリアルを使用する必要がある要求の場合、この値は既存のキーのキーコンテナー名に設定できます。 Certutil – key コマンドを使用して、マシンコンテキストで使用可能なキーコンテナーの一覧を表示します。 現在のユーザーのコンテキストに対して certutil – key – user コマンドを使用します。|ランダムな文字列値</br>ヒント:INF 解析の問題を回避するには、空白または特殊文字が含まれている INF キー値の前後に二重引用符を使用する必要があります。|KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}|
|KeyLength|公開キーと秘密キーの長さを定義します。 キーの長さは、証明書のセキュリティレベルに影響します。 キーの長さが多いほど、通常は高いセキュリティレベルになります。ただし、一部のアプリケーションでは、キーの長さに関する制限が適用される場合があります。|暗号化サービスプロバイダーでサポートされている任意の有効なキーの長さ。|KeyLength = 2048|
|KeySpec|キーを署名、Exchange (暗号化)、またはその両方に使用できるかどうかを決定します。|AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE|KeySpec = AT_KEYEXCHANGE|
|KeyUsage|証明書キーを使用する必要があるかどうかを定義します。|CERT_DIGITAL_SIGNATURE_KEY_USAGE--80 (128)</br>ヒント:表示される値は、各ビット定義の16進数 (10 進数) 値です。 以前の構文も使用できます。シンボリック表現ではなく、複数のビットが設定された単一の16進値です。 たとえば、KeyUsage = 0xa0 です。</br>CERT_NON_REPUDIATION_KEY_USAGE--40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE--20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE--10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE--8</br>CERT_KEY_CERT_SIGN_KEY_USAGE--4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE--2</br>CERT_CRL_SIGN_KEY_USAGE--2</br>CERT_ENCIPHER_ONLY_KEY_USAGE--1</br>CERT_DECIPHER_ONLY_KEY_USAGE--8000 (32768)|KeyUsage = "CERT_DIGITAL_SIGNATURE_KEY_USAGE &#124; CERT_KEY_ENCIPHERMENT_KEY_USAGE"</br>ヒント:複数の値は、パイプ&#124;記号 () を使用します。 複数の値を使用する場合は、INF 解析の問題を回避するために二重引用符を使用してください。|
|Keyのプロパティ|秘密キーを使用できる特定の目的を識別する値を取得します。|NCRYPT_ALLOW_DECRYPT_FLAG--1</br>NCRYPT_ALLOW_SIGNING_FLAG--2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG--4</br>NCRYPT_ALLOW_ALL_USAGES--ffffff (16777215)|KeyNCRYPT_ALLOW_DECRYPT_FLAG プロパティ = " &#124; NCRYPT_ALLOW_SIGNING_FLAG"|
|MachineKeySet|このキーは、ユーザーではなく、コンピューターによって所有されている証明書を作成する必要がある場合に重要です。 生成されるキーマテリアルは、要求を作成したセキュリティプリンシパル (ユーザーまたはコンピューターアカウント) のセキュリティコンテキストで保持されます。 管理者がコンピューターの代わりに証明書要求を作成する場合、キーマテリアルは、管理者のセキュリティコンテキストではなく、コンピューターのセキュリティコンテキストで作成する必要があります。 そうしないと、管理者のセキュリティコンテキストにあるため、コンピューターは秘密キーにアクセスできませんでした。|true、false|MachineKeySet = true</br>ヒント:既定値は false です。|
|NotBefore|要求を発行できない日付または日付と時刻を指定します。 NotBefore は、ValidityPeriod および ValidityPeriodUnits と共に使用できます。|日付または日付と時刻|NotBefore = "7/24/2012 10:31 AM"</br>ヒント:NotBefore と NotAfter は、RequestType = cert のみを対象としています。日付の解析は、ロケールを区別するように試行されます。月の名前を使用すると、すべてのロケールで明確になり、機能します。|
|NotAfter|要求を発行できない日付または日付と時刻を指定します。 NotAfter は、ValidityPeriod または ValidityPeriodUnits と共に使用することはできません。|日付または日付と時刻|NotAfter = "9/23/2014 10:31 AM"</br>ヒント:NotBefore と NotAfter は、RequestType = cert のみを対象としています。日付の解析は、ロケールを区別するように試行されます。月の名前を使用すると、すべてのロケールで明確になり、機能します。|
|PrivateKeyArchive|PrivateKeyArchive 設定は、対応する RequestType が "CMC" に設定されている場合にのみ機能します。これは、証明書管理メッセージ (CMC) の要求形式のみが、キーのアーカイブのために要求元の秘密キーを CA に安全に転送できるためです。|true、false|PrivateKeyArchive = True|
|EncryptionAlgorithm|使用する暗号化アルゴリズム。|使用可能なオプションは、オペレーティングシステムのバージョンとインストールされている暗号化サービスプロバイダーのセットによって異なります。 使用可能なアルゴリズムの一覧を表示するには<code>certutil -oid 2 &#124; findstr pwszCNGAlgid</code> 、コマンドを実行します。指定された CSP は、指定された対称暗号化アルゴリズムと長さもサポートしている必要があります。|EncryptionAlgorithm = 3des|
|EncryptionLength|使用する暗号化アルゴリズムの長さ。|指定した EncryptionAlgorithm で許可されている任意の長さ。|EncryptionLength = 128|
|ProviderName|プロバイダー名は、CSP の表示名です。|使用している CSP のプロバイダー名がわからない場合は、コマンドラインから certutil – csplist を実行します。 このコマンドは、ローカルシステムで使用可能なすべての Csp の名前を表示します。|ProviderName = "Microsoft RSA SChannel Cryptographic Provider"|
|ProviderType|プロバイダーの種類は、"RSA Full" などの特定のアルゴリズム機能に基づいて特定のプロバイダーを選択するために使用されます。|使用している CSP のプロバイダーの種類がわからない場合は、コマンドラインプロンプトから certutil – csplist を実行します。 このコマンドは、ローカルシステムで使用可能なすべての Csp のプロバイダーの種類を表示します。|ProviderType = 1|
|RenewalCert|証明書の要求が生成されたシステム上に存在する証明書を更新する必要がある場合は、その証明書のハッシュをこのキーの値として指定する必要があります。|証明書要求が作成されたコンピューターで使用可能な証明書の証明書ハッシュ。 証明書のハッシュがわからない場合は、証明書 MMC スナップインを使用して、更新する必要がある証明書を確認します。 証明書のプロパティを開き、証明書の "拇印" 属性を確認します。 証明書の更新には、PKCS # 7 または CMC 要求の形式が必要です。|RenewalCert = 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D|
|RequesterName</br>注:これにより、別のユーザー要求に代わって要求が登録されます。また、登録エージェント証明書を使用して要求に署名する必要があります。これを行わないと、CA は要求を拒否します。 -Cert オプションを使用して、登録エージェント証明書を指定します。|RequestType が PKCS # 7 または CMC に設定されている場合、証明書の要求に対して要求者名を指定できます。 RequestType が PKCS # 10 に設定されている場合、このキーは無視されます。 Requestername は、要求の一部としてのみ設定できます。 保留中の要求では Requestername を操作できません。|\|Requestername = "Contoso\BSmith"|
|RequestType|証明書要求を生成して送信するために使用される標準を決定します。|PKCS10--1</br>PKCS7--2</br>CMC--3</br>Cert--4</br>SCEP--fd00 (64768)</br>ヒント:このオプションは、自己署名または自己発行の証明書を示します。 要求を生成するのではなく、新しい証明書を作成してから、証明書をインストールします。"自己署名" は既定値です。– Cert オプションを使用して署名証明書を指定し、自己署名されていない自己発行の証明書を作成します。|RequestType = CMC|
|SecurityDescriptor</br>ヒント:これは、コンピューターコンテキストのスマートカード以外のキーにのみ関連します。|セキュリティ保護可能なオブジェクトに関連付けられているセキュリティ情報を格納します。 ほとんどのセキュリティ保護可能なオブジェクトでは、オブジェクトを作成する関数呼び出しでオブジェクトのセキュリティ記述子を指定できます。|[セキュリティ記述子定義言語](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx)に基づく文字列。|SecurityDescriptor = "d: P (A;;GA、;、SY) (A;;GA、;、BA) "|
|AlternateSignatureAlgorithm|PKCS # 10 要求または証明書署名の署名アルゴリズムオブジェクト識別子 (OID) が不連続であるか結合されているかを示すブール値を指定して取得します。|true、false|AlternateSignatureAlgorithm = false</br>ヒント:RSA 署名の場合、false は Pkcs1 v 1.5 を示します。 True は、version 2.1 の署名を示します。|
|Silent|既定では、このオプションを使用すると、ユーザーの対話型デスクトップにアクセスしたり、スマートカードの PIN などの情報を要求したりすることができます。 このキーが TRUE に設定されている場合、CSP はデスクトップと対話する必要がなく、ユーザーインターフェイスの表示がブロックされます。|true、false|Silent = true|
|S|このパラメーターが TRUE に設定されている場合、オブジェクト識別子の値1.2.840.113549.1.9.15 を持つ拡張機能が要求に追加されます。 オブジェクト識別子の数は、インストールされているオペレーティングシステムのバージョンと CSP の機能によって異なります。これは、Outlook などの Secure Multipurpose Internet Mail Extensions (S/MIME) アプリケーションで使用される対称暗号化アルゴリズムを指します。|true、false|SMIME = true|
|UseExistingKeySet|このパラメーターは、既存のキーペアを証明書要求の作成に使用することを指定するために使用されます。 このキーが TRUE に設定されている場合は、RenewalCert キーまたは KeyContainer 名の値も指定する必要があります。 既存のキーのプロパティを変更することはできないため、エクスポート可能なキーは設定しないでください。 この場合、証明書の要求の作成時にキーマテリアルは生成されません。|true、false|UseExistingKeySet = true|
|KeyProtection|秘密キーを使用する前に保護する方法を示す値を指定します。|XCN_NCRYPT_UI_NO_PROTCTION_FLAG--0</br>XCN_NCRYPT_UI_PROTECT_KEY_FLAG--1</br>XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG--2|KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG|
|SuppressDefaults|既定の拡張機能と属性が要求に含まれるかどうかを示すブール値を指定します。 既定値は、オブジェクト識別子 (Oid) によって表されます。|true、false|SuppressDefaults = true|
|FriendlyName|新しい証明書のフレンドリ名。|テキスト|FriendlyName = "Server1"|
|ValidityPeriodUnits</br>注:これは、要求の種類が cert の場合にのみ使用されます。|ValidityPeriod で使用する単位の数を指定します。|数値|ValidityPeriodUnits = 3|
|ValidityPeriod</br>注:これは、要求の種類が cert の場合にのみ使用されます。|VValidityPeriod は米国英語の複数形の期間である必要があります。|年、月、週、日、時間、分、秒|ValidityPeriod = 年|

[コンテンツ](#BKMK_Contents)に戻る

**補助**

このセクションは省略可能です。


|  拡張 OID   | 定義 | 値 |                                                                                                                                                                                                                                                                                                                                                                                                                      例                                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------|------------|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    2.5.29.17     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                2.5.29.17 = "{text}"                                                                                                                                                                                                                                                                                                                                                                                                                |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *continue* = "UPN =User@Domain.com&"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *continue* = "EMail =User@Domain.com&"                                                                                                                                                                                                                                                                                                                                                                                                        |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                        *continue* = "DNS = host. domain .com &"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                               *continue* = "DIRECTORYNAME = CN = NAME, Dc = DOMAIN, dc = com &"                                                                                                                                                                                                                                                                                                                                                                                               |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                             *continue* = "URL =<http://host.domain.com/default.html&>"                                                                                                                                                                                                                                                                                                                                                                                              |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                         *continue* = "IPAddress = 10.0.0.1 &"                                                                                                                                                                                                                                                                                                                                                                                                         |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                       *continue* = "registeredid = 1.2.3.4.5 &"                                                                                                                                                                                                                                                                                                                                                                                                       |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                      *continue* = "1.2.3.4.6.1 = {Utf8} 文字列 &"                                                                                                                                                                                                                                                                                                                                                                                                      |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                  *continue* = "1.2.3.4.6.2 = {オクテット} AAECAwQFBgc = &"                                                                                                                                                                                                                                                                                                                                                                                                   |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                          *continue* = "1.2.3.4.6.2 = {オクテット} {hex} 00 01 02 03 04 05 06 07 &"                                                                                                                                                                                                                                                                                                                                                                                           |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                 *continue* = "1.2.3.4.6.3 = {Asn} BAgAAQIDBAUGBw = = &"                                                                                                                                                                                                                                                                                                                                                                                                  |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                           *continue* = "1.2.3.4.6.3 = {hex} 04 08 00 01 02 03 04 05 06 07"                                                                                                                                                                                                                                                                                                                                                                                            |
|    2.5.29.37     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 2.5.29.37 = "{text}"                                                                                                                                                                                                                                                                                                                                                                                                                 |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                            *continue* = "1.3.6.1.5.5.7.                                                                                                                                                                                                                                                                                                                                                                                                            |
|    *まま*    |            |       |                                                                                                                                                                                                                                                                                                                                                                                                          *continue* = "1.3.6.1.5.5.7.3.1"                                                                                                                                                                                                                                                                                                                                                                                                          |
|    2.5.29.19     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                              "{text} ca = 0pathlength = 3"                                                                                                                                                                                                                                                                                                                                                                                                              |
|     重大     |            |       |                                                                                                                                                                                                                                                                                                                                                                                                                 Critical = 2.5.29.19                                                                                                                                                                                                                                                                                                                                                                                                                 |
|     KeySpec      |            |       |                                                                                                                                                                                                                                                                                                                                                                                             AT_NONE--0</br>AT_SIGNATURE--2</br>AT_KEYEXCHANGE--1                                                                                                                                                                                                                                                                                                                                                                                             |
|   RequestType    |            |       |                                                                                                                                                                                                                                                                                                                                                                                   PKCS10--1</br>PKCS7--2</br>CMC--3</br>Cert--4</br>SCEP--fd00 (64768)                                                                                                                                                                                                                                                                                                                                                                                   |
|     KeyUsage     |            |       |                                                                                                                                                                                                       CERT_DIGITAL_SIGNATURE_KEY_USAGE--80 (128)</br>CERT_NON_REPUDIATION_KEY_USAGE--40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE--20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE--10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE--8</br>CERT_KEY_CERT_SIGN_KEY_USAGE--4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE--2</br>CERT_CRL_SIGN_KEY_USAGE--2</br>CERT_ENCIPHER_ONLY_KEY_USAGE--1</br>CERT_DECIPHER_ONLY_KEY_USAGE--8000 (32768)                                                                                                                                                                                                       |
| Keyのプロパティ |            |       |                                                                                                                                                                                                                                                                                                                                            NCRYPT_ALLOW_DECRYPT_FLAG--1</br>NCRYPT_ALLOW_SIGNING_FLAG--2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG--4</br>NCRYPT_ALLOW_ALL_USAGES--ffffff (16777215)                                                                                                                                                                                                                                                                                                                                             |
|  KeyProtection   |            |       |                                                                                                                                                                                                                                                                                                                                                                NCRYPT_UI_NO_PROTECTION_FLAG--0</br>NCRYPT_UI_PROTECT_KEY_FLAG--1</br>NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG--2                                                                                                                                                                                                                                                                                                                                                                 |
| SubjectNameFlags |  テンプレート  |       |                                                                           CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME--4000万 (1073741824)</br>CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH--8000万 (2147483648)</br>CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN--1000万 (268435456)</br>CT_FLAG_SUBJECT_REQUIRE_EMAIL--2000万 (536870912)</br>CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME--8</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID--100万 (16777216)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DNS--800万 (134217728)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS--40万 (4194304)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL--400万 (67108864)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_SPN--80万 (8388608)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_UPN--200万 (33554432)                                                                            |
|  「X500nameflags   |            |       | CERT_NAME_STR_NONE--0</br>CERT_OID_NAME_STR--2</br>CERT_X500_NAME_STR--3</br>CERT_NAME_STR_SEMICOLON_FLAG--4000万 (1073741824)</br>CERT_NAME_STR_NO_PLUS_FLAG--2000万 (536870912)</br>CERT_NAME_STR_NO_QUOTING_FLAG--1000万 (268435456)</br>CERT_NAME_STR_CRLF_FLAG--800万 (134217728)</br>CERT_NAME_STR_COMMA_FLAG--400万 (67108864)</br>CERT_NAME_STR_REVERSE_FLAG--200万 (33554432)</br>CERT_NAME_STR_FORWARD_FLAG--100万 (16777216)</br>CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG--1万 (65536)</br>CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG--2万 (131072)</br>CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG--4万 (262144)</br>CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG--8万 (524288)</br>CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG--10万 (1048576)</br>CERT_NAME_STR_ENABLE_PUNYCODE_FLAG--20万 (2097152) |

[コンテンツ](#BKMK_Contents)に戻る

> [!NOTE]
> SubjectNameFlags を使用すると、INF ファイルは、現在のユーザーまたは現在のコンピューターのプロパティに基づいて、certreq によって自動的に設定される Subject および SubjectAltName extension フィールドを指定できます。DNS 名、UPN など。 "Template" というリテラルを使用すると、代わりにテンプレート名フラグが使用されます。 これにより、1つの INF ファイルを複数のコンテキストで使用して、コンテキスト固有のサブジェクト情報を含む要求を生成できます。
>
> 「X500nameflags は、サブジェクトの INF キー値が asn.1 エンコードされた識別名に変換されるときに、CertStrToName API に直接渡されるフラグを指定します。

Certreq-new を使用して証明書を要求するには、次の例の手順を使用します。

> [!WARNING]
> このトピックの内容は、Windows Server 2008 AD CS の既定の設定に基づいています。たとえば、キーの長さを2048に設定し、Microsoft ソフトウェアキー記憶域プロバイダーを CSP として選択し、セキュアハッシュアルゴリズム 1 (SHA1) を使用します。 これらの選択は、会社のセキュリティポリシーの要件に照らして評価します。

ポリシーファイル (.inf) を作成し、次の例をメモ帳で保存して、RequestConfig という名前を付けて保存します。
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
証明書を要求しているコンピューターで、次のコマンドを実行します。
```
CertReq –New RequestConfig.inf CertRequest.req 
```
次の例では、Oid に対して [Strings] セクション構文を実装し、その他の方法でデータを解釈する方法を示します。 EKU 拡張の新しい {text} 構文例では、Oid のコンマ区切りリストを使用しています。
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
[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_accept"></a>Certreq-accept

```
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]
```
– Accept パラメーターを指定すると、以前に生成された秘密キーが発行済みの証明書とリンクされ、保留中の証明書要求が、証明書が要求されたシステムから削除されます (一致する要求がある場合)。

この例を使用すると、手動で証明書を受け入れることができます。
```
certreq -accept certnew.cer 
```

> [!WARNING]
> -Accept 動詞、-user および– machine オプションは、インストールする証明書をユーザーまたはコンピューターのコンテキストにインストールする必要があるかどうかを示します。 インストールされている公開キーに一致するいずれかのコンテキストで未処理の要求がある場合、これらのオプションは必要ありません。 未処理の要求がない場合は、これらのいずれかを指定する必要があります。

[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_policy"></a>Certreq-ポリシー

```
certreq -policy [-attrib AttributeString] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]
```
-   限定従属が定義されている場合に CA 証明書に適用される制約を定義する構成ファイルは、"ポリシー .inf." と呼ばれます。
-   ポリシーの .inf ファイルの例については、 [「クロス証明と限定従属の計画と実装](https://technet.microsoft.com/library/cc738878(WS.10).aspx)」ホワイトペーパーを参照してください。
-   追加のパラメーターを指定せずに certreq ポリシーを入力すると、ダイアログウィンドウが開き、要求された xfs (req、cmc、txt、der、cer、または crt) を選択できます。 要求されたファイルを選択して [開く] ボタンをクリックすると、別のダイアログウィンドウが開き、INF ファイルが選択されます。

この例を使用すると、クロス証明書要求を作成できます。
```
certreq -policy Certsrv.req Policy.inf newcertsrv.req 
```
[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_sign"></a>Certreq-sign

```
certreq -sign [Options] [RequestFileIn [RequestFileOut]]
```
-   追加のパラメーターを指定せずに certreq を入力すると、ダイアログウィンドウが開き、要求されたファイル (req、cmc、txt、der、cer、または crt) を選択できます。
-   限定従属の要求に署名するには、エンタープライズ管理者の資格情報が必要になることがあります。 これは、限定従属の署名証明書を発行するためのベストプラクティスです。
-   限定従属の要求に署名するために使用される証明書は、限定従属テンプレートを使用して作成されます。 エンタープライズ管理者は、証明書に署名する個人に対して、要求に署名するか、ユーザーにアクセス許可を付与する必要があります。
-   CMC 要求に署名する場合、限定従属に関連付けられている保証レベルに応じて、複数の担当者にこの要求に署名する必要がある場合があります。
-   インストールする限定された下位 CA の親 CA がオフラインの場合は、オフラインの親から限定された下位 CA の CA 証明書を取得する必要があります。 親 CA がオンラインの場合は、証明書サービスのインストールウィザードで、限定された下位 CA の CA 証明書を指定します。

次の一連のコマンドは、新しい証明書要求を作成し、署名して送信する方法を示しています。
```
certreq -new policyfile.inf MyRequest.req
certreq -sign MyRequest.req MyRequest_Sign.req
certreq -submit MyRequest_Sign.req MyRequest_cert.cer 
```
[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_enroll"></a>Certreq-登録

証明書に登録するには
```
certreq –enroll [Options] TemplateName
```
既存の証明書を更新するには
```
certreq –enroll –cert CertId [Options] Renew [ReuseKeys]
```
有効期限のある証明書のみを更新できます。 期限切れの証明書は更新できないため、新しい証明書で置き換える必要があります。

次に、シリアル番号を使用して証明書を更新する例を示します。
```
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" Renew
```
ここでは、* (*) を使用して、Web サーバーという証明書テンプレートに登録し、U/I 経由でポリシーサーバーを選択する例を示します。
```
certreq -enroll –machine –policyserver * "WebServer"
```
[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_Options"></a>オプション

|および|説明|
|-------|-----------|
|-任意|ICertRequest:: Submit を強制して、エンコードの種類を決定します。|
|-attrib \<attributestring >|名前と値の文字列のペアをコロンで区切って指定します。</br>名前と値の文字列のペアを \n で区切ります (例: Name1: Value1\nName2: Value2)。|
|-バイナリ|出力ファイルを base64 でエンコードされた形式ではなくバイナリとして書式設定します。|
|-Policyserver  *\<policyserver >*|"ldap:  *\<path >* "</br>証明書の登録ポリシー Web サービスを実行しているコンピューターの URI または一意の ID を挿入します。</br>参照によって要求ファイルを使用するように指定するには、  *\<policyserver >* にマイナス記号 (-) を使用するだけです。|
|-config \<configstring >|構成文字列で指定されている CA (Cahost\ caname) を使用して操作を処理します。 Https 接続の場合は、登録サーバーの URI を指定します。 ローカルコンピューターストアの CA の場合は、マイナス記号 (-) を使用します。|
|-匿名|証明書の登録 Web サービスには匿名の資格情報を使用します。|
|-Kerberos|証明書の登録 Web サービスには、Kerberos (ドメイン) 資格情報を使用します。|
|-ClientCertificate  *\<ClientCertId >*|*\<ClientCertID >* は、証明書の拇印、CN、EKU、template、email、UPN、および新しい name = value 構文に置き換えることができます。|
|-ユーザー  *\<名の >*|証明書の登録 Web サービスで使用されます。 *\<ユーザー名 >* を SAM 名または domain\user に置き換えることができます。 このオプションは、-p オプションと共に使用します。|
|-p  *\<パスワード >*|証明書の登録 Web サービスで使用されます。 *\<パスワード >* を実際のユーザーのパスワードに置き換えます。 このオプションは、-UserName オプションと共に使用します。|
|-ユーザー|新しい証明書要求の-ユーザーコンテキストを構成するか、証明書の受け入れのコンテキストを指定します。 これは、INF またはテンプレートで何も指定されていない場合の既定のコンテキストです。|
|-コンピューター|新しい証明書要求を構成するか、コンピューターコンテキストに対する証明書の受け入れのコンテキストを指定します。 新しい要求の場合、MachineKeyset INF キーとテンプレートコンテキストとの一貫性がある必要があります。 このオプションが指定されておらず、テンプレートでコンテキストが設定されていない場合、既定値はユーザーコンテキストになります。|
|-crl|CertChainFileOut で指定された base64 エンコード PKCS #7 ファイル、または RequestFileOut によって指定された base64 でエンコードされたファイルへの出力に証明書失効リスト (Crl) を含めます。|
|-rpc|分散 COM ではなくリモートプロシージャコール (RPC) サーバー接続を使用するように Active Directory 証明書サービス (AD CS) に指示します。|
|-AdminForceMachine|キーサービスまたは偽装を使用して、ローカルシステムコンテキストから要求を送信します。 このオプションを呼び出しているユーザーは、ローカル管理者のメンバーである必要があります。|
|-RenewOnBehalfOf|署名証明書で特定されたサブジェクトに代わって更新を送信します。 [ICertRequest:: Submit](https://technet.microsoft.com/subscriptions/aa385040.aspx)を呼び出すと、CR_IN_ROBO が設定します。|
|-f|既存のファイルを強制的に上書きします。 これにより、テンプレートとポリシーのキャッシュも省略されます。|
|-q|サイレントモードを使用します。すべての対話型プロンプトを非表示にします。|
|-Unicode|標準出力がリダイレクトされるとき、または別のコマンドにパイプ処理されるときに、Unicode 出力を書き込みます。これは、Windows PowerShell®スクリプトから呼び出された場合に役立ちます。|
|-UnicodeText|Base64 テキストでエンコードされたデータ blob をファイルに書き込むときに、Unicode 出力を送信します。|

[コンテンツ](#BKMK_Contents)に戻る

## <a name="BKMK_Formats"></a>83'7d

|83'7d|説明|
|-------|-----------|
|RequestFileIn|Base64 でエンコードされた、またはバイナリ入力ファイル名:PKCS #10 証明書の要求、CMS 証明書の要求、PKCS #7 証明書の更新要求、x.509 証明書をクロス認定にする、または Ssh-keygen タグ形式の証明書要求。|
|RequestFileOut|Base64 でエンコードされた出力ファイル名|
|CertFileOut|Base64 でエンコードされた X-509 ファイル名。|
|PKCS10FileOut|[Certreq-policy](#BKMK_policy)動詞でのみ使用します。 Base64 でエンコードされた PKCS10 出力ファイル名。|
|CertChainFileOut|Base64 でエンコードされた PKCS #7 ファイル名。|
|FullResponseFileOut|Base64 でエンコードされた完全な応答ファイル名。|
|PolicyFileIn|[Certreq-policy](#BKMK_policy)動詞でのみ使用します。 要求を限定するために使用される拡張機能のテキスト表現を含む INF ファイル。|

## <a name="BKMK_Examples"></a>その他の certreq の例

次の記事には、certreq の使用例が含まれています。
-   [カスタムのサブジェクト代替名を使用して証明書を要求する方法](https://technet.microsoft.com/library/ff625722.aspx)
-   [テスト ラボ ガイド:AD CS 2 層 PKI 階層の展開](https://technet.microsoft.com/library/hh831348.aspx)
-   [付録 3:Certreq 構文](https://technet.microsoft.com/library/cc736326.aspx)
-   [Web サーバーの SSL 証明書を手動で作成する方法](http://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)
-   [Windows Server 2008 CA を使用して AMT プロビジョニング証明書を要求する](https://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)
-   [System Center Operations Manager エージェントの証明書の登録](https://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)
-   [AD CS ステップバイステップガイド:2層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)
-   [サードパーティの証明機関を使用して SSL 経由で LDAP を有効にする方法](https://support.microsoft.com/kb/321051)

[コンテンツ](#BKMK_Contents)に戻る
