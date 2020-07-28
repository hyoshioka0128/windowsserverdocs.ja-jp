---
title: certutil
description: Certutil コマンドのリファレンス記事。これは、証明機関 (CA) の構成情報のダンプと表示、証明書サービスの構成、CA コンポーネントのバックアップと復元、証明書、キーペア、証明書チェーンの検証を行うコマンドラインプログラムです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 12ef5e7fa5ff305b1670c2f88645f57500c4fb5b
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87178588"
---
# <a name="certutil"></a>certutil

Certutil.exe は、証明書サービスの一部としてインストールされるコマンドラインプログラムです。 certutil.exe を使用すると、証明機関 (CA) の構成情報のダンプと表示、証明書サービスの構成、CA コンポーネントのバックアップと復元、証明書、キーペア、証明書チェーンの検証を行うことができます。

Certutil を追加パラメーターを指定せずに証明機関で実行すると、現在の証明機関の構成が表示されます。 Certutil が非証明機関で実行されている場合、コマンドは既定でコマンドを実行し `certutil [-dump]` ます。

> [!IMPORTANT]
> 以前のバージョンの certutil では、このドキュメントで説明されているすべてのオプションが提供されない場合があります。 またはを実行することで、certutil の特定のバージョンで提供されるすべてのオプションを確認でき `certutil -?` `certutil <parameter> -?` ます。

## <a name="parameters"></a>パラメーター

### <a name="-dump"></a>-ダンプ

構成情報またはファイルをダンプします。

```
certutil [options] [-dump]
certutil [options] [-dump] file
```

```
[-f] [-silent] [-split] [-p password] [-t timeout]
```

### <a name="-asn"></a>-asn

Asn.1 ファイルを解析します。

```
certutil [options] -asn file [type]
```

`[type]`: 数値 CRYPT_STRING_ * デコード型

### <a name="-decodehex"></a>-decodehex

16進数でエンコードされたファイルをデコードします。

```
certutil [options] -decodehex infile outfile [type]
```

`[type]`: 数値 CRYPT_STRING_ * エンコードの種類

```
[-f]
```

### <a name="-decode"></a>-デコード

Base64 でエンコードされたファイルをデコードします。

```
certutil [options] -decode infile outfile
```

```
[-f]
```

### <a name="-encode"></a>-エンコード

ファイルを Base64 にエンコードします。

```
certutil [options] -encode infile outfile
```

```
[-f] [-unicodetext]
```

### <a name="-deny"></a>-拒否

保留中の要求を拒否します。

```
certutil [options] -deny requestID
```

```
[-config Machine\CAName]
```

### <a name="-resubmit"></a>-再送信

保留中の要求を再送信します。

```
certutil [options] -resubmit requestId
```

```
[-config Machine\CAName]
```

### <a name="-setattributes"></a>-setattributes

保留中の証明書要求の属性を設定します。

```
certutil [options] -setattributes RequestID attributestring
```

各値の説明:

- **requestID**は、保留中の要求の数値要求 ID です。

- **attributestring**は、要求属性の名前と値のペアです。

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 名前と値はコロンで区切る必要がありますが、複数の名前と値のペアは改行で区切る必要があります。 たとえば `CertificateTemplate:User\nEMail:User@Domain.com` 、 `\n` シーケンスが改行区切り記号に変換されます。

### <a name="-setextension"></a>-setextension

保留中の証明書要求の拡張機能を設定します。

```
certutil [options] -setextension requestID extensionname flags {long | date | string | \@infile}
```

各値の説明:

- **requestID**は、保留中の要求の数値要求 ID です。

- **extensionname**は、拡張機能の ObjectId 文字列です。

- **フラグ**は、拡張機能の優先順位を設定します。 `0`が推奨されますが、では `1` 拡張機能が critical に設定され、拡張機能が無効になり、両方が実行され `2` `3` ます。

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 最後のパラメーターが数値の場合は、 **Long**として取得されます。

- 最後のパラメーターを日付として解析できる場合は、**日付**として取得されます。

- 最後のパラメーターがで始まる場合 `\@` 、トークンの残りの部分は、バイナリデータまたは ascii テキストの16進数ダンプを含むファイル名として取得されます。

- 最後のパラメーターがその他の場合は、文字列として取得されます。

### <a name="-revoke"></a>-revoke

証明書を失効します。

```
certutil [options] -revoke serialnumber [reason]
```

各値の説明:

- **シリアル化は、** 失効する証明書のシリアル番号のコンマ区切りの一覧です。

- **理由**は、失効理由の数値または記号表現で、次のようになります。

  - **0 CRL_REASON_UNSPECIFIED** -指定なし (既定)

  - **1. CRL_REASON_KEY_COMPROMISE**キーの侵害

  - **2. CRL_REASON_CA_COMPROMISE** -証明機関のセキュリティ侵害

  - **3. CRL_REASON_AFFILIATION_CHANGED** -所属が変更されました

  - **4. CRL_REASON_SUPERSEDED** -置き換え済み

  - **5. CRL_REASON_CESSATION_OF_OPERATION** -操作の中断

  - **6. CRL_REASON_CERTIFICATE_HOLD** -証明書保留

  - **8. CRL_REASON_REMOVE_FROM_CRL** -CRL からの削除

  - **1. 失効**取り消し-失効取り消し

```
[-config Machine\CAName]
```

### <a name="-isvalid"></a>-isvalid

現在の証明書の処理を表示します。

```
certutil [options] -isvalid serialnumber | certhash
```

```
[-config Machine\CAName]
```

### <a name="-getconfig"></a>-getconfig

既定の構成文字列を取得します。

```
certutil [options] -getconfig
```

```
[-config Machine\CAName]
```

### <a name="-ping"></a>-ping

Active Directory 証明書サービスの要求インターフェイスに接続します。

```
certutil [options] -ping [maxsecondstowait | camachinelist]
```

各値の説明:

- **camachinelist**は、CA コンピューター名のコンマ区切りの一覧です。 1台のコンピューターの場合は、終了コンマを使用します。 このオプションでは、各 CA コンピューターのサイトコストも表示されます。

```
[-config Machine\CAName]
```

### <a name="-cainfo"></a>-cainfo

証明機関に関する情報を表示します。

```
certutil [options] -cainfo [infoname [index | errorcode]]
```

各値の説明:

- **infoname**は、次の infoname 引数構文に基づいて、表示する CA プロパティを示します。

  - **ファイル**ファイルのバージョン

  - **製品**-製品バージョン

  - **exitcount** -Exit モジュール数

  - **終了 `[index]` **-モジュールの終了の説明

  - **ポリシー** -ポリシーモジュールの説明

  - **名前**-CA 名

  - **sanitizedname** -校正した CA 名

  - **dsname** -校正 CA の短い名前 (DS 名)

  - **共有フォルダ**-共有フォルダー

  - **Error1 ErrorCode** -エラーメッセージテキスト

  - **Error2 ErrorCode** -エラーメッセージテキストとエラーコード

  - **種類**-CA の種類

  - **情報**-CA 情報

  - **親**-親 CA

  - **certcount** -CA 証明書数

  - **xchgcount** -CA exchange 証明書数

  - **kracount** -KRA cert count

  - **kraused** -KRA cert used count

  - **propidmax** -最大 CA PropId

  - **certstate `[index]` **-CA 証明書

  - **certversion `[index]` **-CA 証明書のバージョン

  - **certstatuscode `[index]` **-CA 証明書検証の状態

  - **crlstate `[index]` **-CRL

  - **krastate `[index]` **-KRA cert

  - **クロス状態 + `[index]` **-クロス証明書を転送する

  - **クロス状態- `[index]` **-下位のクロス証明書

  - **証明 `[index]` 書**-CA 証明書

  - **certchain `[index]` **-CA 証明書チェーン

  - **certcrlchain `[index]` **-Crl を使用する CA 証明書チェーン

  - **xchg `[index]` **-CA exchange 証明書

  - **xchgchain `[index]` **-CA exchange 証明書チェーン

  - **xchgcrlchain `[index]` **-Crl を使用する CA exchange 証明書チェーン

  - **kra `[index]` **-KRA cert

  - **クロス + `[index]` **-クロス証明書を転送する

  - **クロス `[index]` **-下位のクロス証明書

  - **CRL `[index]` **-Base CRL

  - **deltacrl `[index]` **-Delta CRL

  - **crlstatus `[index]` **-CRL 発行ステータス

  - **deltacrlstatus `[index]` **-Delta CRL の公開ステータス

  - **dns** -dns 名

  - **ロール**ロールの分離

  - **広告**-高度なサーバー

  - **テンプレート**-テンプレート

  - **csp `[index]` **-OCSP Url

  - **aia `[index]` **-AIA Url

  - **cdp `[index]` **-CDP Url

  - **localename** -CA ロケール名

  - **subjecttemplateoids** -サブジェクトテンプレート oid

  - **&#42;** -すべてのプロパティを表示します

