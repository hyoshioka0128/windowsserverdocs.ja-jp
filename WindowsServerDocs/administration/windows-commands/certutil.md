---
title: certutil
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8248f5ae540866394169229f0d7cf11497c9dcf2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834723"
---
# <a name="certutil"></a>certutil



Certutil.exe は、証明書サービスの一部としてインストールされているコマンド ライン プログラムです。 Certutil.exe を使用して、ダンプ、証明機関 (CA) の構成情報を表示し、証明書サービスを構成するバックアップし復元 CA コンポーネント、および証明書、キーのペアと証明書チェーンを確認します。

追加のパラメーターを指定せず、証明機関で certutil を実行すると、現在の証明機関の構成が表示されます。 Cerutil が実行される非証明機関でのコマンドは、既定値は、certutil を実行している[-ダンプ](#BKMK_dump)動詞。

> [!WARNING]
> Certutil の以前のバージョンでは、一部がこのドキュメントで説明されているオプションの使用可能性がありますできません。 Certutil の特定のバージョンの提供に示すようにコマンドを実行しているすべてのオプションを表示、[構文表記](#BKMK_notations)セクション。

## <a name="BKMK_menu"></a>メニュー

このドキュメントで主要なセクションでは、次のとおりです。
-   [動詞](#BKMK_Verbs)
-   [構文の表記](#BKMK_notations)
-   [[オプション](#BKMK_Options)]
-   [Certutil の他の例](#BKMK_AddedExamples)

## <a name="BKMK_Verbs"></a>動詞

次の表では、certutil コマンドで使用できる動詞について説明します。

|[動詞]|説明|
|-----|-----------|
|[-ダンプ](#BKMK_dump)|ダンプの構成情報やファイル|
|[-asn](#BKMK_asn)|ASN.1 ファイルを解析します。|
|[-decodehex](#BKMK_decodehex)|16 進数でエンコードされたファイルをデコードします。|
|[デコード](#BKMK_decode)|Base64 でエンコードされたファイルをデコードします。|
|[-エンコード](#BKMK_encode)|ファイルを Base64 をエンコードします。|
|[-拒否](#BKMK_deny)|保留中の証明書の要求を拒否します。|
|[-再送信](#BKMK_resubmit)|保留中の証明書の要求を再送信します。|
|[-setattributes](#BKMK_setattributes)|保留中の証明書の要求の属性を設定します。|
|[-setextension](#BKMK_setextension)|保留中の証明書の要求の拡張機能を設定します。|
|[-revoke](#BKMK_revoke)|証明書の失効|
|[-isvalid](#BKMK_isvalid)|現在の証明書のディス ポジションを表示します。|
|[-getconfig](#BKMK_getconfig)|既定の構成文字列を取得します。|
|[-ping](#BKMK_ping)|Active Directory 証明書サービスの要求インターフェイスにお問い合わせくださいしようとしてください。|
|-pingadmin|Active Directory 証明書サービスの管理者インターフェイスにお問い合わせくださいしようとしてください。|
|[-Cainfo](#BKMK_CAInfo)|証明機関に関する情報を表示します。|
|[-ca.cert](#BKMK_ca.cert)|証明機関の証明書を取得します。|
|[-ca.chain](#BKMK_ca.chain)|証明機関の証明書チェーンを取得します。|
|[-GetCRL](#BKMK_GetCRL)|証明書失効リスト (CRL) を取得します。|
|[-CRL](#BKMK_CRL)|新しい証明書失効リスト (Crl) または delta Crl のみ] を発行します。|
|[-shutdown](#BKMK_shutdown)|Active Directory 証明書サービスをシャット ダウン|
|[-installCert](#BKMK_installcert)|証明機関の証明書をインストールします。|
|[-renewCert](#BKMK_renewcert)|証明機関の証明書を更新します。|
|[-schema](#BKMK_schema)|証明書のスキーマをダンプします。|
|[ビュー](#BKMK_view)|証明書の表示をダンプします。|
|[-db](#BKMK_db)|生のデータベースをダンプします。|
|[-deleterow](#BKMK_deleterow)|サーバーのデータベースから行を削除します。|
|[-backup](#BKMK_backup)|バックアップの Active Directory 証明書サービス|
|[-backupDB](#BKMK_backupDB)|Active Directory Certificate Services データベースをバックアップします。|
|[-backupKey](#BKMK_backupKey)|Active Directory 証明書サービスの証明書と秘密キーをバックアップします。|
|[-restore](#BKMK_restore)|Active Directory 証明書サービスを復元します。|
|[-restoreDB](#BKMK_restoreDB)|Active Directory Certificate Services データベースを復元します。|
|[-restoreKey](#BKMK_restorekey)|Active Directory 証明書サービスの証明書と秘密キーを復元します。|
|[-importPFX](#BKMK_importPFX)|証明書のインポートと秘密キー|
|[-dynamicfilelist](#BKMK_dynamicfilelist)|動的ファイルの一覧を表示します。|
|[-databaselocations](#BKMK_databaselocations)|データベースの場所を表示します。|
|[-hashfile](#BKMK_hashfile)|生成およびファイルの暗号化ハッシュを表示します。|
|[-store](#BKMK_Store)|証明書ストアをダンプします。|
|[-addstore](#BKMK_addstore)|ストアに証明書を追加します。|
|[-delstore](#BKMK_delstore)|ストアから証明書を削除します。|
|[-verifystore](#BKMK_verifystore)|ストアに証明書を確認します。|
|[-repairstore](#BKMK_repairstore)|キーの関連付けを修復または証明書のプロパティまたはキーのセキュリティ記述子の更新|
|[-viewstore](#BKMK_viewstore)|証明書ストアをダンプします。|
|[-viewdelstore](#BKMK_viewdelstore)|ストアから証明書を削除します。|
|[-dsPublish](#BKMK_dsPublish)|証明書または証明書失効リスト (CRL) を Active Directory に発行します。|
|[-ADTemplate](#BKMK_ADTemplate)|AD テンプレートを表示します|
|[-テンプレート](#BKMK_template)|証明書テンプレートを表示します。|
|[-TemplateCAs](#BKMK_TemplateCAs)|証明書テンプレートの証明機関 (Ca) の表示します。|
|[-CATemplates](#BKMK_CATemplates)|CA のテンプレートを表示します。|
|[-SetCASites](#BKMK_SetCASites)|Ca の名前をサイトを管理します。|
|[-enrollmentServerURL](#BKMK_enrollmentServerURL)|表示、追加または CA に関連付けられている登録サーバーの Url を削除|
|[-ADCA](#BKMK_ADCA)|AD Ca を表示します|
|[CA](#BKMK_CA)|ポリシー Ca の登録を表示します|
|[-ポリシー](#BKMK_Policy)|登録ポリシーを表示します。|
|[-PolicyCache](#BKMK_PolicyCache)|登録ポリシーのキャッシュ エントリを削除または表示|
|[-CredStore](#BKMK_Credstore)|表示、追加、または資格情報ストアのエントリを削除します。|
|[-InstallDefaultTemplates](#BKMK_InstallDefaultTemplates)|証明書テンプレートの既定をインストールします。|
|[-URLCache](#BKMK_URLCache)|URL キャッシュ エントリを削除または表示|
|[-pulse](#BKMK_pulse)|Pulse の自動登録のイベント|
|[-MachineInfo](#BKMK_MachineInfo)|Active Directory コンピューター オブジェクトに関する情報を表示します。|
|[-DCInfo](#BKMK_DCInfo)|ドメイン コント ローラーに関する情報を表示します。|
|[-EntInfo](#BKMK_EntInfo)|エンタープライズ CA に関する情報を表示します。|
|[-Tcainfo](#BKMK_TCAInfo)|CA に関する情報を表示します。|
|[-SCInfo](#BKMK_SCInfo)|スマート カードに関する情報を表示します。|
|[-SCRoots](#BKMK_SCRoots)|スマート カードのルート証明書を管理します。|
|[-verifykeys](#BKMK_verifykeys)|パブリックまたはプライベート キーのセットを確認します。|
|[-確認](#BKMK_verify)|証明書、証明書失効リスト (CRL)、または証明書チェーンを確認します。|
|[-verifyCTL](#BKMK_verifyCTL)|AuthRoot を確認するか、許可されない証明書の CTL|
|[-sign](#BKMK_sign)|証明書失効リスト (CRL) または証明書を再署名します。|
|[-vroot](#BKMK_vroot)|作成または web 仮想ルートとファイル共有の削除|
|[-vocsproot](#BKMK_vocsproot)|作成または OCSP の web プロキシの web 仮想ルートを削除します。|
|[-addEnrollmentServer](#BKMK_addEnrollmentServer)|登録サーバーのアプリケーションを追加します。|
|[-deleteEnrollmentServer](#BKMK_deleteEnrollmentServer)|登録サーバー アプリケーションを削除します。|
|[-addPolicyServer](#BKMK_addPolicyServer)|ポリシー サーバー アプリケーションを追加します。|
|[-deletePolicyServer](#BKMK_deletePolicyServer)|ポリシー サーバー アプリケーションを削除します。|
|[-oid](#BKMK_oid)|オブジェクトの識別子を表示または表示名を設定します。|
|[-error](#BKMK_error)|エラー コードに関連付けられたメッセージ テキストを表示します。|
|[-getreg](#BKMK_getreg)|レジストリ値を表示します。|
|[-setreg](#BKMK_setreg)|レジストリ値を設定します。|
|[-delreg](#BKMK_delreg)|レジストリ値を削除します。|
|[-ImportKMS](#BKMK_ImportKMS)|キーのアーカイブ用にサーバー データベースにユーザーのキーと証明書をインポートします。|
|[-ImportCert](#BKMK_ImportCert)|証明書ファイルをデータベースにインポートします。|
|[-GetKey](#BKMK_GetKey)|アーカイブされた秘密キーの回復、blob を取得します。|
|[-RecoverKey](#BKMK_RecoverKey)|アーカイブ済みの秘密キーを回復します。|
|[-MergePFX](#BKMK_MergePFX)|PFX ファイルをマージします。|
|[-ConvertEPF](#BKMK_ConvertEPF)|PFX ファイルを EPF ファイルに変換します。|
|-?|動詞の一覧を表示します。|
|-*\<verb>* -?|指定された動詞のヘルプを表示します。|
|-? -v|動詞の完全な一覧を表示し、|

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_notations"></a>構文の表記

-   基本的なコマンドライン構文は、次のように実行します。 `certutil -?`
-   構文については、特定の動詞を使用して certutil を使用して、実行**certutil** *\<動詞 >* **-でしょうか。**
-   テキスト ファイルに送信する certutil 構文のすべては、するには、次のコマンドを実行します。  
    -   `certutil -v -? > certutilhelp.txt`
    -   `notepad certutilhelp.txt`

次の表では、コマンドラインの構文を示すために使用される表記について説明します。

|表記法|説明|
|--------|-----------|
|角かっこまたは中かっこのないテキスト|項目に示すように入力する必要があります。|
|\<山かっこ内のテキスト >|プレース ホルダーの値を指定する必要があります。|
|[角かっこ内のテキスト]|省略可能な項目|
|{中かっこ内のテキスト}|必要な項目のセットいずれかを選択します。|
|垂直バー (|)|相互に排他的な項目の区切り記号いずれかを選択します。|
|省略記号 (...)|項目を繰り返すことができます。|

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_dump"></a>-ダンプ

CertUtil [オプション] [-ダンプ]

CertUtil [オプション] [-ダンプ] ファイル

ダンプの構成情報やファイル

[-f]。[-サイレント][-の分割][--p パスワード][-t タイムアウト]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_asn"></a>-asn

CertUtil [オプション] - asn ファイル [種類]

ASN.1 ファイルを解析します。

type: numeric CRYPT_STRING_* decoding type

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_decodehex"></a>-decodehex

CertUtil [オプション] - decodehex InFile OutFile [種類]

type: numeric CRYPT_STRING_* encoding type

[-f]。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_decode"></a>デコード

CertUtil [オプション] - InFile をデコードする出力ファイル

Base64 でエンコードされたファイルをデコードします。

[-f]。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_encode"></a>-エンコード

CertUtil [オプション] - InFile エンコード出力ファイル

ファイルを Base64 にエンコードします。

[-f] [-UnicodeText]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_deny"></a>-拒否

CertUtil [オプション] - RequestId を拒否します。

保留中の要求を拒否します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_resubmit"></a>-再送信

CertUtil [オプション] - RequestId を再送信

保留中の要求を再送信します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_setattributes"></a>-setattributes

CertUtil [オプション] - setattributes RequestId AttributeString

保留中の要求属性を設定します

RequestId: 要求の数値 Id 保留中の要求

AttributeString - 属性の名前と値のペアを要求します。
-   名前と値は、コロンで区切られたです。
-   複数の名前と値のペアは、改行で区切ります。
-   例:"CertificateTemplate:User\nEMail:User@Domain.com"
-   各"\n"シーケンスは、改行の区切り記号に変換されます。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_setextension"></a>-setextension

CertUtil [Options] -setextension RequestId ExtensionName Flags {Long | Date | String | @InFile}

保留中の要求のセットの拡張機能

数値の要求 Id、保留中の要求の RequestId--

拡張機能の ExtensionName--ObjectId 文字列

Flags--0 はお勧めします。  拡張機能は、重要な 1、2 が無効にする、3 は両方。

最後のパラメーターが数値の場合は、Long として取得されます。

日付として解析できなかった場合は、日付として取得されます。

始まる場合 ' @'、トークンの残りの部分はデータのバイナリまたは ascii テキストの 16 進数ダンプを含むファイル名。

その他は、文字列として扱われます。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_revoke"></a>-revoke

CertUtil [オプション]-[理由] SerialNumber を取り消す

証明書を失効します。

シリアル番号:失効させる証明書のシリアル番号のコンマ区切りリスト

理由: 数値または記号の失効の理由
-   0:CRL_REASON_UNSPECIFIED:指定されていない (既定値)
-   1:CRL_REASON_KEY_COMPROMISE:キーの侵害
-   2:CRL_REASON_CA_COMPROMISE:CA の侵害
-   3:CRL_REASON_AFFILIATION_CHANGED:所属変更
-   4:CRL_REASON_SUPERSEDED:置き換え済み
-   5:CRL_REASON_CESSATION_OF_OPERATION:利用中止
-   6:CRL_REASON_CERTIFICATE_HOLD:証明書保留
-   8:CRL_REASON_REMOVE_FROM_CRL:CRL から削除します。
-   -1:失効を取り消します。失効を取り消す

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_isvalid"></a>-isvalid

CertUtil [Options] -isvalid SerialNumber | CertHash

現在の証明書廃棄を表示

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_getconfig"></a>-getconfig

CertUtil [オプション] getconfig

既定の構成文字列を取得します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ping"></a>-ping

CertUtil [Options] -ping [MaxSecondsToWait | CAMachineList]

Ping Active Directory 証明書サービスの要求インターフェイス

CAMachineList - コンマ区切りの CA コンピューター名 の一覧
1.  1 台のコンピューターの終端のコンマを使用して、
2.  CA コンピューターごとにサイト コストを表示します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_CAInfo"></a>-Cainfo

CertUtil [オプション] CAInfo [InfoName [Index |ErrorCode]

CA 情報を表示

InfoName--では、CA プロパティ (下記参照) を表示することを示します。 使用して"*"のすべてのプロパティ。

省略可能なプロパティのインデックスをインデックス {\pict}

ErrorCode - 数値エラー コード

[-f]。[-の分割][-config Machine\CAName]

InfoName 引数の構文:
-   ファイル:ファイル バージョン
-   製品:製品バージョン
-   exitcount:終了モジュール数
-   [Index] を終了します。終了モジュールの説明
-   ポリシー:ポリシー モジュールの説明
-   名:CA 名
-   sanitizedname:CA 名の先頭が英文字
-   dsname:先頭が英文字 CA 短い名前 (DS 名)
-   共有:共有フォルダー
-   error1 ErrorCode:エラー メッセージ テキスト
-   エラー 2-エラー コード:エラー メッセージ テキストとエラー コード
-   種類:CA の種類
-   情報:CA の情報
-   親:親 CA
-   certcount:CA 証明書の数
-   xchgcount:CA exchange 証明書の数
-   kracount:KRA 証明書の数
-   kraused:KRA 証明書の使用数
-   propidmax:最大 CA PropId
-   certstate [Index]:CA の証明書
-   certversion [Index]:CA 証明書のバージョン
-   certstatuscode [Index]:CA の証明書は、状態を確認します。
-   crlstate [Index]:CRL
-   krastate [Index]:KRA 証明書
-   crossstate + [Index]:順方向のクロス証明書
-   crossstate - [Index]:旧バージョンとのクロス証明書
-   [Index] 証明書:CA の証明書
-   certchain [Index]:CA 証明書チェーン
-   certcrlchain [Index]:Crl と CA 証明書チェーン
-   xchg [Index]:Exchange 証明書の CA
-   xchgchain [Index]:Exchange の CA 証明書チェーン
-   xchgcrlchain [Index]:Crl と CA exchange 証明書チェーン
-   kra [Index]:KRA 証明書
-   クロス + [Index]:順方向のクロス証明書
-   クロス [Index]:旧バージョンとのクロス証明書
-   CRL [Index]:ベース CRL
-   deltacrl [Index]:Delta CRL
-   crlstatus [Index]:CRL の発行状態
-   deltacrlstatus [Index]:Delta CRL の発行状態
-   dns:DNS 名
-   ロール:役割の分離
-   広告:Advanced Server
-   テンプレート:テンプレート
-   ocsp [Index]:OCSP の Url
-   aia [Index]:AIA の Url
-   cdp [Index]:CDP Url
-   localename:CA ロケール名
-   subjecttemplateoids:サブジェクトのテンプレートの Oid

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ca.cert"></a>-ca.cert

CertUtil [オプション] - ca.cert OutCACertFile [Index]

CA の証明書を取得します。

OutCACertFile: 出力ファイル

インデックス:CA 証明書の更新インデックス (既定値は、最新)

[-f]。[-の分割][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ca.chain"></a>-ca.chain

CertUtil [オプション] - ca.chain OutCACertChainFile [Index]

CA の証明書チェーンを取得します。

OutCACertChainFile: 出力ファイル

インデックス:CA 証明書の更新インデックス (既定値は、最新)

[-f]。[-の分割][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_GetCRL"></a>-GetCRL

CertUtil [オプション] - GetCRL OutFile [Index] [差分]

CRL を取得します。

インデックス:CRL のインデックスまたはキーのインデックス (最新のキーの既定の CRL に)

デルタ: delta CRL (既定値は base CRL)

[-f]。[-の分割][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_CRL"></a>-CRL

CertUtil [オプション] - CRL [dd:hh | 再発行] [差分]

新しい Crl または delta Crl のみ] を発行します。

dd:hh - 日付と時間で新しい CRL の有効期間

再発行--最新の Crl を再発行します。

差分 - delta Crl のみ (既定値は、ベースと差分の Crl は)

[-split] [-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_shutdown"></a>-シャット ダウン

CertUtil [オプション] - シャット ダウン

Active Directory 証明書サービスをシャット ダウン

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_installcert"></a>-installcert

CertUtil [オプション]-installcert [CACertFile]

証明機関の証明書をインストールします。

[-f] [-silent] [-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_renewcert"></a>-renewCert

CertUtil [Options] -renewCert [ReuseKeys] [Machine\ParentCAName]

証明機関の証明書を更新します。

-F を使用して、未処理の更新の要求を無視して、新しい要求を生成します。

[-f] [-silent] [-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_schema"></a>-スキーマ

CertUtil [オプション] - スキーマ [Ext |Attrib |CRL]

証明書のスキーマをダンプします。

既定値は要求と証明書のテーブル

Ext:拡張テーブル

Attrib:属性テーブル

CRL:CRL テーブル

[-split] [-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_view"></a>ビュー

CertUtil [Options] -view [Queue | Log | LogFail | Revoked | Ext | Attrib | CRL] [csv]

ダンプの証明書の表示

キュー:要求キュー

ログ :発行または失効した証明書、および失敗した要求

LogFail:失敗した要求

取り消されました。失効した証明書

Ext:拡張テーブル

Attrib:属性テーブル

CRL:CRL テーブル

csv:コンマ区切りの値と出力

すべてのエントリの StatusCode 列を表示する-StatusCode アウト。

最後のエントリのすべての列を表示する-制限"RequestId$ = ="。

3 つの要求の RequestId と廃棄を表示する:-制限"RequestId > 37、RequestId =\<40"-"RequestId、廃棄"アウト

すべての Base Crl の行 Id と CRL の数字を表示する:-制限"CRLMinBase = 0"-"CRLRowId CRLNumber"アウト CRL

Base CRL 番号 3 を表示する-v-制限"CRLMinBase = 0、CRLNumber = 3"-"CRLRawCRL"CRL を。

CRL テーブル全体を表示するには。CRL

使用して"日付 [+ |-dd:hh]"の日付の制限

現在の時間を基準と日付の「現在 + dd:hh」を使用します。

[-サイレント][-の分割][-config Machine\CAName][-RestrictionList を制限する][-ColumnList out]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_db"></a>-db

CertUtil [オプション] - db

生のデータベースをダンプします。

[-config Machine\CAName][-RestrictionList を制限する][-ColumnList out]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_deleterow"></a>-deleterow

CertUtil [オプション] - deleterow RowId |日付 [要求 |Cert |Ext |Attrib |CRL]

サーバー データベースの行を削除します。

要求:失敗、保留中の要求 (提出日)

Cert:期限切れ、失効した証明書 (有効期限)

Ext:拡張テーブル

Attrib:属性テーブル

CRL:CRL テーブル (有効期限)

失敗したと保留中の要求を削除するには、2001 年 1 月 22 日によって送信されました。1/22/2001 要求

有効期限が切れたすべての証明書を削除する、2001 年 1 月 22 日で。証明書の 1/22/2001

RequestId 37 の証明書の行、属性、および拡張機能を削除します。37

有効期限が切れている Crl を削除する、2001 年 1 月 22 日で。1/22/2001 CRL

[-f]。[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_backup"></a>-バックアップ

CertUtil [オプション] - BackupDirectory [増分] [KeepLog] のバックアップ

バックアップの Active Directory 証明書サービス

データをバックアップを格納するディレクトリをバックアップ ディレクトリ。

増分: 増分バックアップのみを実行する (既定値は完全バックアップ)

KeepLog: (既定では、ログ ファイルを切り捨てる) データベースのログ ファイルを保持します。

[-f]。[-config Machine\CAName][--p パスワード]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_backupDB"></a>-backupDB

CertUtil [Options] -backupDB BackupDirectory [Incremental] [KeepLog]

Active Directory Certificate Services データベースのバックアップ

データベース ファイルをバックアップを格納するディレクトリをバックアップ ディレクトリ。

増分: 増分バックアップのみを実行する (既定値は完全バックアップ)

KeepLog: (既定では、ログ ファイルを切り捨てる) データベースのログ ファイルを保持します。

[-f]。[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_backupKey"></a>-backupKey

CertUtil [オプション] - backupKey BackupDirectory

バックアップの Active Directory 証明書サービスの証明書と秘密キー

PFX ファイルをバックアップを格納するディレクトリをバックアップ ディレクトリ。

[-f]。[-config Machine\CAName][--p パスワード][-t タイムアウト]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_restore"></a>-復元

CertUtil [オプション] --restore

Active Directory 証明書サービスを復元します。

BackupDirectory: ディレクトリを復元するデータを含む

[-f]。[-config Machine\CAName][--p パスワード]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_restoreDB"></a>-restoreDB

CertUtil [Options] -restoreDB BackupDirectory

Active Directory Certificate Services データベースを復元します。

BackupDirectory: ディレクトリを復元するデータベース ファイルを含む

[-f]。[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_restorekey"></a>-restoreKey

CertUtil [Options] -restoreKey BackupDirectory | PFXFile

Active Directory 証明書サービスの証明書と秘密キーを復元します。

BackupDirectory: ディレクトリを復元する PFX ファイルを含む

PFXFile:PFX ファイルを復元するには

[-f]。[-config Machine\CAName][--p パスワード]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_importPFX"></a>-importPFX

CertUtil [オプション]-importpfx [CertificateStoreName] PFXFile [修飾子]

証明書のインポートと秘密キー

証明:証明書ストアの名前。  参照してください[-格納](#BKMK_Store)します。

PFXFile:PFX ファイルをインポートします。

修飾子:次の 1 つ以上のコンマ区切りリスト。
1.  AT_SIGNATURE:KeySpec をシグネチャに変更します。
2.  AT_KEYEXCHANGE:変更するキーの交換 KeySpec
3.  NoExport:秘密キーをエクスポートできないこと
4.  NoCert:証明書をインポートできません。
5.  NoChain:証明書チェーンをインポートできません。
6.  NoRoot:ルート証明書をインポートできません。
7.  保護します。パスワードを使用してキーを保護します。
8.  NoProtect:パスワードではなくキーを保護します。

パーソナル コンピューター ストアの既定値です。

[-f]。[-ユーザー][--p パスワード][-csp プロバイダー]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_dynamicfilelist"></a>-dynamicfilelist

CertUtil [オプション] dynamicfilelist

動的ファイルの一覧を表示します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_databaselocations"></a>-databaselocations

CertUtil [オプション] databaselocations

データベースの場所を表示します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_hashfile"></a>-hashfile

CertUtil [オプション]-hashfile InFile [HashAlgorithm]

生成およびファイルの暗号化ハッシュを表示します。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_Store"></a>格納

CertUtil [Options] -store [CertificateStoreName [CertId [OutputFile]]]

証明書ストアをダンプします。

証明:証明書ストアの名前。 例:
-   "My", "CA" (default), "Root",
-   "ldap:///CN 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか 1 つですか? objectClass 証明機関を ="(ルートの証明書を表示)。
-   "ldap:///CN CAName、CN = 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか基本でしょうか。 objectClass 証明機関を ="(ルート証明書の変更)。
-   "ldap:///CN CAName、CN = MachineName、CN = CDP、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? certificateRevocationList でしょうか基本でしょうか。 objectClass = cRLDistributionPoint"(Crl) の表示。
-   "ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority" (Enterprise CA Certificates)
-   ldap:(AD コンピューター オブジェクトの証明書)
-   -ユーザーの ldap:(AD ユーザー オブジェクトの証明書)

CertId:証明書または CRL の一致するトークン。  これは、シリアル番号、または指定できます、sha-1 証明書、CRL、CTL 公開キー ハッシュ、証明書を数値インデックス (0、1、およびなど)、数値 CRL インデックス (. 0 や.1、)、CTL の数値インデックス (..0、.1、およびなど)、公開キー、署名または拡張機能オブジェクト Id、証明書のサブジェクト共通名、電子メール アドレスでは、UPN または DNS 名、キー コンテナーの名前または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーション ポリシーの ObjectId または CRL の発行者の共通名。 これらの多くにより、複数の一致する可能性があります。

一致する証明書を保存するファイルを出力ファイル:

-を使用して、ユーザー、コンピューター ストアではなくユーザー ストアにアクセスします。

使用してコンピューターのエンタープライズ ストアにアクセスする企業。

-を使用して、サービス コンピューターのサービス ストアにアクセスします。

マシン グループのポリシー ストアにアクセスする - グループ ポリシーを使用します。

例:
-   -エンタープライズ NTAuth
-   -エンタープライズ ルート 37
-   -ユーザー、26e0aaaf000000000004
-   CA.11

[-f] [-enterprise] [-user] [-GroupPolicy] [-silent] [-split] [-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_addstore"></a>-addstore

CertUtil [オプション] - addstore CertificateStoreName InFile

証明書をストアの追加します。

証明:証明書ストアの名前。  参照してください[-格納](#BKMK_Store)します。

InFile:ストアに追加する証明書または CRL のファイル。

[-f]。[-エンタープライズ][-ユーザー][-グループ ポリシー][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_delstore"></a>-delstore

CertUtil [オプション]-delstore CertificateStoreName CertId

証明書ストアから削除します。

証明:証明書ストアの名前。  参照してください[-格納](#BKMK_Store)します。

CertId:証明書または CRL の一致するトークン。  参照してください[-格納](#BKMK_Store)します。

[-enterprise] [-user] [-GroupPolicy] [-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_verifystore"></a>-verifystore

CertUtil [オプション] - verifystore CertificateStoreName [CertId]

ストアに証明書を確認します。

証明:証明書ストアの名前。  参照してください[-格納](#BKMK_Store)します。

CertId:証明書または CRL の一致するトークン。  参照してください[-格納](#BKMK_Store)します。

[-エンタープライズ][-ユーザー][-グループ ポリシー][-サイレント][-の分割][-dc DCName][-t タイムアウト]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_repairstore"></a>-repairstore

CertUtil [オプション] - repairstore CertificateStoreName CertIdList [PropertyInfFile |SDDLSecurityDescriptor]

キーの関連付けを修復または証明書のプロパティまたはキーのセキュリティ記述子の更新

証明:証明書ストアの名前。  参照してください[-格納](#BKMK_Store)します。

証明書または CRL の一致するトークンの CertIdList: コンマ区切り一覧。 参照してください[-格納](#BKMK_Store)CertId 説明します。

PropertyInfFile--INF を外部のプロパティを含むファイル:
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
[-f]。[-エンタープライズ][-ユーザー][-グループ ポリシー][-サイレント][-の分割][-csp プロバイダー]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_viewstore"></a>-viewstore

[オプション] の CertUtil-viewstore [CertificateStoreName [CertId [OutputFile]]

証明書ストアをダンプします。

証明:証明書ストアの名前。  例:
-   "My", "CA" (default), "Root",
-   "ldap:///CN 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか 1 つですか? objectClass 証明機関を ="(ルートの証明書を表示)。
-   "ldap:///CN CAName、CN = 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか基本でしょうか。 objectClass 証明機関を ="(ルート証明書の変更)。
-   "ldap:///CN CAName、CN = MachineName、CN = CDP、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? certificateRevocationList でしょうか基本でしょうか。 objectClass = cRLDistributionPoint"(Crl) の表示。
-   "ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority" (Enterprise CA Certificates)
-   ldap:(AD コンピューター オブジェクトの証明書)
-   -ユーザーの ldap:(AD ユーザー オブジェクトの証明書)

CertId:証明書または CRL の一致するトークン。 これは、シリアル番号、または指定できます、sha-1 証明書、CRL、CTL 公開キー ハッシュ、証明書を数値インデックス (0、1、およびなど)、数値 CRL インデックス (. 0 や.1、)、CTL の数値インデックス (..0、.1、およびなど)、公開キー、署名または拡張機能オブジェクト Id、証明書のサブジェクト共通名、電子メール アドレスでは、UPN または DNS 名、キー コンテナーの名前または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーション ポリシーの ObjectId または CRL の発行者の共通名。 これらの多くにより、複数の一致する可能性があります。

一致する証明書を保存するファイルを出力ファイル:

-を使用して、ユーザー、コンピューター ストアではなくユーザー ストアにアクセスします。

使用してコンピューターのエンタープライズ ストアにアクセスする企業。

-を使用して、サービス コンピューターのサービス ストアにアクセスします。

マシン グループのポリシー ストアにアクセスする - グループ ポリシーを使用します。

例:
1.  -エンタープライズ NTAuth
2.  -エンタープライズ ルート 37
3.  -ユーザー、26e0aaaf000000000004
4.  CA.11

[-f]。[-エンタープライズ][-ユーザー][-グループ ポリシー][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_viewdelstore"></a>-viewdelstore

CertUtil [Options] -viewdelstore [CertificateStoreName [CertId [OutputFile]]]

証明書ストアから削除します。

証明:証明書ストアの名前。  例:
-   "My", "CA" (default), "Root",
-   "ldap:///CN 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか 1 つですか? objectClass 証明機関を ="(ルートの証明書を表示)。
-   "ldap:///CN CAName、CN = 証明機関、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? cACertificate でしょうか基本でしょうか。 objectClass 証明機関を ="(ルート証明書の変更)。
-   "ldap:///CN CAName、CN = MachineName、CN = CDP、CN = Public Key Services、CN = Services, CN = Configuration, DC = cpandl、DC = com を = ですか? certificateRevocationList でしょうか基本でしょうか。 objectClass = cRLDistributionPoint"(Crl) の表示。
-   "ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority" (Enterprise CA Certificates)
-   ldap:(AD コンピューター オブジェクトの証明書)
-   -ユーザーの ldap:(AD ユーザー オブジェクトの証明書)

CertId:証明書または CRL の一致するトークン。 これは、シリアル番号、または指定できます、sha-1 証明書、CRL、CTL 公開キー ハッシュ、証明書を数値インデックス (0、1、およびなど)、数値 CRL インデックス (. 0 や.1、)、CTL の数値インデックス (..0、.1、およびなど)、公開キー、署名または拡張機能オブジェクト Id、証明書のサブジェクト共通名、電子メール アドレスでは、UPN または DNS 名、キー コンテナーの名前または CSP 名、テンプレート名または ObjectId、EKU またはアプリケーション ポリシーの ObjectId または CRL の発行者の共通名。 これらの多くにより、複数の一致する可能性があります。

一致する証明書を保存するファイルを出力ファイル:

-を使用して、ユーザー、コンピューター ストアではなくユーザー ストアにアクセスします。

使用してコンピューターのエンタープライズ ストアにアクセスする企業。

-を使用して、サービス コンピューターのサービス ストアにアクセスします。

マシン グループのポリシー ストアにアクセスする - グループ ポリシーを使用します。

例:
1.  -エンタープライズ NTAuth
2.  -エンタープライズ ルート 37
3.  -ユーザー、26e0aaaf000000000004
4.  CA.11

[-f]。[-エンタープライズ][-ユーザー][-グループ ポリシー][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_dsPublish"></a>-dsPublish

CertUtil [Options] -dsPublish CertFile [NTAuthCA | RootCA | SubCA | CrossCA | KRA | User | Machine]

[オプション] の CertUtil-dspublish CRLFile [DSCDPContainer [DSCDPCN]

Active Directory に証明書または CRL を発行します。

CertFile: 証明書ファイルを発行するには

NTAuthCA:DS エンタープライズ ストアに証明書を発行します。

ルート Ca:DS の信頼されたルート ストアに証明書を発行します。

SubCA:DS CA のオブジェクトに CA の証明書を発行します。

CrossCA:クロス DS CA オブジェクトに証明書を発行します。

KRA:DS Key Recovery Agent オブジェクトへの証明書を発行します。

ユーザー:ユーザーの DS オブジェクトに証明書を発行します。

マシンの場合:マシン DS オブジェクトに証明書を発行します。

CRLFile:CRL ファイルを発行するには

DSCDPContainer:DS CDP コンテナー CN、通常は CA のコンピューター名

DSCDPCN:DS CDP はオブジェクトの CN、先頭が英文字の CA の短い名前とキーのインデックスに基づく通常

-F を使用すると、DS オブジェクトを作成します。

[-f]。[-ユーザー][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ADTemplate"></a>-ADTemplate

CertUtil [オプション] - ADTemplate [テンプレート]

AD テンプレートを表示します

[-f]。[-ユーザー][-ut][-mt][-dc DCName]

## <a name="BKMK_template"></a>-テンプレート

CertUtil [オプション] - テンプレート [テンプレート]

登録ポリシー テンプレートを表示します

[-f] [-user] [-silent] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName UserName] [-p Password]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_TemplateCAs"></a>-TemplateCAs

CertUtil [オプション] - TemplateCAs テンプレート

テンプレートの CAs で表示

[-f]。[-ユーザー][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_CATemplates"></a>-CATemplates

CertUtil [オプション] - CATemplates [テンプレート]

CA のテンプレートを表示します。

[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_SetCASites"></a>-SetCASites

CertUtil [オプション] - SetCASites [セット] [サイト名]

CertUtil [オプション] SetCASites は、[サイト名] を確認します。

CertUtil [オプション] - SetCASites delete

サイト名のセットを確認または CA の削除
-   構成オプションを使用して、単一の CA を対象とする (既定値はすべての Ca)
-   *SiteName*単一の CA を対象とする場合にのみ
-   -F を使用して、指定した検証エラーをオーバーライドする*SiteName*
-   -F を使用して、すべての CA サイト名を削除するには

[-f] [-config Machine\CAName] [-dc DCName]

> [!NOTE]
> Active Directory Domain Services (AD DS) サイト認識用の Ca の構成の詳細については、次を参照してください。 [AD CS および PKI クライアント用の AD DS サイト認識](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx)します。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_enrollmentServerURL"></a>-enrollmentServerURL

CertUtil [オプション] - enrollmentServerURL [URL AuthenticationType 優先順位 [修飾子]

CertUtil [オプション] - enrollmentServerURL URL の削除

表示、追加または CA に関連付けられている登録サーバーの Url を削除

AuthenticationType:URL を追加するときに、次のクライアント認証方法のいずれかを指定します。
1.  Kerberos:Kerberos の SSL 資格情報を使用します。
2.  ユーザー名:名前付きのアカウントを使用して、SSL 資格情報
3.  ClientCertificate:X.509 証明書の SSL 資格情報を使用します。
4.  Anonymous:匿名の SSL 資格情報を使用します。

削除: CA に関連付けられている指定された URL を削除します。

優先順位: 既定値は '1' URL を追加するときに指定しない場合

修飾子: コンマ区切りの次の 1 つ以上のリスト。
1.  AllowRenewalsOnly:この URL を使用してこの CA に証明書更新要求のみを送信できます。
2.  AllowKeyBasedRenewal:AD に関連付けられているアカウントを持たない証明書を使用できるようにします。 これは ClientCertificate と AllowRenewalsOnly モードでのみ適用されます。

[-config Machine\CAName] [-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ADCA"></a>-ADCA

CertUtil [オプション] - ADCA [ca 名]

AD Ca を表示します

[-f]。[-の分割][-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_CA"></a>CA

CertUtil [Options] -CA [CAName | TemplateName]

ポリシー Ca の登録を表示します

[-f] [-user] [-silent] [-split] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName UserName] [-p Password]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_Policy"></a>-ポリシー

登録ポリシーを表示します。

[-f] [-user] [-silent] [-split] [-PolicyServer URLOrId] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName UserName] [-p Password]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_PolicyCache"></a>-PolicyCache

CertUtil [オプション] - PolicyCache [delete]

登録ポリシーのキャッシュ エントリを削除または表示

削除: ポリシー サーバーのキャッシュ エントリを削除します。

-f:-f を使用して、すべてのキャッシュ エントリを削除するには

[-f]。[-ユーザー][-PolicyServer URLOrId]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_Credstore"></a>-CredStore

CertUtil [オプション] - CredStore [URL]

CertUtil [オプション] CredStore URL を追加します。

CertUtil [オプション] CredStore URL を削除します。

表示、追加、または資格情報ストアのエントリを削除します。

URL: ターゲット URL。  使用して * すべてのエントリが一致するようにします。 使用 https://machine* URL プレフィックスの一致するようにします。

追加: 資格情報ストアのエントリを追加します。 SSL 資格情報も指定する必要があります。

削除: 資格情報ストアのエントリを削除します。

-エントリを上書きするか、複数のエントリを削除する、f: は-f を使用します。

[-f] [-user] [-silent] [-Anonymous] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName UserName] [-p Password]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_InstallDefaultTemplates"></a>-InstallDefaultTemplates

CertUtil [オプション] InstallDefaultTemplates

証明書テンプレートの既定をインストールします。

[-dc DCName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_URLCache"></a>-URLCache

CertUtil [Options] -URLCache [URL | CRL | * [delete]]

URL キャッシュ エントリを削除または表示

キャッシュされた URL の URL:

すべてのキャッシュされた CRL ・ Url のみに対して CRL:

*: キャッシュされたすべての Url の動作

削除: 現在のユーザーのローカル キャッシュから関連する Url を削除

-F を使用して、特定の URL の取得およびキャッシュの更新を強制します。

[-f]。[-の分割]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_pulse"></a>-パルス

CertUtil [オプション] - パルス

Pulse の自動登録イベント

[-ユーザー]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_MachineInfo"></a>-MachineInfo

CertUtil [Options] -MachineInfo DomainName\MachineName$

Active Directory コンピューター オブジェクトの情報を表示します。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_DCInfo"></a>-DCInfo

CertUtil [オプション] - DCInfo [ドメイン] [確認 |DeleteBad |DeleteAll]

ドメイン コント ローラーの情報を表示します。

既定値が検証なしの DC の証明書を表示するには

[-f] [-user] [-urlfetch] [-dc DCName] [-t Timeout]

> [!TIP]
> Active Directory Domain Services (AD DS) ドメインを指定する機能 **[ドメイン]** とドメイン コント ローラーを指定する (**dc**) Windows Server 2012 で追加されました。 コマンドを正常に実行するには、メンバーであるアカウントを使用する必要があります**Domain Admins**または**Enterprise Admins**します。 このコマンドの動作の変更は次のとおりです。</br>> 1.  ドメインが指定されていない、特定のドメイン コント ローラーが指定されていない場合は、このオプションは既定のドメイン コント ローラーから、処理するドメイン コント ローラーの一覧を返します。</br>> 2.  ドメインが指定されていないが、ドメイン コント ローラーが指定されて、指定されたドメイン コント ローラーで、証明書のレポートが生成されます。</br>> 3.  ドメインを指定すると、ドメイン コント ローラーが指定されていない場合、リスト内の各ドメイン コント ローラー用の証明書でのレポートと併せてドメイン コントローラの一覧が生成されます。</br>> 4.  ドメインとドメイン コント ローラーを指定すると、対象となるドメイン コント ローラーからドメイン コントローラの一覧が生成されます。 リスト内の各ドメイン コント ローラー用の証明書のレポートが生成されます。

たとえば、CPANDL DC1 という名前のドメイン コント ローラーと CPANDL をという名前のドメインがあるとします。 でしたを実行する、次のコマンドのドメイン コント ローラーとその証明書の一覧を取得する CPANDL DC1 から: certutil -dc cpandl dc1-dcinfo cpandl

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_EntInfo"></a>-EntInfo

CertUtil [Options] -EntInfo DomainName\MachineName$

[-f]。[-ユーザー]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_TCAInfo"></a>-Tcainfo

CertUtil [オプション]-tcainfo [DomainDN |-]

CA 情報を表示

[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t Timeout]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_SCInfo"></a>-SCInfo

CertUtil [Options] -SCInfo [ReaderName [CRYPT_DELETEKEYSET]]

スマート カードの情報を表示します。

CRYPT_DELETEKEYSET:スマート カード上のすべてのキーを削除します。

[-サイレント][-の分割][-urlfetch][-t タイムアウト]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_SCRoots"></a>-SCRoots

CertUtil [Options] -SCRoots update [+][InputRootFile] [ReaderName]

CertUtil [オプション] SCRoots 保存@OutputRootFile[ReaderName]

CertUtil [Options] -SCRoots view [InputRootFile | ReaderName]

CertUtil [オプション] SCRoots [ReaderName] の削除します。

スマート カードのルート証明書を管理します。

[-f]。[-の分割][--p パスワード]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_verifykeys"></a>-verifykeys

CertUtil [オプション] - verifykeys [キーコンテナー名 CACertFile]

公開/秘密キーのセットを確認します。

キーコンテナー名: ことを確認するキーの名前をキー コンテナーです。 マシン キーの既定値です。  使用してユーザーのユーザー キー。

CACertFile: 署名または暗号化証明書ファイル

引数が指定されていない場合は、その秘密キーに対して各署名 CA 証明書が検証されます。

この操作は、ローカルの CA またはローカル キーに対してのみ実行できます。

[-f]。[-ユーザー][-サイレント][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_verify"></a>-確認

CertUtil [Options] -verify CertFile [ApplicationPolicyList | - [IssuancePolicyList]]

CertUtil [オプション] - CertFile [CACertFile [CrossedCACertFile] を確認します。

CertUtil [Options] -verify CRLFile CACertFile [IssuedCertFile]

CertUtil [オプション] - CRLFile CACertFile [DeltaCRLFile] を確認します。

証明書、CRL またはチェーンを確認します。

CertFile:証明書を確認するには

必要なアプリケーション ポリシーの Objectid の ApplicationPolicyList: 省略可能なコンマ区切りの一覧

必要な発行ポリシーの Objectid の IssuancePolicyList: 省略可能なコンマ区切りの一覧

CACertFile: 省略可能な発行元 CA 証明書を検証対象

CrossedCACertFile: 省略可能な証明書をクロス証明された、CertFile

CRLFile:CRL を確認

IssuedCertFile: 省略可能な発行された証明書 CRLFile 覆わ

省略可能な delta CRL を DeltaCRLFile:

ApplicationPolicyList が指定されている場合、チェーンを構築は、指定したアプリケーション ポリシーの有効なチェーンに限定されます。

IssuancePolicyList が指定されている場合、チェーンを構築は、指定した発行ポリシーの有効なチェーンに限定されます。

CACertFile が指定されている場合は、CACertFile 内のフィールドが CertFile または CRLFile に対して検証されます。

CACertFile が指定されていない場合は、CertFile が構築や完全なチェーンの検証に使用されます。

CACertFile と CrossedCACertFile 両方を指定する場合は、CACertFile と CrossedCACertFile 内のフィールドが CertFile に対して検証されます。

IssuedCertFile が指定されている場合は、IssuedCertFile 内のフィールドが CRLFile に対して検証されます。

DeltaCRLFile が指定されている場合は、DeltaCRLFile 内のフィールドが CRLFile に対して検証されます。

[-f]。[-エンタープライズ][-ユーザー][-サイレント][-の分割][-urlfetch][-t タイムアウト]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_verifyCTL"></a>-verifyCTL

CertUtil [オプション] - verifyCTL CTLObject [CertDir] [CertFile]

AuthRoot を確認するか、許可されない証明書の CTL

CTLObject:確認する CTL を識別します。
-   AuthRootWU: は、URL のキャッシュから AuthRoot CAB と一致する証明書を読み取る。 代わりに Windows Update からダウンロードするには、-f を使用します。
-   DisallowedWU: では、証明書の許可されていない CAB を読み取り、URL のキャッシュからの証明書ストアのファイルを実行できません。  代わりに Windows Update からダウンロードするには、-f を使用します。
-   AuthRoot: レジストリの読み取りは、AuthRoot CTL をキャッシュします。  -F を使用して、レジストリの更新を強制的に信頼されていない CertFile AuthRoot と許可されていない証明書の Ctl をキャッシュします。
-   [許可しない]: レジストリの読み取りでは、許可されていない証明書の CTL がキャッシュされます。 -f AuthRoot と同様、同じ動作が。
-   CTLFileName: ファイルまたは http: CTL または CAB へのパス

CTL のエントリに一致する証明書を含む CertDir: フォルダーです。 Http: フォルダーのパスはパス区切り記号で終了する必要があります。 AuthRoot または許可しないフォルダーが指定されていない場合の証明書に一致する複数の場所が検索されます。 ローカルの証明書ストア、crypt32.dll リソースとローカルの URL キャッシュします。 -F を使用すると、必要な場合に、Windows Update からダウンロードできます。 それ以外の場合、CTLObject として同じフォルダーまたは web サイトに既定で。

CertFile: コンテンツを確認する証明書を含むファイル。 証明書は、CTL のエントリと一致して、表示される結果と一致します。 ほとんどの既定の出力を抑制します。

[-f]。[-ユーザー][-の分割]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_sign"></a>-sign

CertUtil [オプション] - サインイン InFileList |SerialNumber |CRL OutFileList [StartDate + dd:hh] [+ SerialNumberList | SerialNumberList-| - ObjectIdList |@ExtensionFile]

CertUtil [オプション] - サインイン InFileList |SerialNumber |CRL OutFileList [#HashAlgorithm] [AlternateSignatureAlgorithm + | - AlternateSignatureAlgorithm]

CRL または証明書を再署名します。

証明書または CRL のファイルを変更して再署名の InFileList: コンマ区切りのリスト

シリアル番号:作成する証明書のシリアル番号。 有効期間やその他のオプションは表示されませんする必要があります。

CRL:空の CRL を作成します。 有効期間やその他のオプションは表示されませんする必要があります。

変更された証明書または CRL の出力ファイルの OutFileList: コンマ区切り一覧。 ファイルの数は、InFileList と一致する必要があります。

StartDate + dd:hh: 新しい有効期間: プラス; 省略可能な日付省略可能な日と時間の有効期間。両方が指定されている場合は、プラス記号 (+) の区切り記号を使用します。 "現時点で [+ 使用 dd:hh]"を現在の時刻に開始します。 (Crl のみ) の有効期限がないように、"never"を使用します。

SerialNumberList: コンマ区切りのシリアル番号の一覧を追加または削除

ObjectIdList: コンマ区切りの拡張機能オブジェクト Id リストを削除するには

@ExtensionFile: INF ファイルを更新または削除する拡張機能を含む:
```
[Extensions]
     2.5.29.31 = ; Remove CRL Distribution Points extension
     2.5.29.15 = "{hex}" ; Update Key Usage extension
     _continue_="03 02 01 86"
```
HashAlgorithm:# 記号に続くハッシュ アルゴリズムの名前

AlternateSignatureAlgorithm: 代替署名アルゴリズムの指定子

マイナス記号は、シリアル番号と拡張機能を削除するとします。 プラス記号には、CRL に追加するシリアル番号が原因です。 CRL から項目を削除するときに、リストはシリアル番号と Objectid の両方を含めることができます。 AlternateSignatureAlgorithm と従来の署名の形式を使用する前にマイナス記号。 AlternateSignatureAlgorithm する前に、プラス記号は、alternature 署名の表示形式を指定します。 AlternateSignatureAlgorithm が指定されていない場合は、証明書または CRL 署名の形式が使用されます。

[-nullsign][-f]。[-サイレント][-Cert CertId]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_vroot"></a>-vroot

CertUtil [オプション] - vroot [delete]

Web の仮想ルートの作成/削除し、ファイル共有

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_vocsproot"></a>-vocsproot

CertUtil [オプション] - vocsproot [delete]

OCSP の web プロキシの web 仮想ルートの作成/削除

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_addEnrollmentServer"></a>-addEnrollmentServer

CertUtil [オプション] - addEnrollmentServer Kerberos |ユーザー名 |ClientCertificate [AllowRenewalsOnly] [AllowKeyBasedRenewal]

登録サーバーのアプリケーションを追加します。

登録サーバーのアプリケーションと、必要に応じて、指定された CA のアプリケーション プールを追加します。 このコマンドは、バイナリまたはパッケージにはインストールされません。 次に、クライアントが証明書の登録サーバーに接続する認証方法の 1 つ。
-   Kerberos:Kerberos の SSL 資格情報を使用します。
-   ユーザー名:名前付きのアカウントを使用して、SSL 資格情報
-   ClientCertificate:X.509 証明書の SSL 資格情報を使用します。
-   AllowRenewalsOnly:この URL を使用してこの CA に証明書更新要求のみを送信できます。
-   AllowKeyBasedRenewal--では、AD に関連付けられているアカウントを持たない証明書を使用できるようにします。 これは ClientCertificate と AllowRenewalsOnly モードでのみ適用されます。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_deleteEnrollmentServer"></a>-deleteEnrollmentServer

CertUtil [Options] -deleteEnrollmentServer Kerberos | UserName | ClientCertificate

登録サーバー アプリケーションを削除します。

登録サーバーのアプリケーションと、必要に応じて、指定された CA のアプリケーション プールを削除します。 このコマンドでは、バイナリまたはパッケージは削除されません。 次に、クライアントが証明書の登録サーバーに接続する認証方法の 1 つ。
1.  Kerberos:Kerberos の SSL 資格情報を使用します。
2.  ユーザー名:名前付きのアカウントを使用して、SSL 資格情報
3.  ClientCertificate:X.509 証明書の SSL 資格情報を使用します。

[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_addPolicyServer"></a>-addPolicyServer

CertUtil [オプション] - addPolicyServer Kerberos |ユーザー名 |ClientCertificate [KeyBasedRenewal]

ポリシー サーバー アプリケーションを追加します。

必要な場合は、ポリシー サーバーのアプリケーションとアプリケーション プールを追加します。 このコマンドは、バイナリまたはパッケージにはインストールされません。 次に、クライアントが証明書のポリシー サーバーに接続する認証方法のいずれか:
-   Kerberos:Kerberos の SSL 資格情報を使用します。
-   ユーザー名:名前付きのアカウントを使用して、SSL 資格情報
-   ClientCertificate:X.509 証明書の SSL 資格情報を使用します。
-   KeyBasedRenewal:KeyBasedRenewal テンプレートが含まれているポリシーのみがクライアントに返されます。 このフラグは、ユーザー名と ClientCertificate 認証にのみ適用されます。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_deletePolicyServer"></a>-deletePolicyServer

CertUtil [オプション] - deletePolicyServer Kerberos |ユーザー名 |ClientCertificate [KeyBasedRenewal]

ポリシー サーバー アプリケーションを削除します。

必要な場合は、ポリシー サーバーのアプリケーションとアプリケーション プールを削除します。 このコマンドでは、バイナリまたはパッケージは削除されません。 次に、クライアントが証明書のポリシー サーバーに接続する認証方法のいずれか:
1.  Kerberos:Kerberos の SSL 資格情報を使用します。
2.  ユーザー名:名前付きのアカウントを使用して、SSL 資格情報
3.  ClientCertificate:X.509 証明書の SSL 資格情報を使用します。
4.  KeyBasedRenewal:KeyBasedRenewal ポリシー サーバー

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_oid"></a>-oid

CertUtil [オプション] - oid ObjectId [DisplayName | [LanguageId [Type] を削除]

CertUtil [オプション] - oid GroupId

CertUtil [Options] -oid AlgId | AlgorithmName [GroupId]

ObjectId を表示または表示名を設定します。
-   ObjectId - ObjectId を表示または表示名を追加するには
-   列挙する Objectid の 10 進 GroupId の数を GroupId--
-   ObjectId を検索する 16 進数の AlgId を AlgId--
-   AlgorithmName--アルゴリズムの名前で、ObjectId を検索するには
-   DisplayName -- Display Name to store in DS
-   削除--表示名を削除
-   LanguageId--言語 Id (既定値は現在。1033)
-   型 - DS オブジェクトの作成の種類。テンプレート (既定)、発行ポリシーは、アプリケーション ポリシーの 3 2 1
-   -F を使用すると、DS オブジェクトを作成します。

[-f]。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_error"></a>-error

CertUtil [オプション] - エラーのエラー コード

エラー コードのメッセージ テキストを表示します。

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_getreg"></a>-getreg

CertUtil [Options] -getreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]][RegistryValueName]

レジストリ値を表示します。

ca:使用して CA のレジストリ キー

復元します。使用して CA の復元のレジストリ キー

ポリシー:ポリシー モジュールのレジストリ キーを使用します。

終了:使用終了モジュールのレジストリ キー

テンプレート:テンプレートのレジストリ キーを使用して (使用して、ユーザー テンプレートのユーザー)

登録します。登録のレジストリ キーを使用して (使用 - ユーザーのコンテキストのユーザー)

チェーン:チェーン configuration レジストリ キーを使用します。

PolicyServers:ポリシー サーバーのレジストリ キーを使用します。

ProgId:ポリシーを使用するか、終了モジュールの ProgId (レジストリ サブキーの名前)

RegistryValueName: レジストリ値の名前 (使用して「名前 *」一致のプレフィックス)

値: 新しい数値、文字列または日付のレジストリ値またはファイル名。 数値の値で始まる場合「+」または"-"、新しい値で指定されたビットを設定または既存のレジストリ値をクリアします。

文字列値で始まる場合「+」または"-"、既存の値は、REG_MULTI_SZ 値と、文字列が追加または既存のレジストリ値から削除します。 REG_MULTI_SZ 値の作成を強制するには、文字列値の末尾に"\n"を追加します。

値で始まる場合"@"、値の残りの部分はバイナリ値の 16 進数のテキスト表現を含むファイルの名前です。 有効なファイルを参照していない場合は代わりに解析結果は [Date] として [+ |-] [dd:hh]--プラスまたはマイナス省略可能な日と時間の省略可能な日付。 両方が指定されている場合は、プラス記号 (+) またはマイナス記号 (-) の区切り記号を使用します。 現在の時間を基準と日付の「現在 + dd:hh」を使用します。

使用して"chain\ChainCacheResyncFiletime @now"にキャッシュされた Crl を効果的にフラッシュします。

[-f]。[-ユーザー][-グループ ポリシー][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_setreg"></a>-setreg

CertUtil [Options] -setreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]]RegistryValueName Value

レジストリ値の設定

ca:使用して CA のレジストリ キー

復元します。使用して CA の復元のレジストリ キー

ポリシー:ポリシー モジュールのレジストリ キーを使用します。

終了:使用終了モジュールのレジストリ キー

テンプレート:テンプレートのレジストリ キーを使用して (使用して、ユーザー テンプレートのユーザー)

登録します。登録のレジストリ キーを使用して (使用 - ユーザーのコンテキストのユーザー)

チェーン:チェーン configuration レジストリ キーを使用します。

PolicyServers:ポリシー サーバーのレジストリ キーを使用します。

ProgId:ポリシーを使用するか、終了モジュールの ProgId (レジストリ サブキーの名前)

RegistryValueName: レジストリ値の名前 (使用して「名前 *」一致のプレフィックス)

値: 新しい数値、文字列または日付のレジストリ値またはファイル名。 数値の値で始まる場合「+」または"-"、新しい値で指定されたビットを設定または既存のレジストリ値をクリアします。

文字列値で始まる場合「+」または"-"、既存の値は、REG_MULTI_SZ 値と、文字列が追加または既存のレジストリ値から削除します。 REG_MULTI_SZ 値の作成を強制するには、文字列値の末尾に"\n"を追加します。

値で始まる場合"@"、値の残りの部分はバイナリ値の 16 進数のテキスト表現を含むファイルの名前です。 有効なファイルを参照していない場合は代わりに解析結果は [Date] として [+ |-] [dd:hh]--プラスまたはマイナス省略可能な日と時間の省略可能な日付。 両方が指定されている場合は、プラス記号 (+) またはマイナス記号 (-) の区切り記号を使用します。 現在の時間を基準と日付の「現在 + dd:hh」を使用します。

使用して"chain\ChainCacheResyncFiletime @now"にキャッシュされた Crl を効果的にフラッシュします。

[-f]。[-ユーザー][-グループ ポリシー][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_delreg"></a>-delreg

CertUtil [Options] -delreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]][RegistryValueName]

レジストリ値を削除します。

ca:使用して CA のレジストリ キー

復元します。使用して CA の復元のレジストリ キー

ポリシー:ポリシー モジュールのレジストリ キーを使用します。

終了:使用終了モジュールのレジストリ キー

テンプレート:テンプレートのレジストリ キーを使用して (使用して、ユーザー テンプレートのユーザー)

登録します。登録のレジストリ キーを使用して (使用 - ユーザーのコンテキストのユーザー)

チェーン:チェーン configuration レジストリ キーを使用します。

PolicyServers:ポリシー サーバーのレジストリ キーを使用します。

ProgId:ポリシーを使用するか、終了モジュールの ProgId (レジストリ サブキーの名前)

RegistryValueName: レジストリ値の名前 (使用して「名前 *」一致のプレフィックス)

値: 新しい数値、文字列または日付のレジストリ値またはファイル名。 数値の値で始まる場合「+」または"-"、新しい値で指定されたビットを設定または既存のレジストリ値をクリアします。

文字列値で始まる場合「+」または"-"、既存の値は、REG_MULTI_SZ 値と、文字列が追加または既存のレジストリ値から削除します。 REG_MULTI_SZ 値の作成を強制するには、文字列値の末尾に"\n"を追加します。

値で始まる場合"@"、値の残りの部分はバイナリ値の 16 進数のテキスト表現を含むファイルの名前です。 有効なファイルを参照していない場合は代わりに解析結果は [Date] として [+ |-] [dd:hh]--プラスまたはマイナス省略可能な日と時間の省略可能な日付。 両方が指定されている場合は、プラス記号 (+) またはマイナス記号 (-) の区切り記号を使用します。 現在の時間を基準と日付の「現在 + dd:hh」を使用します。

使用して"chain\ChainCacheResyncFiletime @now"にキャッシュされた Crl を効果的にフラッシュします。

[-f]。[-ユーザー][-グループ ポリシー][-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ImportKMS"></a>-ImportKMS

CertUtil [オプション] - ImportKMS UserKeyAndCertFile [CertId]

キーのアーカイブ用のサーバーのデータベースにユーザーのキーと証明書をインポートします。

UserKeyAndCertFile--データは、ユーザーの秘密キーおよびアーカイブする証明書を含むファイルします。  次のいずれかを指定できます。
-   Exchange キーの管理サーバー (KMS) ファイルをエクスポートします。
-   PFX ファイル

CertId:KMS は、ファイルの復号化証明書の一致するトークンをエクスポートします。  参照してください[-格納](#BKMK_Store)します。

-F を使用して、CA によって発行されていない証明書をインポートします。

[-f] [-silent] [-split] [-config Machine\CAName] [-p Password] [-symkeyalg SymmetricKeyAlgorithm[,KeyLength]]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ImportCert"></a>-ImportCert

CertUtil [オプション] - ImportCert Certfile [ExistingRow]

証明書ファイルをデータベースにインポートします。

ExistingRow を使用すると、同じキーの保留中の要求の代わりに証明書をインポートできます。

-F を使用して、CA によって発行されていない証明書をインポートします。

CA は、外部の証明書のインポートをサポートするように構成する必要もあります certutil-setreg ca\KRAFlags + KRAF_ENABLEFOREIGN。

[-f]。[-config Machine\CAName]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_GetKey"></a>-GetKey

CertUtil [オプション] - GetKey SearchToken [RecoveryBlobOutFile]

CertUtil [オプション] - GetKey SearchToken スクリプト OutputScriptFile

CertUtil [オプション] - GetKey SearchToken の取得 |OutputFileBaseName を回復します。

アーカイブされた秘密キーの回復の blob を取得、復旧スクリプトを生成またはアーカイブされたキーの回復

スクリプト: 取得し、(既定の動作または複数の一致する回復候補が見つかった場合、出力ファイルがない場合指定) キーを回復するスクリプトを生成します。

取得します 1 つまたは複数のキー回復の Blob の取得 (既定の動作と一致する 1 つだけの回復候補が見つかった場合、出力ファイルが指定されている場合)。

回復: 取得および秘密キー (Key Recovery Agent 証明書と秘密キーが必要) 1 つの手順での回復

SearchToken:キーと回復する証明書を選択するために使用します。

次のいずれかになります。
1.  証明書共通名
2.  証明書のシリアル番号
3.  証明書の sha-1 ハッシュ (拇印)
4.  証明書 KeyId sha-1 ハッシュ (サブジェクト キー識別子)
5.  要求者名 (domain \user)
6.  UPN (user@domain)

証明書チェーンと 1 つまたは複数の Key Recovery Agent 証明書をまだ暗号化されて、関連付けられている秘密キーを含む RecoveryBlobOutFile: 出力ファイル。

OutputScriptFile: は、バッチ スクリプトを取得し、秘密キーの回復を含むファイルを出力します。

OutputFileBaseName: 出力ファイルの基本名です。 取得は、任意の拡張機能は切り捨てられ、各 blob のキー回復証明書に固有の文字列と .rec 拡張機能を追加します。  各ファイルには、証明書チェーンと 1 つまたは複数の Key Recovery Agent 証明書をまだ暗号化されて、関連付けられている秘密キーが含まれています。 回復は、任意の拡張機能は切り捨てられ、.p12 拡張機能が追加されます。  回復証明書チェーンと関連付けられている秘密キー、PFX ファイルとして格納されているが含まれています。

[-f] [-UnicodeText] [-silent] [-config Machine\CAName] [-p Password] [-ProtectTo SAMNameAndSIDList] [-csp Provider]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_RecoverKey"></a>-Recoverkey

[オプション] の CertUtil-recoverkey RecoveryBlobInFile [PFXOutFile [RecipientIndex]

アーカイブされた秘密キーを回復します。

[-f] [-user] [-silent] [-split] [-p Password] [-ProtectTo SAMNameAndSIDList] [-csp Provider] [-t Timeout]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_MergePFX"></a>-MergePFX

CertUtil [オプション] - MergePFX PFXInFileList PFXOutFile [ExtendedProperties]

PFXInFileList:コンマ区切りの PFX ファイルの入力リスト

PFXOutFile:PFX の出力ファイル

ExtendedProperties:拡張プロパティを含める

コマンドラインで指定されたパスワードでは、コンマ区切りのパスワードの一覧を示します。  1 つ以上のパスワードが指定されている場合、出力ファイルの最後にパスワードが使用されます。  のみを指定する 1 つのパスワード、または前回のパスワードが"*"をユーザーは、出力ファイルのパスワードを求められます。

[-f]。[-ユーザー][-の分割][--p パスワード][-ProtectTo SAMNameAndSIDList][-csp プロバイダー]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_ConvertEPF"></a>-ConvertEPF

CertUtil [オプション] - ConvertEPF PFXInFileList EPFOutFile [キャスト | キャスト-] [V3CACertId] [, Salt]

PFX ファイルを EPF ファイルに変換します。

PFXInFileList:コンマ区切りの PFX ファイルの入力リスト

EPF:EPF 出力ファイル

キャスト:キャスト 64 の暗号化を使用します。

キャストの:キャスト 64 暗号化 (エクスポート) を使用します。

V3CACertId:V3 の CA 証明書の一致するトークンです。  参照してください[-格納](#BKMK_Store)CertId 説明します。

Salt。EPF 出力ファイルの salt 文字列

コマンドラインで指定されたパスワードでは、コンマ区切りのパスワードの一覧を示します。 1 つ以上のパスワードが指定されている場合、出力ファイルの最後にパスワードが使用されます。  のみを指定する 1 つのパスワード、または前回のパスワードが"*"をユーザーは、出力ファイルのパスワードを求められます。

[-f] [-silent] [-split] [-dc DCName] [-p Password] [-csp Provider]

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_Options"></a>オプション

このセクションでは、コマンドを使用して指定できるオプションを定義します。

|オプション|説明|
|-------|-----------|
|-nullsign|署名とデータのハッシュを使用します。|
|-f|強制的に上書き|
|-エンタープライズ|ローカル コンピューターのエンタープライズ レジストリ証明書ストアを使用します。|
|-ユーザー|HKEY_CURRENT_USER キーまたは証明書ストアを使用します。|
|-グループ ポリシー|グループ ポリシーの証明書ストア|
|-ut|ユーザー テンプレートを表示します。|
|-mt|マシン テンプレートを表示します。|
|Unicode|Unicode のリダイレクトされた出力を書き込む|
|-UnicodeText|Unicode で出力ファイルを書き込み|
|-gmt|GMT としての表示時間|
|-秒|秒とミリ秒で時間が表示されます。|
|-サイレント|サイレント フラグを使用して、crypt コンテキストを取得するには|
|-の分割|埋め込みの ASN.1 要素を分割し、ファイルに保存|
|-v|詳細な操作|
|-privatekey|パスワードと秘密キーのデータを表示します。|
|-暗証番号 (pin) をピン留め|スマート カード暗証番号 (pin)|
|-urlfetch|取得し、証明書の AIA と CDP Crl を確認します。|
|-config Machine\CAName|CA とコンピューター名の文字列|
|-PolicyServer URLOrId|ポリシー サーバーの URL または id。選択 U - PolicyServer の使用は、/。 すべてのポリシー サーバーの使用 - PolicyServer *|
|匿名|匿名の SSL 資格情報を使用します。|
|-Kerberos|Kerberos の SSL 資格情報を使用します。|
|-ClientCertificate ClientCertId|X.509 証明書の SSL 資格情報を使用します。 U を選択/は使用 clientCertificate します。|
|-ユーザー名のユーザー名|SSL 資格情報の名前付きのアカウントを使用します。 選択 U - ユーザー名を使用するには、/。|
|証明書 CertId|署名用の証明書|
|-dc DCName|特定のドメイン コント ローラーのターゲット|
|-RestrictionList を制限します。|コンマ区切りの制限の一覧。 各制限は、列名、関係演算子と定数整数、文字列または日で構成されます。 1 つの列名の前に、プラス記号またはマイナス記号を並べ替え順序を示すために可能性があります。 例:</br>"RequestId = 47"</br>"+ RequesterName > =、RequesterName < b"</br>"-RequesterName > DOMAIN, Disposition = 21"|
|-ColumnList アウト|コンマ区切りの列の一覧|
|-p パスワード|パスワード|
|-ProtectTo SAMNameAndSIDList|コンマ区切りの SAM 名/SID リスト|
|csp プロバイダー|プロバイダー|
|-t タイムアウト|URL のフェッチのタイムアウト (ミリ秒)|
|-symkeyalg SymmetricKeyAlgorithm[,KeyLength]|省略可能なキーの長さで対称キー アルゴリズムの名前の例。128 または 3 des、AES|

戻り[メニュー](#BKMK_menu)

## <a name="BKMK_AddedExamples"></a>Certutil の他の例

このコマンドを使用する方法の例については、次を参照してください。
1.  [コマンドラインから Active Directory 証明書サービス (AD CS) を管理するための Certutil 例](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)
2.  [証明書を管理するための Certutil タスク](https://technet.microsoft.com/library/cc772898.aspx)
3.  [CertUtil.exe コマンド ライン ツールのチュートリアルを使用してバイナリの要求のエクスポート](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)
4.  [ルート CA 証明書の更新](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)
5.  [certutil](https://msdn.microsoft.com/subscriptions/cc773087.aspx)

戻り[メニュー](#BKMK_menu)
