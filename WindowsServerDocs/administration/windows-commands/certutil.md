---
title: certutil
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c9946cc53fe3a901c3f6ee53f082a5b3d086c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379653"
---
# <a name="certutil"></a>certutil

Certutil は、証明書サービスの一部としてインストールされるコマンドラインプログラムです。 Certutil を使用して、証明機関 (CA) の構成情報のダンプと表示、証明書サービスの構成、CA コンポーネントのバックアップと復元、証明書、キーペア、証明書チェーンの検証を行うことができます。

追加のパラメーターを指定せずに証明機関で certutil を実行すると、現在の証明機関の構成が表示されます。 Cerutil が非証明機関で実行される場合、コマンドは既定で certutil [-dump](#-dump)動詞を実行します。

> [!WARNING]
> 以前のバージョンの certutil では、このドキュメントで説明されているすべてのオプションが提供されない場合があります。 「[構文表記](#syntax-notations)」セクションに示されているコマンドを実行すると、certutil の特定のバージョンで提供されるすべてのオプションを確認できます。

## <a name="menu"></a>Menu

このドキュメントの主なセクションは次のとおりです。

- [助動詞](#verbs)
- [構文表記](#syntax-notations)
- [[オプション](#options)]
- [その他の certutil の例](#additional-certutil-examples)

## <a name="verbs"></a>[動詞]

次の表では、certutil コマンドで使用できる動詞について説明します。

|[動詞]|説明|
|-----|-----------|
|[-ダンプ](#-dump)|構成情報またはファイルをダンプする|
|[-asn](#-asn)|Asn.1 ファイルを解析する|
|[-decodehex](#-decodehex)|16進数でエンコードされたファイルのデコード|
|[-デコード](#-decode)|Base64 でエンコードされたファイルをデコードする|
|[-エンコード](#-encode)|Base64 へのファイルのエンコード|
|[-拒否](#-deny)|保留中の証明書の要求を拒否する|
|[-再送信](#-resubmit)|保留中の証明書要求を再送信する|
|[-setattributes](#-setattributes)|保留中の証明書要求の属性を設定する|
|[-setextension](#-setextension)|保留中の証明書要求の拡張機能を設定する|
|[-revoke](#-revoke)|証明書の失効|
|[-isvalid](#-isvalid)|現在の証明書の処理を表示する|
|[-getconfig](#-getconfig)|既定の構成文字列を取得する|
|[-ping](#-ping)|Active Directory 証明書サービスの要求インターフェイスに接続しようとしました|
|-ping 管理者|Active Directory Certificate Services 管理インターフェイスに接続しようとしました|
|[-CAInfo](#-cainfo)|証明機関に関する情報を表示する|
|[-ca. cert](#-cacert)|証明機関の証明書を取得します。|
|[-ca. チェーン](#-cachain)|証明機関の証明書チェーンを取得します。|
|[-GetCRL](#-getcrl)|証明書失効リスト (CRL) を取得する|
|[-CRL](#-crl)|新しい証明書失効リスト (Crl) を発行する (または delta Crl のみ)|
|[-shutdown](#-shutdown)|Active Directory 証明書サービスのシャットダウン|
|[-installCert](#-installcert)|証明機関証明書のインストール|
|[-renewCert](#-renewcert)|証明機関証明書を更新する|
|[-スキーマ](#-schema)|証明書のスキーマをダンプする|
|[-ビュー](#-view)|証明書ビューをダンプする|
|[-db](#-db)|Raw データベースをダンプする|
|[-deleterow](#-deleterow)|サーバーデータベースからの行の削除|
|[-バックアップ](#-backup)|バックアップ Active Directory 証明書サービス|
|[-backupDB](#-backupdb)|Active Directory 証明書サービスデータベースをバックアップする|
|[-backupKey](#-backupkey)|Active Directory 証明書サービスの証明書と秘密キーをバックアップする|
|[-復元](#-restore)|Active Directory 証明書サービスの復元|
|[-restoreDB](#-restoredb)|Active Directory 証明書サービスデータベースを復元する|
|[-restoreKey](#-restorekey)|Active Directory 証明書サービスの証明書と秘密キーを復元する|
|[-importPFX](#-importpfx)|証明書と秘密キーのインポート|
|[-dynamicfilelist](#-dynamicfilelist)|動的ファイルリストの表示|
|[-databaselocations](#-databaselocations)|データベースの場所の表示|
|[-hashfile](#-hashfile)|ファイルに暗号化ハッシュを生成して表示する|
|[-ストア](#-store)|証明書ストアをダンプする|
|[-addstore](#-addstore)|証明書をストアに追加する|
|[-delstore](#-delstore)|ストアから証明書を削除する|
|[-verifystore](#-verifystore)|ストア内の証明書を確認する|
|[-repairstore](#-repairstore)|キーの関連付けを修復するか、証明書のプロパティまたはキーのセキュリティ記述子を更新します。|
|[-viewstore](#-viewstore)|証明書ストアをダンプする|
|[-viewdelstore](#-viewdelstore)|ストアから証明書を削除する|
|[-dsPublish](#-dspublish)|証明書または証明書失効リスト (CRL) を Active Directory に発行する|
|[-ADTemplate](#-adtemplate)|AD テンプレートの表示|
|[-テンプレート](#-template)|証明書テンプレートを表示する|
|[-TemplateCAs](#-templatecas)|証明書テンプレートの証明機関 (Ca) を表示する|
|[-CATemplates](#-catemplates)|CA のテンプレートを表示する|
|[-SetCASites](#-setcasites)|Ca のサイト名を管理する|
|[-enrollmentServerURL](#-enrollmentserverurl)|CA に関連付けられている登録サーバーの Url を表示、追加、または削除する|
|[-ADCA](#-adca)|AD CAs を表示する|
|[-CA](#-ca)|登録ポリシーの Ca を表示する|
|[-ポリシー](#-policy)|登録ポリシーを表示する|
|[-PolicyCache](#-policycache)|登録ポリシーのキャッシュエントリを表示または削除する|
|[-CredStore](#-credstore)|資格情報ストアのエントリを表示、追加、または削除する|
|[-InstallDefaultTemplates](#-installdefaulttemplates)|既定の証明書テンプレートをインストールする|
|[-URLCache](#-urlcache)|URL キャッシュエントリを表示または削除する|
|[-pulse](#-pulse)|パルス自動登録イベント|
|[-MachineInfo](#-machineinfo)|Active Directory マシンオブジェクトに関する情報を表示する|
|[-DCInfo](#-dcinfo)|ドメインコントローラーに関する情報を表示する|
|[-EntInfo](#-entinfo)|エンタープライズ CA に関する情報を表示する|
|[-TCAInfo](#-tcainfo)|CA に関する情報を表示する|
|[-SCInfo](#-scinfo)|スマートカードに関する情報を表示する|
|[-SCRoots](#-scroots)|スマートカードのルート証明書の管理|
|[-verifykeys](#-verifykeys)|公開キーまたは秘密キーのセットを確認する|
|[-verify](#-verify)|証明書、証明書失効リスト (CRL)、または証明書チェーンを検証する|
|[-verifyCTL](#-verifyctl)|AuthRoot または許可されていない証明書の CTL を確認する|
|[-sign](#-sign)|証明書失効リスト (CRL) または証明書に再署名する|
|[-vroot](#-vroot)|Web 仮想ルートとファイル共有を作成または削除する|
|[-vocsproot](#-vocsproot)|OCSP web プロキシの web 仮想ルートを作成または削除する|
|[-addEnrollmentServer](#-addenrollmentserver)|登録サーバーアプリケーションの追加|
|[-deleteEnrollmentServer](#-deleteenrollmentserver)|登録サーバーアプリケーションの削除|
|[-addPolicyServer](#-addpolicyserver)|ポリシーサーバーアプリケーションの追加|
|[-deletePolicyServer](#-deletepolicyserver)|ポリシーサーバーアプリケーションの削除|
|[-oid](#-oid)|オブジェクト識別子を表示するか、表示名を設定します。|
|[-エラー](#-error)|エラーコードに関連付けられたメッセージテキストを表示する|
|[-getreg](#-getreg)|レジストリ値の表示|
|[-setreg](#-setreg)|レジストリ値の設定|
|[-delreg](#-delreg)|レジストリ値の削除|
|[-ImportKMS](#-importkms)|キーのアーカイブ用にユーザーキーと証明書をサーバーデータベースにインポートする|
|[-ImportCert](#-importcert)|証明書ファイルをデータベースにインポートする|
|[-GetKey](#-getkey)|アーカイブされた秘密キーの回復 blob を取得する|
|[-回復キー](#-recoverkey)|アーカイブされた秘密キーを回復する|
|[-MergePFX](#-mergepfx)|PFX ファイルのマージ|
|[-収束 Tepf](#-convertepf)|PFX ファイルを EPF ファイルに変換する|
|-?|動詞の一覧を表示します|
|- *\<動詞 >* -?|指定された動詞のヘルプを表示します。|
|-? -v|動詞との完全な一覧を表示します。|

[メニュー](#menu)に戻る

## <a name="syntax-notations"></a>構文表記

- 基本的なコマンドライン構文については、`certutil -?` を実行してください。
- 特定の動詞で certutil を使用する構文については、 **certutil** *\<verb >* **-?**
- すべての certutil 構文をテキストファイルに送信するには、次のコマンドを実行します。  
  - `certutil -v -? > certutilhelp.txt`
  - `notepad certutilhelp.txt`

次の表では、コマンドライン構文を示すために使用される表記法について説明します。


|            表し             |                  説明                  |
|---------------------------------|-----------------------------------------------|
| 角かっこまたは中かっこを含まないテキスト |         表示されるように入力する必要がある項目          |
|  山かっこ内のテキストを \<>  | 値を指定する必要があるプレースホルダー |
|  [角かっこ内のテキスト]  |                省略可能な項目                 |
|      {中かっこ内のテキスト}       |       必須項目のセット1つ選択する       |
|         縦棒 (          |                       )                       |
|          省略記号 (...)           |          繰り返し可能な項目           |

[メニュー](#menu)に戻る

## <a name="-dump"></a>-ダンプ

CertUtil [オプション] [-dump]

CertUtil [オプション] [-dump] ファイル

構成情報またはファイルをダンプする

[-f][-silent][-split][-p パスワード][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-asn"></a>-asn

CertUtil [オプション]-asn ファイル [種類]

Asn.1 ファイルを解析する

型: numeric CRYPT\_STRING\_\* デコード型

[メニュー](#menu)に戻る

## <a name="-decodehex"></a>-decodehex

CertUtil [オプション]-decodehex InFile 出力 [種類]

型: numeric CRYPT\_STRING\_\* encoding 型

[-f]

[メニュー](#menu)に戻る

## <a name="-decode"></a>-デコード

CertUtil [オプション]-InFile 出力のデコード

Base64 でエンコードされたファイルのデコード

[-f]

[メニュー](#menu)に戻る

## <a name="-encode"></a>-エンコード

CertUtil [オプション]-エンコード InFile の出力

Base64 へのファイルのエンコード

[-f][-UnicodeText]

[メニュー](#menu)に戻る

## <a name="-deny"></a>-拒否

CertUtil [オプション]-deny RequestId

保留中の要求を拒否する

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-resubmit"></a>-再送信

CertUtil [オプション]-RequestId を再送信する

保留中の要求の再送信

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-setattributes"></a>-setattributes

CertUtil [オプション]-setattributes RequestId AttributeString

保留中の要求の属性を設定する

RequestId--保留中の要求の数値要求 Id

AttributeString--属性名と値のペアを要求する

- 名前と値はコロンで区切られます。
- 複数の名前、値のペアは改行で区切られています。
- 例: "CertificateTemplate:User\nEMail:User@Domain.com"
- 各 "\n" シーケンスは改行区切り記号に変換されます。

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-setextension"></a>-setextension

CertUtil [オプション]-setextension RequestId ExtensionName フラグ {Long |Date |String |\@InFile}

保留中の要求の拡張機能の設定

RequestId--保留中の要求の数値要求 Id

ExtensionName--拡張機能の ObjectId 文字列

Flags--0 をお勧めします。  1拡張が重大になるようにします。2によって無効になります。

最後のパラメーターが数値の場合は、Long として取得されます。

日付として解析できる場合は、日付として取得されます。

'\@' で始まる場合、トークンの残りの部分は、バイナリデータまたは ascii テキストの16進ダンプを含むファイル名です。

他のものはすべて文字列として取得されます。

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-revoke"></a>-revoke

CertUtil [オプション]-シリアル化を取り消す [理由]

証明書の失効

シリアル化: 失効する証明書のシリアル番号のコンマ区切りの一覧

理由: 数値またはシンボルの失効理由

- 0: CRL_REASON_UNSPECIFIED: 指定されていません (既定)。
- 1: CRL_REASON_KEY_COMPROMISE: キーのセキュリティ侵害
- 2: CRL_REASON_CA_COMPROMISE: CA のセキュリティ侵害
- 3: CRL_REASON_AFFILIATION_CHANGED: 所属の変更
- 4: CRL_REASON_SUPERSEDED: 置き換えられる
- 5: CRL_REASON_CESSATION_OF_OPERATION: 操作の中断
- 6: CRL_REASON_CERTIFICATE_HOLD: 証明書保留
- 8: CRL_REASON_REMOVE_FROM_CRL: CRL からの削除
- -1: 取り消し取り消し: 失効取り消し

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-isvalid"></a>-isvalid

CertUtil [オプション]-isvalid シリアル |CertHash

現在の証明書の廃棄を表示する

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-getconfig"></a>-getconfig

CertUtil [オプション]-getconfig

既定の構成文字列を取得する

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-ping"></a>-ping

CertUtil [オプション]-ping [Maxセカンダリ Dstowait |CAMachineList]

Ping Active Directory 証明書サービスの要求インターフェイス

CAMachineList--コンマで区切られた CA コンピューター名の一覧

1. 1台のコンピューターの場合は、終了コンマを使用します。
2. 各 CA コンピューターのサイトコストが表示されます。

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-cainfo"></a>-CAInfo

CertUtil [オプション]-CAInfo [InfoName [Index |ErrorCode]]

CA 情報を表示する

InfoName--表示する CA プロパティを示します (下記参照)。 すべてのプロパティに対して "\*" を使用します。

Index--省略可能な0から始まるプロパティインデックス

ErrorCode--数値エラーコード

[-f][-split][-config Machine\CAName]

InfoName 引数の構文:

- ファイル: ファイルバージョン
- 製品: 製品バージョン
- exitcount: 終了モジュール数
- 終了 [インデックス]: モジュールの終了の説明
- ポリシー: ポリシーモジュールの説明
- 名前: CA 名
- sanitizedname: 校正した CA 名
- dsname: 校正 CA の短い名前 (DS 名)
- sharedfolder: 共有フォルダー
- error1 ErrorCode: エラーメッセージテキスト
- error2 ErrorCode: エラーメッセージテキストとエラーコード
- 種類: CA の種類
- 情報: CA 情報
- 親: 親 CA
- certcount: CA 証明書数
- xchgcount: CA exchange 証明書数
- kracount: KRA cert count
- kraused: KRA cert used count
- propidmax: 最大 CA PropId
- certstate [インデックス]: CA 証明書
- certversion [Index]: CA 証明書のバージョン
- certstatuscode [Index]: CA 証明書検証の状態
- crlstate [インデックス]: CRL
- krastate [Index]: KRA cert
- クロスステート + [Index]: クロス証明書を転送します
- クロス状態-[インデックス]: 下位のクロス証明書
- 証明書 [インデックス]: CA 証明書
- certchain [インデックス]: CA 証明書チェーン
- certcrlchain [Index]: Crl を持つ CA 証明書チェーン
- xchg [Index]: CA exchange cert
- xchgchain [インデックス]: CA exchange 証明書チェーン
- xchgcrlchain [Index]: Crl を使用する CA exchange 証明書チェーン
- kra [インデックス]: KRA cert
- クロス + [インデックス]: クロス証明書を転送する
- クロス [インデックス]: 下位のクロス証明書
- CRL [インデックス]: Base CRL
- deltacrl [Index]: Delta CRL
- crlstatus [Index]: CRL 発行ステータス
- deltacrlstatus [Index]: Delta CRL の公開ステータス
- dns: DNS 名
- 役割: 役割の分離
- 広告: 高度なサーバー
- テンプレート: テンプレート
- csp [インデックス]: OCSP Url
- aia [インデックス]: AIA Url
- cdp [インデックス]: CDP Url
- localename: CA のロケール名
- subjecttemplateoids: サブジェクトテンプレート Oid

[メニュー](#menu)に戻る

## <a name="-cacert"></a>-ca. cert

CertUtil [オプション]-ca. cert OutCACertFile [Index]

CA の証明書を取得する

OutCACertFile: 出力ファイル

インデックス: CA 証明書の更新インデックス (既定では最新)

[-f][-split][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-cachain"></a>-ca. チェーン

CertUtil [オプション]-OutCACertChainFile [インデックス]

CA の証明書チェーンを取得する

OutCACertChainFile: 出力ファイル

インデックス: CA 証明書の更新インデックス (既定では最新)

[-f][-split][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-getcrl"></a>-GetCRL

CertUtil [オプション]-GetCRL 出力 [インデックス] [差分]

CRL を取得する

インデックス: CRL インデックスまたはキーインデックス (最新のキーの既定値は CRL)

デルタ: delta CRL (既定は base CRL)

[-f][-split][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-crl"></a>-CRL

CertUtil [オプション]-CRL [dd: hh | 再発行] [差分]

新しい Crl を発行する [または delta Crl のみ]

dd: hh--新しい CRL の有効期間 (日数と時間)

再発行--最新の Crl を再発行します。

差分--delta Crl のみ (既定は base および delta Crl)

[-split][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-shutdown"></a>-shutdown

CertUtil [オプション]-shutdown

Active Directory 証明書サービスのシャットダウン

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-installcert"></a>-installCert

CertUtil [オプション]-installCert [CACertFile]

証明機関証明書のインストール

[-f][-silent][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-renewcert"></a>-renewCert

CertUtil [オプション]-renewCert [ReuseKeys] [Machine\ParentCAName]

証明機関証明書の更新

未処理の更新要求を無視し、新しい要求を生成するには、-f を使用します。

[-f][-silent][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-schema"></a>-スキーマ

CertUtil [オプション]-schema [Ext |Attrib |.CRL

証明書スキーマのダンプ

要求と証明書テーブルの既定値

Ext: 拡張テーブル

Attrib: 属性テーブル

CRL: CRL テーブル

[-split][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-view"></a>-ビュー

CertUtil [オプション]-view [Queue |Log |LogFail |取り消し |Ext |Attrib |CRL] [csv]

証明書ビューのダンプ

Queue: 要求キュー

ログ: 発行または失効した証明書、および失敗した要求

LogFail: 失敗した要求

失効: 失効した証明書

Ext: 拡張テーブル

Attrib: 属性テーブル

CRL: CRL テーブル

csv: コンマ区切り値として出力

すべてのエントリの StatusCode 列を表示するには:-out StatusCode

最後のエントリのすべての列を表示する場合:-restrict "RequestId = = $"

3つの要求に対して RequestId と後処理を表示するには:-restrict "RequestId > = 37, RequestId\<40"-out "RequestId, ディスポジション"

すべての Base Crl の行 Id と CRL 番号を表示するには:-restrict "CRLMinBase = 0"-out "CRLRowId, CRLNumber" CRL

Base CRL Number 3 を表示するには:-v-制限 "CRLMinBase = 0, CRLNumber = 3"-out "CRLRawCRL" CRL

CRL テーブル全体を表示するには: CRL

日付制限には、"Date [+ |-dd: hh]" を使用します。

現在の時刻を基準とする日付に "now + dd: hh" を使用します。

[-silent][-split][-config Machine\CAName][-制限 RestrictionList][-out ColumnList]

[メニュー](#menu)に戻る

## <a name="-db"></a>-db

CertUtil [オプション]-db

Raw データベースをダンプする

[-config Machine\CAName][-制限 RestrictionList][-out ColumnList]

[メニュー](#menu)に戻る

## <a name="-deleterow"></a>-deleterow

CertUtil [オプション]-deleterow RowId |日付 [Request |Cert |Ext |Attrib |.CRL

サーバーデータベース行の削除

要求: 失敗した要求と保留中の要求 (送信日)

証明書: 期限切れおよび失効した証明書 (有効期限)

Ext: 拡張テーブル

Attrib: 属性テーブル

CRL: CRL テーブル (有効期限)

2001: 1/22/2001 要求によって送信された失敗した要求と保留中の要求を削除するには

2001年1月22日に期限切れになったすべての証明書を削除するには 1/22/2001 Cert

RequestId 37:37 の証明書行、属性、および拡張機能を削除するには

2001年1月22日に期限切れになった Crl を削除するには 1/22/2001 CRL

[-f][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-backup"></a>-バックアップ

CertUtil [オプション]-backup BackupDirectory [増分] [KeepLog]

バックアップ Active Directory 証明書サービス

BackupDirectory: バックアップされたデータを格納するディレクトリ

増分: 増分バックアップのみを実行します (既定値は完全バックアップです)

KeepLog: データベースログファイルを保持します (既定では、ログファイルが切り捨てられます)

[-f][-config Machine\CAName][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-backupdb"></a>-backupDB

CertUtil [オプション]-backupDB BackupDirectory [増分] [KeepLog]

バックアップ Active Directory 証明書サービスデータベース

BackupDirectory: バックアップされたデータベースファイルを格納するディレクトリ

増分: 増分バックアップのみを実行します (既定値は完全バックアップです)

KeepLog: データベースログファイルを保持します (既定では、ログファイルが切り捨てられます)

[-f][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-backupkey"></a>-backupKey

CertUtil [オプション]-backupKey BackupDirectory

証明書サービス証明書と秘密キーのバックアップ Active Directory

BackupDirectory: バックアップされた PFX ファイルを格納するディレクトリ

[-f][-config Machine\CAName][-p パスワード][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-restore"></a>-復元

CertUtil [オプション]-BackupDirectory の復元

Active Directory 証明書サービスの復元

BackupDirectory: 復元するデータを含むディレクトリ

[-f][-config Machine\CAName][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-restoredb"></a>-restoreDB

CertUtil [オプション]-restoreDB BackupDirectory

Active Directory 証明書サービスデータベースの復元

BackupDirectory: 復元するデータベースファイルが格納されているディレクトリ

[-f][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-restorekey"></a>-restoreKey

CertUtil [オプション]-restoreKey BackupDirectory |PFXFile

Active Directory 証明書サービス証明書と秘密キーを復元する

BackupDirectory: 復元する PFX ファイルを含むディレクトリ

PFXFile: 復元する PFX ファイル

[-f][-config Machine\CAName][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-importpfx"></a>-importPFX

CertUtil [オプション]-importPFX [証明] PFXFile [Modifiers]

証明書と秘密キーのインポート

証明: 証明書ストアの名前。  「 [-Store」を](#-store)参照してください。

PFXFile: インポートする PFX ファイル

修飾子: 次の1つまたは複数のコンマ区切りのリスト。

1. AT_SIGNATURE: KeySpec を署名に変更する
2. AT_KEYEXCHANGE: KeySpec をキー交換に変更する
3. NoExport: 秘密キーをエクスポート不可にします。
4. NoCert: 証明書をインポートしません
5. NoChain: 証明書チェーンをインポートしません
6. NoRoot: ルート証明書をインポートしない
7. 保護: パスワードを使用してキーを保護する
8. NoProtect: パスワード保護キーを入力しません

既定値はパーソナルコンピューターストアです。

[-f][-ユーザー][-p パスワード][-csp プロバイダー]

[メニュー](#menu)に戻る

## <a name="-dynamicfilelist"></a>-dynamicfilelist

CertUtil [オプション]-dynamicfilelist

動的ファイルリストの表示

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-databaselocations"></a>-databaselocations

CertUtil [オプション]-databaselocations 場所

データベースの場所の表示

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-hashfile"></a>-hashfile

CertUtil [オプション]-hashfile InFile [HashAlgorithm]

ファイルに暗号化ハッシュを生成して表示する

[メニュー](#menu)に戻る

## <a name="-store"></a>-ストア

CertUtil [オプション]-store [証明 [CertId [OutputFile]]]

証明書ストアのダンプ

証明: 証明書ストアの名前。 例:

- "My"、"CA" (既定値)、"Root"、
- "ldap:///CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? one? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の表示)
- "ldap:///CN=CAName,CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の変更)
- "ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services、CN = Services、CN = Configuration、DC = cpandl、DC = com? certificateRevocationList? base? objectClass = cRLDistributionPoint" (Crl の表示)
- "ldap:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (エンタープライズ CA 証明書)
- ldap: (AD コンピューターオブジェクトの証明書)
- -ユーザー ldap: (AD ユーザーオブジェクト証明書)

CertId: 証明書または CRL 一致トークン。  これには、シリアル番号、SHA-1 証明書、CRL、CTL または公開キーハッシュ、数値証明書インデックス (0、1など)、数値の CRL インデックス (.0、.1 など)、数値 CTL インデックス (.) を指定できます。0、..1など)、公開キー、署名、または拡張 ObjectId、証明書のサブジェクトの共通名、電子メールアドレス、UPN または DNS 名、キーコンテナー名または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーションポリシーの ObjectId、または CRL 発行者の共通名。 多くの場合、複数の一致が発生する可能性があります。

OutputFile: 一致する証明書を保存するファイル

コンピューターストアではなくユーザーストアにアクセスするには、-user を使用します。

-Enterprise を使用して、マシンのエンタープライズストアにアクセスします。

-Service を使用して、マシンサービスストアにアクセスします。

コンピューターグループポリシーストアにアクセスするには、-grouppolicy を使用します。

例:

- -エンタープライズ NTAuth
- -エンタープライズルート37
- -ユーザー My 26e0aaaf000000000004
- カナダ. 11

[-f][-enterprise][-ユーザー][-GroupPolicy][-silent][-split][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-addstore"></a>-addstore

CertUtil [オプション]-addstore 証明 InFile

証明書をストアに追加

証明: 証明書ストアの名前。  「 [-Store」を](#-store)参照してください。

InFile: ストアに追加する証明書または CRL ファイル。

[-f][-enterprise][-ユーザー][-GroupPolicy][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-delstore"></a>-delstore

CertUtil [オプション]-delstore 証明 CertId

ストアから証明書を削除

証明: 証明書ストアの名前。  「 [-Store」を](#-store)参照してください。

CertId: 証明書または CRL 一致トークン。  「 [-Store」を](#-store)参照してください。

[-enterprise][-ユーザー][-GroupPolicy][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-verifystore"></a>-verifystore

CertUtil [オプション]-verifystore 証明 [CertId]

ストアの証明書を確認する

証明: 証明書ストアの名前。  「 [-Store」を](#-store)参照してください。

CertId: 証明書または CRL 一致トークン。  「 [-Store」を](#-store)参照してください。

[-enterprise][-ユーザー][-GroupPolicy][-silent][-split][-dc DCName][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-repairstore"></a>-repairstore

CertUtil [オプション]-repairstore 証明 CertIdList [PropertyInfFile |SDDLSecurityDescriptor]

キーの関連付けを修復するか、証明書のプロパティまたはキーのセキュリティ記述子を更新します。

証明: 証明書ストアの名前。  「 [-Store」を](#-store)参照してください。

CertIdList: 証明書または CRL 一致トークンのコンマ区切りの一覧。 「 [-Store](#-store) CertId description」を参照してください。

PropertyInfFile--外部プロパティを含む INF ファイル:

```
[Properties]
     19 = Empty ; Add archived property, OR:
     19 =       ; Remove archived property

     11 = "{text}Friendly Name" ; Add friendly name property

     127 = "{hex}" ; Add custom hexadecimal property
         _continue_ = "00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f"
         _continue_ = "10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f"

     2 = "{text}" ; Add Key Provider Information property
       _continue_ = "Container=Container Name&"
       _continue_ = "Provider=Microsoft Strong Cryptographic Provider&"
       _continue_ = "ProviderType=1&"
       _continue_ = "Flags=0&"
       _continue_ = "KeySpec=2"

     9 = "{text}" ; Add Enhanced Key Usage property
       _continue_ = "1.3.6.1.5.5.7.3.2,"
       _continue_ = "1.3.6.1.5.5.7.3.1,"
```

[-f][-enterprise][-ユーザー][-GroupPolicy][-silent][-split][-csp プロバイダー]

[メニュー](#menu)に戻る

## <a name="-viewstore"></a>-viewstore

CertUtil [オプション]-viewstore [証明 [CertId [OutputFile]]]

証明書ストアのダンプ

証明: 証明書ストアの名前。 例:

- "My"、"CA" (既定値)、"Root"、
- "ldap:///CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? one? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の表示)
- "ldap:///CN=CAName,CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の変更)
- "ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services、CN = Services、CN = Configuration、DC = cpandl、DC = com? certificateRevocationList? base? objectClass = cRLDistributionPoint" (Crl の表示)
- "ldap:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (エンタープライズ CA 証明書)
- ldap: (AD コンピューターオブジェクトの証明書)
- -ユーザー ldap: (AD ユーザーオブジェクト証明書)

CertId: 証明書または CRL 一致トークン。 これには、シリアル番号、SHA-1 証明書、CRL、CTL または公開キーハッシュ、数値証明書インデックス (0、1など)、数値の CRL インデックス (.0、.1 など)、数値 CTL インデックス (.) を指定できます。0、..1など)、公開キー、署名、または拡張 ObjectId、証明書のサブジェクトの共通名、電子メールアドレス、UPN または DNS 名、キーコンテナー名または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーションポリシーの ObjectId、または CRL 発行者の共通名。 多くの場合、複数の一致が発生する可能性があります。

OutputFile: 一致する証明書を保存するファイル

コンピューターストアではなくユーザーストアにアクセスするには、-user を使用します。

-Enterprise を使用して、マシンのエンタープライズストアにアクセスします。

-Service を使用して、マシンサービスストアにアクセスします。

コンピューターグループポリシーストアにアクセスするには、-grouppolicy を使用します。

例:

1. -エンタープライズ NTAuth
2. -エンタープライズルート37
3. -ユーザー My 26e0aaaf000000000004
4. カナダ. 11

[-f][-enterprise][-ユーザー][-GroupPolicy][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-viewdelstore"></a>-viewdelstore

CertUtil [オプション]-viewdelstore [証明 [CertId [OutputFile]]]

ストアから証明書を削除

証明: 証明書ストアの名前。 例:

- "My"、"CA" (既定値)、"Root"、
- "ldap:///CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? one? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の表示)
- "ldap:///CN=CAName,CN=Certification オーソリティ, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (ルート証明書の変更)
- "ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services、CN = Services、CN = Configuration、DC = cpandl、DC = com? certificateRevocationList? base? objectClass = cRLDistributionPoint" (Crl の表示)
- "ldap:///CN=NTAuthCertificates,CN=Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com? Cacertificate を? base? objectClass = Microsoft-windows-certificationauthority" (エンタープライズ CA 証明書)
- ldap: (AD コンピューターオブジェクトの証明書)
- -ユーザー ldap: (AD ユーザーオブジェクト証明書)

CertId: 証明書または CRL 一致トークン。 これには、シリアル番号、SHA-1 証明書、CRL、CTL または公開キーハッシュ、数値証明書インデックス (0、1など)、数値の CRL インデックス (.0、.1 など)、数値 CTL インデックス (.) を指定できます。0、..1など)、公開キー、署名、または拡張 ObjectId、証明書のサブジェクトの共通名、電子メールアドレス、UPN または DNS 名、キーコンテナー名または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーションポリシーの ObjectId、または CRL 発行者の共通名。 多くの場合、複数の一致が発生する可能性があります。

OutputFile: 一致する証明書を保存するファイル

コンピューターストアではなくユーザーストアにアクセスするには、-user を使用します。

-Enterprise を使用して、マシンのエンタープライズストアにアクセスします。

-Service を使用して、マシンサービスストアにアクセスします。

コンピューターグループポリシーストアにアクセスするには、-grouppolicy を使用します。

例:

1. -エンタープライズ NTAuth
2. -エンタープライズルート37
3. -ユーザー My 26e0aaaf000000000004
4. カナダ. 11

[-f][-enterprise][-ユーザー][-GroupPolicy][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-dspublish"></a>-dsPublish

CertUtil [オプション]-dsPublish CertFile [NTAuthCA |RootCA |SubCA |CrossCA |KRA |ユーザー |装置

CertUtil [オプション]-dsPublish CRLFile [Dsc/Container [DSCDPCN]]

証明書または CRL を Active Directory に発行する

CertFile: 発行する証明書ファイル

NTAuthCA: DS Enterprise store に証明書を発行します

RootCA: 証明書を DS の信頼されたルートストアに発行する

SubCA: DS CA オブジェクトに CA 証明書を発行します。

CrossCA: クロス証明書を DS CA オブジェクトに発行する

KRA: 証明書を DS キー回復エージェントオブジェクトに発行します

ユーザー: ユーザー DS オブジェクトに証明書を発行します

コンピューター: 証明書をコンピューター DS オブジェクトに発行します

CRLFile: 発行する CRL ファイル

Dsc(コンテナー): DS CDP コンテナー CN、通常は CA マシン名

DSCDPCN: DS CDP オブジェクト CN。通常は、校正された CA の短い名前とキーのインデックスに基づいています。

DS オブジェクトを作成するには、-f を使用します。

[-f][-ユーザー][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-adtemplate"></a>-ADTemplate

CertUtil [オプション]-ADTemplate [テンプレート]

AD テンプレートの表示

[-f][-ユーザー][-ut][-mt][-dc DCName]

## <a name="-template"></a>-テンプレート

CertUtil [オプション]-テンプレート [テンプレート]

登録ポリシーテンプレートを表示する

[-f][-ユーザー][-silent][-PolicyServer URLOrId][-匿名][-Kerberos][-ClientCertificate ClientCertId][-ユーザー名ユーザー名][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-templatecas"></a>-TemplateCAs

CertUtil [オプション]-TemplateCAs テンプレート

テンプレートの Ca を表示する

[-f][-ユーザー][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-catemplates"></a>-CATemplates

CertUtil [オプション]-CATemplates [テンプレート]

CA のテンプレートを表示する

[-f][-ユーザー][-ut][-mt][-config Machine\CAName][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-setcasites"></a>-SetCASites

CertUtil [オプション]-SetCASites [set] [SiteName]

CertUtil [オプション]-SetCASites 確認する [SiteName]

CertUtil [オプション]-SetCASites 削除

CA サイト名の設定、検証、または削除

- -Config オプションを使用して単一の CA を対象にする (既定はすべての Ca)
- *SiteName*は、単一の CA を対象とする場合にのみ許可されます。
- -F を使用して、指定した*SiteName*の検証エラーを上書きします。
- すべての CA サイト名を削除するには-f を使用します

[-f][-config Machine\CAName][-dc DCName]

> [!NOTE]
> Active Directory Domain Services (AD DS) サイト認識用に Ca を構成する方法の詳細については、「 [AD CS および PKI クライアントのサイト認識の AD DS](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx)」を参照してください。

[メニュー](#menu)に戻る

## <a name="-enrollmentserverurl"></a>-enrollmentServerURL

CertUtil [オプション]-enrollmentServerURL [URL AuthenticationType [Priority] [修飾子]]

CertUtil [オプション]-enrollmentServerURL URL の削除

CA に関連付けられている登録サーバーの Url を表示、追加、または削除する

AuthenticationType: URL を追加するときに、次のいずれかのクライアント認証方法を指定します。

1. Kerberos: Kerberos SSL 資格情報を使用する
2. ユーザー名: SSL 資格情報に名前付きアカウントを使用する
3. ClientCertificate: x.509 証明書の SSL 資格情報を使用します。
4. 匿名: 匿名の SSL 資格情報を使用する

削除: CA に関連付けられている指定された URL を削除します。

Priority: URL を追加するときに指定しない場合、既定値は ' 1 ' になります。

[修飾子]--次の1つ以上のコンマ区切りのリスト。

1. AllowRenewalsOnly: この URL を使用してこの CA に送信できるのは更新要求のみです
2. Allowkeyベースの更新: AD に関連付けられているアカウントがない証明書を使用できます。 これは、ClientCertificate および AllowRenewalsOnly モードでのみ適用されます。

[-config Machine\CAName][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-adca"></a>-ADCA

CertUtil [オプション]-ADCA [CAName]

AD CAs を表示する

[-f][-split][-dc DCName]

[メニュー](#menu)に戻る

## <a name="-ca"></a>-CA

CertUtil [オプション]-CA [CAName |TemplateName

登録ポリシーの Ca を表示する

[-f][-ユーザー][-silent][-split][-PolicyServer URLOrId][-匿名][-Kerberos][-ClientCertificate ClientCertId][-ユーザー名ユーザー名][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-policy"></a>-ポリシー

登録ポリシーを表示する

[-f][-ユーザー][-silent][-split][-PolicyServer URLOrId][-匿名][-Kerberos][-ClientCertificate ClientCertId][-ユーザー名ユーザー名][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-policycache"></a>-PolicyCache

CertUtil [オプション]-PolicyCache [delete]

登録ポリシーのキャッシュエントリを表示または削除する

削除: ポリシーサーバーのキャッシュエントリを削除します。

-f: すべてのキャッシュエントリを削除するには、-f を使用します。

[-f][-ユーザー][-PolicyServer URLOrId]

[メニュー](#menu)に戻る

## <a name="-credstore"></a>-CredStore

CertUtil [オプション]-CredStore [URL]

CertUtil [オプション]-CredStore URL の追加

CertUtil [オプション]-CredStore の URL の削除

資格情報ストアのエントリを表示、追加、または削除する

URL: ターゲット URL。  すべてのエントリを一致させるには、\* を使用します。 URL プレフィックスと一致させるには、 https://machine\* を使用します。

追加: 資格情報ストアエントリを追加します。 SSL 資格情報も指定する必要があります。

削除: 資格情報ストアのエントリを削除します。

-f: エントリを上書きする場合、または複数のエントリを削除する場合は、-f を使用します。

[-f][-ユーザー][-silent][-匿名][-Kerberos][-ClientCertificate ClientCertId][-ユーザー名ユーザー名][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-installdefaulttemplates"></a>-InstallDefaultTemplates

CertUtil [オプション]-InstallDefaultTemplates

既定の証明書テンプレートをインストールする

[-dc DCName]

[メニュー](#menu)に戻る

## <a name="-urlcache"></a>-URLCache

CertUtil [オプション]-URLCache [URL |CRL |\* [delete]]

URL キャッシュエントリを表示または削除する

URL: キャッシュされた URL

CRL: すべてのキャッシュされた CRL Url のみを操作します

\*: キャッシュされたすべての Url を操作します

削除: 現在のユーザーのローカルキャッシュから関連する Url を削除します。

特定の URL を強制的にフェッチしてキャッシュを更新するには、-f を使用します。

[-f][-split]

[メニュー](#menu)に戻る

## <a name="-pulse"></a>-pulse

CertUtil [オプション]-pulse

パルス自動登録イベント

[-ユーザー]

[メニュー](#menu)に戻る

## <a name="-machineinfo"></a>-MachineInfo

CertUtil [オプション]-MachineInfo DomainName\MachineName $

Active Directory コンピューターオブジェクトの情報を表示する

[メニュー](#menu)に戻る

## <a name="-dcinfo"></a>-DCInfo

CertUtil [オプション]-DCInfo [ドメイン] [Verify |DeleteBad |DeleteAll

ドメインコントローラー情報を表示する

既定では、確認なしで DC 証明書が表示されます

[-f][-ユーザー][-urlfetch][-dc DCName][-t タイムアウト]

> [!TIP]
> Active Directory Domain Services (AD DS) ドメイン **[ドメイン]** を指定し、ドメインコントローラー ( **-dc**) を指定する機能は、Windows Server 2012 で追加されました。 コマンドを正常に実行するには、 **Domain admins**または**Enterprise admins**のメンバーであるアカウントを使用する必要があります。 このコマンドの動作変更は次のとおりです。</br>> 1 です。  ドメインが指定されておらず、特定のドメインコントローラーが指定されていない場合、このオプションは、既定のドメインコントローラーから処理するドメインコントローラーの一覧を返します。</br>> 2  ドメインが指定されておらず、ドメインコントローラーが指定されている場合は、指定されたドメインコントローラー上の証明書のレポートが生成されます。</br>> 3。  ドメインが指定されていても、ドメインコントローラーが指定されていない場合は、一覧の各ドメインコントローラーの証明書について、ドメインコントローラーの一覧が生成されます。</br>> 4。  ドメインとドメインコントローラーが指定されている場合は、ドメインコントローラーの一覧が対象のドメインコントローラーから生成されます。 一覧内の各ドメインコントローラーの証明書のレポートも生成されます。

たとえば、cpandl-DC1 という名前のドメインコントローラーを持つ CPANDL という名前のドメインがあるとします。 次のコマンドを実行して、CPANDL.-DC1: certutil-dc cpandl.-dc1-dcinfo cpandl. から、ドメインコントローラーとその証明書の一覧を取得することができます。

[メニュー](#menu)に戻る

## <a name="-entinfo"></a>-EntInfo

CertUtil [オプション]-EntInfo DomainName\MachineName $

[-f][-ユーザー]

[メニュー](#menu)に戻る

## <a name="-tcainfo"></a>-TCAInfo

CertUtil [オプション]-TCAInfo [DomainDN |-]

CA 情報を表示する

[-f][-enterprise][-ユーザー][-urlfetch][-dc DCName][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-scinfo"></a>-SCInfo

CertUtil [オプション]-SCInfo [CRYPT_DELETEKEYSET]]

スマートカードの情報を表示する

CRYPT_DELETEKEYSET: スマートカードのすべてのキーを削除します。

[-silent][-split][-urlfetch][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-scroots"></a>-SCRoots

CertUtil [オプション]-SCRoots update [+] [InputRootFile] [ReaderName]

CertUtil [オプション]-SCRoots \@OutputRootFile [ReaderName]

CertUtil [オプション]-SCRoots ビュー [InputRootFile |ReaderName]

CertUtil [オプション]-SCRoots delete [ReaderName]

スマートカードのルート証明書の管理

[-f][-split][-p パスワード]

[メニュー](#menu)に戻る

## <a name="-verifykeys"></a>-verifykeys

CertUtil [オプション]-verifykeys [KeyContainerName CACertFile]

公開/秘密キーセットの確認

KeyContainerName: 検証するキーのキーコンテナー名。 既定値はマシンキーです。  ユーザーキーには-user を使用します。

CACertFile: 署名または暗号化証明書ファイル

引数を指定しない場合は、各署名 CA 証明書が秘密キーに対して検証されます。

この操作は、ローカルの CA またはローカルキーに対してのみ実行できます。

[-f][-ユーザー][-silent][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-verify"></a>-verify

CertUtil [オプション]-検証 CertFile [ApplicationPolicyList |-[IssuancePolicyList]]

CertUtil [オプション]-CertFile を検証する [CACertFile [CrossedCACertFile]]

CertUtil [オプション]-CRLFile CACertFile を確認する [IssuedCertFile]

CertUtil [オプション]-CRLFile CACertFile を確認する [DeltaCRLFile]

証明書、CRL、またはチェーンの検証

CertFile: 検証する証明書

ApplicationPolicyList: 必要なアプリケーションポリシー ObjectIds のコンマ区切りのリスト (省略可能)

IssuancePolicyList: 省略可能。必須の発行ポリシー ObjectIds のコンマ区切りの一覧です。

CACertFile: オプションで検証する発行元 CA 証明書

CrossedCACertFile: 省略可能な証明書 (CertFile によるクロス認定)

CRLFile: 検証する CRL

IssuedCertFile: 省略可能な発行済み証明書 (CRLFile)

DeltaCRLFile: オプションの delta CRL

ApplicationPolicyList が指定されている場合、チェーン構築は、指定されたアプリケーションポリシーに対して有効なチェーンに制限されます。

IssuancePolicyList を指定した場合、チェーン構築は、指定された発行ポリシーに対して有効なチェーンに制限されます。

CACertFile が指定されている場合、CACertFile のフィールドは CertFile または CRLFile に対して検証されます。

CACertFile が指定されていない場合、完全なチェーンを構築および検証するために CertFile が使用されます。

CACertFile と CrossedCACertFile の両方が指定されている場合、CACertFile と CrossedCACertFile のフィールドは CertFile に対して検証されます。

IssuedCertFile を指定した場合、IssuedCertFile 内のフィールドは CRLFile に対して検証されます。

DeltaCRLFile を指定した場合、DeltaCRLFile 内のフィールドは CRLFile に対して検証されます。

[-f][-enterprise][-ユーザー][-silent][-split][-urlfetch][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-verifyctl"></a>-verifyCTL

CertUtil [オプション]-verifyCTL CTLObject [CertDir] [CertFile]

AuthRoot または許可されていない証明書の CTL を確認する

CTLObject: 検証する CTL を識別します。

- AuthRootWU: AuthRoot CAB と一致する証明書を URL キャッシュから読み取ります。 代わりに、-f を使用して Windows Update からダウンロードしてください。
- DisallowedWU: 許可されていない証明書の CAB と、URL キャッシュからの許可されていない証明書ストアファイルを読み取ります。  代わりに、-f を使用して Windows Update からダウンロードしてください。
- AuthRoot: レジストリのキャッシュされた AuthRoot CTL を読み取ります。  -F と、既に信頼されていない CertFile を使用して、レジストリキャッシュされた AuthRoot および許可されていない証明書 Ctl を強制的に更新します。
- 許可されていません: 読み取りレジストリのキャッシュされていない証明書の CTL。 -f は、AuthRoot と同じ動作をします。
- CTLFileName: file または http: CTL または CAB へのパス

CertDir: CTL エントリと一致する証明書を含むフォルダー。 Http: フォルダーのパスは、パスの区切り記号で終わる必要があります。 フォルダーが AuthRoot と共に指定されていない場合、または禁止されている場合は、一致する証明書 (ローカル証明書ストア、crypt32.dll リソース、およびローカル URL キャッシュ) に対して複数の場所が検索されます。 必要に応じて、-f を使用して Windows Update からダウンロードします。 それ以外の場合、既定では、CTLObject と同じフォルダーまたは web サイトになります。

CertFile: 検証する証明書を含むファイル。 証明書は CTL エントリと照合され、一致した結果が表示されます。 ほとんどの既定の出力を抑制します。

[-f][-ユーザー][-split]

[メニュー](#menu)に戻る

## <a name="-sign"></a>-sign

CertUtil [オプション]-署名 InFileList |シリアルの |CRL OutFileList [StartDate + dd: hh] [+ SerialNumberList |-SerialNumberList |-ObjectIdList | \@ExtensionFile]

CertUtil [オプション]-署名 InFileList |シリアルの |CRL OutFileList [#HashAlgorithm] [+ AlternateSignatureAlgorithm | AlternateSignatureAlgorithm]

CRL または証明書に再署名する

InFileList: 変更および再署名する証明書または CRL ファイルのコンマ区切りの一覧

シリアル値: 作成する証明書のシリアル番号。 有効期間とその他のオプションを指定することはできません。

CRL: 空の CRL を作成します。 有効期間とその他のオプションを指定することはできません。

OutFileList: 変更された証明書または CRL 出力ファイルのコンマ区切りの一覧。 ファイルの数は、InFileList と一致している必要があります。

StartDate + dd: hh: 新しい有効期間: 省略可能な日付 +オプションの日付と時間の有効期間。両方が指定されている場合は、正符号 (+) 区切り記号を使用します。 現在の時刻から開始するには、"now [+ dd: hh]" を使用します。 有効期限を設定しない場合は、"never" を使用します (Crl の場合のみ)。

SerialNumberList: コンマ区切りのシリアル番号リストを追加または削除します。

ObjectIdList: コンマ区切りの拡張 ObjectId リストを削除します。

\@ExtensionFile: 更新または削除する拡張子を含む INF ファイル:

```
[Extensions]
     2.5.29.31 = ; Remove CRL Distribution Points extension
     2.5.29.15 = "{hex}" ; Update Key Usage extension
     _continue_="03 02 01 86"
```

HashAlgorithm: # 記号を前に付けたハッシュアルゴリズムの名前

AlternateSignatureAlgorithm: 代替署名アルゴリズム指定子

マイナス記号を付けると、シリアル番号と拡張機能が削除されます。 プラス記号を使用すると、シリアル番号が CRL に追加されます。 CRL から項目を削除する場合、一覧にはシリアル番号と ObjectIds の両方が含まれる場合があります。 AlternateSignatureAlgorithm の前にマイナス記号を付けると、従来の署名形式が使用されます。 AlternateSignatureAlgorithm の前にプラス記号を付けると、alternature signature 形式が使用されます。 AlternateSignatureAlgorithm が指定されていない場合は、証明書または CRL の署名形式が使用されます。

[-nullsign][-f][-silent][-Cert CertId]

[メニュー](#menu)に戻る

## <a name="-vroot"></a>-vroot

CertUtil [オプション]-vroot [delete]

Web 仮想ルートとファイル共有の作成/削除

[メニュー](#menu)に戻る

## <a name="-vocsproot"></a>-vocsproot

CertUtil [オプション]-vocsproot [delete]

OCSP web プロキシの web 仮想ルートを作成または削除する

[メニュー](#menu)に戻る

## <a name="-addenrollmentserver"></a>-addEnrollmentServer

CertUtil [オプション]-addEnrollmentServer Kerberos |UserName |ClientCertificate [AllowRenewalsOnly] [Allowkeyby 更新]

登録サーバーアプリケーションの追加

必要に応じて、指定した CA の登録サーバーアプリケーションとアプリケーションプールを追加します。 このコマンドでは、バイナリまたはパッケージはインストールされません。 次のいずれかの認証方法を使用して、クライアントが証明書登録サーバーに接続します。

- Kerberos: Kerberos SSL 資格情報を使用する
- ユーザー名: SSL 資格情報に名前付きアカウントを使用する
- ClientCertificate: x.509 証明書の SSL 資格情報を使用します。
- AllowRenewalsOnly: この URL を使用してこの CA に送信できるのは更新要求のみです
- Allowkey: 書き換え--AD にアカウントが関連付けられていない証明書を使用できるようにします。 これは、ClientCertificate および AllowRenewalsOnly モードでのみ適用されます。

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-deleteenrollmentserver"></a>-deleteEnrollmentServer

CertUtil [オプション]-deleteEnrollmentServer Kerberos |UserName |ClientCertificate

登録サーバーアプリケーションの削除

必要に応じて、指定した CA の登録サーバーアプリケーションとアプリケーションプールを削除します。 このコマンドでは、バイナリやパッケージは削除されません。 次のいずれかの認証方法を使用して、クライアントが証明書登録サーバーに接続します。

1. Kerberos: Kerberos SSL 資格情報を使用する
2. ユーザー名: SSL 資格情報に名前付きアカウントを使用する
3. ClientCertificate: x.509 証明書の SSL 資格情報を使用します。

[-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-addpolicyserver"></a>-addPolicyServer

CertUtil [オプション]-addPolicyServer Kerberos |UserName |ClientCertificate [キーベースの更新]

ポリシーサーバーアプリケーションの追加

必要に応じて、ポリシーサーバーアプリケーションとアプリケーションプールを追加します。 このコマンドでは、バイナリまたはパッケージはインストールされません。 次のいずれかの認証方法で、クライアントが証明書ポリシーサーバーに接続します。

- Kerberos: Kerberos SSL 資格情報を使用する
- ユーザー名: SSL 資格情報に名前付きアカウントを使用する
- ClientCertificate: x.509 証明書の SSL 資格情報を使用します。
- キーベースの更新: キーベースの更新テンプレートを含むポリシーのみがクライアントに返されます。 このフラグは、ユーザー名と ClientCertificate 認証にのみ適用されます。

[メニュー](#menu)に戻る

## <a name="-deletepolicyserver"></a>-deletePolicyServer

CertUtil [オプション]-deletePolicyServer Kerberos |UserName |ClientCertificate [キーベースの更新]

ポリシーサーバーアプリケーションの削除

必要に応じて、ポリシーサーバーアプリケーションとアプリケーションプールを削除します。 このコマンドでは、バイナリやパッケージは削除されません。 次のいずれかの認証方法で、クライアントが証明書ポリシーサーバーに接続します。

1. Kerberos: Kerberos SSL 資格情報を使用する
2. ユーザー名: SSL 資格情報に名前付きアカウントを使用する
3. ClientCertificate: x.509 証明書の SSL 資格情報を使用します。
4. キーベースの更新: キーベースの更新ポリシーサーバー

[メニュー](#menu)に戻る

## <a name="-oid"></a>-oid

CertUtil [オプション]-oid ObjectId [DisplayName | delete [LanguageId [Type]]]

CertUtil [オプション]-oid GroupId

CertUtil [オプション]-oid AlgId |AlgorithmName [GroupId]

ObjectId を表示するか、表示名を設定します

- ObjectId--表示名を表示または追加するための ObjectId
- GroupId--列挙する ObjectIds の10進数の GroupId 番号
- AlgId--ObjectId が検索する16進数の AlgId
- AlgorithmName--検索する ObjectId のアルゴリズム名
- DisplayName--DS に格納する表示名
- 削除--表示名の削除
- LanguageId--言語 Id (既定値は 1033)
- 次のように入力します。作成するオブジェクトの種類は、テンプレートの場合は 1 (既定)、発行ポリシーの場合は2、アプリケーションポリシーの場合は3です。
- DS オブジェクトを作成するには、-f を使用します。

[-f]

[メニュー](#menu)に戻る

## <a name="-error"></a>-エラー

CertUtil [オプション]-エラー ErrorCode

エラーコードメッセージテキストを表示します

[メニュー](#menu)に戻る

## <a name="-getreg"></a>-getreg

CertUtil [オプション]-getreg [{ca | restore | policy | exit | template | enroll | chain |PolicyServers}\[ProgId\]] [RegistryValueName]

レジストリ値の表示

ca: CA のレジストリキーを使用する

復元: CA の復元レジストリキーを使用します。

ポリシー: ポリシーモジュールのレジストリキーを使用します。

終了: 最初の終了モジュールのレジストリキーを使用します

テンプレート: テンプレートレジストリキーを使用します (ユーザーテンプレートにユーザーを使用します)

登録: 登録レジストリキーを使用します (ユーザーコンテキストにユーザーを使用します)

チェーン: チェーン構成のレジストリキーを使用する

PolicyServers: ポリシーサーバーのレジストリキーを使用します。

ProgId: ポリシーまたは終了モジュールの ProgId (レジストリサブキー名) を使用します。

RegistryValueName: レジストリ値の名前 (プレフィックスと一致するには "Name\*" を使用します)

値: 新しい数値、文字列、または日付のレジストリ値またはファイル名。 数値が "+" または "-" で始まる場合は、新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

文字列値が "+" または "-" で始まっていて、既存の値が REG_MULTI_SZ 値の場合は、既存のレジストリ値に対して文字列が追加または削除されます。 REG_MULTI_SZ 値を強制的に作成するには、文字列値の末尾に "\n" を追加します。

値が "\@" で始まる場合、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルを参照していない場合は、代わりに [Date] [+ |-] [dd: hh]--省略可能な日付またはマイナス (省略可能) として解析されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 現在の時刻を基準とした日付には、"now + dd: hh" を使用します。

キャッシュされた Crl を効果的にフラッシュするには、"chain\ChainCacheResyncFiletime \@now" を使用します。

[-f][-ユーザー][-GroupPolicy][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-setreg"></a>-setreg

CertUtil [オプション]-setreg [{ca | restore | policy | exit | template | enroll | chain |PolicyServers}\[ProgId\]] RegistryValueName 値

レジストリ値の設定

ca: CA のレジストリキーを使用する

復元: CA の復元レジストリキーを使用します。

ポリシー: ポリシーモジュールのレジストリキーを使用します。

終了: 最初の終了モジュールのレジストリキーを使用します

テンプレート: テンプレートレジストリキーを使用します (ユーザーテンプレートにユーザーを使用します)

登録: 登録レジストリキーを使用します (ユーザーコンテキストにユーザーを使用します)

チェーン: チェーン構成のレジストリキーを使用する

PolicyServers: ポリシーサーバーのレジストリキーを使用します。

ProgId: ポリシーまたは終了モジュールの ProgId (レジストリサブキー名) を使用します。

RegistryValueName: レジストリ値の名前 (プレフィックスと一致するには "Name\*" を使用します)

値: 新しい数値、文字列、または日付のレジストリ値またはファイル名。 数値が "+" または "-" で始まる場合は、新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

文字列値が "+" または "-" で始まっていて、既存の値が REG_MULTI_SZ 値の場合は、既存のレジストリ値に対して文字列が追加または削除されます。 REG_MULTI_SZ 値を強制的に作成するには、文字列値の末尾に "\n" を追加します。

値が "\@" で始まる場合、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルを参照していない場合は、代わりに [Date] [+ |-] [dd: hh]--省略可能な日付またはマイナス (省略可能) として解析されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 現在の時刻を基準とした日付には、"now + dd: hh" を使用します。

キャッシュされた Crl を効果的にフラッシュするには、"chain\ChainCacheResyncFiletime \@now" を使用します。

[-f][-ユーザー][-GroupPolicy][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-delreg"></a>-delreg

CertUtil [オプション]-delreg [{ca | restore | policy | exit | template | enroll | chain |PolicyServers}\[ProgId\]] [RegistryValueName]

レジストリ値の削除

ca: CA のレジストリキーを使用する

復元: CA の復元レジストリキーを使用します。

ポリシー: ポリシーモジュールのレジストリキーを使用します。

終了: 最初の終了モジュールのレジストリキーを使用します

テンプレート: テンプレートレジストリキーを使用します (ユーザーテンプレートにユーザーを使用します)

登録: 登録レジストリキーを使用します (ユーザーコンテキストにユーザーを使用します)

チェーン: チェーン構成のレジストリキーを使用する

PolicyServers: ポリシーサーバーのレジストリキーを使用します。

ProgId: ポリシーまたは終了モジュールの ProgId (レジストリサブキー名) を使用します。

RegistryValueName: レジストリ値の名前 (プレフィックスと一致するには "Name\*" を使用します)

値: 新しい数値、文字列、または日付のレジストリ値またはファイル名。 数値が "+" または "-" で始まる場合は、新しい値に指定されたビットが既存のレジストリ値で設定またはクリアされます。

文字列値が "+" または "-" で始まっていて、既存の値が REG_MULTI_SZ 値の場合は、既存のレジストリ値に対して文字列が追加または削除されます。 REG_MULTI_SZ 値を強制的に作成するには、文字列値の末尾に "\n" を追加します。

値が "\@" で始まる場合、値の残りの部分は、バイナリ値の16進数のテキスト表現を含むファイルの名前になります。 有効なファイルを参照していない場合は、代わりに [Date] [+ |-] [dd: hh]--省略可能な日付またはマイナス (省略可能) として解析されます。 両方が指定されている場合は、正符号 (+) または負符号 (-) の区切り記号を使用します。 現在の時刻を基準とした日付には、"now + dd: hh" を使用します。

キャッシュされた Crl を効果的にフラッシュするには、"chain\ChainCacheResyncFiletime \@now" を使用します。

[-f][-ユーザー][-GroupPolicy][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-importkms"></a>-ImportKMS

CertUtil [オプション]-ImportKMS UserKeyAndCertFile [CertId]

キーのアーカイブ用にユーザーキーと証明書をサーバーデータベースにインポートする

UserKeyAndCertFile--アーカイブされるユーザーの秘密キーと証明書を含むデータファイル。  次のいずれかを指定できます。

- Exchange キー管理サーバー (KMS) エクスポートファイル
- PFX ファイル

CertId: KMS エクスポートファイルの暗号化解除証明書の一致トークン。  「 [-Store」を](#-store)参照してください。

CA によって発行されていない証明書をインポートするには、-f を使用します。

[-f][-silent][-split][-config Machine\CAName][-p パスワード][-symkeyalg SymmetricKeyAlgorithm [, KeyLength]]

[メニュー](#menu)に戻る

## <a name="-importcert"></a>-ImportCert

CertUtil [オプション]-ImportCert Certfile [ExistingRow]

証明書ファイルをデータベースにインポートする

同じキーに対して保留中の要求の代わりに証明書をインポートするには、ExistingRow を使用します。

CA によって発行されていない証明書をインポートするには、-f を使用します。

CA は、外部証明書のインポートをサポートするように構成する必要がある場合もあります。 certutil-setreg ca\KRAFlags + KRAF_ENABLEFOREIGN

[-f][-config Machine\CAName]

[メニュー](#menu)に戻る

## <a name="-getkey"></a>-GetKey

CertUtil [オプション]-GetKey SearchToken [RecoveryBlobOutFile]

CertUtil [オプション]-GetKey SearchToken スクリプト OutputScriptFile

CertUtil [オプション]-GetKey SearchToken の取得 |OutputFileBaseName の回復

アーカイブされた秘密キーの回復 blob の取得、回復スクリプトの生成、またはアーカイブされたキーの回復

スクリプト: キーを取得して回復するスクリプトを生成します (複数の一致する回復候補が検出された場合、または出力ファイルが指定されていない場合は既定の動作)。

取得: 1 つまたは複数のキー回復 Blob を取得します (同じ回復候補が1つだけ見つかった場合は既定の動作、出力ファイルが指定されている場合は)

回復: 1 回の手順で秘密キーを取得して回復します (キー回復エージェントの証明書と秘密キーが必要です)

SearchToken: 回復するキーと証明書を選択するために使用します。

次のいずれかを指定できます。

1. 証明書の共通名
2. 証明書のシリアル番号
3. 証明書 SHA-1 ハッシュ (拇印)
4. 証明書キー Id SHA-1 ハッシュ (サブジェクトキー識別子)
5. 要求者名 (ドメイン \ ユーザー)
6. UPN (ユーザー\@ドメイン)

RecoveryBlobOutFile: 証明書チェーンと関連付けられた秘密キーを含む出力ファイルで、1つまたは複数のキー回復エージェントの証明書に対して暗号化されたままです。

OutputScriptFile: 秘密キーの取得と復旧を行うバッチスクリプトを含む出力ファイル。

OutputFileBaseName: 出力ファイルのベース名。 取得の場合、すべての拡張機能が切り捨てられ、証明書固有の文字列と、各キー回復 blob に対して拡張子が追加されます。  各ファイルには、証明書チェーンと関連付けられている秘密キーが含まれ、1つまたは複数のキー回復エージェントの証明書に対して引き続き暗号化されます。 回復の場合、すべての拡張機能が切り捨てられ、. p12 拡張子が追加されます。  回復した証明書チェーンと、PFX ファイルとして格納されている関連する秘密キーが含まれます。

[-f][-UnicodeText][-silent][-config Machine\CAName][-p パスワード][-ProtectTo SAMNameAndSIDList][-csp プロバイダー]

[メニュー](#menu)に戻る

## <a name="-recoverkey"></a>-回復キー

CertUtil [オプション]-回復キー RecoveryBlobInFile [PFXOutFile [受信者インデックス]]

アーカイブされた秘密キーの回復

[-f][-ユーザー][-silent][-split][-p パスワード][-ProtectTo SAMNameAndSIDList][-csp プロバイダー][-t タイムアウト]

[メニュー](#menu)に戻る

## <a name="-mergepfx"></a>-MergePFX

CertUtil [オプション]-MergePFX PFXInFileList PFXOutFile [ExtendedProperties]

PFXInFileList: コンマ区切りの PFX 入力ファイルリスト

PFXOutFile: PFX 出力ファイル

ExtendedProperties: 拡張プロパティを含める

コマンドラインで指定したパスワードは、コンマで区切られたパスワードの一覧です。  複数のパスワードを指定した場合は、最後のパスワードが出力ファイルに使用されます。  パスワードが1つしか指定されていない場合、または最後のパスワードが "\*" の場合、ユーザーは出力ファイルのパスワードの入力を求められます。

[-f][-ユーザー][-split][-p パスワード][-ProtectTo SAMNameAndSIDList][-csp プロバイダー]

[メニュー](#menu)に戻る

## <a name="-convertepf"></a>-収束 Tepf

CertUtil [オプション]-収束 Tepf PFXInFileList EPFOutFile [cast | cast-] [V3CACertId] [, Salt]

PFX ファイルを EPF ファイルに変換する

PFXInFileList: コンマ区切りの PFX 入力ファイルリスト

EPF: EPF 出力ファイル

cast: CAST 64 encryption を使用します。

cast-: CAST 64 encryption (export) を使用します。

V3CACertId: V3 CA 証明書の一致トークン。  「 [-Store](#-store) CertId description」を参照してください。

Salt: EPF 出力ファイル salt 文字列

コマンドラインで指定したパスワードは、コンマで区切られたパスワードの一覧です。 複数のパスワードを指定した場合は、最後のパスワードが出力ファイルに使用されます。  パスワードが1つしか指定されていない場合、または最後のパスワードが "\*" の場合、ユーザーは出力ファイルのパスワードの入力を求められます。

[-f][-silent][-split][-dc DCName][-p パスワード][-csp プロバイダー]

[メニュー](#menu)に戻る

## <a name="options"></a>オプション

このセクションでは、コマンドで指定できるオプションを定義します。

|オプション|説明|
|-------|-----------|
|-nullsign|データのハッシュを署名として使用する|
|-f|強制的に上書きする|
|-enterprise|ローカルコンピューターのエンタープライズレジストリ証明書ストアを使用する|
|-ユーザー|HKEY_CURRENT_USER キーまたは証明書ストアを使用する|
|-GroupPolicy|グループポリシー証明書ストアを使用する|
|-ut|ユーザーテンプレートの表示|
|-mt|コンピューターテンプレートを表示する|
|-Unicode|Unicode でリダイレクトされた出力を書き込む|
|-UnicodeText|出力ファイルを Unicode で書き込む|
|-gmt|時刻を GMT として表示します|
|-秒|秒とミリ秒を使用して時刻を表示する|
|-サイレント|サイレントフラグを使用して crypt コンテキストを取得する|
|-分割|埋め込みの asn.1 要素を分割し、ファイルに保存する|
|-v|詳細操作|
|-privatekey|パスワードと秘密キーのデータを表示する|
|-pin のピン留め|スマートカードの PIN|
|-urlfetch|AIA 証明書と CDP Crl を取得して検証する|
|-config Machine\CAName|CA とコンピューター名の文字列|
|-PolicyServer URLOrId|ポリシーサーバーの URL または Id。選択 U/I の場合は、-PolicyServer を使用します。 すべてのポリシーサーバーで、-PolicyServer \* を使用します。|
|-匿名|匿名の SSL 資格情報を使用する|
|-Kerberos|Kerberos SSL 資格情報を使用する|
|-ClientCertificate ClientCertId|X.509 証明書の SSL 資格情報を使用します。 選択 U/I の場合は、-clientCertificate を使用します。|
|-ユーザー名|SSL 資格情報には名前付きアカウントを使用します。 選択 U/I の場合は、-UserName を使用します。|
|-Cert CertId|署名用の証明書|
|-dc DCName|特定のドメインコントローラーをターゲットにする|
|-RestrictionList を制限する|コンマ区切りの制限リスト。 各制限は、列名、関係演算子、および定数整数、文字列、または日付で構成されます。 並べ替え順序を示すには、1つの列名の前にプラスまたはマイナス記号を付けることができます。 例:</br>"RequestId = 47"</br>"+ RequesterName > = a, RequesterName < b"</br>"-RequesterName > ドメイン、ディスポジション = 21"|
|-out ColumnList|コンマ区切りの列リスト|
|-p パスワード|パスワード|
|-ProtectTo SAMNameAndSIDList|SAM 名/SID リストをコンマで区切って指定します。|
|-csp プロバイダー|プロバイダー|
|-t タイムアウト|URL フェッチのタイムアウト (ミリ秒)|
|-symkeyalg SymmetricKeyAlgorithm [, KeyLength]|オプションのキー長を持つ対称キーアルゴリズムの名前 (例: AES、128、または 3DES)|

[メニュー](#menu)に戻る

## <a name="additional-certutil-examples"></a>その他の certutil の例

このコマンドの使用方法の例については、「」を参照してください。

1. [コマンドラインから Active Directory 証明書サービス (AD CS) を管理するための Certutil の例](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)
2. [証明書を管理するための Certutil タスク](https://technet.microsoft.com/library/cc772898.aspx)
3. [CertUtil コマンドラインツールチュートリアルを使用したバイナリ要求のエクスポート](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)
4. [ルート CA 証明書の書き換え](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)
5. [Certutil](https://msdn.microsoft.com/subscriptions/cc773087.aspx)

[メニュー](#menu)に戻る