- **index**は、オプションの0から始まるプロパティインデックスです。

- **errorcode**は数値エラーコードです。

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cacert"></a>-ca. cert

証明機関の証明書を取得します。

```
certutil [options] -ca.cert outcacertfile [index]
```

各値の説明:

- **outcacertfile**は出力ファイルです。

- **index**は CA 証明書の更新インデックスです (既定では [最新])。

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cachain"></a>-ca. チェーン

証明機関の証明書チェーンを取得します。

```
certutil [options] -ca.chain outcacertchainfile [index]
```

各値の説明:

- **outcacertchainfile**は出力ファイルです。

- **index**は CA 証明書の更新インデックスです (既定では [最新])。

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-getcrl"></a>-getcrl

証明書失効リスト (CRL) を取得します。

certutil [オプション]-getcrl 出力 [インデックス] [差分]

各値の説明:

- **index**は crl インデックスまたはキーインデックスです (最新のキーの既定値は crl です)。

- **delta は DELTA** crl (既定では base crl) です。

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-crl"></a>-crl

新しい証明書失効リスト (Crl) または delta Crl を公開します。

```
certutil [options] -crl [dd:hh | republish] [delta]
```

各値の説明:

- **dd: hh**は、新しい CRL の有効期間 (日数と時間) です。

- 再パブリッシュすると、最新の Crl が再**発行**されます。

- **delta は**delta crl のみを公開します (既定では base と delta crl)。

```
[-split] [-config Machine\CAName]
```

### <a name="-shutdown"></a>-shutdown

Active Directory 証明書サービスをシャットダウンします。

```
certutil [options] -shutdown
```

```
[-config Machine\CAName]
```

### <a name="-installcert"></a>-installcert

証明機関証明書をインストールします。

```
certutil [options] -installcert [cacertfile]
```

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-renewcert"></a>-renewcert

証明機関の証明書を更新します。

```
certutil [options] -renewcert [reusekeys] [Machine\ParentCAName]
```

- `-f`未処理の更新要求を無視し、新しい要求を生成するには、を使用します。

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-schema"></a>-スキーマ

証明書のスキーマをダンプします。

```
certutil [options] -schema [ext | attrib | cRL]
```
各値の説明:

- コマンドの既定値は、要求テーブルと証明書テーブルです。

- **ext**は拡張テーブルです。

- **属性は属性**テーブルです。

- **crl は crl**テーブルです。

```
[-split] [-config Machine\CAName]
```

### <a name="-view"></a>-ビュー

証明書ビューをダンプします。

```
certutil [options] -view [queue | log | logfail | revoked | ext | attrib | crl] [csv]
```

各値の説明:

- **キュー**は特定の要求キューをダンプします。

- **ログ**には、発行または失効した証明書、および失敗した要求がダンプされます。

- **logfail**は、失敗した要求をダンプします。

- 失効した証明書のダンプを**取り消し**ます。

- **拡張テーブルをダンプし**ます。

- **属性テーブルをダンプし**ます。

- **crl は**crl テーブルをダンプします。

- **csv**では、コンマ区切り値を使用して出力が提供されます。

```
[-silent] [-split] [-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

#### <a name="remarks"></a>解説

- すべてのエントリの**StatusCode**列を表示するには、「」と入力します。`-out StatusCode`

- 最後のエントリのすべての列を表示するには、次のように入力します。`-restrict RequestId==$`

- 3つの要求の**RequestID**と**後処理**を表示するには、次のように入力します。`-restrict requestID>37,requestID<40 -out requestID,disposition`

- すべての Base Crl の行 Id**行 id**と**CRL 番号**を表示するには、次のように入力します。`-restrict crlminbase=0 -out crlrowID,crlnumber crl`

- を表示するには、次のように入力します。`-v -restrict crlminbase=0,crlnumber=3 -out crlrawcrl crl`

- CRL テーブル全体を表示するには、次のように入力します。`CRL`

- `Date[+|-dd:hh]`日付の制限に使用します。

- `now+dd:hh`現在の時刻を基準とする日付に使用します。

### <a name="-db"></a>-db

生のデータベースをダンプします。

```
certutil [options] -db
```

```
[-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

### <a name="-deleterow"></a>-deleterow

サーバーデータベースから行を削除します。

```
certutil [options] -deleterow rowID | date [request | cert | ext | attrib | crl]
```

各値の説明:

- **要求**は、送信日に基づいて、失敗した要求と保留中の要求を削除します。

- **証明書**は、有効期限の日付に基づいて、期限切れの証明書と失効した証明書を削除します。

- **ext**拡張テーブルを削除します。

- **属性は**、属性テーブルを削除します。

- **crl は**crl テーブルを削除します。

```
[-f] [-config Machine\CAName]
```

#### <a name="examples"></a>例

- 2001年1月22日に送信された失敗した保留中の要求を削除するには、次のように入力します。`1/22/2001 request`

- 2001年1月22日に期限切れになったすべての証明書を削除するには、次のように入力します。`1/22/2001 cert`

- RequestID 37 の証明書の行、属性、および拡張を削除するには、次のように入力します。`37`

- 2001年1月22日に期限切れになった Crl を削除するには、次のように入力します。`1/22/2001 crl`

### <a name="-backup"></a>-backup

Active Directory 証明書サービスをバックアップします。

```
certutil [options] -backup backupdirectory [incremental] [keeplog]
```

各値の説明:

- **backupdirectory**は、バックアップされたデータを格納するディレクトリです。

- **増分**バックアップのみを実行します (既定では完全バックアップ)。

- **keeplog**では、データベースログファイルが保持されます (既定では、ログファイルが切り捨てられます)。

```
[-f] [-config Machine\CAName] [-p Password]
```

### <a name="-backupdb"></a>-backupdb

Active Directory 証明書サービスデータベースをバックアップします。

```
certutil [options] -backupdb backupdirectory [incremental] [keeplog]
```

各値の説明:

- **backupdirectory**は、バックアップされたデータベースファイルを格納するディレクトリです。

- **増分**バックアップのみを実行します (既定では完全バックアップ)。

- **keeplog**では、データベースログファイルが保持されます (既定では、ログファイルが切り捨てられます)。

```
[-f] [-config Machine\CAName]
```

### <a name="-backupkey"></a>-backupkey

Active Directory 証明書サービスの証明書と秘密キーをバックアップします。

```
certutil [options] -backupkey backupdirectory
```

各値の説明:

- **backupdirectory**は、バックアップされた PFX ファイルを格納するディレクトリです。

```
[-f] [-config Machine\CAName] [-p password] [-t timeout]
```

### <a name="-restore"></a>-restore

Active Directory 証明書サービスを復元します。

```
certutil [options] -restore backupdirectory
```

各値の説明:

- **backupdirectory**は、復元するデータが格納されているディレクトリです。

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-restoredb"></a>-restoredb

Active Directory 証明書サービスデータベースを復元します。

```
certutil [options] -restoredb backupdirectory
```

各値の説明:

- **backupdirectory**は、復元するデータベースファイルが格納されているディレクトリです。

```
[-f] [-config Machine\CAName]
```

### <a name="-restorekey"></a>-restorekey

Active Directory 証明書サービス証明書と秘密キーを復元します。

```
certutil [options] -restorekey backupdirectory | pfxfile
```

各値の説明:

- **backupdirectory**は、復元する PFX ファイルが格納されているディレクトリです。

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-importpfx"></a>-importpfx

証明書と秘密キーをインポートします。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -importpfx [certificatestorename] pfxfile [modifiers]
```

各値の説明:

- **証明**証明書ストアの名前を指定します。

- **修飾子**はコンマ区切りのリストで、次の1つ以上を含めることができます。

  1. **AT_SIGNATURE** -keyspec を署名に変更します

  2. **AT_KEYEXCHANGE** -keyspec をキー交換に変更します。

  3. **Noexport** -秘密キーをエクスポート不可にします。

  4. **Nocert** -証明書をインポートしません

  5. **Nochain** -証明書チェーンをインポートしません

  6. **Noroot** -ルート証明書がインポートされません

  7. **保護**-パスワードを使用してキーを保護します

  8. **Noprotect** -パスワードを使用してキーを保護しません

```
[-f] [-user] [-p password] [-csp provider]
```

#### <a name="remarks"></a>解説

- 既定値はパーソナルコンピューターストアです。

### <a name="-dynamicfilelist"></a>-dynamicfilelist

動的ファイルリストを表示します。

```
certutil [options] -dynamicfilelist
```

```
[-config Machine\CAName]
```

### <a name="-databaselocations"></a>-databaselocations

データベースの場所を表示します。

```
certutil [options] -databaselocations
```

```
[-config Machine\CAName]
```

### <a name="-hashfile"></a>-hashfile

ファイルに暗号化ハッシュを生成して表示します。

```
certutil [options] -hashfile infile [hashalgorithm]
```

### <a name="-store"></a>-ストア

証明書ストアをダンプします。

```
certutil [options] -store [certificatestorename [certID [outputfile]]]
```

各値の説明:

- **証明**は、証明書ストアの名前です。 次に例を示します。

  - `My, CA (default), Root,`

  - `ldap:///CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?one?objectClass=certificationAuthority (View Root Certificates)`

  - `ldap:///CN=CAName,CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Modify Root Certificates)`

  - `ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?certificateRevocationList?base?objectClass=cRLDistributionPoint (View CRLs)`

  - `ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Enterprise CA Certificates)`

  - `ldap: (AD computer object certificates)`

  - `-user ldap: (AD user object certificates)`

- **certID**は、証明書または CRL の一致トークンです。 これには、シリアル番号、SHA-1 証明書、CRL、CTL または公開キーハッシュ、数値証明書インデックス (0、1など)、数値の CRL インデックス (.0、.1 など)、数値 CTL インデックス (.) を指定できます。0、..1など)、公開キー、署名、または拡張 ObjectId、証明書のサブジェクトの共通名、電子メールアドレス、UPN または DNS 名、キーコンテナー名または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーションポリシーの ObjectId、または CRL 発行者の共通名。 多くの場合、複数の一致が発生する可能性があります。

- **outputfile**は、一致する証明書を保存するために使用するファイルです。

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-silent] [-split] [-dc DCName]
```

#### <a name="options"></a>オプション

- この `-user` オプションは、コンピューターストアではなくユーザーストアにアクセスします。

- オプションは、 `-enterprise` コンピューターのエンタープライズストアにアクセスします。

- オプションは、 `-service` machine service ストアにアクセスします。

- この `-grouppolicy` オプションは、コンピューターグループポリシーストアにアクセスします。

次に例を示します。

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-addstore"></a>-addstore

ストアに証明書を追加します。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -addstore certificatestorename infile
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **infile**には、ストアに追加する証明書または CRL ファイルを指定します。

```
[-f] [-user] [-enterprise] [-grouppolicy] [-dc DCName]
```

### <a name="-delstore"></a>-delstore

ストアから証明書を削除します。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -delstore certificatestorename certID
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **certID**は、証明書または CRL の一致トークンです。

```
[-enterprise] [-user] [-grouppolicy] [-dc DCName]
```

### <a name="-verifystore"></a>-verifystore

ストア内の証明書を検証します。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -verifystore certificatestorename [certID]
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **certID**は、証明書または CRL の一致トークンです。

```
[-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-dc DCName] [-t timeout]
```

### <a name="-repairstore"></a>-repairstore

キーの関連付けを修復するか、証明書のプロパティまたはキーのセキュリティ記述子を更新します。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -repairstore certificatestorename certIDlist [propertyinffile | SDDLsecuritydescriptor]
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **certIDlist**は、証明書または CRL 一致トークンのコンマ区切りの一覧です。 詳細については、この記事の説明を参照してください `-store certID` 。

- **propertyinffile**は、次のような外部プロパティを含む INF ファイルです。

  ```
  [Properties]
      19 = Empty ; Add archived property, OR:
      19 =       ; Remove archived property

      11 = {text}Friendly Name ; Add friendly name property

      127 = {hex} ; Add custom hexadecimal property
          _continue_ = 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
          _continue_ = 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f

      2 = {text} ; Add Key Provider Information property
        _continue_ = Container=Container Name&
        _continue_ = Provider=Microsoft Strong Cryptographic Provider&
        _continue_ = ProviderType=1&
        _continue_ = Flags=0&
        _continue_ = KeySpec=2

      9 = {text} ; Add Enhanced Key Usage property
        _continue_ = 1.3.6.1.5.5.7.3.2,
        _continue_ = 1.3.6.1.5.5.7.3.1,
  ```

```
[-f] [-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-csp provider]
```

### <a name="-viewstore"></a>-viewstore

証明書ストアをダンプします。 詳細については、 `-store` この記事のパラメーターを参照してください。

```
certutil [options] -viewstore [certificatestorename [certID [outputfile]]]
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **certID**は、証明書または CRL の一致トークンです。

- **outputfile**は、一致する証明書を保存するために使用するファイルです。

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>オプション

- この `-user` オプションは、コンピューターストアではなくユーザーストアにアクセスします。

- オプションは、 `-enterprise` コンピューターのエンタープライズストアにアクセスします。

- オプションは、 `-service` machine service ストアにアクセスします。

- この `-grouppolicy` オプションは、コンピューターグループポリシーストアにアクセスします。

次に例を示します。

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-viewdelstore"></a>-viewdelstore

ストアから証明書を削除します。

```
certutil [options] -viewdelstore [certificatestorename [certID [outputfile]]]
```

各値の説明:

- **証明**は、証明書ストアの名前です。

- **certID**は、証明書または CRL の一致トークンです。

- **outputfile**は、一致する証明書を保存するために使用するファイルです。

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>オプション

- この `-user` オプションは、コンピューターストアではなくユーザーストアにアクセスします。

- オプションは、 `-enterprise` コンピューターのエンタープライズストアにアクセスします。

- オプションは、 `-service` machine service ストアにアクセスします。

- この `-grouppolicy` オプションは、コンピューターグループポリシーストアにアクセスします。

次に例を示します。

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-dspublish"></a>-dspublish

証明書または証明書失効リスト (CRL) を Active Directory に発行します。

```
certutil [options] -dspublish certfile [NTAuthCA | RootCA | SubCA | CrossCA | KRA | User | Machine]
```

```
certutil [options] -dspublish CRLfile [DSCDPContainer [DSCDPCN]]
```

各値の説明:

- **certfile**は、発行する証明書ファイルの名前です。

- **Ntauthca**は、DS エンタープライズストアに証明書を発行します。

- **Rootca**は、DS の信頼されたルートストアに証明書を発行します。

- **サブ ca**は、ca 証明書を DS ca オブジェクトに発行します。

- **Crossca**は、クロス証明書を DS CA オブジェクトに発行します。

- **KRA**は、DS キー回復エージェントオブジェクトに証明書を発行します。

- **ユーザーは**、ユーザー DS オブジェクトに証明書を発行します。

- **コンピューターは**、コンピューター DS オブジェクトに証明書を発行します。

- **CRLfile**には、発行する CRL ファイルの名前を指定します。

- **Dsc/container**は、DS CDP コンテナー CN (通常は CA コンピューター名) です。

- **DSCDPCN**は DS CDP オブジェクト CN で、通常は、校正された CA の短い名前とキーのインデックスに基づいています。

- `-f`新しい DS オブジェクトを作成するには、を使用します。

```
[-f] [-user] [-dc DCName]
```

### <a name="-adtemplate"></a>-adtemplate

Active Directory テンプレートを表示します。

```
certutil [options] -adtemplate [template]
```

```
[-f] [-user] [-ut] [-mt] [-dc DCName]
```

### <a name="-template"></a>-テンプレート

証明書テンプレートが表示されます。

```
certutil [options] -template [template]
```

```
[-f] [-user] [-silent] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-templatecas"></a>-templatecas

証明書テンプレートの証明機関 (Ca) を表示します。

```
certutil [options] -templatecas template
```

```
[-f] [-user] [-dc DCName]
```

### <a name="-catemplates"></a>-catemplates

証明機関のテンプレートが表示されます。

```
certutil [options] -catemplates [template]
```

```
[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]
```

### <a name="-setcasites"></a>-setcasites

証明機関のサイト名の設定、検証、および削除を含む、サイト名を管理します。

```
certutil [options] -setcasites [set] [sitename]
certutil [options] -setcasites verify [sitename]
certutil [options] -setcasites delete
```

各値の説明:

- **sitename**は、1つの証明機関を対象とする場合にのみ使用できます。

```
[-f] [-config Machine\CAName] [-dc DCName]
```

#### <a name="remarks"></a>解説

- この `-config` オプションは、単一の証明機関を対象とします (既定値はすべての ca です)。

- オプションを使用すると、 `-f` 指定した**sitename**の検証エラーを上書きしたり、すべての CA sitenames 削除したりできます。

> [!NOTE]
> Active Directory Domain Services (AD DS) サイト認識用に Ca を構成する方法の詳細については、「 [AD CS および PKI クライアントのサイト認識の AD DS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11))」を参照してください。

### <a name="-enrollmentserverurl"></a>-enrollmentserverURL

CA に関連付けられている登録サーバーの Url を表示、追加、または削除します。

```
certutil [options] -enrollmentServerURL [URL authenticationtype [priority] [modifiers]]
certutil [options] -enrollmentserverURL URL delete
```

各値の説明:

- **authenticationtype**は、URL を追加するときに、次のいずれかのクライアント認証方法を指定します。

  1. **kerberos** -kerberos SSL 資格情報を使用します。

  2. **ユーザー名**-SSL 資格情報に名前付きアカウントを使用します。

  3. **clientcertificate**:-X.509 証明書の SSL 資格情報を使用します。

  4. **匿名**の SSL 資格情報を使用します。

- **delete**は、CA に関連付けられている指定された URL を削除します。

- **priority** `1` URL を追加するときに指定しない場合、優先順位の既定値はになります。

- **修飾子**はコンマで区切られたリストで、次の1つ以上が含まれます。

1. この URL を使用して、 **allowrenewalsonly**のみの更新要求をこの CA に送信できます。

2. **allowkey: 更新**-AD にアカウントが関連付けられていない証明書を使用できるようにします。 これは、clientcertificate および allowrenewalsonly モードでのみ適用されます。

```
[-config Machine\CAName] [-dc DCName]
```

### <a name="-adca"></a>-adca

Active Directory 証明機関が表示されます。

```
certutil [options] -adca [CAName]
```

```
[-f] [-split] [-dc DCName]
```

### <a name="-ca"></a>-ca

登録ポリシーの証明機関が表示されます。

```
certutil [options] -CA [CAName | templatename]
```

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policy"></a>-ポリシー

登録ポリシーが表示されます。

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policycache"></a>-policycache

登録ポリシーのキャッシュエントリを表示または削除します。

```
certutil [options] -policycache [delete]
```

各値の説明:

- **delete**は、ポリシーサーバーのキャッシュエントリを削除します。

- **-f すべての**キャッシュエントリを削除します。

```
[-f] [-user] [-policyserver URLorID]
```

### <a name="-credstore"></a>-credstore

資格情報ストアのエントリを表示、追加、または削除します。

```
certutil [options] -credstore [URL]
certutil [options] -credstore URL add
certutil [options] -credstore URL delete
```

各値の説明:

- **Url**はターゲット url です。 また、を使用して `*` 、すべてのエントリを一致させたり `https://machine*` 、URL プレフィックスを一致させたりすることもできます。

- [**追加追加**する資格情報ストアエントリを追加します。 このオプションを使用する場合は、SSL 資格情報を使用する必要もあります。

- **delete**は、資格情報ストアのエントリを削除します。

- **-f**は、1つのエントリを上書きするか、複数のエントリを削除します。

```
[-f] [-user] [-silent] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-installdefaulttemplates"></a>-installdefaulttemplates

既定の証明書テンプレートをインストールします。

```
certutil [options] -installdefaulttemplates
```

```
[-dc DCName]
```

### <a name="-urlcache"></a>-URLcache

URL キャッシュエントリを表示または削除します。

```
certutil [options] -URLcache [URL | CRL | * [delete]]
```

各値の説明:

- **Url**はキャッシュされた url です。

- **Crl**は、キャッシュされているすべての crl url でのみ実行されます。

- **&#42;** は、キャッシュされたすべての url に対して動作します。

- **delete**は、現在のユーザーのローカルキャッシュから関連する url を削除します。

- **-f**は、特定の URL のフェッチとキャッシュの更新を強制します。

```
[-f] [-split]
```

### <a name="-pulse"></a>-pulse

自動登録イベントをパルスします。

```
certutil [options] -pulse
```

```
[-user]
```

### <a name="-machineinfo"></a>-machineinfo

Active Directory マシンオブジェクトに関する情報を表示します。

```
certutil [options] -machineinfo domainname\machinename$
```

### <a name="-dcinfo"></a>-DCInfo

ドメインコントローラーに関する情報を表示します。 既定では、確認なしで DC 証明書が表示されます。

```
certutil [options] -DCInfo [domain] [verify | deletebad | deleteall]
```

```
[-f] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

> [!TIP]
> Active Directory Domain Services (AD DS) ドメイン **[ドメイン]** を指定し、ドメインコントローラー (**-dc**) を指定する機能は、Windows Server 2012 で追加されました。 コマンドを正常に実行するには、 **Domain admins**または**Enterprise admins**のメンバーであるアカウントを使用する必要があります。 このコマンドの動作変更は次のとおりです。<ol><li>1. ドメインが指定されておらず、特定のドメインコントローラーが指定されていない場合、このオプションは、既定のドメインコントローラーから処理するドメインコントローラーの一覧を返します。</li><li>2. ドメインが指定されておらず、ドメインコントローラーが指定されている場合は、指定されたドメインコントローラー上の証明書のレポートが生成されます。</li><li>3. ドメインが指定されていても、ドメインコントローラーが指定されていない場合は、一覧の各ドメインコントローラーの証明書に関するレポートと共に、ドメインコントローラーの一覧が生成されます。</li><li>4. ドメインとドメインコントローラーが指定されている場合は、ドメインコントローラーの一覧が対象のドメインコントローラーから生成されます。 一覧内の各ドメインコントローラーの証明書のレポートも生成されます。</li></ol>
>
>たとえば、cpandl-DC1 という名前のドメインコントローラーを持つ CPANDL という名前のドメインがあるとします。 次のコマンドを実行して、CPANDL-DC1 からドメインコントローラーとその証明書の一覧を取得できます。`certutil -dc cpandl-dc1 -DCInfo cpandl`

### <a name="-entinfo"></a>-entinfo

エンタープライズ証明機関に関する情報を表示します。

```
certutil [options] -entinfo domainname\machinename$
```

```
[-f] [-user]
```

### <a name="-tcainfo"></a>-tcainfo

証明機関に関する情報を表示します。

```
certutil [options] -tcainfo [domainDN | -]
```

```
[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

### <a name="-scinfo"></a>-scinfo

スマートカードに関する情報を表示します。

```
certutil [options] -scinfo [readername [CRYPT_DELETEKEYSET]]
```

各値の説明:

- **CRYPT_DELETEKEYSET**スマートカードのすべてのキーを削除します。

```
[-silent] [-split] [-urlfetch] [-t timeout]
```

### <a name="-scroots"></a>-scroots

スマートカードのルート証明書を管理します。

```
certutil [options] -scroots update [+][inputrootfile] [readername]
certutil [options] -scroots save \@in\\outputrootfile [readername]
certutil [options] -scroots view [inputrootfile | readername]
certutil [options] -scroots delete [readername]
```

```
[-f] [-split] [-p Password]
```

### <a name="-verifykeys"></a>-verifykeys

公開キーまたは秘密キーのセットを検証します。

```
certutil [options] -verifykeys [keycontainername cacertfile]
```

各値の説明:

- **cspparameters.keycontainername**は、検証するキーのキーコンテナーの名前です。 このオプションの既定値は [マシンキー] です。 ユーザーキーに切り替えるには、を使用 `-user` します。

- **cacertfile**は、証明書ファイルを署名または暗号化します。

```
[-f] [-user] [-silent] [-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 引数を指定しない場合は、各署名 CA 証明書がその秘密キーに対して検証されます。

- この操作は、ローカルの CA またはローカルキーに対してのみ実行できます。

### <a name="-verify"></a>-verify

証明書、証明書失効リスト (CRL)、または証明書チェーンを検証します。

```
certutil [options] -verify certfile [applicationpolicylist | - [issuancepolicylist]]
certutil [options] -verify certfile [cacertfile [crossedcacertfile]]
certutil [options] -verify CRLfile cacertfile [issuedcertfile]
certutil [options] -verify CRLfile cacertfile [deltaCRLfile]
```

各値の説明:

- **certfile**検証する証明書の名前を指定します。

- **applicationpolicylist**は、必要なアプリケーションポリシー ObjectIds のコンマ区切りのリストです (省略可能)。

- **issuancepolicylist**は、必須の発行ポリシー ObjectIds のコンマ区切りのリストです (省略可能)。

- **cacertfile**は、検証対象の発行元 CA 証明書です (省略可能)。

- **crossedcacertfile**は、 **certfile**によってクロス証明されたオプションの証明書です。

- **CRLfile**は、 **cacertfile**を検証するために使用される CRL ファイルです。

- **issuedcertfile**は、CRLfile によってカバーされる、省略可能な発行証明書です。

- **deltaCRLfile**は、オプションの delta CRL ファイルです。

```
[-f] [-enterprise] [-user] [-silent] [-split] [-urlfetch] [-t timeout]
```

#### <a name="remarks"></a>解説

- **Applicationpolicylist**を使用すると、チェーンの構築が、指定されたアプリケーションポリシーに対して有効なチェーンのみに制限されます。

- **Issuancepolicylist**を使用すると、チェーンの構築が、指定された発行ポリシーに対して有効なチェーンのみに制限されます。

- **Cacertfile**を使用して、ファイル内のフィールドを**Certfile**または**CRLfile**に対して検証します。

- **Issuedcertfile**を使用して、ファイル内のフィールドを**CRLfile**に対して検証します。

- DeltaCRLfile を使用すると、ファイル内のフィールドが**certfile**に対して検証されます。

- **Cacertfile**が指定されていない場合は、完全なチェーンが**certfile**に対して構築および検証されます。

- **Cacertfile**と**crossedcacertfile**の両方が指定されている場合、両方のファイルのフィールドが**certfile**に対して検証されます。

### <a name="-verifyctl"></a>-verifyCTL

AuthRoot または許可されていない証明書の CTL を確認します。

```
certutil [options] -verifyCTL CTLobject [certdir] [certfile]
```

各値の説明:

- **Ctlobject**は、確認する CTL を次のように識別します。

  - **AuthRootWU** -AUTHROOT CAB と一致する証明書を URL キャッシュから読み取ります。 `-f`代わりに、を使用して Windows Update からダウンロードしてください。

  - **Disallowedwu** -許可されていない証明書の CAB を読み取り、URL キャッシュから許可されていない証明書ストアファイルを読み取ります。 `-f`代わりに、を使用して Windows Update からダウンロードしてください。

  - **Authroot** -レジストリにキャッシュされた AUTHROOT CTL を読み取ります。 とを使用し、 `-f` 信頼されていない**certfile**を使用して、レジストリにキャッシュされた authroot を強制的に更新します。

  - **許可**しない-レジストリでキャッシュされた許可されていない証明書の CTL を読み取ります。 とを使用し、 `-f` 信頼されていない**certfile**を使用して、レジストリにキャッシュされた authroot を強制的に更新します。

- **CTLFILENAME** CTL または CAB ファイルへのファイルまたは http パスを指定します。

- **certdir** CTL エントリに一致する証明書を含むフォルダーを指定します。 既定値は、 **Ctlobject**と同じフォルダーまたは web サイトです。 Http フォルダーパスを使用するには、末尾にパスの区切り文字が必要です。 **Authroot**を指定しない場合、または**許可**しない場合は、ローカル証明書ストア、crypt32.dll リソース、ローカル URL キャッシュなど、一致する証明書が複数の場所で検索されます。 必要に応じ `-f` て Windows Update からダウンロードするには、を使用します。

- **certfile**検証する証明書を指定します。 証明書は CTL エントリと照合され、結果が表示されます。 このオプションを選択すると、ほとんどの既定の出力が抑制されます。

```
[-f] [-user] [-split]
```

### <a name="-sign"></a>-sign

証明書失効リスト (CRL) または証明書に再署名します。

```
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [startdate+dd:hh] [+serialnumberlist | -serialnumberlist | -objectIDlist | \@extensionfile]
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [#hashalgorithm] [+alternatesignaturealgorithm | -alternatesignaturealgorithm]
```

各値の説明:

- **infilelist**は、変更して再署名する証明書または CRL ファイルのコンマ区切りの一覧です。

- **シリアル値は、** 作成する証明書のシリアル番号です。 有効期間とその他のオプションを指定することはできません。

- **Crl**によって空の crl が作成されます。 有効期間とその他のオプションを指定することはできません。

- **outfilelist**は、変更された証明書または CRL 出力ファイルのコンマ区切りの一覧です。 ファイルの数は、infilelist と一致している必要があります。

- **startdate + dd: hh**は、証明書または CRL ファイルの新しい有効期間です。これには次のものが含まれます。

  - 任意の日付 +

  - オプションの日付と時間の有効期間

  両方を指定する場合は、正符号 (+) 区切り記号を使用する必要があります。 `now[+dd:hh]`現在の時刻からを開始するには、を使用します。 `never`有効期限がない場合は、を使用します (crl の場合のみ)。

- **serialnumberlist**には、追加または削除するファイルのコンマ区切りのシリアル番号の一覧を指定します。

- **objectIDlist**は、削除するファイルのコンマ区切りの拡張子 ObjectId リストです。

- ** \@ extensionfile**は、更新または削除する拡張機能を含む INF ファイルです。 次に例を示します。

  ```
  [Extensions]
      2.5.29.31 = ; Remove CRL Distribution Points extension
      2.5.29.15 = {hex} ; Update Key Usage extension
      _continue_=03 02 01 86
  ```

- **hashalgorithm**ハッシュアルゴリズムの名前を指定します。 これには、記号の前にあるテキストのみを指定する必要があり `#` ます。

- **alternatesignaturealgorithm**は、代替署名アルゴリズム指定子です。

```
[-nullsign] [-f] [-silent] [-cert certID]
```

#### <a name="remarks"></a>解説

- 負符号 (-) を使用すると、シリアル番号と拡張機能が削除されます。

- 正符号 (+) を使用して、シリアル番号を CRL に追加します。

- 一覧を使用して、シリアル番号と ObjectIDs の両方を CRL から同時に削除することができます。

- **Alternatesignaturealgorithm**の前にマイナス記号を使用すると、従来の署名形式を使用できます。 プラス記号を使用すると、代替署名形式を使用できます。 **Alternatesignaturealgorithm**を指定しない場合は、証明書または CRL の署名形式が使用されます。

### <a name="-vroot"></a>-vroot

Web 仮想ルートとファイル共有を作成または削除します。

```
certutil [options] -vroot [delete]
```

### <a name="-vocsproot"></a>-vocsproot

OCSP web プロキシの web 仮想ルートを作成または削除します。

```
certutil [options] -vocsproot [delete]
```

### <a name="-addenrollmentserver"></a>-addenrollmentserver

必要に応じて、指定した証明機関の登録サーバーアプリケーションとアプリケーションプールを追加します。 このコマンドでは、バイナリまたはパッケージはインストールされません。

```
certutil [options] -addenrollmentserver kerberos | username | clientcertificate [allowrenewalsonly] [allowkeybasedrenewal]
```

各値の説明:

- **addenrollmentserver**では、次のような証明書登録サーバーへのクライアント接続に認証方法を使用する必要があります。

  - **kerberos**は、kerberos SSL 資格情報を使用します。

  - **ユーザー名**は、SSL 資格情報に名前付きアカウントを使用します。

  - **clientcertificate**は、X.509 証明書の SSL 資格情報を使用します。

- **allowrenewalsonly**では、URL を介して証明機関に更新要求を送信することのみが許可されます。

- **allowkeyベースの更新**では、Active Directory にアカウントが関連付けられていない証明書を使用できます。 これは、 **clientcertificate**および**allowrenewalsonly**モードで使用する場合に適用されます。

```
[-config Machine\CAName]
```

### <a name="-deleteenrollmentserver"></a>-deleteenrollmentserver

必要に応じて、指定した証明機関の登録サーバーアプリケーションとアプリケーションプールを削除します。 このコマンドでは、バイナリまたはパッケージはインストールされません。

```
certutil [options] -deleteenrollmentserver kerberos | username | clientcertificate
```

各値の説明:

- **deleteenrollmentserver**では、次のような証明書登録サーバーへのクライアント接続に認証方法を使用する必要があります。

  - **kerberos**は、kerberos SSL 資格情報を使用します。

  - **ユーザー名**は、SSL 資格情報に名前付きアカウントを使用します。

  - **clientcertificate**は、X.509 証明書の SSL 資格情報を使用します。

```
[-config Machine\CAName]
```

### <a name="-addpolicyserver"></a>-addpolicyserver

必要に応じて、ポリシーサーバーアプリケーションとアプリケーションプールを追加します。 このコマンドでは、バイナリまたはパッケージはインストールされません。

```
certutil [options] -addpolicyserver kerberos | username | clientcertificate [keybasedrenewal]
```

各値の説明:

- **addpolicyserver**では、次のような証明書ポリシーサーバーへのクライアント接続に認証方法を使用する必要があります。

  - **kerberos**は、kerberos SSL 資格情報を使用します。

  - **ユーザー名**は、SSL 資格情報に名前付きアカウントを使用します。

  - **clientcertificate**は、X.509 証明書の SSL 資格情報を使用します。

- **キーベースの更新**では、キーベースの更新テンプレートを含むクライアントに返されたポリシーを使用できます。 このオプションは、**ユーザー名**と**clientcertificate**認証にのみ適用されます。

### <a name="-deletepolicyserver"></a>-deletepolicyserver

必要に応じて、ポリシーサーバーアプリケーションとアプリケーションプールを削除します。 このコマンドでは、バイナリやパッケージは削除されません。

certutil [オプション]-deletePolicyServer kerberos |username |clientcertificate [キーベースの更新]

各値の説明:

- **deletepolicyserver**では、次のような証明書ポリシーサーバーへのクライアント接続に認証方法を使用する必要があります。

  - **kerberos**は、kerberos SSL 資格情報を使用します。

  - **ユーザー名**は、SSL 資格情報に名前付きアカウントを使用します。

  - **clientcertificate**は、X.509 証明書の SSL 資格情報を使用します。

- **キーベースの更新**では、キーベース更新ポリシーサーバーを使用できます。

### <a name="-oid"></a>-oid

オブジェクト識別子を表示するか、表示名を設定します。

```
certutil [options] -oid objectID [displayname | delete [languageID [type]]]
certutil [options] -oid groupID
certutil [options] -oid agID | algorithmname [groupID]
```

各値の説明:

- **objectID**には、表示名を追加するためのまたはが表示されます。

- **groupid**は、objectIDs を列挙する groupid の数 (decimal) です。

- **algID**は、objectID が検索する16進数の ID です。

- **algorithmname**は、objectID が検索するアルゴリズムの名前です。

- **DISPLAYNAME** DS に格納する名前を表示します。

- **削除**すると、表示名が削除されます。

- **LanguageId**言語 ID の値を指定します (既定値は 1033)。

- **Type**は、次を含む、作成する DS オブジェクトの種類です。

  - `1`-Template (既定値)

  - `2`-発行ポリシー

  - `3`-アプリケーションポリシー

- `-f`DS オブジェクトを作成します。

### <a name="-error"></a>-エラー

エラーコードに関連付けられたメッセージテキストを表示します。

```
certutil [options] -error errorcode
```

### <a name="-getreg"></a>-getreg

レジストリ値を表示します。

```
certutil [options] -getreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

各値の説明:

- **ca**は、証明機関のレジストリキーを使用します。

- **復元**では、証明機関の restore レジストリキーが使用されます。

- **ポリシーは**、ポリシーモジュールのレジストリキーを使用します。

- **exit**は、最初の終了モジュールのレジストリキーを使用します。

- **テンプレート**は、テンプレートレジストリキーを使用し `-user` ます (ユーザーテンプレートに使用されます)。

- **登録**では、登録レジストリキーを使用し `-user` ます (ユーザーコンテキストに使用します)。

- **チェーン**は、チェーン構成のレジストリキーを使用します。

- **policyservers**は、ポリシーサーバーのレジストリキーを使用します。

- **progid**は、ポリシーまたは終了モジュールの progid (レジストリサブキー名) を使用します。

- **registryvaluename**では、レジストリ値の名前 `Name*` を使用します (をプレフィックスと一致させます)。

- **値**は、新しい数値、文字列、または日付のレジストリ値またはファイル名を使用します。 数値がまたはで始まる場合は、 `+` `-` 新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 文字列値がまたはで始まり、 `+` `-` 既存の値が値の場合は、 `REG_MULTI_SZ` 既存のレジストリ値に対して文字列が追加または削除されます。 値を強制的に作成するには `REG_MULTI_SZ` 、 `\n` 文字列値の末尾にを追加します。

- 値がで始まる場合 `\@` 、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルが参照されていない場合は、代わりに `[Date][+|-][dd:hh]` 省略可能な日付またはマイナス (省略可能) として解釈されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 `now+dd:hh`現在の時刻を基準とする日付に使用します。

- `chain\chaincacheresyncfiletime \@now`キャッシュされた crl を効果的にフラッシュするには、を使用します。

### <a name="-setreg"></a>-setreg

レジストリ値を設定します。

```
certutil [options] -setreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]]registryvaluename value
```

各値の説明:

- **ca**は、証明機関のレジストリキーを使用します。

- **復元**では、証明機関の restore レジストリキーが使用されます。

- **ポリシーは**、ポリシーモジュールのレジストリキーを使用します。

- **exit**は、最初の終了モジュールのレジストリキーを使用します。

- **テンプレート**は、テンプレートレジストリキーを使用し `-user` ます (ユーザーテンプレートに使用されます)。

- **登録**では、登録レジストリキーを使用し `-user` ます (ユーザーコンテキストに使用します)。

- **チェーン**は、チェーン構成のレジストリキーを使用します。

- **policyservers**は、ポリシーサーバーのレジストリキーを使用します。

- **progid**は、ポリシーまたは終了モジュールの progid (レジストリサブキー名) を使用します。

- **registryvaluename**では、レジストリ値の名前 `Name*` を使用します (をプレフィックスと一致させます)。

- **値**は、新しい数値、文字列、または日付のレジストリ値またはファイル名を使用します。 数値がまたはで始まる場合は、 `+` `-` 新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 文字列値がまたはで始まり、 `+` `-` 既存の値が値の場合は、 `REG_MULTI_SZ` 既存のレジストリ値に対して文字列が追加または削除されます。 値を強制的に作成するには `REG_MULTI_SZ` 、 `\n` 文字列値の末尾にを追加します。

- 値がで始まる場合 `\@` 、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルが参照されていない場合は、代わりに `[Date][+|-][dd:hh]` 省略可能な日付またはマイナス (省略可能) として解釈されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 `now+dd:hh`現在の時刻を基準とする日付に使用します。

- `chain\chaincacheresyncfiletime \@now`キャッシュされた crl を効果的にフラッシュするには、を使用します。

### <a name="-delreg"></a>-delreg

レジストリ値を削除します。

```
certutil [options] -delreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

各値の説明:

- **ca**は、証明機関のレジストリキーを使用します。

- **復元**では、証明機関の restore レジストリキーが使用されます。

- **ポリシーは**、ポリシーモジュールのレジストリキーを使用します。

- **exit**は、最初の終了モジュールのレジストリキーを使用します。

- **テンプレート**は、テンプレートレジストリキーを使用し `-user` ます (ユーザーテンプレートに使用されます)。

- **登録**では、登録レジストリキーを使用し `-user` ます (ユーザーコンテキストに使用します)。

- **チェーン**は、チェーン構成のレジストリキーを使用します。

- **policyservers**は、ポリシーサーバーのレジストリキーを使用します。

- **progid**は、ポリシーまたは終了モジュールの progid (レジストリサブキー名) を使用します。

- **registryvaluename**では、レジストリ値の名前 `Name*` を使用します (をプレフィックスと一致させます)。

- **値**は、新しい数値、文字列、または日付のレジストリ値またはファイル名を使用します。 数値がまたはで始まる場合は、 `+` `-` 新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>解説

- 文字列値がまたはで始まり、 `+` `-` 既存の値が値の場合は、 `REG_MULTI_SZ` 既存のレジストリ値に対して文字列が追加または削除されます。 値を強制的に作成するには `REG_MULTI_SZ` 、 `\n` 文字列値の末尾にを追加します。

- 値がで始まる場合 `\@` 、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルが参照されていない場合は、代わりに `[Date][+|-][dd:hh]` 省略可能な日付またはマイナス (省略可能) として解釈されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 `now+dd:hh`現在の時刻を基準とする日付に使用します。

- `chain\chaincacheresyncfiletime \@now`キャッシュされた crl を効果的にフラッシュするには、を使用します。

### <a name="-importkms"></a>-importKMS

キーのアーカイブのために、ユーザーキーと証明書をサーバーデータベースにインポートします。

```
certutil [options] -importKMS userkeyandcertfile [certID]
```

各値の説明:

- **userkeyandcertfile**は、ユーザーの秘密キーとアーカイブされる証明書を含むデータファイルです。 このファイルは次のようになります。

  - Exchange キー管理サーバー (KMS) エクスポートファイル。

  - PFX ファイル。

- certID は、KMS エクスポートファイルの暗号化解除証明書の一致トークンです。 詳細については、 `-store` この記事のパラメーターを参照してください。

- `-f`証明機関によって発行されていない証明書をインポートします。

```
[-f] [-silent] [-split] [-config Machine\CAName] [-p password] [-symkeyalg symmetrickeyalgorithm[,keylength]]
```

### <a name="-importcert"></a>-importcert

証明書ファイルをデータベースにインポートします。

```
certutil [options] -importcert certfile [existingrow]
```

各値の説明:

- **existingrow**は、同じキーに対して保留中の要求の代わりに証明書をインポートします。

- `-f`証明機関によって発行されていない証明書をインポートします。

```
[-f] [-config Machine\CAName]
```

#### <a name="remarks"></a>解説

また、外部証明書をサポートするように証明機関を構成する必要がある場合もあります。 これを行うには、「」と入力 `import - certutil -setreg ca\KRAFlags +KRAF_ENABLEFOREIGN` します。

### <a name="-getkey"></a>-getkey

アーカイブされた秘密キーの回復 blob を取得し、回復スクリプトを生成するか、アーカイブされたキーを回復します。

```
certutil [options] -getkey searchtoken [recoverybloboutfile]
certutil [options] -getkey searchtoken script outputscriptfile
certutil [options] -getkey searchtoken retrieve | recover outputfilebasename
```

各値の説明:

- **スクリプト**は、キーを取得および回復するスクリプトを生成します (複数の一致する回復候補が検出された場合、または出力ファイルが指定されていない場合は既定の動作です)。

- **取得**は、1つまたは複数のキー回復 blob を取得します (一致する復旧候補が1つだけ見つかった場合、および出力ファイルが指定されている場合は既定の動作)。 このオプションを使用すると、すべての拡張機能が切り捨てられ、キー回復 blob ごとに証明書固有の文字列と拡張子が追加されます。  各ファイルには、証明書チェーンと関連付けられている秘密キーが含まれ、1つまたは複数のキー回復エージェントの証明書に対して引き続き暗号化されます。

- **回復**は、1回の手順で (キー回復エージェントの証明書と秘密キーを必要とする) 秘密キーを取得して回復します。 このオプションを使用すると、拡張子が切り捨てられ、p12 拡張子が追加されます。  各ファイルには、回復した証明書チェーンと、PFX ファイルとして格納されている関連する秘密キーが含まれています。

- **searchtoken**は、回復するキーと証明書を選択します。次にその一部を示します。

  - 1. [証明書の共通名]

  - 2. 証明書のシリアル番号

  - 3. 証明書 SHA-1 ハッシュ (拇印)

  - 4. 証明書キー Id SHA-1 ハッシュ (サブジェクトキー識別子)

  - 5. 要求者名 (ドメイン \ ユーザー)

  - 6. UPN (ユーザー \@ ドメイン)

- **recoverybloboutfile**は、証明書チェーンと関連付けられた秘密キーを含むファイルを出力しますが、1つまたは複数のキー回復エージェントの証明書に対して暗号化されます。

- **outputscriptfile**は、プライベートキーを取得して回復するためのバッチスクリプトを含むファイルを出力します。

- **outputfilebasename**は、ファイルのベース名を出力します。

```
[-f] [-unicodetext] [-silent] [-config Machine\CAName] [-p password] [-protectto SAMnameandSIDlist] [-csp provider]
```

### <a name="-recoverkey"></a>-回復キー

アーカイブされた秘密キーを回復します。

```
certutil [options] -recoverkey recoveryblobinfile [PFXoutfile [recipientindex]]
```

```
[-f] [-user] [-silent] [-split] [-p password] [-protectto SAMnameandSIDlist] [-csp provider] [-t timeout]
```

### <a name="-mergepfx"></a>-mergePFX

PFX ファイルをマージします。

```
certutil [options] -mergePFX PFXinfilelist PFXoutfile [extendedproperties]
```

各値の説明:

- **PFXinfilelist**は、PFX 入力ファイルのコンマ区切りの一覧です。

- **PFXoutfile**は PFX 出力ファイルの名前です。

- **extendedproperties**には、すべての拡張プロパティが含まれます。

```
[-f] [-user] [-split] [-p password] [-protectto SAMnameAndSIDlist] [-csp provider]
```

#### <a name="remarks"></a>解説

- コマンドラインで指定するパスワードは、コンマ区切りのパスワードリストである必要があります。

- 複数のパスワードを指定した場合は、最後のパスワードが出力ファイルに使用されます。 パスワードが1つしか指定されていない場合、または最後のパスワードがの場合は `*` 、出力ファイルのパスワードを入力するように求められます。

### <a name="-convertepf"></a>-収束 Tepf

PFX ファイルを EPF ファイルに変換します。

```
certutil [options] -convertEPF PFXinfilelist PFXoutfile [cast | cast-] [V3CAcertID][,salt]
```

各値の説明:


- **PFXinfilelist**は、PFX 入力ファイルのコンマ区切りの一覧です。

- **PFXoutfile**は PFX 出力ファイルの名前です。

- **EPF** EPF 出力ファイルの名前を指定します。

- **cast**は、cast 64 暗号化を使用します。

- **cast-** cast 64 encryption (export) を使用します。

- **V3CAcertID**は、V3 CA 証明書の一致トークンです。 詳細については、 `-store` この記事のパラメーターを参照してください。

- **salt**は、EPF 出力ファイルの salt 文字列です。

```
[-f] [-silent] [-split] [-dc DCName] [-p password] [-csp provider]
```

#### <a name="remarks"></a>解説

- コマンドラインで指定するパスワードは、コンマ区切りのパスワードリストである必要があります。

- 複数のパスワードを指定した場合は、最後のパスワードが出力ファイルに使用されます。 パスワードが1つしか指定されていない場合、または最後のパスワードがの場合は `*` 、出力ファイルのパスワードを入力するように求められます。

### <a name="-"></a>-?

パラメーターの一覧を表示します。

```
certutil -?
certutil <name_of_parameter> -?
certutil -? -v
```

各値の説明:

- **-?** パラメーターの完全な一覧を表示します。

- **-`<name_of_parameter>` -?** 指定されたパラメーターのヘルプコンテンツを表示します。

- **-?-v**では、パラメーターとオプションの完全な一覧が表示されます。

## <a name="options"></a>オプション

このセクションでは、コマンドに基づいて、指定できるすべてのオプションを定義します。 各パラメーターには、使用できるオプションに関する情報が含まれています。

| オプション | 説明 |
| ------- | ----------- |
| -nullsign | データのハッシュを署名として使用します。 |
| -f | 強制的に上書きします。 |
| -enterprise | ローカルコンピューターのエンタープライズレジストリ証明書ストアを使用します。 |
| -ユーザー | HKEY_CURRENT_USER キーまたは証明書ストアを使用します。 |
| -GroupPolicy | グループポリシー証明書ストアを使用します。 |
| -ut | ユーザーテンプレートを表示します。 |
| -mt | コンピューターテンプレートを表示します。 |
| -Unicode | Unicode でリダイレクト出力を書き込みます。 |
| -UnicodeText | 出力ファイルを Unicode で書き込みます。 |
| -gmt | GMT を使用して時刻を表示します。 |
| -秒 | 秒とミリ秒を使用して時刻を表示します。 |
| -silent | フラグを使用して、 `silent` crypt コンテキストを取得します。 |
| -分割 | 埋め込みの asn.1 要素を分割し、ファイルに保存します。 |
| -v | 詳細情報を入力します (詳細)。 |
| -privatekey | パスワードと秘密キーのデータを表示します。 |
| -pin のピン留め | スマートカードの PIN。 |
| -urlfetch | AIA 証明書および CDP Crl を取得および検証します。 |
| -config Machine\CAName | 証明機関とコンピューター名の文字列。 |
| -policyserver URLorID | ポリシーサーバーの URL または ID。 選択 U/I の場合は、を使用 `-policyserver` します。 すべてのポリシーサーバーで、を使用します。`-policyserver *`|
| -匿名 | 匿名の SSL 資格情報を使用します。 |
| -kerberos | Kerberos SSL 資格情報を使用します。 |
| -clientcertificate clientcertID | X.509 証明書の SSL 資格情報を使用します。 選択 U/I の場合は、を使用 `-clientcertificate` します。 |
| -ユーザー名 | SSL 資格情報には名前付きアカウントを使用します。 選択 U/I の場合は、を使用 `-username` します。 |
| -cert certID | 署名証明書。 |
| -dc DCName | 特定のドメインコントローラーをターゲットにします。 |
| -restrictionlist を制限する | コンマ区切りの制限リスト。 各制限は、列名、関係演算子、および定数整数、文字列、または日付で構成されます。 並べ替え順序を示すには、1つの列名の前にプラスまたはマイナス記号を付けることができます。 たとえば、`requestID = 47`、`+requestername >= a, requestername`、`-requestername > DOMAIN, Disposition = 21` などがあります。 |
| -out columnlist | コンマ区切りの列リスト。 |
| -p パスワード | Password |
| -protectto SAMnameandSIDlist | コンマ区切りの SAM 名/SID リスト。 |
| -csp プロバイダー | プロバイダー |
| -t タイムアウト | URL フェッチのタイムアウト (ミリ秒)。 |
| -symkeyalg symmetrickeyalgorithm [, keylength] | オプションのキー長を持つ対称キーアルゴリズムの名前。 例: `AES,128` または `3DES` |

### <a name="additional-references"></a>その他のリファレンス

このコマンドの使用方法に関するその他の例については、「」を参照してください。

- [Active Directory 証明書サービス (AD CS)](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11))

- [証明書を管理するための Certutil タスク](/previous-versions/orphan-topics/ws.10/cc772898(v=ws.10))

- [certutil コマンド](certutil.md)
